###Database Seeders

####Information:

`Seeders` are classes that seeds the database with specific data, this data might need to exist in the application after installation (example: Roles and Permissions with Defaule Users types).
r creating and the database tables automatically.

For more information about the `Database Seeders` read [this](https://laravel.com/docs/master/seeding).


####Code sample:

`Seeder` Class:

```php
use Bican\Roles\Models\Permission;
use Bican\Roles\Models\Role;
use Illuminate\Database\Seeder;

class SeedRolesAndPermissions extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        $listUsersPermission = Permission::create([
            'name' => 'List users',
            'slug' => 'list.users',
            'description' => 'List all registered Users.',
        ]);

        $adminRole = Role::create([
            'name' => 'Admin',
            'slug' => 'admin',
            'description' => 'Admin access',
            'level' => 1,
        ]);


        $adminRole->attachPermission($listUsersPermission);

		 // ...

    }
}
```



####Notes:

Every Seeder from any Module or Service must be registered in the `Hello\Modules\Core\Seeders\DatabaseSeeder` (Careful this is NOT the default `DatabaseSeeder.php`, this one is in the `Services/Core/Seeders` directory). See below for how to register your Seeder.




###Knowledge Base:


#### Register a Seeder Class

Go to `Hello\Modules\Core\Seeders\DatabaseSeeder` and add your Seeser class in the `$seeders` property.


#### Run the Seeders

After registering the seeders in `Hello\Modules\Core\Seeders\DatabaseSeeder` run this command:

```shell
php artisan db:seed --class="Hello\Modules\Core\Seeders\DatabaseSeeder"
```

To run Specific Seeder class you can specific it's class in the parameter as follow:

```shell
php artisan db:seed --class="your\single\seeder\goes-here"
```





