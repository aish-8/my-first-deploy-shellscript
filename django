# my-first-deploy-shellscript
#1/bin/bash


code_clone() {
	echo " cloning the django app.."
	     git clone https://github.com/aish-8/django-notes-app.git
}

#required libraries


install_requirements() {
	echo "installing dependencies"
	sudo apt-get install docker.io docker-compose -y
}


required_restarts() { 
	sudo systemctl stop nginx
	sudo systemctl disable nginx
	sudo systemctl enable docker
	systemctl restart docker
}


deploy() {
	cd django-notes-app
        docker-compose down --volumes
        docker system prune -f
	docker build -t notes-app .
        docker-compose up -d --build
	docker run -d -p 8080:8000 notes-app:latest

}

echo "deployment started"

if ! [ -d "django-notes-app" ]; then
	echo "repo already exists"
fi


if ! install_requirements; then
echo "installation failed"
exit 1
fi

if ! required_restarts; then
	echo "system fault identified"
	exit 1
fi

if ! deploy; then
	echo "the folder doesn't exist"
	exit 1
fi
echo "deployemnt ended"
