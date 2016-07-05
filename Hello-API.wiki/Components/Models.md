<a name="Models"></a>
###Models

####Information:

`Models` are objects representing data, in the database. (same as in MVC Architecture).

Each `Model` SHOULD define the Relations between itself and any other `Model` from other `Modules` (in case a relation exist).

For more info visit this [link](https://github.com/Mahmoudz/Freestyle-Architecture#Models).

####Code sample:

`Model` Class:

```php
use Hello\Modules\Core\Model\Abstracts\Model;

class Tag extends Model
{
    protected $table = 'tags';

    protected $fillable = [
        'label',
        'user_id'
    ];

    protected $hidden = [];

    public function user()
    {
        return $this->belongsTo(\Hello\Modules\User\Models\User::class);
    }
}

```

####Notes:

Every `Model` SHOULD extend from `Hello\Modules\Core\Model\Abstracts\Model`.

A `Model` SHOULD only hold code and data the represents itself *(it's relationships with other models, hidden fields, table name, fillabale attributes,...)*.










