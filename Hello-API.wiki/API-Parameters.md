Users often need to control the data request, thus the Hello API support out of the box the most useful parameters.


### Parameters
*(You can include these parameters on almost every `[GET]` endpoint).*


####Locating:

```
?page=22
```

####Sorting & Ordering:
```
?orderBy=id&sortedBy=asc
```

```
?orderBy=created_at&sortedBy=desc
```

####Searching:

```
?search=John%20Doe
```
Notice should replace the space with `%20`.


#####Define search fields for search:

```
?search=name:John Doe;email:john@main.com
```

#####Define the query condition for search:

```
?searchFields=name:like
```

```
?searchFields=email:=
```

```
?searchFields=name:like;email:=
```

```
?search=git&searchFields=url:like
```

####Filtering:

Select your columns:

```
?search=git&filter=id;url;note
```


####Relationships:
Get an object with his relationships:

using `include` with comma `,` separator:

```
include=tags,user
```
For this to work the `Transformer` should have the relationships defined on it. *Check the Transformer Page.*

####Caching:
By default the API has caching enableded if you want to skip the cahe and perform a query you can use this parameter:

```
?skipCache=true
```

Not recommanded to keep skipping cache as it has bad impact on the performance.


### Configuration
Most of these request paraemters are configurable from the `config/repository.php` file.


### More
For more details on these parameters check out these links:

- [l5-repository](https://github.com/andersao/l5-repository#example-the-criteria)
- [Fractal Transformers](http://fractal.thephpleague.com/transformers/)


