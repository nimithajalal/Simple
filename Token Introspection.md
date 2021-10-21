



# Getting Started

Token Api introspection API will help the partners to generate access/refresh token and return metadata information. 

# URL 

POST https://www.linkedin.com/oauth/v2/introspectToken

# Header

| Header Name  | Description            | Required |
| ------------ | ---------------------- | -------- |
| Content-Type | x-www-form-url-encoded | Required |

# Methods

| Method | Description                 |
| ------ | --------------------------- |
| POST   | Token Introspection Request |

# Query Parameters

| Element   | Description           | Type   | Required | Notes                                                        |
| --------- | --------------------- | ------ | -------- | ------------------------------------------------------------ |
| `Client_ID` | Application Client ID | String | Required | `Client_ID` of the third party application required for authentication. |
| `Client_Secret` | Application Client Secret | String | Required | `Client_Secret` of the third party application required for authentication |
| `Token` | Access token or the refresh token | String | Required | Access token or refresh token returned from the token endpoint. Refer [ Token Introspect Auth](POST /oauth/v2/introspect HTTP/1.1) from the References section to know more. |

# Sample Request
 ``` 
 POST /oauth/v2/introspect HTTP/1.1
 Host: https://www.linkedin-ei.com
 Accept: application/json
 Content-Type: application/x-www-form-urlencoded
 
 token=<token_to_be_introspected>&client_id=<client_id>&client_secret=<client_secret>
 
 ```



# Response

A successful token introspection request returns a JSON object containing the following fields:

| Element | Type                                              | Description                                                  |
| ------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Active  | Boolean | Indicator of whether or not the presented token is currently active. Values: Active/Inactive |
| Status  | String                                   | Status of the token.                                         |
| scope   | String                      | Scopes associated with this token. Eg : `r_basicprofile`   |
|Client_ID | String | Client identifier for the OAuth 2.0 client that requested this token. |
| created_at | Integer | Timestamp measured in the number of seconds since January 1 1970 UTC, indicating when this token was originally issues. |
| expires_at | Integer | Timestamp measured in the number of seconds since January 1 1970 UTC, indicating when this token was originally issues. |
| authorized_at | Integer | Timestamp, measured in the number of seconds since January 1 1970 UTC, indicating when this token was originally issues. |

# Sample Response

## Token revoked:

```Curl
curli -d 'token=AQWLmNqvW4JCbEePhbGpLhr7OesejxQC9YhxisJvIY2t6Pv8zCjGksak3NaLt4gBgU1dyV8SdX5X2fA1ebcJ7eVdvwX7Ii_m3pSr_2OveUf4NpAr5vnkeNJXa7av6KBn4IKQhJ7ao0YqI91g6miZ3puQBksYFoTtckOBVvH4z-T_C4it5kcVsGTKcvZn5aQ9JdNABKTLhSeoFu6Q52cRWWaT_jbdHU6E4jjazjNQUKOZiKA6h5pnh2ppSJcQUUwCvBiSfiA2oe205Kp3txqvYkPdkDrEHuCqlUHDixQhWcepWL3pkV4fKLLj9kNJq0X2dCRYLSuTCZXYuye6yYsDfxmwt1Dp_Q&client_id=84o1i5mjq59xuv&client_secret=Yn4GaPGMZSwmG2J3' https://www.linkedin-ei.com/oauth/v2/introspectToken -v -H "Content-Type: application/x-www-form-urlencoded"
```



```   {
    "active": false,
    "client_id": "84o1i5mjq59xuv",
    "created_at": 1587497291083,
    "status": "revoked",
    "expires_in": 1587497620127,
    "scope": "r_basicprofile,rw_organization,w_share"
}
```

Similar responses will be returned for the below types of responses as well:

- Token Expired
- Valid Token
- Passedin client information doesn’t match the token information

# Status codes and Errors

| Code | Description       | Notes                                                    |
| ---- | ----------------- | -------------------------------------------------------- |
| 401  | Unauthorized      | If client credentials passed in the request is not valid |
| 429  | Too Many Requests | If app hits fuse throttling for this endpoint.           |

# References

Please refer the link for more information on OAuth 2.0 Token Introspection : https://tools.ietf.org/html/rfc7662 

