<h1 align="center">Github Unofficial Trending API</h1>

## API Status

API status is available at [uptimerobot](https://stats.uptimerobot.com/GWJMDFJ5WP).

### Trending Repositories

Receive an array of trending repositories.

**URL Endpoint:**

https://api.gitterapp.com/repositories?language=javascript&since=weekly

**Parameters:**

- `language`: **optional**, list trending repositories of certain programming languages, possible values are listed [here](./src/languages.json).
- `since`: **optional**, default to `daily`, possible values: `daily`, `weekly` and `monthly`.
- `spoken_language`: **optional**, list trending repositories of certain spoken languages (e.g English, Chinese), possible values are listed [here](./src/spoken-languages.json).

**Response:**

```json
[
  ...
  {
    "author": "google",
    "name": "gvisor",
    "avatar": "https://github.com/google.png",
    "url": "https://github.com/google/gvisor",
    "description": "Container Runtime Sandbox",
    "language": "Go",
    "languageColor": "#3572A5",
    "stars": 3320,
    "forks": 118,
    "currentPeriodStars": 1624,
    "builtBy": [
      {
        "href": "https://github.com/viatsko",
        "avatar": "https://avatars0.githubusercontent.com/u/376065",
        "username": "viatsko"
      }
    ]
  }
  ...
]
```

> Note that [GitHub trending page](http://github.com/trending) sometimes is empty, in that case this API returns `[]` in response, your application should be able to handle it or read from previous cache.

### Trending Developers

Receive an array of trending developers.

**URL Endpoint:**

https://api.gitterapp.com/developers?language=javascript&since=weekly

**Parameters:**

- `language`: **optional**, list trending repositories of certain programming languages, possible values are listed [here](./src/languages.json).
- `since`: **optional**, default to `daily`, possible values: `daily`, `weekly` and `monthly`.

**Response:**

```json
[
  {
    "username": "google",
    "name": "Google",
    "type": "organization",
    "url": "https://github.com/google",
    "avatar": "https://avatars0.githubusercontent.com/u/1342004",
    "repo": {
      "name": "traceur-compiler",
      "description": "Traceur is a JavaScript.next-to-JavaScript-of-today compiler",
      "url": "https://github.com/google/traceur-compiler"
    }
  }
]
```

> `type` could be `organization` or `user`.

### List Languages

**URL Endpoint:**

https://api.gitterapp.com/languages

**Response:**

```json
[
  {
    "color": "#814CCC",
    "url": "https://github.com/trending?l=1C Enterprise",
    "name": "1c-enterprise",
    "title": "1C Enterprise"
  },
  {
    "color": "#38761D",
    "url": "https://github.com/trending?l=2-Dimensional Array",
    "name": "2-dimensional-array",
    "title": "2-Dimensional Array"
  },
  {
    "color": "#004289",
    "url": "https://github.com/trending?l=4D",
    "name": "4d",
    "title": "4D"
  },
  {
    "color": "#E8274B",
    "url": "https://github.com/trending?l=ABAP",
    "name": "abap",
    "title": "ABAP"
  }
]
```

### List Spoken Languages

**URL Endpoint:**

https://api.gitterapp.com/spoken_languages

**Response:**

```json
[
  {
    "name": "ab",
    "title": "Abkhazian"
  },
  {
    "name": "aa",
    "title": "Afar"
  },
  {
    "name": "af",
    "title": "Afrikaans"
  },
  {
    "name": "ak",
    "title": "Akan"
  }
]
```

## NPM Package

You could also use the API as a NPM package.

### Install

```sh
$ npm install --save @huchenme/github-trending
```

### Usage

```js
import {
  languages,
  spokenLanguages,
  fetchRepositories,
  fetchDevelopers,
} from '@huchenme/github-trending';

fetchRepositories({ language: 'ruby', since: 'monthly' }).then(
  (repositories) => {
    console.log(repositories);
  }
);

fetchDevelopers({ language: 'javascript' }).then((developers) => {
  console.log(developers);
});

console.log(languages);
console.log(spokenLanguages);
```

### API

#### languages

List all languages

```js
[
  {
    "color": "#814CCC",
    "url": "https://github.com/trending?l=1C Enterprise",
    "name": "1c-enterprise",
    "title": "1C Enterprise"
  },
  {
    "color": "#38761D",
    "url": "https://github.com/trending?l=2-Dimensional Array",
    "name": "2-dimensional-array",
    "title": "2-Dimensional Array"
  },
  {
    "color": "#004289",
    "url": "https://github.com/trending?l=4D",
    "name": "4d",
    "title": "4D"
  },
  {
    "color": "#E8274B",
    "url": "https://github.com/trending?l=ABAP",
    "name": "abap",
    "title": "ABAP"
  },
];
```

#### spokenLanguages

List all spoken languages

```js
[
  {
    name: 'ab',
    title: 'Abkhazian',
  },
  {
    name: 'aa',
    title: 'Afar',
  },
  {
    name: 'af',
    title: 'Afrikaans',
  },
  {
    name: 'ak',
    title: 'Akan',
  },
];
```

#### fetchRepositories(params)

Receive an array of trending repositories.

**params**:

- `language`: possible values are the the ones from `languages` or [just find here](./src/languages.json).
- `since`: `daily`, `weekly` or `monthly`, default to `daily`.
- `spokenLanguageCode`: possible values are the the ones from `spokenLanguages` or [just find here](./src/spoken-languages.json).

```js
[
  ...
  {
    author: 'google',
    name: 'gvisor',
    avatar: 'https://github.com/google.png',
    url: 'https://github.com/google/gvisor',
    description: 'Container Runtime Sandbox',
    language: 'Go',
    languageColor: '#3572A5',
    stars: 3320,
    forks: 118,
    currentPeriodStars: 1624,
    "builtBy": [
      {
        "href": "https://github.com/viatsko",
        "avatar": "https://avatars0.githubusercontent.com/u/376065",
        "username": "viatsko"
      }
    ]
  }
  ...
]
```

#### fetchDevelopers(params)

Receive an array of trending developers.

**params**:

- `language`: possible values are the the ones from `languages` or [just find here](languages.json).
- `since`: `daily`, `weekly` or `monthly`, default to `daily`.

```js
[
  ...
  {
    username: 'google',
    name: 'Google',
    type: 'organization',
    url: 'https://github.com/google',
    avatar: 'https://avatars0.githubusercontent.com/u/1342004',
    repo: {
      name: 'traceur-compiler',
      description:
        'Traceur is a JavaScript.next-to-JavaScript-of-today compiler',
      url: 'https://github.com/google/traceur-compiler'
    }
  }
  ...
]
```

## Backers

<a href="https://www.buymeacoffee.com/wangying" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: auto !important;width: auto !important;" ></a>


## License

MIT
