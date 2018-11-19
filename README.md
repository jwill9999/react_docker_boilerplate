# Create-React-App 2.0 Dockerized

## In Development

```
> git clone

> sudo docker image build -t < container name here> .

> sudo docker container run -it -p 3000:3000 -p 35729:35729 -v $(pwd):/app < container name here >


```

## Testing

```
> sudo docker container run -it -v $(pwd):/app < container name here >  test

```

## Jest options

```
sudo docker container run -it -v $(pwd):/app < container name here > test --coverage
sudo docker container run -it -v $(pwd):/app < container name here > test --help

```

## To Debug

```
> sudo docker container run -it -p 3000:3000 -p 35729:35729 -v $(pwd):/app --name mydebugging < container name here >

####################### open a  separate terminal ###################

> sudo docker exec -it mydebugging bash

######################################################################

> this will give you root access to your container terminal
```

## To build

```
> sudo docker container run -it -v $(pwd):/app  < container name here >  build

```

# Example Dockerfile

```yml
FROM node:8

ADD yarn.lock /yarn.lock
ADD package.json /package.json

ENV NODE_PATH=/node_modules
ENV PATH=$PATH:/node_modules/.bin
RUN yarn

WORKDIR /app
ADD . /app

EXPOSE 3000
EXPOSE 35729

ENTRYPOINT ["/bin/bash", "/app/run.sh"]
CMD ["start"]

```

# Example shebang file

```sh
#!/usr/bin/env bash
set -eo pipefail

case $1 in
  start)
    # The '| cat' is to trick Node that this is an non-TTY terminal
    # then react-scripts won't clear the console.
    yarn start | cat
    ;;
  build)
    yarn build
    ;;
  test)
    yarn test $@
    ;;
  *)
    exec "$@"
    ;;
esac

```

# Further development

Why not add a docker-compose file? 



> ## link >  [Futher documentaion here](https://www.peterbe.com/plog/how-to-create-react-app-with-docker)

### Credits:

[Peter Bengtsson ](https://www.peterbe.com/)


<hr>

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app) and [Docker](https://www.docker.com/get-started)

