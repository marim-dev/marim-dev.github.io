---
    title: Home
    layout: index
---
**Declare** your service
```
service dvdrental

version v1
```
---

**Specify** its API
```
api service dvdrental version v1

path "/category"
	query parameter $first
	query parameter $top

path "/category/" categoryId
	path parameter categoryId	
```
---

**Implement** it
```
implementation service dvdrental version v1

path "/category"
	datasource dvdrental

	query "select category_id as id, name from category limit coalesce(cast(" $top " as integer), 100) offset coalesce(cast(" $first "as integer), 0)"

path "/category/" categoryId
	datasource dvdrental

	query "select category_id as id, name from category where category_id = cast(" categoryId " as integer)"
```
---

**Define** its datasource
```
datasource dvdrental
	driver "org.postgresql.Driver"
	url "jdbc:postgresql://localhost:5432/dvdrental"
	user "postgres"
	password "postgres"
```
---

**Run** it
```
docker run -it --rm -v $(pwd):/projects -p 8080:8080 marimplatform/runtime
```
---

**Be Happy!!! :)** 

1. Your service is ready at `http://localhost:8080/dvdrental/v1/rest`
2. Its [Open API](https://www.openapis.org/) specification is at `http://localhost:8080/dvdrental/v1/openapi`
3. You can view it in a human-friendly way through the integrated [Swagger UI](https://swagger.io/tools/swagger-ui/) application at `http://localhost:8080/dvdrental/v1/swagger-ui`