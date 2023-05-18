# API documentation for Post
Posts in Interact Social are public messages.

## Post Object

### Post Structure
NAME | TYPE | DESCRIPTION
---- | ---- | -----------
account | integer | The author of the post.
id | integer | The ID of the post.
content | string | The content of the post.
tags | array of strings | The tags of the post.
replies | array of [reply objects](/docs/post#replyobjects) | The replies of the post.
likes | array of integers | The likes of the post.
shadow | boolean | Whether or not the post should be shadowed.

### Reply objects
Reply objects are json objects that represent the reply to the post.

```
{"AUTHOR'S ID": "CONTENT"}
```
example:
```
{"1": "Hello, World!"}
```

### Example Post
```
{
    "account":1,
    "id":1,
    "content":"Hi, I'm Artic!",
    "tags":[],
    "replies":[],
    "likes":[1,3],
    "shadow":false
}
```

## Minified Post Object

### Minified Post Structure
NAME | TYPE | DESCRIPTION
---- | ---- | -----------
content | string | The content of the post.
id | integer | The id of the post.

### Example Minified Post
```
{   
    "content":"Hi, I'm Artic!",
    "id":1
}
```
---

## **GET** `/post/{id}`
Get the Post by the ID.

### Parameters

#### In URL
(integer) **id** *required* : The post's ID.

### Responses

#### Status Code 200
It returns the Post.
```
{
    "account":1,
    "id":1,
    "content":"Hi, I'm Artic!",
    "tags":[],
    "replies":[],
    "likes":[1,3],
    "shadow":false
}
```

#### Status Code 404
It returns a json object.
It returns this json object when the Post is not found.

```
{"message": "Invalid Post."}
```

## **GET** `/post/last`
Get the last Post.

### Parameters
Nothing.

### Response
It returns the last Post.

## **GET** `/min/post/{id}`
Get the minified Post by ID.

### Parameters

#### In URL
(integer) **id** *required* : The Post's ID.

### Responses

#### Status Code 200
It returns the minified Post.
```
{   
    "content":"Hi, I'm Artic!",
    "id":1
}
```

#### Status Code 404
It returns a json object.
It returns this json object when the Post is not found.
```
{"message": "Invalid Post."}
```

## **POST** `/post`
Send a Post.

### Parameters

#### In Body (json)
(string) **content** *required* : The content of the post.

### Responses

#### Status Code 201
OK, your Post was created successfully.
It returns this json object.
```
{"message": "Post sent."}
```

#### Status Code 400
Maybe there's no content or there's too many characters in your content.

No content
```
{"message": "There's no content."}
```

Too many characters
```
{"message": `There's too many characters. (${limit} characters max)`}
```

The "limit" parameter is the maximum number of characters that your account can send.

#### Status Code 401
You need to log into an account.
```
{"message": "You need to log into an account before."}
```

## **POST** `/post/{id}/reply`
Send a reply to a Post by ID.

### Parameters

#### In URL
(integer) **id** *required* : The Post's ID.

#### In Body (json)
(string) **content** *required* : The Reply's content.

### Responses

#### Status Code 201
OK, your Reply has been created.
```
{"message": "Reply sent."}
```

#### Status Code 401
You need to log into an account.
```
{"message": "You need to log into an account before."}
```

## **POST** `/post/{id}/action`
Send an Action to a Post by ID.

### Parameters

#### In URL
(integer) **id** *required* : The Post's ID.

### Responses

#### Status Code 201
OK, your Action has been created.
```
{"message": `${action} sent.`}
```

The "action" parameter can be "Like" or "Unlike", it depends if the Post has already been liked by the logged account or not.

#### Status Code 401
You need to log into an account.
```
{"message": "You need to log into an account before."}
```

## **POST** `/search`
Search a Post using the content.

### Parameters

#### In Body (json)
(string) **content** *required* : The content to search.

### Response
It returns an array of Posts.

## Useful Links

- [Introduction](/docs/intro)
- [Table of Contents](/docs/table)
