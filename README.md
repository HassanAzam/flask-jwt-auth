# Flask JWT Auth
### flaskapi-token-auh
Token based authentication with Flask

### Cookies vs Token based authentication
Source : https://stackoverflow.com/questions/17000835/token-authentication-vs-cookies

 - Http is stateless. In order to authorize you, you have to "sign" every single request you're sending to server.
 - **Token authentication**
    - A request to the server is signed by a "token" - usually it means setting specific http headers, however, they can be sent in any part of the http request (POST body, etc.)
    - Immune to XSRF attack
    - Cookies are bound to a single domain. A cookie created on the domain foo.com can't be read by the domain bar.com, while you             can send tokens to any domain you like.
    - You have to store the token somewhere; while cookies are stored "out of the box". See link for more details
    - It is slightly easier to do XSS attack against token based authentication (i.e. if I'm able to run an injected script on your site, I can steal your token; however, cookie based authentication is not a silver bullet either - while cookies marked as http-only can't be read by the client, the client can still make requests on your behalf that will automatically include the authorization cookie.)
    
- **Cookie authentication**
    - Cookies are sent out for every single request, (even for requests that don't require authentication).
    - Vulnerable to XSRF. You have to implement extra measures to make your site protected against cross site request forgery.
    - Bound to a single domain. (So if you have a single page application that makes requests to multiple services, you can end up            doing crazy stuff like a reverse proxy.)
    

## Quick Start

### Basics

1. Activate a virtualenv
1. Install the requirements

### Set Environment Variables

Update *project/server/config.py*, and then run:

```sh
$ export APP_SETTINGS="project.server.config.DevelopmentConfig"
```

or

```sh
$ export APP_SETTINGS="project.server.config.ProductionConfig"
```

### Create DB

Create the databases in `psql`:

```sh
$ psql
# create database flask_jwt_auth
# create database flask_jwt_auth_testing
# \q
```

Create the tables and run the migrations:

```sh
$ python manage.py create_db
$ python manage.py db init
$ python manage.py db migrate
```

### Run the Application

```sh
$ python manage.py runserver
```

So access the application at the address [http://localhost:5000/](http://localhost:5000/)

> Want to specify a different port?

> ```sh
> $ python manage.py runserver -h 0.0.0.0 -p 8080
> ```

### Testing

Without coverage:

```sh
$ python manage.py test
```

With coverage:

```sh
$ python manage.py cov
```
