---
title: 'Summoner-V3'
category: 'API'
---

## Summoner-V3 API

[Official Documentation](https://developer.riotgames.com/api-methods/#summoner-v3/)

### Legend

 - [Endpoints](#endpoints)
   - [Endpoint Parameters Explained](#endpoint-parameters)
 - [Return Data](#returns)


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
