# Backend-Project
32Bit Toyota backend project assignment


* [General Info](#general-info)
* [What is it?](#what-is-it)
* [Currently Working](#currently-working)
* [Planned](#planned)
* [Deployment](#deployment)
* [Mappings](#mappings)
* [How to use](#how-to-use)


## General Info
This application's purpose is to learn and apply for a backend position as a student.


## What is it?
It is an API with token based authentication and authorization that allows the user to manage two entities, User and Vehicle.



## Currently working

* CRUD Operations
* Data entry validation.
* DTO <-> DAO conversion.
* Logging.
* Token-based Authentication and Authorization.
* Error Input and Listing (Vehicle Management Service).

## Planned
* Terminal Service.
* Unit Testing.


## Deployment
You need to do the following in order to run this api on your machine.

First, Open a terminal in the project's directory.
Then, follow the steps below.

##### To recompile the application.
```console
mvn clean compile
```

##### to package .jar file
```console
mvn install
```
##### to build a docker image from the app file.

```console
docker build -t backend-project.jar .
```


##### to run the database and the api

```console
docker-compose up -d
```

## Mappings

| Method  | URL |
| ------- | ---- |
| POST  | http://localhost:8001/api/auth/signup |
| POST  | http://localhost:8001/api/auth/signin |


| Method  | User Entity |
| ------- | ---------- |
| GET   | http://localhost:8002/user-management/list-users |
| DEL   | http://localhost:8002/user-management/deactivate-user/{id} |
| PUT   | http://localhost:8002/user-management/update-user/{id} |

| Method | Vehicle Entity |
| ------ | -------------- |
| POST   | http://localhost:8003/vehicle-management/add-vehicle |
| PUT    | http://localhost:8003/vehicle-management/update-vehicle/{id} |
| GET    | http://localhost:8003/vehicle-management/list-vehicles |


## How to use
Before you can access the server, you must sign up.

| Role  | Description |
| ----  | ----------- |
| ADMIN | This role has access to the user management service. |
| OPERATOR | This role has access to the vehicle management service. |
| TEAMLEADER | This role has no access ( TO BE CHANGED LATER ) |

An example on what to send in the json body when requesting to signup.

*Note: if the roles are not specified, the OPERATOR role will be applied by default.*
```json

"name":"YourName",
"username":"YourUserName02",
"email":"YourUserName02@outlook.com",
"password": "YourPassword",
"active": true
   
```

Or you can send in the json body above multiple roles like this
```json
  "active": true,
  "roles": ["OPERATOR", "ADMIN", "TEAMLEADER"]
```

### User Management Service

#### Update a user
You can write the same properties in the signup request json body but you must change at least the username and email.
```json
"name":"YourNameUpdated",
"username":"YourUserName02Updated",
"email":"YourUserName02Updated@outlook.com2",
"password":"YourPasswordUpdated",
"active": true,
"roles": ["TEAMLEADER"]
```
#### Get users list 
To see all *active* users, you can use the list-users method.

#### Delete a user 
*Note: Soft-delete approach is applied here.*

All you have to do is supply the id in the URL.

To reactive a user, use the update method.


### Vehicle Management Service


#### Add a vehicle
You must supply the following json body in order to successfully save a vehicle in the database.
```json
"make": "Toyota",
"model": "BAC2020",
"vehicle_defects": [{
	"types": ["DAMAGE", "WHEELS"],
	"defect_locations": [{
		"x_coordinate": 25.2,
		"y_coordinate": 25.3
		}]

	}]
```
Or you can add a vehicle without ```"vehicle_defects" ```


#### Update a vehicle
You must supply the id in the URL.

The json body is the same as the one above.

If you want to remove the ``` vehicle_defects ```, you must write it in this way
```json
"make": "Toyota",
"model": "CBA2023",
"vehicle_defects": []
```

#### Get vehicles list.
You can use the list-vehicles method.

