<a name="Exceptions"></a>
###Exceptions

####Information:

`Exceptions` are classes to be thrown in case of errors.
<br>
`Exceptions` can be thrown from anywhere in the application.


####Code sample:

`Exception` Class:

```php
use Hello\Modules\Core\Exception\Abstracts\ApiException;
use Symfony\Component\HttpFoundation\Response;

class AccountFailedException extends ApiException
{
    public $httpStatusCode = Response::HTTP_CONFLICT;

    public $message = 'Failed creating new User.';
}
```

Usage from anywhere:

```php
throw new AccountFailedException();
```


Usage with **Log** for Debugging:

```php
throw (new AccountFailedException())->debug($e); // debug() accepts string or \Exception instance
```

Usage and overriding the default `message`:

```php
throw new AccountFailedException('I am the message to be displayed for the user');
```

####Notes:

The `Exception` can have two properties `httpStatusCode` and `message`, both properties will be displayed when an error occurs, if not proveded in the parameter while throwing the error.

`Exceptions` can be thrown from anywhere in the application.

Module specific `Exceptions` can be placed in the `Modules` and general Exeptions SHOULD be placed in `src/Services/Core/Exception`.
