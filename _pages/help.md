---
layout: page
title: Help
include_in_header: true
---
# General

Esse is a swiss army knife of text transformation for iOS and macOS, it is built around a simple idea: you input text, apply transformation functions, and get text in result. That's it!

Some examples of things you can do:
* Enforce your text case preferred text case styling
* Remove unnecessary characters or lines
* Extract names, phones, emails, and addresses
* Prettify or minify JSON
* and much more

# iOS app

Esse is available on iOS and iPadOS as a paid upfront universal app, all features are available without subscription and in-app purchases.

Main features:
* **Library** - all Esse functions, including Custom Functions and External scripts, are grouped by category and available through search. Each function has an information screen and can be tested right there.
* **Quick** - this screen provides an Input field and a selection of functions(can be edited), the idea is to put your most-used functions there and one-tap copy the result.
* **Scratchpad** - this screen gives allows you to apply a sequence of functions to input text. This sequence can be saved as Custom Function
* **Share** and **Widget** - control functions that are exposed in Share Sheet Action and Today Widget.

## **Shortcuts**

Two shortcuts are exposed by Esse:
* **Transform Text** - accepts Text and Esse Functions, returns result of transformation.
* **Transform Text File** - accepts File Esse Functions, returns result of transformation. Optionally you can provide "Limit Scope(Pattern)" regular expression, to apply transformation only to selected parts of the file, i.e. apply text case styling only to headers in a markdown document.

## **Action Extension**

Action Extension is available anywhere in iOS though Share Sheet, it accepts text and provides a list of Esse Functions with a preview of transformation result - just one-tap to copy it to clipboard.

## **Today(Legacy) Widget**

Today Widget(widgets available before iOS 14) gives you quick access to Esse functions, tapping on function in widget takes clipboard content, applies selected function, and puts the result back to the clipboard.

# macOS

Esse strives to be a great macOS app and be available right where you need it, these are currently available features:
* The app itself features a clean two-panel UI, where you can see Input and Result next to each other, along with applied functions below it. The best experience comes with using keyboard shortcuts, refer to the menu items to discover it.
* Menu bar item gives you quick access to all Esse functions, your Favorites will appear on the first level with all other functions grouped by category. Clicking on functions in Esse's menu bar applies this function to clipboard content and puts the result back to the clipboard.
* Esse provides System Service for text, which means you can access it from any app in the Services menu or using a hotkey. System Service puts selected text into Esse' Input field.
* Command line tool - all Esse functions are available through a command line interface, which means you can integrate Esse in shell scripts. Official [Alfred Workflow](https://github.com/amebalabs/Esse/tree/master/Alfred) is an example of command line tool usage.

# Functions Library

## **Built-in Functions**

Esse bundled with more than 60 functions out of the box, these functions are grouped in 8 categories:

* Cleaning 
* Case
* Developer
* Quatation Marks
* Convert
* Extract
* ASCII
* Other

## **Custom Functions**

You can be a productivity ninja and combine a sequence of functions in one "Custom Function". This is the easiest way to customize Esse and build your functions.

For example you can build a "Clean Text" function by combining "Remove Duplicate Lines" -> "Remove Empty Lines" -> "Remove Quote Prefixes" -> "Truncate Spaces". 

## **External Scripts**

External scripts are JavaScript files that follow a specific structure and can be used to add new functions to Esse.

External scripts are stored in Esse' folder on the iCloud drive, you can access it in the Files app on iOS and in Finder on macOS. Esse monitors this folder for changes and refreshes scripts automatically, but you can do it manually as well from app settings.

### Scripts Repository

The official repository for Esse external scripts can be found on [GitHub](https://github.com/amebalabs/Esse). Feel free to open a pull request if you want to fix a bug or add a new script!

Currently, there is no integration of scripts repository with the app, just download scripts and put them into the scripts folder.

### Script Structure

#### Metadata

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

#### Entry Point

The script must declare a top level function main() which takes one parameter and returns a string.

```jsx
function main(input) {
 // do something
 return value //return a string
}
```

#### Example Script

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

## **URL Scheme**

The Esse app registers the custom URL scheme **esse://**. The following paths are currently implemented:

### iOS and macOS

* **replace?text=Text** - clear Input field and put **Text** into it
* **clipboard** - clear Input field and put clipboard content into it
* **clear** - clear Input field

### macOS

* **copyresult** - copy Result field to clipboard
* **resetfunctions** - reset selected functions\transforms