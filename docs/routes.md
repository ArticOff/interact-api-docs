# Routes

## **GET** `/`
The main route.

### Parameters
Nothing.

### Response
It returns a json object.

```
{"message": "Hello, World!"}
```

## **GET** `/random`
The "questions"/"infos" route.

### Parameters
Nothing.

### Responses
[List of responses.](/docs/random)

```
{"title": "placeholder"}
```
example:
```
{"Never Gonna Give You Up": "Never Gonna let you down..."}
```

## **GET** `/cdn/{file}`
Get a file from the CDN.

### Parameters

#### In URL
(string) **file** *required* : The file name.

### Responses

#### Status Code 200
It returns the file content.

#### Status Code 500
It returns a json object.

```
{"error": "Failed to load this content."}
```

## Useful Links

- [Introduction](/docs/intro)
- [Table of Contents](/docs/table)
