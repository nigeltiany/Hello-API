###Policies

####Information:

`Policies` are plain PHP classes that group authorization logic based on the resource they authorize.

For more information about the `Policies` read [this](https://laravel.com/docs/5.1/authorization#policies).



####Code sample:

`Ploicy` Class:

```php
use Illuminate\Auth\Access\HandlesAuthorization;
use Hello\Modules\User\Models\User;

class UserPolicy
{
    use HandlesAuthorization;

    public function update(User $user, $inputUserId)
    {
        // authorize only if a user is updating it's own records
        return ($user->id == $inputUserId) ? true : false;
    }

    public function delete(User $user, $inputUserId)
    {
        // authorize only if a user is deleting it's own records
        return ($user->id == $inputUserId) ? true : false;
    }
}
```

Usage from `Request`:

```php
    /**
     * Determine if the user is authorized to make this request.
     *
     * @param \Illuminate\Contracts\Auth\Access\Gate $gate
     *
     * @return bool
     */
    public function authorize(Gate $gate)
    {
        return $gate->getPolicyFor(User::class)->update($this->user(), $this->id);
    }
```

###Notes:

The best place to use the `Policies` is from the `Requests` inside the `authorize()` function.

Everytime you create a new `Policy` you must register it in the Module **AuthServiceProvider**.


<br>

###Knowledge Base:

####How to register a Policy

Inside your Module you should have **AuthServiceProvider**.

(Example in case of a User Module, the path will be `src/Modules/User/Providers/AuthServiceProvider.php`).

Open the Module **AuthServiceProvider** and add your `Policy` in the `$policies` property next to it's Model.

Example:

```php
protected $policies = [
    User::class => UserPolicy::class
    // ... add more
];
```



