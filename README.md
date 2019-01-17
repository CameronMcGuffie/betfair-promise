Betfair API-NG for Node.js promisified. 
Based in https://github.com/AlgoTrader/betfair project.
================================================

[![NPM](https://nodei.co/npm/betfair-promise.png?downloads=true)](https://nodei.co/npm/betfair-promise/)

## Installation ##

    npm install betfair-promise --save


## Synopsis ##

Login to Betfair
```JavaScript
const betfair = require('betfair-promise');
const session = new betfair.BetfairSession("yourAppKey");

const testLoging = async () => {
    try {
        await session.login("yourUsername", "yourPassword");
        await session.keepAlive();
        await session.logout();
    } catch(error) {
        console.log("Something was wrong");
        console.log(error);
    }
};

testLoging();
```


If you need to set different Betfair endpoints (Spain, Italy ... check here: https://docs.developer.betfair.com/display/1smk3cen4v3lu3yomq5qye0ni/Interactive+Login+-+API+Endpoint#InteractiveLogin-APIEndpoint-OtherJurisdictions), init Betfair session with this options:


```JavaScript
const betfair = require('betfair-promise');

// Spain URL's
const AUTH_URLS_ES = {
    interactiveLogin: 'https://identitysso.betfair.es:443/api/login',
    botLogin: 'https://identitysso-api.betfair.es:443/api/certlogin',
    logout: 'https://identitysso.betfair.es:443/api/logout',
    keepAlive: 'https://identitysso.betfair.es:443/api/keepAlive'
};

const session = new betfair.BetfairSession("yourAppKey", {authUrls: AUTH_URLS_ES});
```



Request countries list

```JavaScript
const betfair = require('betfair-promise');
const session = new betfair.BetfairSession("yourAppKey");

const testListOfCountries = async () => {
    await session.login("yourUsername", "yourPassword");
    const listOfCountries = await betfair.getListOfCountries();
    for(let country of listOfCountries) {
        console.log("country:%s markets:%s", country.counrtyCode, country.marketCount);
    }
};

testListOfCountries();
```

