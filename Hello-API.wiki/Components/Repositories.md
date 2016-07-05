<a name="Repositories"></a>
###Repositories

####Information:

`Repositories` are the implementation of the Repository Design Pattern.

`Repositories` save and retrieve `Models` to or from the underlying storage mechanism.

The `Repository` is used to separate the logic that retrieves the data and maps it to a `Model`, from the business logic that acts on the `Model`.


####Code sample:

`Repository` Class:

```php
use Hello\Modules\Core\Repository\Abstracts\Repository;
use Hello\Modules\User\Contracts\UserRepositoryInterface;
use Hello\Modules\User\Models\User;

class UserRepository extends Repository implements UserRepositoryInterface
{
    protected $fieldSearchable = [
        'name'  => 'like',
        'email' => '=',
    ];

    public function model()
    {
        return User::class;
    }
}
```

Usage from `Task`:

```php
$users = $userRepository->paginate(10);
```

###Notes:

Every `Model` SHOULD have a `Repository`.

MUST not directly access a `Model` to perform any query. Instead this SHOULD be done through a Repository.

All `Repositories` SHOULD extend from `Hello\Modules\Core\Repository\Abstracts\Repository`.

Extending from `Hello\Modules\Core\Repository\Abstracts\Repository` give you all the essential function that a repository could have like (`find`, `create`, `update` and much more), so no need to write them manually.

MUST define the the model searchable fields on the repository to make it easely for the API users to play with your API using the query parameters like (`?search=text`,...)

For more details about what's provided by the Repository Class check out this [documentation](https://github.com/andersao/l5-repository).
