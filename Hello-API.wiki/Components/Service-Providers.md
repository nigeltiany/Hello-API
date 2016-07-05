<a name="Service Providers"></a>
###Service Providers

####Information:

The `Service Providers` allows registering *stuff* on the framework service container (IoC).

Each `Module` MUST have at least one (main) `Service Providers`. And it MUST be named similar to the Module name. Example the `User` Module should have `UserServiceProvider`.

It is possible to have multiple `Service Providers` inside a `Module` 
However, in that case you must register all the extra service providers in the `config/modules.php` config file.
*See the {Register the internal Module service providers} section below for how to do this.*

The main `Service Provider` will be automatically registered in the Core Service Provider (`src/Services/Core/Providers/CoreServiceProvider.php`), Therefore, you don't need to define it in the `config/modules.php` config file.

For more information about the `Service Providers` read [this](https://laravel.com/docs/master/providers).



####Code sample:

`Service Provider` Class (belongs to a `User Module`):

```php
use Hello\Modules\User\Contracts\UserRepositoryInterface;
use Hello\Modules\User\Repositories\Eloquent\UserRepository;
use Hello\Modules\Core\Providers\Abstracts\ServiceProvider;

class UserServiceProvider extends ServiceProvider
{

    protected $defer = false;


    public function boot()
    {

    }

    public function register()
    {
        $this->app->bind(UserRepositoryInterface::class, UserRepository::class);
    }
}
```

####Notes:

The `Module` MUST be registered in the `config/modules.php` config file, inorder for its main `Service Provider` to get auto loaded.

###Knowledge Base:

####Register the internal Module service providers:
You can add as many service providers as you want in a Module, but in order to get them loaded you must register them in the `config/modules.php` Config file:

```php
'extraServiceProviders' => [
    Hello\Modules\User\Providers\AuthServiceProvider::class,
    // ...
],
```
There's no need to register the main Module Service Provider.


####Register the Core Service Provider in the Framework:
In case of Laravel you MUST register the `CoreServiceProvider` (`src/Services/Core/Providers/CoreServiceProvider.php`) in the `providers` array of the `config/app.php`, like this:

```php
'providers' => [
	Hello\Modules\Core\Providers\CoreServiceProvider::class,
],
```
