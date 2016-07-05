<a name="Routes"></a>
###Routes

####Information:

The `Routes` are the first receivers (ports) of the Request in a `Module`.

The `Routes` files can be **API**, **Web** or anything else.

A `Route` file can contain multiple `Endpoints`.

The `Endpoint ` main job is to call a particular `Controller` once a Request is made.

For more info visit this [link](https://github.com/Mahmoudz/Freestyle-Architecture#Routes).



####Code sample:

Normal `Endpoint`:

```php
$router->post('login', [
    'uses' => 'LoginController@handle'
]);
```

Protected `Endpoint`:
(User must login first before accessing this endpoint.)

```php
$router->get('users', [
    'uses'       => 'ListAllUsersController@handle',
    'middleware' => [
        'api.auth',
    ]
]);
```


`Endpoint` With DockBlock ([Api Doc Js](http://apidocjs.com/))

```php
/***********
 * @apiGroup           User
 * @apiName            Login
 * @api                {post} /login Login a user
 * @apiDescription     Login existing User
 * @apiVersion         1.0.0
 * @apiPermission      none
 * @apiUse             Headers_Normal
 * @apiParam           {String}     email
 * @apiParam           {String}     password
 * @apiSuccessExample  {json}       Success-Response:
HTTP/1.1 200 OK

{
  "data": {
    "id": 1,
    "name": "Mahmoud Zalt",
    "email": "mahmoud@zalt.me",
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjEsIm..."
    "created_at": {
      "date": "2016-00-00 01:22:33.000000",
      "timezone_type": 3,
      "timezone": "UTC"
    },
    "updated_at": {
      "date": "2016-00-00 02:33:44.000000",
      "timezone_type": 3,
      "timezone": "UTC"
    }
  }
}
 */
$router->post('login', [
    'uses' => 'LoginController@handle'
]);

```


####Notes:


Each `Endpoint` SHOULD have a dedicated `Controller` for it.

An `Endpoint` SHOULD only call the `handle` Function on it's `Controller`.

You can have many routes files in the same `Module` where each `Route` file can represent a version of the API (example: `src/Modules/User/Routes/Api/v1.php`).

`Routes` MUST be created inside the `Api` and `Web` directories which lives inside a `Routes` directory, as follow (this is case sensitive):

```
- Routes
	- Api
		- v1.php
		- v2.php
		- ...
	- Web
		- main.php
		- ...
```



###Knowledge Base:


####Register route files:

You MUST register every route you create, to register a route:

1) Create the Route file (example: `Routes/Api/v2.php`).

2) Go to the `config/modules.php` config file and set your route name (and version in case of API routes) inside the registered Model. Example:

```
'register' => [
    'MyModule' => [
        'routes' => [
            'api' => [
                ['fileName' => 'v2', 'versionNumber' => '2']
            ],
            'web' => [
					...
            ]
        ]
    ],
],
```



####Protect an Endpoint:

To protect an Endpoint, add the the `api.auth` middleware to it.



####Rate limiting:

The API rate limiting middleware is applied to all the Module Endpoints by default, to edit the value check the `.env` file. To remove it edit the Module `RoutesServiceProvider.php` file.






