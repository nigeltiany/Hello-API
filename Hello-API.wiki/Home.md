<a name="introduction"></a>
###Introduction

`Hello API` is built to be customized by you.

The Hello-API Code is architected using a super easy yet powerful Software Architecture called the **Freestyle Architecture**.
You MUST read it's little cute [Documentation](https://github.com/Mahmoudz/Freestyle-Architecture) to be able to easily understand how the code is structured.




<a name="requirements"></a>
## Requirements

- [GIT](https://git-scm.com/downloads)
- [Composer](https://getcomposer.org/download/)





<a name="installation"></a>
## Installation

### A) Application Setup:

1) Clone the project:
 
 ```shell
git clone https://github.com/Mahmoudz/Hello-API.git
 ```

2) Install the PHP dependency packages: 

```shell
composer install
```

3) Provide some Laravel permissions:

```shell
sudo chmod -R 777 storage && sudo chmod -R 777 bootstrap/cache
```

4) Create `.env` file and copy the content of `.env.example` inside it.

```shell
cp .env.example .env
```

*Check all the variables and edit whatever you want.*

5) Generate some random keys `APP_KEY` and `JWT_SECRET`.

```shell
php artisan key:generate && php artisan jwt:generate
```

**Note:** make sure the `JWT_SECRET` is set in the `.env` file. If it still having the default value `xXxXx` then you have to place it manually.








<br>
<br>


### B) Development Environment Setup:

`Hello API` can run on top of [Laravel Homestead](https://laravel.com/docs/master/homestead) or [Docker](https://www.docker.com/) (using [LaraDock](https://github.com/LaraDock/laradock)). W'll show you how to use both tools, so you can pick one.


<br>

#### - Using Laravel Homestead:

*W'll use `hello.dev` as local domain (you can change it if you want).*

1) Configure Homestead:

1.1) Open the Homestead config file: 

```shell
homestead edit
```
	
1.2) Map the `api.hello.dev` domain to the project public directory - Example: 

```yaml
sites:
	- map: api.hello.dev
  	  to: /{full-path-to}/Hello-API/public
```

1.3) You can also map other domains like `hello.dev` and `admin.hello.dev` to the user web apps:

```yaml
	- map: hello.dev
  	  to: /{full-path-to}/Hello-API/clients/web/user
	- map: admin.hello.dev
  	  to: /{full-path-to}/Hello-API/clients/web/admin
```


2) Add the domain to the Hosts file:

2.1) Open the Hosts file `/etc/hosts`.
   
2.2) Map the domains to the Vagrant IP Address: 
   
```text
192.168.10.10   hello.dev
192.168.10.10   api.hello.dev
192.168.10.10   admin.hello.dev
```
   
2.3) Run the Virtual Machine:

```shell
homestead up --provision
```

<br>



#### - Using Docker (with LaraDock):

*W'll use `hello.dev` as local domain (you can change it if you want).*

**Note:** you will need to have Docker installed on your machine. Refer to the [LaraDock documentation](https://github.com/LaraDock/laradock#installation) for help.

1) Navigate into the `docker-helloapi` directory:

```shell
cd docker-helloapi
```
This directory contains a `docker-compose.yml` file. (From the LaraDock project).


2) Run the Docker containers:

```shell
docker-compose up -d nginx mysql redis
```

3) Make sure you are setting the `Docker IP` as `Host` for the `DB` and `Redis`  in your `.env` file.

<br>
<br>


### C) Database Setup:


1) Migrate the Database: 

a. To migrate the Database you must first publish the migration files from the Modules directory to the framework migrations directory. 

Publishing the Modules Migrations files:

```php
php artisan vendor:publish --provider="Hello\Modules\Core\Providers\CoreServiceProvider"
```

b. Now you can run the migration artisan command:

```shell
php artisan migrate
```

2) Seed the database: 

```shell
php artisan db:seed --class="Hello\Modules\Core\Seeders\DatabaseSeeder"
```

3) Done! *The project is now yours and is ready for use* : )


<br>
<br>


### D) Testing:

1) Open your browser and visit the api domain
 
```text
http://api.hello.dev
```

You should see a JSON response the message: `Welcome to Hello API.`

2) Make some HTTP calls to the API now

*To make the calls you can use [Postman](https://www.getpostman.com/), [HTTPIE](https://github.com/jkbrzt/httpie) or any other tool you prefer.*

Let's test the (user registration) endpoint `http://api.hello.dev/register ` with **cURL**:

```
curl -X POST -H "Accept: application/json" -F "email=test@something.com" -F "password=secret#pass" -F "name=John Doe" "http://api.hello.dev/register"
```

You should get response like this:

```json
Content-Type → application/json
Date → Wed, 20 Apr 2019 99:99:99 GMT
ETag → "aa07f48670db7b335c7216034eb94cf0"
Server → nginx/1.8.0
Transfer-Encoding → chunked
Vary → Origin
X-RateLimit-Limit → 100
X-RateLimit-Remaining → 99
X-RateLimit-Reset → 1461179200

{
  "data": {
    "id": 1,
    "name": "John Doe",
    "email": "test@something.com",
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjEwLCJpc3MiOiJodHRwOlwvXC9hcGkubWVnYS5wcm9cL3JlZ2lzdGVyIiwiaWF0IjoxNDYxMTc5MTQ4LCJleHAiOjE0NjM4MDcxNDgsIm5iZiI6MTQ2MTE3OTE0OCwianRpIjoiNzQ4YTlkOTY5NjkyNTQyZGNlNzRlYWE0OWM0ZjBhMTYifQ.gJQSuMuKY64t1XQN9gAkn_nmxMuyN0etvSdBN5-CJBw",
    "created_at": {
      "date": "2019-99-99 99:99:99.000000",
      "timezone_type": 3,
      "timezone": "UTC"
    },
    "updated_at": {
      "date": "2019-99-99 99:99:99.000000",
      "timezone_type": 3,
      "timezone": "UTC"
    }
  }
}
```


3) To run the automated tests you can always type:

```shell
phpunit
```







