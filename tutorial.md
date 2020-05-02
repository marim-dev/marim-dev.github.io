---
    title: Tutorial
    layout: container    
---
# Welcome!
Welcome to the Marim tutorial! Follow the steps below to create your first service in Marim.

# Sample database
This tutorial makes use of a sample database. To execute it, type the command

```shell
docker run -it --rm -p 5432:5432 marimplatform/dvdrental
```

# Project
A Marim project is simply a directory. Therefore, type the command below to create your project

```shell
mkdir ~/marim/project
```

# Service declaration
**Declare** a service named `dvdrental` in the project by creating the `~/marim/project/dvdrental.declaration` file with the following content

```
service dvdrental

version v1
```

# API specification
**Specify** the API of the `v1` version of the `dvdrental` service by creating the `~/marim/project/dvdrental.api` file with the following content

```
api service dvdrental version v1

path "/category"
	query parameter $first
	query parameter $top

path "/category/" categoryId
	path parameter categoryId	
```

# Service implementation
**Implement** the API of the `v1` version of the `dvdrental` service by creating the `~/marim/project/dvdrental.implementation` file with the following content

```
implementation service dvdrental version v1

path "/category"
	datasource dvdrental

	query "select category_id as id, name from category limit coalesce(cast(" $top " as integer), 100) offset coalesce(cast(" $first "as integer), 0)"

path "/category/" categoryId
	datasource dvdrental

	query "select category_id as id, name from category where category_id = cast(" categoryId " as integer)"
```

# Datasource definition
**Define** the datasource that the implementation of the `v1` version of the `dvdrental` service access by creating the `~/marim/project/dvdrental.datasource` file with the following content

```
datasource dvdrental
	driver "org.postgresql.Driver"
	url "jdbc:postgresql://localhost:5432/dvdrental"
	user "postgres"
	password "postgres"
```