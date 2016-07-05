<a name="Models-Factory"></a>
###Models Factory

####Information:

`Models factories` are used to generate some fake data with the help of Faker to be used while testing.

For more information about the `Models factories ` read [this](https://laravel.com/docs/master/testing#model-factories).

####Code sample:

Factory Generaotr for a User:

```php
$factory->define(Hello\Modules\User\Models\User::class, function (Faker\Generator $faker) {
    return [
        'name'     => $faker->name,
        'email'    => $faker->email,
        'password' => bcrypt(str_random(10)),
    ];
});
...
```

Usage from `Test` or anywhere else:

```php
$accounts = factory(Account::class, 3)->create();
```

Usage with relationships:

```php
$factory->define(Hello\Modules\Account\Models\Account::class, function (Faker\Generator $faker) {
    return [
        'user_id'  => factory(Hello\Modules\User\Models\User::class)->create()->id,
        'url'      => $faker->url,
        'username' => $faker->userName,
        'secret'   => $faker->password(),
        'note'     => $faker->text(100),
        'tag_id'   => factory(Hello\Modules\Account\Models\Tag::class)->create()->id,
    ];
});
```

Usage while overriding some values:

```php
$accounts = factory(Account::class, 3)->create()->each(function ($account) use ($user) {
    $account->user_id = $user->id;
    $account->save();
});
```



####Notes:
All the factories should be defined in this file `src/Services/Core/ModelsFactory/ModelsFactory.php`. NOT in the default Laravel path.



###Knowledge Base:

####Change the Models Factory path

Go to the `src/Services/Core/Providers/Traits/CoreServiceProviderTrait.php` and update the `changeTheDefaultDatabaseModelsFactoriesPath` function.

