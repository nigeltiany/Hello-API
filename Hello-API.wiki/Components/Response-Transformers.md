<a name="Response-Transformers"></a>
###Response Transformers

####Information:

`Transformers` are responsible for taking an instance of a `Model` or a collection of `Models` or instance of Paginator and converting it to a formatted Array that is easy to be *Serialized*.

For more information about the `Transformers` read [this](http://fractal.thephpleague.com/transformers/).


####Code sample:

`Transformer` Class:

```php
use Hello\Modules\Core\Transformer\Abstracts\Transformer;
use Hello\Modules\User\Models\User;

class UserTransformer extends Transformer
{
    public function transform(User $user)
    {
        return [
            'id'    => (int) $user->id,
            'name'  => $user->name,
            'email' => $user->email,
            'boss'  => (bool) $user->isBoss,
        ];
    }
}
```

Usage with Model:

```php
// getting any Model
$user = $this->getUser();

// building the response with the transformer of the Model
$this->response->item($user, new UserTransformer());
```

Usage with Paginator:

```php
// getting many Models Paginated
$users = $this->getUsers();

// building the response with the transformer of the Model
return $this->response->paginator($users, new UserTransformer());
```

<br>

`Transformer` Class with relationships:


You can request data with their relationships directly from the API call using `include=tags,user`. But first the Transformer need to have the `availableIncludes` defined with their functions like this:

```php
namespace Hello\Modules\Account\Transformers;

use Hello\Modules\Core\Transformer\Abstracts\Transformer;
use Hello\Modules\Account\Models\Account;
use Hello\Modules\Tag\Transformers\TagTransformer;
use Hello\Modules\User\Transformers\UserTransformer;

class AccountTransformer extends Transformer
{
    protected $availableIncludes = [
        'tags',
        'user',
    ];

    public function transform(Account $account)
    {
        return [
            'id'       => (int)$account->id,
            'url'      => $account->url,
            'username' => $account->username,
            'secret'   => $account->secret,
            'note'     => $account->note,
        ];
    }

    public function includeTags(Account $account)
    {
        return $this->collection($account->tags, new TagTransformer());
    }

    public function includeUser(Account $account)
    {
        return $this->item($account->user, new UserTransformer());
    }

}

```

Now to get the `Tags` with the response when Accounts are requested pass the `?include=tags` parameter with the [GET] request.

To get Tags with User use the comma separator: `?include=tags,user`.





####Notes:

Each `Transformer` MUST have a `transform` function

Every `Transformer` SHOULD extend from `Hello\Modules\Core\Transformer\Abstracts\Transformer`.

For more information about the `Transformers` concept, read [this](http://fractal.thephpleague.com/transformers/).
