<a name="Tests"></a>
###Tests

####Information:

The two most essential `Tests` types in this architecture are the Unit Tests and the Functional Tests.

`Modules` CAN be covered by Functional `Tests`, (Example testing the `Routes` are doing what's expected from them).

`Services` CAN be covered by Unit `Tests`.


####Code sample:

Functional `Test` Class:

```php
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Hello\Modules\Core\Test\Abstracts\TestCase;

class LoginEndpointTest extends TestCase
{
    use DatabaseMigrations;

    private $endpoint = '/login';

    public function testLoginExistingUser_()
    {
        $name = 'Hello';
        $email = 'testing@hello.dev';
        $password = 'secret';

        $userDetails = [
            'name'     => $name,
            'email'    => $email,
            'password' => $password,
        ];

        // get the logged in user (create one if no one is logged in)
        $this->registerAndLoginTestingUser($userDetails);

        $data = [
            'email'    => $email,
            'password' => $password,
        ];

        // send the HTTP request
        $response = $this->apiCall($this->endpoint, 'post', $data, false);

        // assert response status is correct
        $this->assertEquals($response->getStatusCode(), '200');

        $this->assertResponseContainKeyValue([
            'email' => $email,
            'name'  => $name
        ], $response);

        $this->assertResponseContainKeys(['id', 'token'], $response);
    }
...
```


####Notes:

All the `Tests` SHOULD extend from `Hello\Modules\Core\Test\Abstracts\TestCase`.

*(Additional `Tests` types are Integration Tests and Acceptance Tests).*



###Knowledge Base:

####Testing Helper Functions:

*All your test Classes have access to these functions*

```php
apiCall($endpoint, $verb = 'get', $data = [], $protected = true, $header = [])
```
```php
assertValidationErrorContain($response, array $messages)
```
```php
getLoggedInTestingUser()
```
```php
getLoggedInTestingUserToken()
```
```php
registerAndLoginTestingUser($userDetails = null)
```
```php
assertResponseContainKeys($keys, $response)
```
```php
assertResponseContainValues($values, $response)
```
```php
assertResponseContainKeyValue($data, $response)
```
```php
ddj($json)
```
```php
migrateDatabase()
```

To edit these functions go to `src/Services/Core/Test/Traits/TestingTrait.php`.
