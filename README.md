
# Tinier Reverse Proxy

Tinier is a URL Shortener REST API written in go.

  

## Installation

Open ```nginx.conf``` and set proper addresses for auth and shortener services.

```

$ git clone https://github.com/pooladkhay/tinier-reverse-proxy.git

$ cd tinier-auth-service

$ docker-compose up --build

```
## Routes

### Login
**You send:**  Your  login credentials.
**You get:** An `API-Token` with wich you can make further actions.

**Request:**
```json
POST /auth/login HTTP/1.1
Accept: application/json
Content-Type: application/json
{
	"email":  "",
	"password":  ""
}
```
**Successful Response:**
```json
HTTP/1.1 200 OK
Content-Type: application/json
{
	"name":  "",
	"email":  "",
	"access_token":  ""
}
```
### Register
**You send:**  Your  registration info.
**You get:** An `API-Token` with wich you can make further actions.

**Request:**
```json
POST /auth/register HTTP/1.1
Accept: application/json
Content-Type: application/json
{
	"name": ""
	"email":  "",
	"password":  ""
}
```
**Successful Response:**
```json
HTTP/1.1 200 OK
Content-Type: application/json
{
	"name":  "",
	"email":  "",
	"access_token":  ""
}
```
### Get url
**Request:**
```json
GET /short/:hash HTTP/1.1
Accept: application/json
```
**Successful Response:**
```json
HTTP/1.1 200 OK
{
	"url":  ""
}
```
### Create url
**Request:**
```json
POST /short/ HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: "Bearer TOKEN" //optional - in order to associate url with a user
{
	"url":  "",
	"is_private":  boolean, //optional
	"expires_second":  int //optional
}
```
**Successful Response: (is_private=true)**
```json
HTTP/1.1 200 OK
Content-Type: application/json

{
	"url":  "",
	"hash":  "",
	"user":  "",
	"short_url":  "http://localhost:3012/api/v1/short/5239cf?secret=9ca266899",
	"secret":  "",
	"is_private":  true,
	"expires_at":  "2021-06-25T17:52:37.854668044Z"
}
```
**Successful Response:(is_private=false)**
```json
HTTP/1.1 200 OK
Server: My RESTful API
Content-Type: application/json
Content-Length: xy

{
	"url":  "",
	"hash":  "",
	"user":  "",
	"short_url":  "http://localhost:3012/api/v1/short/5239cf",
	"secret":  "",
	"is_private":  false,
	"expires_at":  ""
}
```
### Delete url

**Request:**
```json
POST /auth/login HTTP/1.1
Accept: application/json
Content-Type: application/json
{
	"hash":  "",
	"secret":  ""
}
```
**Successful Response:**
```json
HTTP/1.1 200 OK
```
### Get All urls
 Get all urls associated with a particular user

**Request:**
```json
POST /auth/login HTTP/1.1
Authorization: "Bearer TOKEN"
Accept: application/json
```
**Successful Response:**
```json
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: xy

[
	{
		"url":  "",
		"hash":  "",
		"user":  "",
		"short_url":  "",
		"secret":  "",
		"is_private":  boolean,
		"expires_at":  ""
	}
]
```

## Design

![Ttinier](tinier-design.png?raw=true)