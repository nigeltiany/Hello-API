<a name="Requests"></a>
###Requests

####Information:

`Requests` are very useful to automatically apply the Validation rules, as well to serve the user input. 

Once they are injected (in the `Controller`) they automatically check if the request data matches the validation rules, if not matched they throw an `Exception` immediately and an Error will be displayed for the User.

`Requests` class are the place to write the validation rules. 

They can also be used to write authorization code, to check if the user is authorized to make this request.

For more information about the `Requests` concept check [this](https://laravel.com/docs/requests).



####Code sample:

`Request` Class:

```php
use Hello\Modules\Core\Request\Abstracts\Request;

class UpdateUserRequest extends Request
{
    public function rules()
    {
        return [
            'password' => 'min:6|max:30',
            'name' => 'min:2|max:50',
        ];
    }

    public function authorize()
    {
        // current logged in user ID
        $currentLoggedInUserId = $this->user()->id;

        // the request input user ID (for the user that needs to be updated)
        $inputUserId = $this->id;

        // authorize only if a user is updating it's own record
        return ($currentLoggedInUserId == $inputUserId) ? true : false;
    }
}

```
Usage from `Controller`:

```php
public function handle(UpdateUserRequest $updateUserRequest)
{
	// by just injecting the request class you already applied the validation and authorization rules.
}
```

Usage and reading data:

```php
public function handle(UpdateUserRequest $updateUserRequest)
{
    $data = $updateUserRequest->all();
    // or
    $name = $updateUserRequest['name'];
}
```

####Notes:

Requests SHOULD only be injected in the `Controllers`. They automatically apply the validation rules.

Every `Request` MUST have a `rules` function, returning an arrays of the validation rules.

Every `Request` SHOULD extend from `Hello\Modules\Core\Request\Abstracts\Request`.


