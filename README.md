# Application

Application runs with PHP 8.1 and MySQL 8

#### Docker

Copy `docker/.env.dist` to `docker/.env` and customise it with your parameters

Build container

```
make build
```

Run container

```
make up
```

Stop container

```
make down
```

Remove database container

```
make rm-db
```

Display container logs

```
make logs
```

Enter into php container

```
make bash
```

#### Init Application

install dependencies

```
make install
```

#### Tests

run all tests

```
make test
```

run unit tests

```
make unit
``` 

run behat tests

```
make behat
``` 

#### Coding Standards

```
make cs
``` 

#### Static Code Analysis

```
make stan
``` 
