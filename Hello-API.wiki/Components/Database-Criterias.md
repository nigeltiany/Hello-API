<a name="Database Criterias"></a>
###Database Criterias

####Information:

`Criterias` are used to apply query condition when retrieving data from the database through a `Repository`.

For more information about the `Criteria` read [this](https://github.com/andersao/l5-repository#create-a-criteria).


####Code sample:

`Criteria` Class:

```php
use Hello\Modules\Core\Repository\Abstracts\Criteria;
use Prettus\Repository\Contracts\RepositoryInterface as PrettusRepositoryInterface;

class OrderByCreationDateDescendingCriteria extends Criteria
{
    public function apply($model, PrettusRepositoryInterface $repository)
    {
        return $model->orderBy('created_at', 'desc');
    }
}

```

Usage from `Task`:

```php
    public function run()
    {
        $this->userRepository->pushCriteria(new OrderByCreationDateDescendingCriteria);

        $users = $this->userRepository->paginate();

        return $users;
    }
```

<br>


`Criteria` Class that accepts data:

```php
namespace Hello\Modules\Core\Repository\Criterias\Eloquent;

use Hello\Modules\Core\Repository\Abstracts\Criteria;
use Prettus\Repository\Contracts\RepositoryInterface as PrettusRepositoryInterface;

class ThisUserCriteria extends Criteria
{

    private $userId;

    public function __construct($userId)
    {
        $this->userId = $userId;
    }

    public function apply($model, PrettusRepositoryInterface $repository)
    {
        return $model->where('user_id', '=', $this->userId);
    }
}

```

Passing data from `Task` to `Criteria`:

```php
    public function run($user)
    {
        $this->accountRepository->pushCriteria(new ThisUserCriteria($user->id));

        $accounts = $this->accountRepository->paginate();

        return $accounts;
    }
```

####Notes:

`Criteria` SHOULD only be used from a `Task`.

Every `Criteria` must have an `apply` function.

A `Criteria` MUST not contain any extra code, if it needs data, the data SHOULD be passed to it from the `Task`. It SHOULD not call any `Task` for data.

There are `Criterias` specific to a `Module` and `Criterias` general that can be used across multiple `Modules`. The specific `Criterias` SHOULD be created inside the `Module` while the general `Criterias` SHOULD be created in `src/Services/Core/Repository/Criterias/Eloquent`.
