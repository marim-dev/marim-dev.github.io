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
A Marim project is simply a directory. Therefore, create a directory named `project`

```shell
mkdir ~/marim/project
```

# Service declaration
Declare a service named `dvdrental` in the project by creating the `~/marim/project/dvdrental.declaration` file with the following content

```shell
service dvdrental

version v1
```

# API specification
Specify the API of the `dvdrental` service by creating the `~/marim/project/dvdrental.api` file with the following content

```shell
api service dvdrental version v1

path "/category"
	query parameter $first
	query parameter $top

path "/category/" categoryId
	path parameter categoryId	
```