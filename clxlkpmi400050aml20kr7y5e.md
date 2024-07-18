---
title: "Free APIs You Need to Know About in 2024"
seoTitle: "Top Free APIs to Use in 2024"
seoDescription: "Discover essential free APIs for 2024 across gaming, music, science, and more to enhance your applications with diverse functionalities. Happy coding!"
datePublished: Wed Jun 19 2024 08:30:40 GMT+0000 (Coordinated Universal Time)
cuid: clxlkpmi400050aml20kr7y5e
slug: free-apis-you-need-to-know-about-in-2024
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718763399011/f6e46d75-7d3b-4fa9-b680-dfddbcc8be99.png
tags: express, programming-blogs, api, javascript, opensource, nodejs, apis, freelancing, reactjs, node, frontend-development, freecodecamp, nodejs-developer, api-basics, backend-developments

---

APIs (Application Programming Interfaces) are essential tools for developers, allowing them to integrate third-party services into their applications. Here is an extensive list of free APIs available in 2024 across various categories, along with website links, descriptions, and sample code for each.

## Gaming APIs

### Steam Community API

* **Website**: [steamcommunity.com/dev](http://steamcommunity.com/dev)
    
* **Description**: The Steamworks Web API provides an interface to various Steam features such as user authentication, inventory management, and game data.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const steamApiKey = 'YOUR_STEAM_API_KEY';
const steamId = 'STEAM_USER_ID';
const url = `http://api.steampowered.com/ISteamUser/GetPlayerSummaries/v0002/?key=${steamApiKey}&steamids=${steamId}`;

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Riot Games API

* **Website**: [developer.riotgames.com](http://developer.riotgames.com)
    
* **Description**: Access data for games like League of Legends, Teamfight Tactics, Valorant, and more. Provides data on matches, rankings, champions, and other game-related statistics.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const riotApiKey = 'YOUR_RIOT_API_KEY';
const summonerName = 'SUMMONER_NAME';
const url = `https://na1.api.riotgames.com/lol/summoner/v4/summoners/by-name/${summonerName}?api_key=${riotApiKey}`;

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Language APIs

### Evil Insult Generator API

* **Website**: [evilinsult.com/api](http://evilinsult.com/api)
    
* **Description**: Generate random insults in various languages for fun or testing purposes.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://evilinsult.com/generate_insult.php?lang=en&type=json';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Fun Translations API

* **Website**: [funtranslations.com/api](http://funtranslations.com/api)
    
* **Description**: Translate text into various fun languages like Yoda, Shakespeare, Minion speak, and more.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const text = 'Hello, world!';
const url = `https://api.funtranslations.com/translate/yoda.json?text=${encodeURIComponent(text)}`;

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Music APIs

### Spotify Web API

* **Website**: [developer.spotify.com/documentation/web-api](http://developer.spotify.com/documentation/web-api)
    
* **Description**: Access music data such as albums, artists, playlists, and user data. Control Spotify playback and more.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const accessToken = 'YOUR_SPOTIFY_ACCESS_TOKEN';
const url = 'https://api.spotify.com/v1/me/player/recently-played';

fetch(url, {
    headers: {
        'Authorization': `Bearer ${accessToken}`
    }
})
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Security APIs

### Have I Been Pwned API

* **Website**: [haveibeenpwned.com/API/v2](http://haveibeenpwned.com/API/v2)
    
* **Description**: Check if your email or username has been part of a data breach. Provides data on breaches, pastes, and password exposure.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const email = 'test@example.com';
const url = `https://haveibeenpwned.com/api/v2/breachedaccount/${email}`;

fetch(url, {
    headers: {
        'User-Agent': 'Node.js'
    }
})
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Shodan API

* **Website**: [developer.shodan.io](http://developer.shodan.io)
    
* **Description**: Shodan is a search engine for Internet-connected devices. It provides data on various servers, devices, and systems worldwide.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const shodanApiKey = 'YOUR_SHODAN_API_KEY';
const query = 'apache';
const url = `https://api.shodan.io/shodan/host/search?key=${shodanApiKey}&query=${query}`;

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Science & Math APIs

### NASA API

* **Website**: [api.nasa.gov](http://api.nasa.gov)
    
* **Description**: Access data from NASA’s datasets including astronomy photos, planetary data, and more.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const nasaApiKey = 'YOUR_NASA_API_KEY';
const url = `https://api.nasa.gov/planetary/apod?api_key=${nasaApiKey}`;

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Wolfram Alpha API

* **Website**: [products.wolframalpha.com/api](http://products.wolframalpha.com/api)
    
* **Description**: Provides access to the vast computational knowledge of Wolfram Alpha, including math calculations, data analysis, and more.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const wolframAppId = 'YOUR_WOLFRAM_APP_ID';
const query = 'integrate x^2';
const url = `http://api.wolframalpha.com/v2/query?input=${encodeURIComponent(query)}&appid=${wolframAppId}&output=json`;

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Open Science Framework API

* **Website**: [developer.osf.io](http://developer.osf.io)
    
* **Description**: Access research data, project management tools, and other scientific resources from the Open Science Framework.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://api.osf.io/v2/nodes/';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Sports APIs

### NBA API

* **Website**: [any-api.com/nba\_com/nba\_com/docs/API\_Description](http://any-api.com/nba_com/nba_com/docs/API_Description)
    
* **Description**: Access data on NBA teams, players, and games.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://api-nba-v1.p.rapidapi.com/teams/league/standard';
const options = {
    method: 'GET',
    headers: {
        'X-RapidAPI-Key': 'YOUR_RAPIDAPI_KEY',
        'X-RapidAPI-Host': 'api-nba-v1.p.rapidapi.com'
    }
};

fetch(url, options)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Web Apps APIs

### Discord API

* **Website**: [discord.com/developers/docs/intro](http://discord.com/developers/docs/intro)
    
* **Description**: Integrate your applications with Discord, allowing for user authentication, messaging, and more.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const discordToken = 'YOUR_DISCORD_BOT_TOKEN';
const url = 'https://discord.com/api/users/@me';

fetch(url, {
    headers: {
        'Authorization': `Bot ${discordToken}`
    }
})
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Slack API

* **Website**: [api.slack.com](http://api.slack.com)
    
* **Description**: Access Slack features such as messaging, user data, and workspace management.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const slackToken = 'YOUR_SLACK_API_TOKEN';
const url = 'https://slack.com/api/conversations.list';

fetch(url, {
    headers: {
        'Authorization': `Bearer ${slackToken}`
    }
})
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Products and Things APIs

### Car Query API

* **Website**: [carqueryapi.com](http://carqueryapi.com)
    
* **Description**: Access data on cars, including
    

make, model, and year information.

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://www.carqueryapi.com/api/0.3/?cmd=getMakes';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Yelp API

* **Website**: [yelp.com/developers](http://yelp.com/developers)
    
* **Description**: Access data on local businesses, including reviews, ratings, and business details.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const yelpApiKey = 'YOUR_YELP_API_KEY';
const url = 'https://api.yelp.com/v3/businesses/search?location=San Francisco';

fetch(url, {
    headers: {
        'Authorization': `Bearer ${yelpApiKey}`
    }
})
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Health APIs

### [Healthcare.gov](http://Healthcare.gov) API

* **Website**: [healthcare.gov/developers](http://healthcare.gov/developers)
    
* **Description**: Access data on healthcare plans, provider directories, and other health-related information.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://data.healthcare.gov/resource/xyz123.json';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Governments & Geography APIs

### [Code.gov](http://Code.gov) API

* **Website**: [code.gov](http://code.gov)
    
* **Description**: Access data on federal government software projects, including code repositories and project details.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://api.code.gov/projects';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### [Data.gov](http://Data.gov) API

* **Website**: [data.gov/developers/apis](http://data.gov/developers/apis)
    
* **Description**: Access a wide range of datasets from the US government, including weather, education, and health data.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://api.data.gov/ed/collegescorecard/v1/schools.json?api_key=YOUR_DATA_GOV_API_KEY';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### [Data.europa.eu](http://Data.europa.eu) API

* **Website**: [data.europa.eu/en](http://data.europa.eu/en)
    
* **Description**: Access open data from European Union institutions and bodies.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://data.europa.eu/api/hub/search/datasets';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### TransLoc API

* **Website**: [rapidapi.com/transloc/api/openapi-1-2/details](http://rapidapi.com/transloc/api/openapi-1-2/details)
    
* **Description**: Access real-time public transit data including arrival predictions, vehicle locations, and more.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const translocApiKey = 'YOUR_TRANSLOC_API_KEY';
const url = 'https://transloc-api-1-2.p.rapidapi.com/agencies.json';

fetch(url, {
    headers: {
        'X-RapidAPI-Key': translocApiKey,
        'X-RapidAPI-Host': 'transloc-api-1-2.p.rapidapi.com'
    }
})
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Food APIs

### Open Food Facts API

* **Website**: [world.openfoodfacts.org/data](http://world.openfoodfacts.org/data)
    
* **Description**: Access data on food products worldwide, including ingredients, nutrition facts, and allergen information.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://world.openfoodfacts.org/api/v0/product/737628064502.json';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Taco Fancy API

* **Website**: [github.com/evz/tacofancy-api](http://github.com/evz/tacofancy-api)
    
* **Description**: Access data on taco recipes, including ingredients and preparation methods.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'http://taco-randomizer.herokuapp.com/random/';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Open Source Projects APIs

### [Libraries.io](http://Libraries.io) API

* **Website**: [libraries.io/api](http://libraries.io/api)
    
* **Description**: Access data on open source projects, including dependency information, version history, and more.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const librariesApiKey = 'YOUR_LIBRARIES_IO_API_KEY';
const url = `https://libraries.io/api/platforms?api_key=${librariesApiKey}`;

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Movies and Comics APIs

### Chuck Norris Jokes API

* **Website**: [api.chucknorris.io](http://api.chucknorris.io)
    
* **Description**: Access a collection of Chuck Norris jokes.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://api.chucknorris.io/jokes/random';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Final Space API

* **Website**: [finalspaceapi.com](http://finalspaceapi.com)
    
* **Description**: Access data from the Final Space TV show, including characters, episodes, and more.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://finalspaceapi.com/api/v0/character';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Kitsu API

* **Website**: [kitsu.docs.apiary.io](http://kitsu.docs.apiary.io)
    
* **Description**: Access data on anime and manga, including series information, reviews, and user ratings.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://kitsu.io/api/edge/anime';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Marvel API

* **Website**: [developer.marvel.com](http://developer.marvel.com)
    
* **Description**: Access data on Marvel comics, characters, and creators.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const marvelPublicKey = 'YOUR_MARVEL_PUBLIC_KEY';
const marvelPrivateKey = 'YOUR_MARVEL_PRIVATE_KEY';
const ts = new Date().getTime();
const hash = require('crypto').createHash('md5').update(ts + marvelPrivateKey + marvelPublicKey).digest('hex');
const url = `https://gateway.marvel.com/v1/public/characters?ts=${ts}&apikey=${marvelPublicKey}&hash=${hash}`;

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### PokeAPI

* **Website**: [pokeapi.co](http://pokeapi.co)
    
* **Description**: Access data on Pokémon, including species, abilities, and game information.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://pokeapi.co/api/v2/pokemon/ditto';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Rick and Morty API

* **Website**: [rickandmortyapi.com](http://rickandmortyapi.com)
    
* **Description**: Access data on the Rick and Morty TV show, including characters, episodes, and locations.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://rickandmortyapi.com/api/character';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Simpsons Quotes API

* **Website**: [thesimpsonsquoteapi.glitch.me](http://thesimpsonsquoteapi.glitch.me)
    
* **Description**: Access a collection of quotes from The Simpsons TV show.
    

#### Sample

Code

```javascript
const fetch = require('node-fetch');

const url = 'https://thesimpsonsquoteapi.glitch.me/quotes';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Star Wars API

* **Website**: [swapi.tech](http://swapi.tech)
    
* **Description**: Access data on the Star Wars universe, including films, characters, starships, and planets.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const url = 'https://swapi.tech/api/people/1';

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Superhero API

* **Website**: [superheroapi.com](http://superheroapi.com)
    
* **Description**: Access data on various superheroes, including their powers, biographies, and images.
    

#### Sample Code

```javascript
const fetch = require('node-fetch');

const superheroApiKey = 'YOUR_SUPERHERO_API_KEY';
const url = `https://superheroapi.com/api/${superheroApiKey}/1`;

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Conclusion

This comprehensive list of free APIs for 2024 spans a wide range of categories, offering developers numerous opportunities to enhance their applications with powerful and diverse functionalities. From gaming and music to science and government data, these APIs provide valuable resources for creating innovative and engaging projects.

Feel free to explore these APIs and integrate them into your projects to unlock new possibilities and features. Happy coding!