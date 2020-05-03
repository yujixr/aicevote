# aicevote

[![npm version](https://img.shields.io/npm/v/aicevote.svg?style=flat-square)](https://www.npmjs.org/package/aicevote)
[![install size](https://badgen.net/packagephobia/install/aicevote?style=flat-square)](https://packagephobia.now.sh/result?p=aicevote)
[![npm downloads](https://img.shields.io/npm/dm/aicevote.svg?style=flat-square)](https://npm-stat.com/charts.html?package=aicevote)
[![MIT License](https://img.shields.io/github/license/aicevote/aicevote.svg?style=flat-square)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/aicevote/aicevote.svg?style=flat-square)](https://github.com/aicevote/aicevote)
![TypeScript](https://img.shields.io/github/languages/top/aicevote/aicevote.svg?style=flat-square)

AICEVOTE API Client Library

## Installing

Using npm:

``` bash
$ npm install aicevote
```

Using yarn:

``` bash
$ yarn add aicevote
```

Using jsDelivr CDN:

``` html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/aicevote/dist/aicevote.min.js"></script>
```

Using unpkg CDN:

``` html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script src="https://unpkg.com/aicevote/dist/aicevote.min.js"></script>
```

> note: aicevote uses [axios](https://github.com/axios/axios) for http requests. Don't forget to load axios.

## Example

``` javascript
aicevote.getAllThemes().then(themes => {
    console.log(themes);
});

// Want to use async/await? Add the "async" keyword to your outer function/method.
async function getAllThemes() {
    const themes = await aicevote.getAllThemes();
    console.log(themes);
}
```

> note: `async/await` is part of ECMAScript 2017 and is not supported in Internet Explorer and older browsers, so use with caution.

### CommonJS usage

while using CommonJS imports with `require()`, use the following approach:

``` javascript
const aicevote = require("aicevote");

// aicevote.<method> will now provide autocomplete and parameter typings
```

### TypeScript usage

aicevote includes [TypeScript](https://www.typescriptlang.org) definitions.

``` typescript
import aicevote from "aicevote";
```

## aicevote API

### Functions

``` typescript
// Auth
function getSessionToken(sessionID: string): Promise<string>;

// Index
function postFeedback(feedback: string): Promise<void>;
function postApplication(application: string): Promise<void>;

// News
function getAllArticles(): Promise<{
    latest: Article[];
    related: Article[][];
}>;
function getRelatedArticles(themeID: number): Promise<Article[]>;

// User
function getMyProfile(sessionToken: string): Promise<Profile>;
function getProfiles(users: {
    userProvider: userProvider;
    userID: string;
}[]): Promise<Profile[]>;

// Theme
function getAllThemes(): Promise<Theme[]>;
function getTheme(themeID: number): Promise<Theme>;

// Vote
function getAllResults(): Promise<Result[]>;
function getResult(themeID: number): Promise<Result>;
function getAllVotes(sessionToken: string): Promise<Vote[][]>;
function getVotes(themeID: number, sessionToken: string): Promise<Vote[]>;
function vote(themeID: number, sessionToken: string, answer: number): Promise<Vote[]>;
function getAllTransitions(): Promise<Transition[]>;
function getTransition(themeID: number): Promise<Transition>;
function getAllComments(): Promise<Comment[][]>;
function getComments(themeID: number): Promise<Comment[]>;
function comment(themeID: number, sessionToken: string, message: string): Promise<Comment[]>;
```

### Types

``` typescript
// News
interface Article {
    source: string;
    author: string;
    title: string;
    description: string;
    uri: string;
    uriToImage: string;
    publishedAt: number;
}

// Theme
interface Theme {
    themeID: number;
    title: string;
    description: string;
    imageURI: string;
    genre: number;
    choices: string[];
    topicality: number;
}

// User
type userProvider = "twitter" | "legacy";
interface Profile {
    userProvider: userProvider;
    userID: number;
    name: string;
    imageURI: string;
    isInfluencer: boolean;
    votes: Vote[];
    comments: Comment[];
}

// Vote
interface Result {
    results: number[];
    counts: number[];
}
interface Vote {    
    themeID: number;
    answer: number;
    userProvider: userProvider;
    userID: string;
    createdAt: number;
}
interface Transition {
    shortTransition: {
        timestamp: number;
        percentage: number[];
    }[];
    longTransition: {
        timestamp: number;
        percentage: number[];
    }[];
}
interface Comment {
    themeID: number;
    message: string;
    userProvider: userProvider;
    userID: string;
    createdAt: number;
}
```

(C) 2020 YUJI