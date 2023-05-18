# Authentication

Like what we said, there are two ways to authenticate into an account.

### How do I get my Auth Token?

1. Go on the [settings page](/settings#token)
2. Click on the button "Copy Auth Token"

Here we go! Your Auth Token is on your clipboard.

### How do I get my ID?

#### Non-API method

1. Log into an account.
2. Click on your account top right.
3. On the URL bar, you can see __social.interact-bot.xyz/user/*number*__
4. The number is your ID, copy it.

GG, you have now copied your ID.

#### API method

1. Log into an account.
2. Go on the URL [https://api.interact-bot.xyz:8443/social/min/user/me](https://api.interact-bot.xyz:8443/social/min/user/me)
3. Copy the "id" property on the returned json object.

You have copied your ID with style 😎

## Auth Token & ID

Logging with the Auth Token and ID is the "bot" way to authenticate to an account.

If you want to authenticate with this method, follow these steps :

1. Get your [Auth Token](#howdoigetmyauthtoken).
2. Get your [ID](#howdoigetmyid).
3. Send a GET request to `/auth/{id}/{token}`, fill the appropriate parameters.
4. If the response contains "Logged in.", you have done the authentication!

But, if you have the message "Unauthorized", check out the GET request to `/auth/{id}/{token}`, with the right parameters.

## Credentials

Logging with the creadentials is the "normal" way to authenticate to an account.

If you want to authenticate with this method, follow these steps :

1. Send a POST request to `/auth/login` with a body (json) that contains your password and your username : `{"password": password, "name": username}`
2. It will returns a JSON response with the Auth Token and the ID of the user, if not, [click here](#itdoesntreturnmyauthtokenandid).
3. Send a GET request to `/auth/{id}/{token}` with the right parameters.
4. If the response contains "Logged in.", you have done the authentication!

But, if you have the message "Unauthorized", check out the GET request to `/auth/{id}/{token}`, with the right parameters.

### It doesn't return my Auth Token and ID.

#### Missing password.

If you have the message "Missing password.", check out the password parameter in your POST request's body, if you don't have the password parameter in the body, change yout body and inclide the password : `{"password": password, "name": username}`.

#### User not found.

If you have this message, check your username, may be you misspelled it.

#### Bad credentials.

Check your credentials, may be you misspelled your password or your username.

## Useful Links

- [Introduction](/docs/intro)
- [Table of Contents](/docs/table)
