Generate an API Documenation from the DocBlock in the Routes files.

### Requirement

`Hello API` is using the [Api Doc Js](http://apidocjs.com/) tool, to read the PHP DocBlock and generate Helloan HTML Documentation. 

*(so make sure you have [ApiDocJs](http://apidocjs.com/#install) installed first).*


### Convention
As convention, all the Endpoints DocBlocks should be written in the Routes files.


### Usage

1 - Run this command from the root directory:

```shell
apidoc -f .php -i src -o public/documentation
```

>Every time you do changes in the DocBlock of the Routes file you need to run this command.

2 - visit this domain `http://api.hello.dev/documentation/`

### Reusable DockBlocks across different Routes files
The reusable DocBlocks can be defined in this file `src/Services/ApiDocs/ApiDocs.php`, they will automatically be detected and used in any of your routes files.

### Documentation Code
The documentation code is in `public/documentation`


### Documentation Configuration
Edit the `apidoc.json` file on the root of your project.

```json
{
  "name": "Hello API",
  "version": "1.0.0",
  "description": "Hello API Description",
  "title": "Hello API TITLE",
  "url" : "https://api.hello.dev"
}
```

