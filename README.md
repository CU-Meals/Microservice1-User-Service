# Microservice1-User-Service

This microservice is a fundamental component of our application, responsible for managing all user-related functionalities. It handles authentication, authorization, and user profile management for both general users and restaurant owners. The User Microservice is built using Django. It operates independently with its own database and exposes a set of RESTful API endpoints for integration with the composite microservice and other sub-microservices.

## Features
- Handles user authentication and authorization.
- Manages user profiles and credentials for both general users and restaurant owners.
- Support for Multiple User Roles.

## User Model
The user data is stored using the following Django model:
```
class users(models.Model):
    uni = models.IntegerField()
    email = models.CharField(max_length=100)
    first_name = models.CharField(max_length=100)
    last_name = models.CharField(max_length=100)
    ID_TYPE_CHOICES = [ ('student', 'Student'), ('faculty', 'Faculty'), ('guest', 'Guest'), ]
    id_type = models.CharField(max_length=10, choices=ID_TYPE_CHOICES)
    password = models.CharField(max_length=16, default="default_password")

def __str__(self):
    return f"{self.first_name} - {self.last_name} - {self.uni}"
```

## API Endpoints

### Base Message
- URL: ```GET /```
- Description: Returns a welcome message or basic information about the microservice.
- Input argument: None
  
### Add User
- URL: ```POST /add_user/```
- Description: Creates a new user account. Expects user data in JSON format in the request body.
- Input argument:
  | Parameter    | Type    |  Description                                     |
  |--------------|---------| -------------------------------------------------|
  | `uni`        | Integer | Unique numeric identifier for the user          |
  | `email`      | String  | Email address of the user                       |
  | `first_name` | String  | First name of the user                          |
  | `last_name`  | String  | Last name of the user                           |
  | `id_type`    | String  | Type of user ID (`student`, `faculty`, `guest`) |
  | `password`   | String  | Password for the user account                   |

  
### Get All Users
- URL: ```GET /get_all_users/```
- Description: Retrieves a list of all registered users.
- Input argument: None
  
### Delete User
- URL: ```DELETE /delete-user/<int:uni>/```
- Description: Deletes a user account specified by user's uni.
- Input argument:
  | Parameter | Type    |  Description                            |
  | --------- | ------- |  -------------------------------------- |
  | `uni`        | Integer | Unique numeric identifier for the user          |


### Check User Password:
- URL: ```GET /get_one_user/```
- Description: Verify if the input uni and password match to the user account.
- Input argument:
  | Parameter | Type    |  Description                            |
  | --------- | ------- |  -------------------------------------- |
  | `uni`        | Integer | Unique numeric identifier for the user          |
  | `password`   | String  | Password for the user account                   |
