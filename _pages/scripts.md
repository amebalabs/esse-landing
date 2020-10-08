---
layout: page
title: External Scripts
include_in_header: false
---

# External Scripts

## What and Why

External scripts are JavaScript files which follow a specific structure and can be used to add new functions to Esse.

External scripts are stored in Esse' folder on iCloud drive, you can access it in Files app on iOS and in Finder on macOS. Esse monitors this folder for changes and refreshes scripts automatically, but you can do it manually as well from app settings.

## Scripts Repository

Official repository for Esse external scripts can be found on [GitHub](https://github.com/amebalabs/Esse). Feel free to open a pull request if you want to fix a bug or add new script!

Currently, there is no integration of scripts repository with the app, just download scripts and put them into the scripts folder.

# Script Structure

## Metadata

```json
/**
{
    "id": "co.ameba.Esse.ExternalFunctions.ReverseSortLines",
    "name":"Reverse sort lines",
    "description":"Sort lines in reverse order",
    "category":"Convert",
    "author":"Ameba Labs",
}
**/
```

- **id** - unique identifier, can be any string
- **name**, **description** and **author** are self explanatory
- **category** can be one of the following: *Custom, Cleaning, Case, Convert, ASCII, Extract, Quotation Marks, Other, Developer.*

## Entry Point

The script must declare a top level function main() which takes one parameter and returns a string.

```jsx
function main(input) {
	// do something
	return value //return a string
}
```

## Example Script

A script to sort lines in reverse order:

```
/**
{
    "id": "co.ameba.Esse.ExternalFunctions.ReverseSortLines",
    "name":"Reverse sort lines",
    "description":"Sort lines in reverse order",
    "category":"Convert",
    "author":"Ameba Labs",
}
**/

function main(input) {
	return input.split('\n').reverse().join('\n');
}
```