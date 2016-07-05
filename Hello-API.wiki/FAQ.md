##Frequently Asked Questions (FAQ)




### How to upgrade the Framework to the latest Laravel realease?

1. Get a fresh copy of the latest Laravel realease.

1. Copy the the Composer extra requirements and install them.

1. Move the `/src` folder to the new framework folder.

1. Let `composer.json` autoload the `/src` directory (using `psr-4`).

1. Publish the config files and edit them (read some config values from the `.env` file).

1. Register the Master `Service Provider` `Services/Core/Providers/CoreServiceProvider.php` in the Framework.

1. Edit the default middlewears of the `app/Http/Kernel.php`.




<br>
### Where do I put my Front-end code?

The front-end Apps code should be in the `clients/web/` direcotry, separated from the Server (Laravel) App code. 

The front-end App should be able to run as a stand alone App, and it will consume the Server API.

You can configure NGINX to server the Front-end and the Back-end each on a different domain or on subdomains (Example `app.com` for the front-end App and `api.app.com` for the API). 

Check the [Hosting Setup] secion in the [Installation] giude.




<br>
### How to enable Query Caching?

Bu default this feature is turned off.

To turn it on, go to the `.env` file and set `ELOQUENT_QUERY_CACHE=true`. The query result will be cleared on `create`, `update` and `delete`. However all these configurations can be changed from `config/repository.php`.




<br>
### How to Debug Database Queries?

From the `.env` set `DEBUG_DATABASE_QUERIES=true`, to enable query debugging. 

For more controll of the function (print in terminal or only in Log file) open the `src/Services/Core/Framework/Providers/ApiBaseRouteServiceProvider.php` and check the `register` function calling `$this->debugDatabaseQueries(true);`.

The `debugDatabaseQueries` function is defined in the `src/Services/Core/Framework/Traits/CoreServiceProviderTrait.php` file.
