###The Headers:

####Request Header

Every request to the API must contain `Accept:application/json` header.

Every protected request must include the JWT Token in the Authorization header like this: `Authorization: Bearer {JWT Token}`.

**Request Header example:**

```
Accept:application/json
Authorization:Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjQsImlzc...
```

####Response Header

Every response contain API Limit `X-RateLimit-Limit:100` and the remaining calls `X-RateLimit-Remaining:77`.

**Response Header example:**

```
Cache-Control:private, must-revalidate
Connection:keep-alive
Content-Type:application/json
Date:Tue, 11 Nov 2011 11:11:11 GMT
ETag:"244216122606707c90d40b45d8f85da1"
Server:nginx/1.8.0
Transfer-Encoding:chunked
X-RateLimit-Limit:100
X-RateLimit-Remaining:77
X-RateLimit-Reset:1458641529
```

###The Payload:



**Specification:**

The default format uses the following skeleton:

```json
{
  "data": [
    {
      "id": 100,
      ...
      "relation 1": {
        "data": [
          {
            "id": 11,
			  ...
          }
        ]
      },
      "relation 2": {
        "data": {
          "id": 22,
          ...
          }
        }
      }
    },
    ...
  ],
  "meta": {
    "pagination": {
      "total": 999,
      "count": 999,
      "per_page": 999,
      "current_page": 999,
      "total_pages": 999,
      "links": {
        "next": "http://api.hello.dev/accounts?page=999"
      }
    }
  }
}
```


**Pagination:**

When data is paginated the response payload will contain a `meta` description about the pagination.

```json
  "meta": {
    "pagination": {
      "total": 18,
      "count": 10,
      "per_page": 10,
      "current_page": 1,
      "total_pages": 2,
      "links": {
        "next": "http://api.hello.dev/accounts?page=2"
      }
    }
  }
```



**Real Response Sample:**

```json
{
  "data": [
    {
      "id": 1,
      "url": "www.facebook.com",
      "username": "Mahmoudz",
      "secret": "password#123",
      "note": "whatever it's just an account",
      "tags": {
        "data": [
          {
            "id": 2,
            "label": "Social",
            "user_id": 1,
            "created_at": {
              "date": "-0001-11-30 00:00:00.000000",
              "timezone_type": 3,
              "timezone": "UTC"
            },
            "updated_at": {
              "date": "-0001-11-30 00:00:00.000000",
              "timezone_type": 3,
              "timezone": "UTC"
            }
          },
          {
            "id": 3,
            "label": "Code",
            "user_id": 1,
            "created_at": {
              "date": "-0001-11-30 00:00:00.000000",
              "timezone_type": 3,
              "timezone": "UTC"
            },
            "updated_at": {
              "date": "-0001-11-30 00:00:00.000000",
              "timezone_type": 3,
              "timezone": "UTC"
            }
          }
        ]
      },
      "user": {
        "data": {
          "id": 1,
          "name": "Mahmoud Zalt",
          "email": "mahmoud@something.com",
          "token": null,
          "created_at": {
            "date": "2016-04-09 02:34:11.000000",
            "timezone_type": 3,
            "timezone": "UTC"
          },
          "updated_at": {
            "date": "2016-04-09 02:34:11.000000",
            "timezone_type": 3,
            "timezone": "UTC"
          }
        }
      }
    },
    {
      "id": 2,
      "url": "www.facebook.com",
      "username": "Mahmoudz",
      "secret": "password#123",
      "note": "whatever it's just an account",
      "tags": {
        "data": [
          {
            "id": 3,
            "label": "Code",
            "user_id": 1,
            "created_at": {
              "date": "-0001-11-30 00:00:00.000000",
              "timezone_type": 3,
              "timezone": "UTC"
            },
            "updated_at": {
              "date": "-0001-11-30 00:00:00.000000",
              "timezone_type": 3,
              "timezone": "UTC"
            }
          }
        ]
      },
      "user": {
        "data": {
          "id": 1,
          "name": "Mahmoud Zalt",
          "email": "mahmoud@something.com",
          "token": null,
          "created_at": {
            "date": "2016-04-09 02:34:11.000000",
            "timezone_type": 3,
            "timezone": "UTC"
          },
          "updated_at": {
            "date": "2016-04-09 02:34:11.000000",
            "timezone_type": 3,
            "timezone": "UTC"
          }
        }
      }
    },
    ...
  ],
  "meta": {
    "pagination": {
      "total": 20,
      "count": 10,
      "per_page": 10,
      "current_page": 1,
      "total_pages": 2,
      "links": {
        "next": "http://api.hello.dev/accounts?page=2"
      }
    }
  }
}
```





**Response Error format:**

```json
{
  "message": "error message goes here",
  "status_code": 500,
  "code": 105
}
```

**Validation error:**

```json
{
    "message": "Could not create new user.",
    "status_code": 422,
    "errors": {
    	"username": [
        	"The username field is required."
    	],
        	"password": [
        	"The password field is required."
    	]
	}
}
```




<br>
###Changing the Response payload format

The default response format (specification) is the `DataArray` Fractal Serializer.

To change the default Fractal Serializer open the `.env` file and change the 

```
FRACTAL_SERIALIZER=DataArray
```

The Supported Serializers are (`JsonApi`, `DataArray` and `Array`).

Check out the `overrideDefaultFractalSerializer()` inside the `boot()` function of the `src/Services/Core/Framework/Providers/CoreServiceProvider.php` file.

### More
For more details check out this [link](https://github.com/dingo/api/wiki/Errors-And-Error-Responses)


