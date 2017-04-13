---
title: 'Summoner-V3'
---

## Summoner-V3 API

[Official Documentation](https://developer.riotgames.com/api-methods/#summoner-v3/)

### Legend

 - [Endpoints](#Endpoints)
   - [Endpoint Parameters Explained](#Endpoint-Parameters)
 - [Return Data](#Returns)
 - [Examples](#Examples)
   - [PHP](#Examples-PHP)


The Summoner-V3 API provides us with 3 possible endpoints to make GET requests to:

### Endpoints

  - /lol/summoner/v3/summoners/by-account/{accountId}
  - /lol/summoner/v3/summoners/by-name/{summonerName}
  - /lol/summoner/v3/summoners/{summonerId}

#### Endpoint Parameters

For the most part each endpoint resembles a basic URL. The last part of the endpoint is a *parameter*, which is a friendly way of accepting an input into the API. In the case of the Summoner-V3 API the parameter determins which summoner Riots servers should attempt to retrieve from their database. With this knowledge in mind we know there are 3 ways to get a summoners information: via their Account ID, their Summoner Name or their Summoner ID.


Each of these endpoints return the same group of data:

### Returns

  - profileIconId (int)
  - name (string)
  - summonerLevel (long)
  - revisionDate (long)
  - id (long)
  - accountId (long)

> NOTE: **id** in this case refers to the **summonerId** endpoint parameter


### Examples

The *summonerName* endpoint is generally speaking the most practical one to use, so we'll put it to work in a couple of examples

#### PHP

When retrieving data in PHP, the most widely available method is likely to use cURL. We'll create a variable reference of cURL, set the URL we'd like to request data from, set the type of data we'd like to receive back

```php
// Initialize cURL 
$ch = curl_init();

// Declare the URL endpoint we'd like to get data from
curl_setopt( $ch, CURLOPT_URL, 'https://na1.api.riotgames.com/lol/summoner/v3/summoners/by-name/TB Pixel?api_key=REPLACE_WITH_YOUR_API_KEY' );

/*
 * Declare the type of data we'd like to receive
 * CURLOPT_RETURNTRANSFER being set to true
 * means that the result will be returned as
 * a string.
*/
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );

// Submit the API Request
$result = curl_exec( $ch );


/*
 * Verify the result is successful
*/
$result_info = curl_getinfo( $ch );

/*
 * We're checking the metadata of the request for possible error codes.
 * The 200 code means OK or successful.
 * We check to see if it is not 200 because that accounts for all possible
 * unsuccessful error codes in one code block.
*/
if ( $result_info['http_code'] !== 200 ) {
  
  // Print the error to the page and kill the script.
  echo $result_info['http_code'];
  die();
}


// Now we just convert the $result from JSON into a PHP Object
$summoner = json_decode( $result );

/*
 * And then have fun with your data!
*/
echo $summoner->name;          // Prints "TB Pixel"
echo $summoner->summonerLevel; // Prints 30
```

You can find a list of all [curl_setopt options here](http://php.net/manual/en/function.curl-setopt.php)