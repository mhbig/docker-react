# Docker Cheat
## Project Setup
`node -v`  
v8.11.x

#create the react project with a generator tool  
`npm install -g create-react-app`  

#create the project with the name (folder) **frontend**  
`create-react-app frontend`

#intercat with the project  
| command | description |
| --- | --- |
| npm run start | Strats up a development server. |
| npm run test | Runs test associated with the project |
| npm run build | Builds a **production** version of the app |

## Creating the Dev Dockerfile
#file name  
`dev.dockerfile`

#build  
`docker build -t front-app-dev -f dev.dockerfile .`

#run  
`docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app front-app-dev`

## Shorthand with Docker Compose
//create file  
`docker-compose.yml`

//run  
`docker-compose up`

//atach to a running container  
`docker ps` --> get container id  
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                    NAMES
fd2ad2f03827        frontend_react-ap   "npm run start"     2 days ago          Up About a minute   0.0.0.0:3000->3000/tcp   frontend_react-ap_1
```
`docker exec -it fd2ad2f03827 npm run test`

//running tests with docker compose  
//adding new service  
```yaml
  tests:
    build:
      context: .
      dockerfile: dev.dockerfile
    volumes:
      - /app/node_modules
      - .:/app
    command: ["npm", "run", "test"]
```
//updating container  
`docker-compose up --build`

//conect to container
`docker attach b94cc8b7a350`

## Prod Enviroment
Using a multi step docker builds.  
Create a new file `prod.dockerfile`. Setup tow steps for the build. Step 1 `build` step 2 `prod`  

`docker build -f prod.dockerfile .`  
`docker run -p 8080:80 731a2dae26f7 .`  
open browser with `http://localhost:8080/`

# Setup Git
Create a new repository on GitHub. Name the repo `docker-react`.  
Setup local git repository:
```
git init
git add.
git commit -m "initial commit"
```
