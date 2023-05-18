# API documentation for User
Users in Interact Social are the base entities. They represent humans and bots.

## User Object

### User Structure

NAME | TYPE | DESCRIPTION
---- | ---- | -----------
name | string | The name of the user.
id | integer | The ID of the user.
avatar | string | The avatar of the user.
bio | string | The biography of the user.
invited | integer ([WARNING](#exceptions)) | The inviter ID.
premium | boolean | Whether the user is premium or not.
badge | integer | The badge.
badges | array or integers | The badges of the user.
shadow | boolean | Whether or not the user should be shadowed.
followers | array of integers | The followers of the user.
follows | array of integers | The follows of the user.
posts | array of integers | The posts of the user.
replies | array of integers | The replies of the user.
liked | array of integers | The likes of the user.

### Exceptions

The first User (1) was invited by nobody, so the invited property is `null`.

### Example User
```
{
    "name":"Interact",
    "id":2,
    "avatar":"https://api.interact-bot.xyz:8443/social/cdn/1678736692483-971570740.png",
    "bio":"Interact's official account",
    "invited":1,
    "premium":true,
    "badge":1,
    "badges":[0,1,3],
    "shadow":false,
    "followers":[3,9,10,1],
    "follows":[3,1],
    "posts":[29,40,41,100],
    "replies":[33],
    "liked":[28,27,26,29,33,39,38,34,41,57,100]
}
```

## Minified User Object

### Minified User Structure

NAME | TYPE | DESCRIPTION
---- | ---- | -----------
name | string | The name of the user.
id | integer | The ID of the user.
avatar | string | The avatar of the user.
badge | integer | The badge of the user.

### Example Minified User
```
{
    "name":"Interact",
    "id":2,
    "avatar":"https://api.interact-bot.xyz:8443/social/cdn/1678736692483-971570740.png",
    "badge":1,
}
```

---

## **GET** `/user/{id}`
Get a User by ID.

### Parameters

#### In URL
(integer) **id** *required* : The ID of the user.

### Responses

#### Status Code 200
OK, you have retrieved the user by ID.
```
{
    "name":"Interact",
    "id":2,
    "avatar":"https://api.interact-bot.xyz:8443/social/cdn/1678736692483-971570740.png",
    "bio":"Interact's official account",
    "invited":1,
    "premium":true,
    "badge":1,
    "badges":[0,1,3],
    "shadow":false,
    "followers":[3,9,10,1],
    "follows":[3,1],
    "posts":[29,40,41,100],
    "replies":[33],
    "liked":[28,27,26,29,33,39,38,34,41,57,100]
}
```

#### Status Code 404
The requested User was not found.
```
{"message": "Invalid User."}
```

## **GET** `/user/me`
Get the logged in User.

### Parameters
Nothing.

### Responses

#### Status Code 200
OK, you have retrieved the logged in User.
```
{
    "name":"Interact",
    "id":2,
    "avatar":"https://api.interact-bot.xyz:8443/social/cdn/1678736692483-971570740.png",
    "bio":"Interact's official account",
    "invited":1,
    "premium":true,
    "badge":1,
    "badges":[0,1,3],
    "shadow":false,
    "followers":[3,9,10,1],
    "follows":[3,1],
    "posts":[29,40,41,100],
    "replies":[33],
    "liked":[28,27,26,29,33,39,38,34,41,57,100]
}
```

#### Status Code 401
You need to log into an account.
```
{"message": "You need to log into an account before."}
```

## **GET** `/min/user/{id}`
Get the minified User by ID.

### Parameters

#### In URL
(integer) **id** *required* : The ID of the user.

### Responses

#### Status Code 200
OK, you have retrieved the user by ID.
```
{
    "name":"Interact",
    "id":2,
    "avatar":"https://api.interact-bot.xyz:8443/social/cdn/1678736692483-971570740.png",
    "badge":1,
}
```

#### Status Code 404
The requested User was not found.
```
{"message": "Invalid User."}
```

## **GET** `/min/user/me`
Get the minified logged in User.

### Parameters
Nothing.

### Responses

#### Status Code 200
OK, you have retrieved the user by ID.
```
{
    "name":"Interact",
    "id":2,
    "avatar":"https://api.interact-bot.xyz:8443/social/cdn/1678736692483-971570740.png",
    "badge":1,
}
```

#### Status Code 401
You need to log into an account.
```
{"message": "You need to log into an account before."}
```

## **GET** `/fetch/user/{username}`
Get a User by the username.

> Avoid this method, use the `/user/{id}`.

### Parameters

#### In URL
(string) **username** *required* : The username.

### Responses

#### Status Code 200
OK, you have retrieved the user by the username.
```
{
    "name":"Interact",
    "id":2,
    "avatar":"https://api.interact-bot.xyz:8443/social/cdn/1678736692483-971570740.png",
    "bio":"Interact's official account",
    "invited":1,
    "premium":true,
    "badge":1,
    "badges":[0,1,3],
    "shadow":false,
    "followers":[3,9,10,1],
    "follows":[3,1],
    "posts":[29,40,41,100],
    "replies":[33],
    "liked":[28,27,26,29,33,39,38,34,41,57,100]
}
```

#### Status Code 404
The requested User was not found.
```
{"message": "Invalid User."}
```

## **POST** `/user/{id}/action`
Send an Action to a User by ID.

### Parameters

#### In URL
(integer) **id** *required* : The ID of the User.

### Responses

#### Status Code 201
OK, your Action has been created.
```
{"message": `${action} sent.`}
```

The "action" parameter can be "Sub" or "Unsub", it depends if the User has already been followed by the logged account or not.

#### Status Code 401
You need to log into an account.
```
{"message": "You need to log into an account before."}
```

#### Status Code 403
You can't follow yourself.
```
{"message": "You can't follow yourself."}
```

#### Status Code 404
The ID is invalid.
```
{"message": "Invalid target ID."}
```

## **POST** `/user/me/edit`
Edit the logged in User, like the avatar, username, badge, password or the bio.

### Parameters

#### In Body (formdata) for avatar
(string) **type** *required* : The type of the editing. ([See types of editing](#typesofediting))

(image) **file** *required* : The new avatar.

#### In Body (json) for username
(string) **type** *required* : The type of the editing. ([See types of editing](#typesofediting))

(string) **username** *required* : The new username.

#### In Body (json) for badge
(string) **type** *required* : The type of the editing. ([See types of editing](#typesofediting))

(integer or null) **badge** *required* : The badge.

#### In Body (json) for password
(string) **type** *required* : The type of the editing. ([See types of editing](#typesofediting))

(string) **actual** *required* : The actual password.

(string) **new** *required* : The new password.

#### In Body (json) for bio
(string) **type** *required* : The type of the editing. ([See types of editing](#typesofediting))

(string) **bio** *required* : The new bio.

### Responses

#### Status Code 200
OK, your edit is applied.

#### Status Code 400
Something is missing in your request body.

#### Status Code 401
You need to log into an account.
```
{"message": "You need to log into an account before."}
```

#### Status Code 403
You can't edit.

### Types of editing

NAME | VALUE
---- | -----
avatar | avatar
username | username
badge | badge
password | password
bio | bio

## **GET** `/user/me/{type}`
Get the invite code or Auth Token.
Delete the logged in account.

### Parameters

#### In URL
(string) **type** *required* : Type of the method. ([See types of methods](#typesofmethods))

### Responses

#### Status Code 200
OK, your request was successful.

#### Status Code 400
Bad request, check your type.
```
{"message": "Bad request."}
```

#### Status Code 401
You need to log into an account.
```
{"message": "You need to log into an account before."}
```

### Types of methods

TYPE | DESCRIPTION
---- | -----
invite | Get the invite code.
token | Get the Auth Token.
delete | Delete the logged in account.

## Useful Links

- [Introduction](/docs/intro)
- [Table of Contents](/docs/table)
