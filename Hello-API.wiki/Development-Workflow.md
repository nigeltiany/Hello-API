###Before coding

1. Write the use case scenario of the app, (listing all the functionalities).

1. Write the objects (models) of the application with their attributes and relationships.


###Setup

1. Get a copy of the `Hello API` Starter.

1. Create a Module *(just an empty folder on the Modules layer)*.

1. Register the Module in the `config/modules.php` config file.

1. Create the Main `Service Provider` for this Module, (name it based on its Module name).


###Write API Documentation

1. Create `Routes` files. And register them in the config file.

1. Write your Endpoints as comments in the `Routes` file *(to be implemented 1 by 1 during the development*).

1. Write the DocBlock for each `Endpoint` and generate a documentation (with the API DOC JS tool).

1. Share the Documentation with the client and get it approved.


###Create Module 
*(repeat these steps for every Module, with steps 2 from the above section)*


1. Create a `Model` in the Module folder *(could have more than one)*.

1. Add the relationships between the `Models`, in case you have many `Models`.

1. Create a `Migration` file for every `Model`.

1. Create a `Repository` for every `Model`.

1. Creare a `Repository Interface` for every `Repository`, and bind the interfaces with the implementations in the `Module` main `Service Provider`.

1. Create `Model Factory` (Fakers) for every Model.

1. Create an empty Tests folder and include it's path in the TestSuite of the phpunit XML config file `phpunit.xml`

###Implement Endpoint 
*(repeat these steps for every Endpoint)*

1. Implement an `Endpoint` (Choose any `Endpoint` from the `Route` file DocBlock and implement it).

1. Create a `Controller` to handle that `Endpoint`.

1. Create a `Test` class, to test your `Endpoint` while working on it. (The first test function should make a call to the `Endpoint` where the `Controller` is printing `Hello Route`).

1. If the `Controller` expected to receive Data, create a `Request` and define the Validation rules.

1. Create a `Task` and write all the business logic here. 

1. If the `Task` needs to deal with Data, inject the Model `Repository`

1. If the `Task` is collecting data, create a `Criteria` to apply some conditions on the query.

1. Go back to the `Test` file of the `Endpoint`, and write the tests and assertions of the success and failure scnarios.

###Configurations (Optional)

1. Check the environments variables in the `.env` and `phpunit.xml` files.

1. Check all the files in the `config/`, most importantly the the `config/modules.php`.







