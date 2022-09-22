# Assignment 02: Create a command line Node.js package that ingests API data from Open-Meteo

This assignment will help you learn to create an installable Node.js command line utility. 

## DO NOT CLONE THIS REPOSITORY DIRECTLY

Use the GitHub classroom link instead: 

**_If you clone this repo directly, it will not be added to the organization as an individual repo associated with your account and you will not be able to push to it._**

## Description

The purpose of this assignment is to create an installable Node.js command line application package.
This is relatively straightforward. 

Read this article for an overview of how to create a 

## Setup

### Clone Bash version

The basis for this package will be a Bash command-line script example that you can find here: https://github.com/jdmar3/galo.sh/

In order for you to sucessfully complete this assignment you might want to clone and run `galo.sh`.
This will provide you with an example of how your new app, `galosh.js` should run. 

So, in a directory other than the working directory for this assignment, clone the `galo.sh` repo.

You must have `curl` and `jq` installed. Links to downloads are listed in the `galo.sh` repo README. They are available as package in most LInux distributions. MacOS users will have to download and install `jq`, but `curl` should already be installed.

## Assessment

The runner for assessing this assignment is configured to run through all of the available command line switches/options specified in the help file.

Your command line app should be able to do the following: 

1. The package should be installable using NPM (i.e., `npm link` should install it on the runner). 
2. Invoking `galosh.js` on the command line after running `npm link` should run the app.
3. `galosh.js -h` should echo the help message (see below) onto STDOUT and exit 0.
4. `galosh.js -j` should echo the JSON that your app ingested from Open-Meteo onto STDOUT and exit 0. 
5. All of the options in the help message below should work. 
6. If the daily precipitation hours in the JSON for the day you are targeting is not 0, log "You might need your galoshes " onto STDOUT. If the value is zero, then log "You will not need your galoshes " onto STDOUT.
7. If `-d 0` then log "today." onto STDOUT. If `-d [2-6]` then log "in NUMBER days." onto STDOUT. If `-d 1` or there is no `-d` specified, then log "tomorrow." onto STDOUT.
8. All of the latitude (`-n` and `-s`) and longitude (`-e` and `-w`) should take any number and convert it to a number with no more than 2 places to the right of the decimal AND be either a positive or negative number as appropriate (i.e., `-n` and `-e` should be positive numbers and `-s` and `-w` should be negative, so that they can be sent to the API correctly.
9. Your app should guess the system timezome and use it if there is no `-z` specified in the command line arguments.

## Instructions

### Setup

To get started, initialize your repo as a package by running `npm init`. 

Make sure that the license you select is the same as the one in the LICENSE file (it will be GPL-3.0-or-later for this and most assignments). This is always going to be expected in assignments.

The test script should be: 

`node cli.js -n 35.92 -w 79.05 -z America/New_York`

In the resulting `package.json` it should have this:

```
  "scripts": {
    "test": "node cli.js -n 35.92 -w 79.05 -z America/New_York"
  },
```

Change the information you input from the defaults so the package is yours (name, author, etc.). Customize it to you.

### Install dependencies

You will need to use npm to install the following packages:

- minimist
- node-fetch
- moment-timezone

### Make package installable

Edit `package.json` to include:

```
  "bin": {
    "galosh.js": "./cli.js"
  },
```

This will allow you to then run `npm link` to install your package and use `galosh.js` instead of `node cli.js`. You can uninstall (unlink) it by running `npm unlink`.

While you're editing `package.json`, add the following so that Node doesn't throw an error:

```
"type": "module",
```

### Create the script file

Create a file called `cli.js`. 

The first line of the file should be a shebang for Node:

```
#!/usr/bin/env node
```

### Create the help text

One of the first things you will want to do is look or the `-h` option in the command line and if it is there, log the following help text and exit 0.
0 is the exit code for "everything worked." 1 means "there was an error."

```
Usage: galosh.js [options] -[n|s] LATITUDE -[e|w] LONGITUDE -z TIME_ZONE
    -h            Show this help message and exit.
    -n, -s        Latitude: N positive; S negative.
    -e, -w        Longitude: E positive; W negative.
    -z            Time zone: uses tz.guess() from moment-timezone by default.
    -d 0-6        Day to retrieve weather: 0 is today; defaults to 1.
    -j            Echo pretty JSON from open-meteo API and exit.
```

### Timezone

### Find the appropriate request URL

### Construct a `fetch()` API call that will return the JSON data you need.

### Create the response text using conditional statements.

### Test your code

Make sure that your code works by doing the following:




