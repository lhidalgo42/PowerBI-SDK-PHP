PowerBI PHP SDK
===============

[![Build Status](https://travis-ci.org/TangentSolutions/PowerBI-SDK-PHP.svg?branch=master)](https://travis-ci.org/TangentSolutions/PowerBI-SDK-PHP)

A SDK which makes it easier to work with the PowerBI REST API.

## Installation

```
composer require tangent-solutions/powerbi-sdk
```

## Usage

You will first have to obtain an authorized access token. See the below
example on how to do this with the [League OAuth2 Client](https://github.com/thephpleague/oauth2-client):

```php
$provider = new \League\OAuth2\Client\Provider\GenericProvider([
    'clientId'                => '<client-id>',
    'clientSecret'            => '<client-secret>',
    'urlAuthorize'            => 'https://login.microsoftonline.com/common/oauth2/v2.0/authorize',
    'urlAccessToken'          => 'https://login.windows.net/<tenant-id>/oauth2/token',
    'urlResourceOwnerDetails' => '',
    'scopes'                  => 'openid',
]);

try {
    // Try to get an access token using the resource owner password credentials grant.
    $accessToken = $provider->getAccessToken('password', [
        'username' => '<Azure-Username>',
        'password' => '<Azure-Password>',
        'resource' => 'https://analysis.windows.net/powerbi/api'
    ]);

    $token = $accessToken->getToken();
} catch (\League\OAuth2\Client\Provider\Exception\IdentityProviderException $e) {
    // Failed to get the access token
    exit($e->getMessage());
}
```

Once you have the access token you can create the client like this:

```php
$client = new \Tngnt\PBI\Client($token);
```

## Issues

View or log issues on the [Issues](https://github.com/microsoftgraph/msgraph-sdk-php/issues) tab on the repo.

## Copyright and License

Copyright (c) Tangent Solutions. All Rights Reserved. Licensed under the MIT [license](LICENSE).
