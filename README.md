# User Micro Service
A Symfony 2 based simple micro service providing user registration and api token management.
## Setup
 1. Set up database config in app/config/parameters.yml
 2. Run database migrations `php app/console doctrine:schema:update --force`
## Usage
### Login
Used to exchange the user's email and password for an API Token.
```
Path:
    /auth/login
Method:
    POST
Parameters:
    email: string, user's email address
    password: string, user's password
Success Response:
    HTTP Code: 200
    Response Type: JSON
    Sample Content:
        {
            "user_id": 123,
            "email": "user@example.com"
        }
Failure Response:
    HTTP Code: 401
    Response Type: Plain Text
    Content: Authentication failed.
```
### API Token Check
Used to validate an API Token and get the associated user's User ID and Email.
```
Path:
    /auth/check
Method:
    POST
Parameters:
    api_token: string, user's api token
Success Response:
    HTTP Code: 200
    Response Type: JSON
    Sample Content:
        {
            "user_id": 123,
            "email": "user@example.com"
        }
Failure Response:
    HTTP Code: 403
    Response Type: Plain Text
    Content: The API Key authentication failed.
```
### Registration
Used to create a new account.
```
Path:
    /auth/register
Method:
    POST
Parameters:
    email: string, user's email
    password: string, user's password
Success Response:
    HTTP Code: 200
    Response Type: JSON
    Sample Content:
        {
            "user_id": 123,
            "api_token": api_token_here
        }
```
## To Do:
 - Create & Document Failure Response For Registration
 - Test Suite
 - Optional Mailer Integration (when enabled ping another service to send thanks for registering email)
 - Change Password
 - Forgot Password
 - Facebook Register / Login (pass in Facebook API token, associate with account via facebook user id)
 - Facebook Merge Account (provide email + password login for existing account and an auth token for a facebook account that uses the same email)
 - Rate limiting (excluding requests coming from another internal server such as the web app)