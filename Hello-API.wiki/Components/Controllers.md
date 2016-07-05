<a name="Controllers"></a>
###Controllers

####Information:

`Controllers` are the same as in MVC, but their responsibilities are different.

A `Controller` has three main roles:

1. reading the request data (user input)
2. running one or multiple `Tasks` (and passing data to them) 
3. building a Response (could be built from the data returned by the `Task`)

`Controllers` SHOULD not have any form of business logic. (It SHOULD run a `Task` to perform a business logic).

For more info visit this [link](https://github.com/Mahmoudz/Freestyle-Architecture#Controllers).




####Code sample:

`Controller` Class:

```php
use Hello\Modules\Core\Controller\Abstracts\ApiController;
use Hello\Modules\User\Requests\LoginRequest;
use Hello\Modules\User\Tasks\LoginTask;
use Hello\Modules\User\Transformers\UserTransformer;

class LoginController extends ApiController
{
    public function handle(LoginRequest $loginRequest, LoginTask $loginTask)
    {
        $user = $loginTask->run($loginRequest['email'], $loginRequest['password']);

        return $this->response->item($user, new UserTransformer());
    }

}
```

Usage from `Routes`:

```php
$router->post('login', [
    'uses' => 'LoginController@handle'
]);
```


####Notes:

Each `Controller` can only respond to a single `Endpoint`. 

Every `Controller` SHOULD have a single function `handle`.

`Controllers` SHOULD only be called from an Endpoint in a `Route` file.

`Controllers` can be for **Web** or for **API**. 

**Web** `Controllers` SHOULD extend from `Hello\Modules\Core\Controller\Abstracts\WebController`.


**Api** `Controllers` SHOULD extend from `Hello\Modules\Core\Controller\Abstracts\ApiController`.
