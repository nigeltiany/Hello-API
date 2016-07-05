<a name="Tasks"></a>
###Tasks

####Information:

`Tasks` are responsible of performing whatever the end user need (Create, Update, Query,...).

Each `Task` has single responsibility and is to handle specific Job.

`Modules` SHOULD have `Tasks` per functionality (each functionality should be wrapped in a `Task`).

The `Task` can do anything inside it's `Module` (use anything internally), and can use external `Services`.

A `Task` can receive and return `Data`. (`Tasks` SHOULD not return a response, the `Controller` job is to return a response).

The `Tasks` concept is pretty much similar to the `Commands` concept in a Command-Oriented Architecture.

For more info visit this [link](https://github.com/Mahmoudz/Freestyle-Architecture#Tasks).



####Code sample:

`Task` Class, performing some job in the run function:

```php
use Exception;
use Illuminate\Support\Facades\Hash;
use Hello\Modules\Core\Task\Abstracts\Task;
use Hello\Modules\User\Contracts\UserRepositoryInterface;
use Hello\Modules\User\Exceptions\AccountFailedException;
use Hello\Services\Authentication\Portals\AuthenticationService;

class CreateUserTask extends Task
{
    private $userRepository;

    private $authenticationService;

    public function __construct(UserRepositoryInterface $userRepository, AuthenticationService $authenticationService)
    {
        $this->userRepository = $userRepository;
        $this->authenticationService = $authenticationService;
    }

    public function run($email, $password, $name, $login = false)
    {
        $hashedPassword = Hash::make($password);

        try {
            // create new user
            $user = $this->userRepository->create([
                'email'    => $email,
                'password' => $hashedPassword,
                'name'     => $name,
            ]);
        } catch(Exception $e) {
            throw (new AccountFailedException())->debug($e);
        }

        if ($login) {
            $user = $this->authenticationService->loginFromObject($user);
        }

        return $user;
    }
}
```

`Task` usage from a `Controller`:

```php
// create and login (true parameter) the new user
$user = $createUserTask->run(
    $registerRequest['email'],
    $registerRequest['password'],
    $registerRequest['name'],
    true
);
```

####Notes:

A `Task` class has one function `run` and can only be called from `Controllers`.

`Tasks` SHOULD only be called from `Controllers`.
