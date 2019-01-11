# Iconify icons collection in JSON format

This is collection of SVG icons created by various authors, released under various free licenses. Some collections require attribution when used for commercial purposes. See [collections.md](./collections.md) for list of collections and their licenses.

All SVG icons have been cleaned up. Content has been optimized, colors for monotone icons have been replaced with currentColor, ready to be inserted in HTML. Tools used for creating this collection are available on [https://iconify.design](http://iconify.design/)

This library is intended to be used in packages that build components, such as Iconify Tools.


## How to get this repository

Instructions below are for Node.js and PHP projects.


#### Node.js

Run this command to add icons to your project:

```
npm install --save @iconify/json
```

Icons will be available in node_modules/@iconify/json

To resolve filename for any json file, use this:

```
const icons = require('@iconify/json');

// returns location of fa.json
let fa = icons.locate('fa');
```


#### PHP

Install and initialize Composer project. See documentation at [https://getcomposer.org](https://getcomposer.org)

Then open composer.json and add following code:

```
"require": {
    "php": ">=5.6",
    "iconify/json": "*"
}
```

then run:

```
composer install
```

Icons will be available in vendor/iconify/json/

If you don't use Composer, clone GitHub repository and add necessary autoload code.

To resolve filename for any json file, use this:

```
// returns location of fa.json
$fa = \Iconify\IconsJSON\Finder::locate('fa');
```


## Format

Icons used by Iconify are in directory json, in Iconify JSON format.

Why JSON instead of SVG? To load images in bulk. 

If you need individual SVG images, you can generate them using Iconify JSON Tools. See instructions for [PHP version](https://github.com/iconify-design/json-tools.php) or [Node.js version](https://github.com/iconify-design/json-tools.js).


Format of json file is very simple:

```
{
    "icons": {
        "icon-name": {
            "body": "svg body",
            "width": width,
            "height": height
        }
    },
    "aliases": {
        "icon-alias": {
            "parent": "icon-name"
        }
    },
    "width": default width,
    "height": default height
}
```

"icons" object contains list of all icons.

Each icon has following properties:
* body - icon body
* width - width in pixels
* height - height in pixels
* rotate - rotation. Default = 0. Values: 0 = 0deg, 1 = 90deg, 2 = 180deg, 3 = 270deg
* hFlip - horizontal flip. Boolean value, default = false
* vFlip - vertical flip. Boolean value, default = false
* hidden - If set to true, icon is hidden. That means icon was removed from collection for some reason, but it is kept in JSON file to prevent applications that rely on old icon from breaking

Width or height might be missing. If icon does not have width or height, use default width or height from root object.
rotate, hFlip and vFlip are all optional.

Optional "aliases" object contains list of aliases for icons. Format is similar to "icons" object, with additional property "parent" that points to parent icon. Any other properties overwrite properties of parent icon.

For more information see developer documentation on [https://iconify.design/docs/json-icon-format/](https://iconify.design/docs/json-icon-format/)

## Extracting individual SVG icons

See JSON tools readme for instructions for [PHP](https://github.com/iconify-design/json-tools.php) or [Node.js](https://github.com/iconify-design/json-tools.js).

```
const fs = require('fs');
const {SVG, Collection} = require('@iconify/json-tools');

let collection = new Collection();
collection.loadIconifyCollection('mdi');
collection.listIcons(true).forEach(icon => {
    let svg = new SVG(collection.getIconData(icon));
    fs.writeFileSync('mdi-' + icon + '.svg', svg.getSVG({
        height: 'auto'
    }));
});
```

```
use \Iconify\JSONTools\Collection;
use \Iconify\JSONTools\SVG;

$collection = new Collection();
$collection->loadIconifyCollection('mdi');
foreach ($collection->listIcons(true) as $icon) {
    $svg = new SVG($collection->getIconData($icon));
    file_put_contents('mdi-' . $icon . '.svg', $svg->getSVG([
        'height'    => 'auto'
    ]));
}
```

## License

This is collection of works by various authors, not original collection.

See [collections.md](./collections.md) for list of collections and their licenses.
