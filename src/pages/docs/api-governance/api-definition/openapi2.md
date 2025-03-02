---
title: "OpenAPI 2.0 warnings"
updated: 2022-07-20
contextual_links:
  - type: section
    name: "Prerequisites"
  - type: link
    name: "API definition warnings"
    url: "https://learning.postman.com/docs/api-governance/api-definition/api-definition-warnings/"
  - type: section
    name: "Additional Resources"
  - type: subtitle
    name: "Blog Posts"
  - type: link
    name: "Introducing Security Warnings During API Validation"
    url: "https://blog.postman.com/security-warnings-during-api-validation/"
  - type: subtitle
    name: "Public Workspaces"
  - type: link
    name: "Postman Security"
    url:  "https://www.postman.com/postman/workspace/62d58d93-7e0c-45bf-9daa-cc8e531fc344"
search_keyword: "api security, api schema, security warnings, schema validation, security validation, api security audit, api security scan, api schema vulnerabilities, security audit, openapi 2.0"
---

You can use Postman to identify any potential security and formatting issues when defining your API.

> **Format linting for [API information](#api-information), [Operations](#operations), and [Models](#models) is in beta.** During the beta period, this feature may not be available to all Postman users and is subject to potential change.

<img alt="Security warnings for OpenAPI 2.0" src="https://assets.postman.com/postman-docs/security-warnings-openapi-2-v9.jpg"/>

### Warnings for OpenAPI 2.0

For all APIs defined in OpenAPI 2.0, the following list describes possible warning messages and potential ways to resolve them.

* [Broken object level authorization](#broken-object-level-authorization)
    * [Scope for OAuth scheme used in security field is not defined in the securityDefinition declaration](#scope-for-oauth-scheme-used-in-security-field-is-not-defined-in-the-securitydefinition-declaration)
    * [Scope for OAuth scheme used is not defined in the securityDefinition declaration](#scope-for-oauth-scheme-used-is-not-defined-in-the-securitydefinition-declaration)
* [Broken user authentication](#broken-user-authentication)
    * [Security field is not defined](#security-field-is-not-defined)
    * [Security field does not contain any item](#security-field-does-not-contain-any-item)
    * [Security field does not contain any scheme](#security-field-does-not-contain-any-scheme)
    * [Security definition object not defined](#security-definition-object-not-defined)
    * [Security definition object does not contain any scheme](#security-definition-object-does-not-contain-any-scheme)
    * [Scheme used in security field is not defined in the security definition object](#scheme-used-in-security-field-is-not-defined-in-the-security-definition-object)
    * [Security field for the operation does not contain any item](#security-field-for-the-operation-does-not-contain-any-item)
    * [Security field for the operation does not contain any scheme](#security-field-for-the-operation-does-not-contain-any-scheme)
    * [Operation does not enforce any security scheme](#operation-does-not-enforce-any-security-scheme)
* [Excessive data exposure](#excessive-data-exposure)
    * [API accepts credentials from OAuth authentication in plain text](#api-accepts-credentials-from-oauth-authentication-in-plain-text)
    * [API accepts API key in plain text](#api-accepts-api-key-in-plain-text)
    * [API accepts basic authentication credentials in plain text](#api-accepts-basic-authentication-credentials-in-plain-text)
    * [Global schemes have HTTP scheme defined](#global-schemes-have-http-scheme-defined)
    * [Operation accepts credentials from OAuth authentication in plain text](#operation-accepts-credentials-from-oauth-authentication-in-plain-text)
    * [Operation accepts API key in plain text](#operation-accepts-api-key-in-plain-text)
    * [Operation accepts basic authentication credentials in plain text](#operation-accepts-basic-authentication-credentials-in-plain-text)
    * [Schemes of the operation have HTTP scheme defined](#schemes-of-the-operation-have-http-scheme-defined)
    * [Authorization URL uses HTTP protocol. Credentials will be transferred as plain text](#authorization-url-uses-http-protocol-credentials-will-be-transferred-as-plain-text)
    * [Token URL uses HTTP protocol](#token-url-uses-http-protocol)
    * [Produces field is not defined](#produces-field-is-not-defined)
    * [Produces field does not contain any item](#produces-field-does-not-contain-any-item)
    * [Produces field for the operation does not contain any item](#produces-field-for-the-operation-does-not-contain-any-item)
    * [Operation does not contain produces field](#operation-does-not-contain-produces-field)
* [Injection](#injection)
    * [Consumes field is not defined](#consumes-field-is-not-defined)
    * [Consumes field does not contain any item](#consumes-field-does-not-contain-any-item)
    * [Consumes field for the operation does not contain any item](#consumes-field-for-the-operation-does-not-contain-any-item)
    * [Operation does not contain consumes field](#operation-does-not-contain-consumes-field)
* [Improper assets management](#improper-assets-management)
    * [OAuth authentication uses the deprecated implicit flow](#oauth-authentication-uses-the-deprecated-implicit-flow)
    * [OAuth authentication uses the deprecated password flow](#oauth-authentication-uses-the-deprecated-password-flow)
* [API information](#api-information)
    * [API must have contact information available](#api-must-have-contact-information-available)
    * [API must have a contact email available](#api-must-have-a-contact-email-available)
    * [API must have a contact name available](#api-must-have-a-contact-name-available)
    * [API must have a contact URL available](#api-must-have-a-contact-url-available)
    * [The info object should have a description](#the-info-object-should-have-a-description)
    * [The info object should have a license](#the-info-object-should-have-a-license)
    * [The info object should have a license URL](#the-info-object-should-have-a-license-url)
    * [The info object should have a terms of service](#the-info-object-should-have-a-terms-of-service)
    * [The info object should have an API ID extension](#the-info-object-should-have-an-api-id-extension)
    * [The info object should have an audience extension](#the-info-object-should-have-an-audience-extension)
    * [There should be no empty paths](#there-should-be-no-empty-paths)
    * [There should be no trailing slashes on paths](#there-should-be-no-trailing-slashes-on-paths)
    * [There should be a central tags object](#there-should-be-a-central-tags-object)
    * [All tags should have a description](#all-tags-should-have-a-description)
    * [There should be at least one tag](#there-should-be-at-least-one-tag)
* [Operations](#operations)
    * [All operations should have descriptions](#all-operations-should-have-descriptions)
    * [All operations should have summaries](#all-operations-should-have-summaries)
    * [Operation summaries shouldn't end with a period](#operation-summaries-shouldnt-end-with-a-period)
    * [All operations should have tags](#all-operations-should-have-tags)
    * [All operations should have at least one tag](#all-operations-should-have-at-least-one-tag)
    * [All parameters should have descriptions](#all-parameters-should-have-descriptions)
    * [All parameters should have examples](#all-parameters-should-have-examples)
    * [POST methods should have request bodies](#post-methods-should-have-request-bodies)
    * [PUT methods should have request bodies](#put-methods-should-have-request-bodies)
    * [PATCH methods should have request bodies](#patch-methods-should-have-request-bodies)
    * [DELETE operations shouldn't have a response body](#delete-operations-shouldnt-have-a-response-body)
    * [DELETE operations should have a 204 status code for the response](#delete-operations-should-have-a-204-status-code-for-the-response)
    * [DELETE operations should have a 500 status code for the response](#delete-operations-should-have-a-500-status-code-for-the-response)
    * [GET operations should have a 200 status code for the response](#get-operations-should-have-a-200-status-code-for-the-response)
    * [GET operations should have a 500 status code for the response](#get-operations-should-have-a-500-status-code-for-the-response)
    * [PATCH operations should have a 200 status code for the response](#patch-operations-should-have-a-200-status-code-for-the-response)
    * [PATCH operations should have a 500 status code for the response](#patch-operations-should-have-a-500-status-code-for-the-response)
    * [POST operations should have a 201 status code for the response](#post-operations-should-have-a-201-status-code-for-the-response)
    * [POST operations should have a 500 status code for the response](#post-operations-should-have-a-500-status-code-for-the-response)
    * [PUT operations should have a 200 status code for the response](#put-operations-should-have-a-200-status-code-for-the-response)
    * [PUT operations should have a 500 status code for the response](#put-operations-should-have-a-500-status-code-for-the-response)
* [Models](#models)
    * [All schemas should have descriptions](#all-schemas-should-have-descriptions)
    * [All schemas should have properties](#all-schemas-should-have-properties)
    * [Integer format should be int32 or int64](#integer-format-should-be-int32-or-int64)
    * [Number format should be decimal32, decimal64, float, double, or decimal128](#number-format-should-be-decimal32-decimal64-float-double-or-decimal128)
    * [Arrays must have minItems and maxItems defined](#arrays-must-have-minitems-and-maxitems-defined)
    * [All schema properties should have descriptions](#all-schema-properties-should-have-descriptions)
    * [All schema properties should have a type property](#all-schema-properties-should-have-a-type-property)
    * [All schemas should have a required property](#all-schemas-should-have-a-required-property)
    * [All schemas should have a type property](#all-schemas-should-have-a-type-property)

## Broken object level authorization

### Scope for OAuth scheme used in security field is not defined in the securityDefinition declaration

| Issue description | Possible fix |
| ----------- | ----------- |
| The OAuth2 scopes used in the global security field need to be defined in the security schemes field. Otherwise, an attacker can introduce their scopes to fill the gap and exploit the system. | Make sure that all the OAuth2 scopes used are defined in the OAuth2 security scheme. |

#### Resolution

```json
swagger: '2.0'
#...
security:
  - OAuth2:
    - read
    - write
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    scopes:
      read: read object
      write: writes object
    authorizationUrl: https://example.com/authorize
    tokenUrl: https://example.com/token
```

&nbsp;

### Scope for OAuth scheme used is not defined in the securityDefinition declaration

| Issue description | Possible fix |
| ----------- | ----------- |
| The OAuth2 scopes used in the  security field of the operation need to be defined in the security schemes field. Otherwise, an attacker can introduce their scopes to fill the gap and exploit the system. | Make sure that all the OAuth2 scopes used are defined in the OAuth2 security scheme. |

#### Resolution

```json
swagger: '2.0'
#...
paths:
  "/user":
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      operationId: listUser
      security:
        - OAuth2:
          - read
          - write
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    scopes:
      read: read object
      write: writes object
    authorizationUrl: https://example.com/authorize
    tokenUrl: https://example.com/token
```

&nbsp;

## Broken user authentication

### Security field is not defined

| Issue description | Possible fix |
| ----------------- | ------------ |
| If the global security field isn't defined, the API doesn't require any authentication by default. Anyone can access the API operations that don't have a security field defined. | The security field needs to be defined in the schema. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  basicAuth:
    type: basic
security:
    - basicAuth: []
```

&nbsp;

### Security field does not contain any item

| Issue description | Possible fix |
| ----------------- | ------------ |
| If the security field contains an empty array, no security scheme is applied to the operations by default. | The security field needs to contain at least one item in the array. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  basicAuth:
    type: basic
security:
    - basicAuth: []
```

&nbsp;

### Security field does not contain any scheme

| Issue description | Possible fix |
| ----------------- | ------------ |
| An empty object in the security field deactivates the authentication completely. Without security fields defined for each operation, anyone can access the API operations without any authentication. | Security field array items can't contain an empty object. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  basicAuth:
    type: basic
security:
    - basicAuth: []
```

&nbsp;

### Security definition object not defined

| Issue description | Possible fix |
| ----------- | ----------- |
| The components object of the API doesn't declare any security definitions which can be used in the security field of the API or individual operations. | Security definitions need to be defined in the schema of the component. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  basicAuth:
    type: basic
```

&nbsp;

### Security definition object does not contain any scheme

| Issue description | Possible fix |
| ----------- | ----------- |
| An empty object in the reusable security definition means that no authentication scheme is defined for each operation, anyone can access the API operations without any authentication. | Security definitions need to contain at least one item in the object. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  basicAuth:
    type: basic
```

&nbsp;

### Scheme used in security field is not defined in the security definition object

| Issue description | Possible fix |
| ----------- | ----------- |
| The authentication scheme used in global or operation security field isn't defined in the security definition object. | The scheme used in the security field needs to be defined in the security definition object. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  basicAuth:
    type: basic
security:
    - basicAuth: []
```

&nbsp;

### Security field for the operation does not contain any item

| Issue description | Possible fix |
| ----------- | ----------- |
| No security scheme is applied to the API operation by default. | The security field in any operation needs to contain at least one item in the array. |

#### Resolution

```json
swagger: '2.0'
#...
paths:
  /user:
    get:
      description: 'Returns details about a particular user'
      security:
          - basicAuth: []
      #...
securityDefinitions:
  basicAuth:
    type: basic
```

&nbsp;

### Security field for the operation does not contain any scheme

| Issue description | Possible fix |
| ----------- | ----------- |
| An empty object in the security field deactivates the authentication completely for the operation. Anyone can access the API operation without any authentication. | Specify at least one security requirement in the operation. |

#### Resolution

```json
swagger: '2.0'
#...
paths:
  /user:
    get:
      description: 'Returns details about a particular user'
      security:
          - basicAuth: []
      #...
securityDefinitions:
  basicAuth:
    type: basic
```

&nbsp;

### Operation does not enforce any security scheme

| Issue description | Possible fix |
| ----------- | ----------- |
|  If both the global security field and operation’s security field aren't defined, anyone can access the API without any authentication. | Define a security field in the operation. |

#### Resolution

```json
swagger: '2.0'
#...
paths:
  /user:
    get:
      description: 'Sample endpoint: Returns details about a particular user'
      security:
          - basicAuth: []
      #...
securityDefinitions:
  basicAuth:
    type: basic
```

&nbsp;

## Excessive data exposure

### API accepts credentials from OAuth authentication in plain text

| Issue description | Possible fix |
| ----------- | ----------- |
| The access tokens are sent as plain text over an unencrypted network. Attackers can intercept the access tokens by listening to the network traffic in a public Wi-Fi network. | Make sure that the scheme used in the schemes array is HTTPS. |

#### Resolution

```json
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://my.auth.example.com/
    tokenUrl: https://my.token.example.com/
security:
 - OAuth2: []
```

&nbsp;

### API accepts API key in plain text

| Issue description | Possible fix |
| ----------- | ----------- |
| API keys are sent as plain text over an unencrypted channel. Attackers can intercept API key by listening to the network traffic in a public Wi-Fi network. | Make sure that the scheme used in the scheme array is HTTPS. |

#### Resolution

```json
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
securityDefinitions:
  apiKeyAuth:
    type: apiKey
    name: api_key
    in: header
security:
  - apiKeyAuth: []
```

&nbsp;

### API accepts basic authentication credentials in plain text

| Issue description | Possible fix |
| ----------- | ----------- |
| The credentials are sent as plain text over an unencrypted network. Attackers can intercept the credentials by listening to the network traffic in a public Wi-Fi network. | Make sure that the scheme used in the scheme array is HTTPS. |

#### Resolution

```json
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
securityDefinitions:
  basicAuth:
    type: basic
security:
 - basicAuth: []
```

&nbsp;

### Global schemes have HTTP scheme defined

| Issue description | Possible fix |
| ----------- | ----------- |
| The server supports unencrypted HTTP connections, all requests and responses will be transmitted in the open. Anyone listening to the network traffic while the calls are being made can intercept them. | Make sure that the scheme used in the scheme array is HTTPS. |

#### Resolution

```json
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
#...
```

&nbsp;

### Operation accepts credentials from OAuth authentication in plain text

| Issue description | Possible fix |
| ----------- | ----------- |
| The API operation accepts the access tokens from a flow that are transported in plain text over an unencrypted channel. Attackers can intercept API calls and retrieve the unencrypted tokens. They can then use the tokens to make other API calls. | Make sure that the scheme used in the scheme array of the operation is HTTPS.|

#### Resolution

```json
swagger: '2.0'
#...
host: 'example.com'
paths:
  "/user":
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      schemes:
          - https
      security:
          - OAuth2: []
      #...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://my.auth.example.com/
    tokenUrl: https://my.token.example.com/
```

&nbsp;

### Operation accepts API key in plain text

| Issue description | Possible fix |
| ----------- | ----------- |
| The API operation accepts API keys that are transported in plain text over an unencrypted channel. Attackers can intercept API calls and retrieve the API key to make other API calls. | Make sure that the scheme used in the scheme array of the operation is HTTPS. |

#### Resolution

```json
swagger: '2.0'
#...
host: 'example.com'
paths:
  "/user":
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      schemes:
          - https
      security:
          - apiKeyAuth: []
      #...
securityDefinitions:
  apiKeyAuth:
    type: apiKey
    name: api_key
    in: header
```

&nbsp;

### Operation accepts basic authentication credentials in plain text

| Issue description | Possible fix |
| ----------- | ----------- |
| The API operation accepts the credentials that are transported in plain text over an unencrypted channel. Attackers can intercept API calls and retrieve the unencrypted tokens. They can then use the tokens to make other API calls. | Make sure that the scheme used in the scheme array of the operation is HTTPS. |

#### Resolution

```json
swagger: '2.0'
#...
host: 'example.com'
paths:
  "/user":
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      schemes:
          - https
      security:
          - BasicAuth: []
      #...
securityDefinitions:
  BasicAuth:
    type: basic
```

&nbsp;

### Schemes of the operation have HTTP scheme defined

| Issue description | Possible fix |
| ----------- | ----------- |
| The API operation supports unencrypted HTTP connections, all requests and responses will be transmitted in the open. Anyone listening to the network traffic while the calls are being made can intercept them. | Make sure that the scheme used in the scheme array of the operation is HTTPS. |

#### Resolution

```json
swagger: '2.0'
#...
host: 'example.com'
paths:
  "/user":
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      schemes:
          - https
      #...
```

&nbsp;

### Authorization URL uses HTTP protocol. Credentials will be transferred as plain text

| Issue description | Possible fix |
| ----------- | ----------- |
| OAuth authorization credentials are transported over an unencrypted channel. Anyone listening to the network traffic while the calls are being made can intercept them. | Make sure that the authorization URL is a valid URL and follows HTTPS protocol. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    #...
    authorizationUrl: https://example.com/authorize
```

&nbsp;

### Token URL uses HTTP protocol

| Issue description | Possible fix |
| ----------- | ----------- |
| OAuth authentication tokens are transported over an unencrypted channel. Anyone listening to the network traffic while the token is being sent can intercept it. | Make sure that the token URL is a valid URL and follows HTTPS protocol. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    #...
    tokenUrl: https://example.com/token
```

&nbsp;

### Produces field is not defined

| Issue description | Possible fix |
| ----------- | ----------- |
| If the global `produces` field isn't defined, the API could potentially return any form of data.  | The `produces` field needs to be defined in the schema.|

#### Resolution

```json
swagger: '2.0'
paths: {}
consumes:
  - application/json
produces:
  - application/json
```

&nbsp;

### Produces field does not contain any item

| Issue description | Possible fix |
| ----------- | ----------- |
| If the `produces` field contains an empty array, the API can return any type of data by default. | The global `produces` field needs to contain at least one item with a valid MIME type in the array. |

#### Resolution

```json
swagger: '2.0'
paths: {}
produces:
  - application/json
...
```

&nbsp;

### Produces field for the operation does not contain any item

| Issue description | Possible fix |
| ----------- | ----------- |
| No `produces` field in the operation means that API can return any type of data by default.| The `produces` field in any operation needs to contain at least one item in the array.|

#### Resolution

```json
swagger: '2.0'
paths:
  /user/{userId}:
    get:
      produces:
        - application/json
```

&nbsp;

### Operation does not contain produces field

| Issue description | Possible fix |
| ----------- | ----------- |
| If both the global `produces` field and operation’s `produces` field for any operation aren't defined, anyone can exploit your API. | Define a `produces` field in the operation if not defined at the global level.|

#### Resolution

```json
swagger: '2.0'
paths:
  /user/{userId}:
    get:
      produces:
        - application/json
  ...
...
```

&nbsp;

## Injection

### Consumes field is not defined

| Issue description | Possible fix |
| ----------- | ----------- |
| If the global `consumes` field isn't defined, the API could potentially accept any form of data as input. This could open your API to any number of potential attacks, like buffer overflow, decoding errors, or SQL injection attacks. | The `consumes` field needs to be defined in the schema. |

#### Resolution

```json
swagger: '2.0'
paths: {}
consumes:
  - application/json
```

&nbsp;

### Consumes field does not contain any item

| Issue description | Possible fix |
| ----------- | ----------- |
| If the `consumes` field contains an empty array, the API can accept any type of input by default. | The global `consumes` field needs to contain at least one item with valid MIME type in the array.  |

#### Resolution

```json
swagger: '2.0'
paths: {}
consumes:
  - application/json
...
```

&nbsp;

### Consumes field for the operation does not contain any item

| Issue description | Possible fix |
| ----------- | ----------- |
| No `consumes` field in the operation means that API can accept any type of input by default. | The `consumes` field in `PUT`/`PATCH`/`POST` operations needs to contain at least one item in the array. |

#### Resolution

```json
swagger: '2.0'
paths:
  /user/{userId}:
    put:
      consumes:
        - application/json
```

&nbsp;

### Operation does not contain consumes field

| Issue description | Possible fix |
| ----------- | ----------- |
| If both the global `consumes` field and operation’s `consumes` field (for `PUT`/`PATCH`/`POST`) aren't defined, anyone can exploit your API. | Define a `consumes` field in the operation if not defined at the global level. |

#### Resolution

```json
swagger: '2.0'
paths:
  /user/{userId}:
    put:
      consumes:
        - application/json
  ...
...
```

&nbsp;

## Improper assets management

### OAuth authentication uses the deprecated implicit flow

| Issue description | Possible fix |
| ----------- | ----------- |
| In OAuth implicit flow, authorization server issues access tokens in the authorization request’s response. Attackers can intercept API calls and retrieve the access tokens to make other API calls. | It's recommended to use accessCode flow. Make sure that the OAuth authentication scheme isn't using the implicit flow. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://my.auth.example.com/
    tokenUrl: https://my.token.example.com/
    scopes:
      write: modify data
      read: read data
```

&nbsp;

### OAuth authentication uses the deprecated password flow

| Issue description | Possible fix |
| ----------- | ----------- |
| Oauth password grant flow uses the user’s credentials to retrieve the access token. Attackers can intercept API calls and retrieve the access tokens to make other API calls. | It's recommended to use accessCode flow. Make sure that the OAuth authentication scheme isn't using the password flow. |

#### Resolution

```json
swagger: '2.0'
#...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://my.auth.example.com/
    tokenUrl: https://my.token.example.com/
    scopes:
      write: modify data
      read: read data

```

&nbsp;

## API information

> **The format linting feature is in beta.** During the beta period, it may not be available to all Postman users and is subject to potential change.

This category of linting rules deals with the OpenAPI info object, which contains metadata about the API.

### API must have contact information available

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [info object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#infoObject) doesn't contain a [contact object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#contactObject), which contains contact information including a name and email address. | Although contact information isn't required, including it allows your users to contact you. Add a contact object to your API schema's info object.  |

#### Resolution

```json
info:
  contact:
    name: Project Name
    email: author@company.com
    url: https://example.com
```

&nbsp;

### API must have a contact email available

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [contact object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#contactObject) doesn't contain an email address for the contact person or organization. | Although contact information isn't required, including it allows your users to communicate with you. Add an email address to your API schema's contact object. |

#### Resolution

```json
info:
  contact:
    name: Project Name
    email: author@company.com
    url: https://example.com
```

&nbsp;

### API must have a contact name available

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [contact object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#contactObject) doesn't contain a name for the contact person or organization. | Although contact information isn't required, including it allows your users to communicate with you. Add a name to your API schema's contact object. |

#### Resolution

```json
info:
  contact:
    name: Project Name
    email: author@company.com
    url: https://example.com
```

&nbsp;

### API must have a contact URL available

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [contact object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#contactObject) doesn't contain the URL of the contact person or organization. | Although contact information isn't required, including it allows your users to communicate with you. Add a URL to your API schema's contact object. |

#### Resolution

```json
info:
  contact:
    name: Project Name
    email: author@company.com
    url: https://example.com
```

&nbsp;

### The info object should have a description

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [info object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#infoObject) doesn't contain a description. | Although a description isn't required, including it allows you to provide your users with information about what the API does. Add a description to your API schema's info object. |

#### Resolution

```json
info:
  description: Project API description
```

&nbsp;

### The info object should have a license

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [info object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#infoObject) doesn't contain a [license object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#licenseObject), which specifies information about the schema's license. | Although a license object isn't required, including one provides your users with important information. Add a license object to your API schema's info object. |

#### Resolution

```json
info:
  license:
    name: Apache 2.0
    url: https://www.apache.org/licenses/LICENSE-2.0.html
```

&nbsp;

### The info object should have a license URL

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [license object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#licenseObject) doesn't contain a URL to the license used for the API. | Although license information isn't required, including it provides your users with important information. Add a URL to your API schema's license object. |

#### Resolution

```json
info:
  license:
    name: Apache 2.0
    url: https://www.apache.org/licenses/LICENSE-2.0.html
```

&nbsp;

### The info object should have a terms of service

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [info object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#infoObject) doesn't contain a URL to the Terms of Service for the API. | Although a link to the Terms of Service isn't required, including it provides your users with important information. Add a URL to the API's Terms of Service to your API schema's info object. |

#### Resolution

```json
info:
  termsOfService: http://example.com/terms/
```

&nbsp;

### The info object should have an API ID extension

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [info object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#infoObject) doesn't contain an API ID extension (`x-api-id`), which is a custom header used to pass an API key. | Although an API ID extension isn't required, including it provides your users with important information. Add an API ID extension to your API schema's info object. |

#### Resolution

```json
info:
  x-api-id: project-name-identifier
```

&nbsp;

### The info object should have an audience extension

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [info object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#infoObject) doesn't contain an audience extension (`x-audience`), which is a custom header used to describe an API's target audience. | Although an audience extension isn't required, including it provides your users with important information about the API. Add an audience extension to your API schema's info object. |

#### Resolution

```json
info:
  x-audience: The details about the target audience
```

&nbsp;

### There should be no empty paths

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema contains one or more empty [path item objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#path-item-object) in the [paths object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#paths-object). | Although you can leave a path item object empty due to [access-control list (ACL) constraints](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#securityFiltering), this doesn't provide your users with a good experience. Add details for any empty path item objects in your API schema. |

#### Resolution

```json
paths:
  '/health_check':
    get:
      operationId: health_check
      description: health check endpoint
      responses:
        default:
          description: default example
```

&nbsp;

### There should be no trailing slashes on paths

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [path item objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#path-item-object) in your API schema's [paths object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#paths-object) have a trailing slash at the end of the path. | Some tools treat a path that ends with a trailing slash (`/path/`) differently from the way that they treat paths without a trailing slash (`/path`). To avoid any ambiguity, remove any trailing slashes from paths in your API schema's paths object. |

#### Resolution

```json
paths:
  '/health_check':
    get:
      operationId: health_check
```

&nbsp;

### There should be a central tags object

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema doesn't contain a root-level [tags object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#tagObject). | The tags object lists all the tags used in the schema's [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject), providing users with important context. Add a tags object to your API schema. |

#### Resolution

```json
tags:
  - name: Tag 1
    description: Tag 1, description explaining the meaning for it.
  - name: Tag 2
    description: Tag 2, description explaining the meaning for it.
```

&nbsp;

### All tags should have a description

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more tags in your API schema's [tags object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#tagObject) don't have an accompanying description. | Tag descriptions enable you to provide your users with important context. Add a description for every tag in the tags object. |

#### Resolution

```json
tags:
  - name: Tag 1
    description: Tag 1, description explaining the meaning for it.
  - name: Tag 2
    description: Tag 2, description explaining the meaning for it.
```

&nbsp;

### There should be at least one tag

| Issue description | Possible fix |
| ----------- | ----------- |
| Your API schema's [tags object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#tagObject) doesn't contain any tags. | Tags enable you to provide your users with important context. Add at least one tag to your schema's tags object. |

#### Resolution

```json
tags:
  - name: Tag 1
    description: Tag 1, description explaining the meaning for it.
  - name: Tag 2
    description: Tag 2, description explaining the meaning for it.
```

&nbsp;

## Operations

> **The format linting feature is in beta.** During the beta period, it may not be available to all Postman users and is subject to potential change.

This category of linting rules deals with operations on an API path.

### All operations should have descriptions

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operation-object) in your API schema doesn't have a description. | A verbose explanation of the operation's behavior provides your users with important context. Add a description for each operation object.

#### Resolution

```json
paths:
  '/health_check':
    get:
      ...
      description: health_check endpoint description.
```

&nbsp;

### All operations should have summaries

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operation-object) in your API schema doesn't have a summary. | A short summary of what the operation does provides your users with important context. Add a summary for each operation object. |

#### Resolution

```json
paths:
  '/health_check':
    get:
      ...
      summary: health_check endpoint summary
```

&nbsp;

### Operation summaries shouldn't end with a period

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operation-object) in your API schema contains a summary that ends with a period (`.`). | Remove the final period from all summaries at the operations object level in your API schema. |

#### Resolution

```json
paths:
  '/health_check':
    get:
      ...
      summary: health_check endpoint summary
```

&nbsp;

### All operations should have tags

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operation-object) in your API schema doesn't contain a `tags` array. | Operation tags can be used to create logical groupings of operations in API documentation. Add a `tags` array for each operation object. |

#### Resolution

```json
paths:
  '/health_check':
    get:
      ...
      tags:
        - Tag 1
```

&nbsp;

### All operations should have at least one tag

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operation-object) in your API schema contains a `tags` array, but the array doesn't contain any items. | Operation tags can be used to create logical groupings of operations in API documentation. Add at least one tag to the `tags` array for each operation object. |

#### Resolution

```json
paths:
  '/health_check':
    get:
      ...
      tags:
        - Tag 1
```

&nbsp;

### All parameters should have descriptions

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [parameter objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#parameter-object) in an [operations object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operation-object) in your API schema doesn't contain a `description` field. | A brief description of the parameter provides your users with important context. Add a `description` field for each parameter object. |

#### Resolution

```json
parameters:
  - in: path
    name: apiId
    schema:
      type: string
      format: uuid
    required: true
    description: Postman API identifier
    example: 002d9b61-961a-469b-898a-ddcf2f70faf7
```

&nbsp;

### All parameters should have examples

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [parameter objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#parameter-object) in an [operations object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operation-object) in your API schema doesn't contain an `example` field. | Add an `example` field to provide your users with an example of the parameter's potential value. |

#### Resolution

```json
parameters:
  - in: path
    name: apiId
    schema:
      type: string
      format: uuid
    required: true
    description: Postman API identifier
    example: 002d9b61-961a-469b-898a-ddcf2f70faf7
```

&nbsp;

### POST methods should have request bodies

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more POST [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain a [request body object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#requestBodyObject). |  A request body object contains a brief description of the response body and information about what a valid response body should look like. Add a request body object to any POST operation objects. |

#### Resolution

```json
paths:
  '/post_endpoint':
    post:
      operationId: post_endpoint
      description: post endpoint
      requestBody:
        required: true
        content:
          application/json:
              schema:
                type: object
              example:
                sample_key: sample_value
      responses:
        default:
          description: post_endpoint example
```

&nbsp;

### PUT methods should have request bodies

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more PUT [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain a [request body object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#requestBodyObject). | A request body object contains a brief description of the response body and information about what a valid response body should look like. Add a request body object to any POST operation objects. |

#### Resolution

```json
paths:
  '/put_endpoint':
    put:
      operationId: put_endpoint
      description: put endpoint
      requestBody:
        required: true
        content:
          application/json:
              schema:
                type: object
      responses:
        default:
          description: put_endpoint example
```

&nbsp;

### PATCH methods should have request bodies

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more PATCH [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain a [request body object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#requestBodyObject). | A request body object contains a brief description of the response body and information about what a valid response body should look like. Add a request body object to any POST operation objects. |

#### Resolution

```json
paths:
  '/patch_endpoint':
    patch:
      operationId: patch_endpoint
      description: patch endpoint
      requestBody:
        required: true
        content:
          application/json:
              schema:
                type: object
      responses:
        default:
          description: patch_endpoint example
```

&nbsp;

### DELETE operations shouldn't have a response body

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more DELETE [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema contains a response body. | Make sure that DELETE methods don't have a response body. |

#### Resolution

```json
delete:
  ...
  parameters:
    - in: path
      name: entityId
      schema:
      type: integer
      required: true
      description: entity identifier.
  responses:
    '204':
      description: Deleted successfully
    '500':
      description: Something went wrong
```

&nbsp;

### DELETE operations should have a 204 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more DELETE [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `204` status code. | Make sure that DELETE methods all have a `204` status code response. |

#### Resolution

```json
delete:
  ...
  parameters:
    - in: path
      name: entityId
      schema:
      type: integer
      required: true
      description: entity identifier.
  responses:
    '204':
      description: Deleted successfully
    '500':
      description: Something went wrong
```

&nbsp;

### DELETE operations should have a 500 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more DELETE [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `500` status code. | Make sure that DELETE methods all have a `500` status code response. |

#### Resolution

```json
delete:
  ...
  parameters:
    - in: path
      name: entityId
      schema:
      type: integer
      required: true
      description: entity identifier.
  responses:
    '204':
      description: Deleted successfully
    '500':
      description: Something went wrong
```

&nbsp;

### GET operations should have a 200 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more GET [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `200` status code. | Make sure that GET methods all have a `200` status code response. |

#### Resolution

```json
get:
  operationId: health_check
  tags:
    - General
  summary: Health-check endpoint
  description: |-
    This is a health checkup route, also used by ELB to keep the instance
    in a group. This will perform all the dependent infra check like
    db-connection by performing a query.
  security: []
  responses:
    '200':
      description: Successful response
      content:
        application/json:
          schema:
            type: object
    '500':
      description: Something went wrong
      content:
        application/json:
          schema:
            type: object
```

&nbsp;

### GET operations should have a 500 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more GET [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `500` status code. | Make sure that GET methods all have a `500` status code response. |

#### Resolution

```json
'500':
  description: Unexpected error
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/ErrorModel'
```

&nbsp;

### PATCH operations should have a 200 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more PATCH [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `200` status code. | Make sure that PATCH methods all have a `200` status code response. |

#### Resolution

```json
paths:
  /users/{GUID}:
    patch:
      summary: Update a user
      parameters:
        - name: GUID
          in: path
          required: true
          type: string
          format: GUID
          description: The GUID of a specific user
        - name: JsonPatch
          in: body
          required: true
          schema:
            $ref: "#/definitions/PatchRequest"
      responses:
        '200':
          description: Successful response
          schema:
            $ref: "#/definitions/User"
```

&nbsp;

### PATCH operations should have a 500 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more PATCH [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `500` status code. | Make sure that PATCH methods all have a `500` status code response. |

#### Resolution

```json
'500':
  description: Unexpected error
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/ErrorModel'
```

&nbsp;

### POST operations should have a 201 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more POST [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `201` status code. | Make sure that POST methods all have a `201` status code response. |

#### Resolution

```json
post:
  summary: Create a pet
  operationId: createPets
  tags:
      - pets
  responses:
      '201':
          description: Null response
```

&nbsp;

### POST operations should have a 500 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more POST [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `500` status code. | Make sure that POST methods all have a `500` status code response. |

#### Resolution

```json
'500':
  description: Unexpected error
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/ErrorModel'
```

&nbsp;

### PUT operations should have a 200 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more PUT [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `200` status code. | Make sure that PUT methods all have a `200` status code response. |

#### Resolution

```json
put:
  operationId: updatePet
  requestBody:
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/Pet"
  responses:
    "200":
      content:
        application/json:
          schema:
            type: boolean
```

&nbsp;

### PUT operations should have a 500 status code for the response

| Issue description | Possible fix |
| ----------- | ----------- |
| The [responses object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#responses-object) for one or more PUT [operation objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operationObject) in your API schema doesn't contain the `500` status code. | Make sure that PUT methods all have a `500` status code response. |

#### Resolution

```json
'500':
  description: Unexpected error
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/ErrorModel'
```

&nbsp;

## Models

> **The format linting feature is in beta.** During the beta period, it may not be available to all Postman users and is subject to potential change.

This category of linting rules deals with how to model various data types.

### All schemas should have descriptions

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [schema objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schemaObject) in your API schema's [components object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#components-object) doesn't contain a `description`. | Add a `description` for every schema object in your API schema. |

#### Resolution

```json
components:
  schemas:
    GeneralError:
      type: object
      description: universal error object
```

&nbsp;

### All schemas should have properties

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [schema objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schemaObject) in your API schema's [components object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#components-object) doesn't contain at least one property. | Add a property for every schema object in your API schema. |

#### Resolution

```json
components:
  schemas:
    GeneralError:
      type: object
      properties:
        code:
```

&nbsp;

### Integer format should be int32 or int64

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [schema objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schemaObject) in your API schema's [components object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#components-object) has an integer type property but doesn't specify `int32` or `int64` format. | Make sure that properties that have integer type in your API schema have a format of `int32` or `int64`. |

#### Resolution

```json
components:
  schemas:
    GeneralError:
      type: object
      properties:
        code:
          type: integer
          format: int32
```

&nbsp;

### Number format should be decimal32, decimal64, float, double, or decimal128

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [schema objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schemaObject) in your API schema's [components object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#components-object) has a number type property but doesn't specify `decimal32`, `decimal64`, `float`, `double`, or `decimal128` format. | Make sure that properties that have number type in your API schema have a format of `decimal32`, `decimal64`, `float`, `double`, or `decimal128`. |

#### Resolution

```json
components:
  schemas:
    GeneralError:
      type: object
      properties:
        iteration:
          type: number
          format: float
```

&nbsp;

### Arrays must have minItems and maxItems defined

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [schema objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schemaObject) in your API schema's [components object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#components-object) has an array type property but doesn't define `minItem` or `maxItem`. | Defining the minimum and maximum boundaries for arrays in your API schema prevents this type of property from being overloaded. Make sure that properties that have array type in your API schema  have `minItem` and `maxItem` defined. |

#### Resolution

```json
type: array
items:
  type: integer
minItems: 1
maxItems: 10
```

&nbsp;

### All schema properties should have descriptions

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more properties in a [schema object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schemaObject) in your API schema's [components object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#components-object) doesn't contain a `description`. | A brief description of properties in the API schema provides your users with important context. Add a `description` for every property in your schema objects. |

#### Resolution

```json
components:
  schemas:
    GeneralError:
      type: object
      properties:
        code:
          type: integer
          format: int32
          description: error code for this error
```

&nbsp;

### All schema properties should have a type property

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more properties in a [schema object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schemaObject) in your API schema's [components object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#components-object) doesn't have a `type` defined. | Add a `type` for every property in your schema objects. |

#### Resolution

```json
components:
  schemas:
    GeneralError:
      type: object
      properties:
        code:
          type: integer
          format: int32
```

&nbsp;

### All schemas should have a required property

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [schema objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schemaObject) in your API schema's [components object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#components-object) doesn't have a `required` property defined. | Add a `required` property to every schema object. |

#### Resolution

```json
components:
  schemas:
    GeneralError:
      type: object
      required: false
```

&nbsp;

### All schemas should have a type property

| Issue description | Possible fix |
| ----------- | ----------- |
| One or more [schema objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schemaObject) in your API schema's [components object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#components-object) doesn't have a `type` property defined. | Add a `type` property to every schema object. |

#### Resolution

```json
components:
  schemas:
    GeneralError:
      type: object
```

&nbsp;
