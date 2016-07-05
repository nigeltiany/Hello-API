<a name="Modules"></a>
###Modules

####Information:


For all info about a `Module` visit this [link](https://github.com/Mahmoudz/Freestyle-Architecture#Modules).


###Notes:

You MUST define every `Module` dependancies in the `config/modules.php` config file (to make it easier for you to track what depend on what), as follow:

```
'User' => [
    'dependencies' => [
        'modules'  => [],
        'services' => [
            'Core',
            'Authentication'
        ],
    ],
],
],
```
In this example the User module depends on the Core and Authentication Services.



###Knowledge Base:

####Register a Module:

After creating a new `Module` you must register it in the `config/modules.php` config file.

Example: registereing a `User`, `Tag` and `List` Modules

```
'modules' => [
    'namespace' => 'Hello',

    'register' => [
        'User' => [
            'routes' => [
                'api' => [
                    ['fileName' => 'v1', 'versionNumber' => '1']
                ],
                'web' => [
                    ['fileName' => 'main']
                ]
            ]
        ],
        'Tag' => [
            'routes' => [
                'api' => [
                    ['fileName' => 'anything', 'versionNumber' => '2']
                ],
            ]
        ],
        'List' => [ ],
    ],

],
```

You must always have the `Namespace` variable defined.