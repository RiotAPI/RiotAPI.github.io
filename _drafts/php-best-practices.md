---
title: 'PHP Best Practices'
---

## PHP Best Practices

### Legend

  - [Introduction](#introduction)
  - [Prerequisites](#prerequisites)
  - [Including Guzzle](#including-guzzle)
  - [Guzzle Requests](#guzzle-requests)
  - [Resources](#resources)


### Introduction

PHP contains a lot of ways to make HTTP requests. Between file_get_contents, cURL and the large collection of libraries available it can be difficult to just get started making API requests. Today, we're going to talk about best practices when making PHP requests to the Riot Games API.


### Prerequisites

We're going to be using a dependency called [Guzzle](https://github.com/guzzle/guzzle) for making our http requests. We can include Guzzle as a dependency in our project via [Composer](https://getcomposer.org/). Composer is a dependency manager much like Nodes NPM except for PHP. Installation instructions can be found on the [Composer Downloads Page](https://getcomposer.org/download/).


### Including Guzzle

Once we have Composer installed, we can move on to including Guzzle into our project. We open the terminal and ```cd``` into our project directory, then run one command ```composer require guzzlehttp/guzzle```. This will reach out and grab the latest version of Guzzle, including it and any of its dependencies into a *vendor* folder of our project. It also creates a *composer.json* file, which lists the dependencies of our project. This is also useful because if anyone else were to download our project they wouldn't need the *vendor* folder, just composer and the *composer.json*. With those they can just run ```sudo composer install``` to install all project dependencies.

The last thing we need to do is include Guzzle into our project. Composer generates an autoload file at *vendor/autoload.php*. In our project, add ```require_once '/vendor/autoload.php';``` to the top of the first file run. This will automatically include all composer dependencies for us to work with.


### Guzzle Requests

We're now ready to work with Guzzle, and it's pretty easy. Lets make a call to the Summoner-V3 API with Guzzle.

```php
<?php

// Includes Composers autoloader
require 'vendor/autoload.php';

// Allows us to reference the following classes as the final name shown
use GuzzleHttp\Client as Guzzle;
use GuzzleHttp\Psr7;
use GuzzleHttp\Exception\RequestException;

/*
 * Set some options for our new Guzzle Client instance,
 * including the base_uri which, in this case, is
 * the NA Riot API
*/
$client_options = [
  'base_uri' => 'https://na.api.riotgames.com',
];

// Store our API key in a reusable variable
$api_key = '?api_key=REPLACE_WITH_YOUR_API_KEY';

// Create a new Guzzle Client instance
$client = new Guzzle( $client_options );

/*
 * Handle Exceptions thrown by the API or Request
*/
try
{
  // Make a GET request to the Summoner-V3 API
  $response = $client->get( '/lol/summoner/v3/summoners/by-name/TB Pixel' . $api_key );
  // Decodes the JSON response from Riots API
  $result = json_decode( $response->getBody() );
  // Do what we want with the $result data
}
catch (RequestException $e)
{
    echo Psr7\str( $e->getRequest() );
    if ( $e->hasResponse() ) {
        echo Psr7\str( $e->getResponse() );
    }
}
```

The great thing about the above code is that it covers errors and exceptions as well. We can get a lot more specific with our error handling based on the API in question, but for many cases the above will do fine.

### Resources
  
  - [Composer](https://getcomposer.org/)
  - [Guzzle Documentation](http://docs.guzzlephp.org/en/latest/index.html)
