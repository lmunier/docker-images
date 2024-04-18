# docker-images

Author : Louis Munier - lmunier@protonmail.com

Here are stored all the base docker images usefull for my different projects. The intention of that repos is to regroup in one place all the base docker images. The architecture is the same for all with :

- docker folder containing the Dockerfile(s)
- src folder containing the source code to be mount as a volume inside docker
- .env file with all the environment variables
- docker-compose.yaml file to define the build / mount parameters
