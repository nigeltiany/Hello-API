###Database Migrations

####Information:

`Migrations` are like version control for the database. 

`Migrations` are very useful for creating and the database tables automatically.

For more information about the `Database Migrations` read [this](https://laravel.com/docs/master/migrations).


####Code sample:

`Migrations` Class (belongs to the `User Module`):

```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;

class CreateUsersTable extends Migration
{
    public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->increments('id');
            
            $table->string('name');
            $table->string('email')->unique();
            $table->string('password');
            
            $table->rememberToken();
            $table->timestamps();
            $table->softDeletes();
            
            $table->integer('somethings_id')->unsigned()->nullable();
            $table->foreign('somethings_id')->references('id')->on('somethings');
        });
    }

    public function down()
    {
        Schema::drop('users');
    }
}

```

####Notes:


`Migrations` should be created inside each `Modue`.

Then using the Core `Service Provider` they will be published to the Framework migrations directory.

So before you are able to use the migration (`php artisan migrate`) you must first publish them (this example will publish all the Module Migrations Files):

```shell
php artisan vendor:publish --provider="Hello\Modules\Core\Providers\CoreServiceProvider"
```










