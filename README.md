VSCODE-TODO-HIGHLIGHT
===

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://opensource.org/licenses/MIT) [![Build Status](https://travis-ci.org/wayou/vscode-todo-highlight.svg?branch=master)](https://travis-ci.org/wayou/vscode-todo-highlight) [![Version](http://vsmarketplacebadge.apphb.com/version-short/wayou.vscode-todo-highlight.svg)](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) [![Installs](http://vsmarketplacebadge.apphb.com/installs-short/wayou.vscode-todo-highlight.svg)](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) [![Ratings](http://vsmarketplacebadge.apphb.com/rating-short/wayou.vscode-todo-highlight.svg)](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight)

Highlight `TODO`,`FIXME` or any annotations within your code.

Sometimes you will forget to review the TODOs added while coding till publish the code to production.
So I've been long for an extension to highlight them and remind me know there're notes or things not done yet.

Hope this extension helps you as well.

### Preview

- with `material night` color theme:
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/material-night.png)

- with `material night eighties` color theme:
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/material-night-eighties.png)

### Config

`TODO:`,`FIXME:` are built in keywords. You can override the look by customizing the setting.

To custom the keywords and other stuff, <kbd>command</kbd> + <kbd>,</kbd> (Windows / Linux: File -> Preferences -> User Settings) open vscode `settings.json` file.

||type|default|description|
|---|---|---|---|
|todohighlight.isEnable|boolean|true|Toggle the highlight, default is true.|
|todohighlight.isCaseSensitive|boolean|true|Whether the keywords are case sensitive or not.|
|todohighlight.keywords|array|N/A|An array of keywords that will be hilighted. You can also specify the style for each keywords here. See example below for more infomation.|
|todohighlight.keywordsPattern|string|N/A|Specify keywords via RegExp instead of `todohighlight.keywords` one by one. NOTE that if this presents, `todohighlight.keywords` will be ignored. And REMEMBER to escapse the back slash if there's any in your regexp (using \\ instead of signle back slash). |
|todohighlight.defaultStyle|object|N/A|Specify the default style for custom keywords, if not specified, build in default style will be applied. [Checkout all the available styling properties](https://code.visualstudio.com/docs/extensionAPI/vscode-api#_a-namedecorationrenderoptionsaspan-classcodeitem-id269decorationrenderoptionsspan).|
|todohighlight.include|string|`{**/*.js,**/*.jsx,**/*.ts,**/*.tsx,**/*.html,`<br>`**/*.php,**/*.css,**/*.scss}`|A glob pattern that defines the files to search for. Only include files you need, DO NOT USE `{**/*.*}` for both permormance and avoiding binary files reason.|
|todohighlight.exclude|string|`{**/node_modules/**,**/bower_components/**,`<br>`**/dist/**,**/build/**,**/.vscode/**,`<br>`**/_output/**,**/*.min.*,**/*.map}`|A glob pattern that defines files and folders to exclude while listing annotations.|
|todohighlight.maxFilesForSearch|number|5120|Max files for searching, mostly you don't need to configure this.|
|todohighlight.toggleURI|boolean|false|If the file path within the output channel not clickable, set this to true to toggle the path patten between `<path>#<line>` and `<path>:<line>:<column>`.|


an example of customizing configuration:

```js
{
    "todohighlight.isEnable": true,
    "todohighlight.isCaseSensitive": true,
    "todohighlight.keywords": [
        "DEBUG:",
        "REVIEW:",
        {  
            "text": "NOTE:",
            "color": "#ff0000",
            "backgroundColor": "yellow",
            "overviewRulerColor": "grey" 
        },
        {
            "text": "HACK:",
            "color": "#000",
            "isWholeLine": false,
        },
        {
            "text": "TODO:",
            "color": "red",
            "borderRadius":"0px",
            "backgroundColor": "rgba(0,0,0,.2)",
            //other styling properties goes here ... 
        }
    ],
    "todohighlight.keywordsPattern": "TODO:|FIXME:|\\(([^)]+)\\)",//highlight `TODO:`,`FIXME:` and content between parentheses
    "todohighlight.defaultStyle": {
        "color": "red",
        "backgroundColor": "#ffab00",
        "overviewRulerColor": "#ffab00",
        "borderRadius":"2px",
        "cursor":"pointer",
        "border":"1px solid #eee",
        "isWholeLine": true,
        //other styling properties goes here ... 
    },
    "todohighlight.include": "{**/*.js,**/*.jsx,**/*.ts,**/*.tsx,**/*.html,**/*.php,**/*.css,**/*.scss}",
    "todohighlight.exclude": "{**/node_modules/**,**/bower_components/**,**/dist/**,**/build/**,**/.vscode/**,**/_output/**,**/*.min.*,**/*.map}",
    "todohighlight.maxFilesForSearch": 5120,
    "todohighlight.toggleURI": false,
}
```

### Commands

This extension contributes the following commands to the Command palette.

- `Toggle highlight` : turn on/off the highlight
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/toggle-highlight.gif)
- `List hilighted annotations` : list annotations and reveal from corresponding file
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/list-annotations.gif)


### Known issue

 The clickable file pattern within the output channel differs from OS platform(`<path>#<line>` for Mac/Windows and `<path>:<line>:<column>` for Linux, for detail see this [issue](https://github.com/Microsoft/vscode/issues/586) ). 

 Basically the extension auto detect OS platform.

 If you find file path not clickable, set `todohighlight.toggleURI` to `true` to toggle the file pattern.
  
