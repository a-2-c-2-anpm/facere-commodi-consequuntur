
# @a-2-c-2-anpm/facere-commodi-consequuntur

Converts XML into a human readable format (pretty print) while respecting the `xml:space` attribute.

Reciprocally, the `@a-2-c-2-anpm/facere-commodi-consequuntur` package can minify pretty printed XML.

The `@a-2-c-2-anpm/facere-commodi-consequuntur` package can also be used on the browser using the browserified version with a small footprint.

[![Build Status](https://github.com/a-2-c-2-anpm/facere-commodi-consequuntur/actions/workflows/ci.yml/badge.svg)](https://github.com/a-2-c-2-anpm/facere-commodi-consequuntur/actions/workflows/ci.yml) [![npm version](https://img.shields.io/npm/v/@a-2-c-2-anpm/facere-commodi-consequuntur.svg)](https://npmjs.org/package/@a-2-c-2-anpm/facere-commodi-consequuntur)

## Installation

```
$ npm install @a-2-c-2-anpm/facere-commodi-consequuntur
```

## Example

### Usage:

```js
import xmlFormat from '@a-2-c-2-anpm/facere-commodi-consequuntur';

xmlFormat('<root><content><p xml:space="preserve">This is <b>some</b> content.</content></p>');
```

### Output:

```xml
<root>
    <content>
        <p xml:space="preserve">This is <b>some</b> content.</p>
    </content>
</root>
```

## Options

- `filter`: Function to filter out unwanted nodes by returning `false`.
  - type: `function(node) => boolean`
  - default: `() => true`
- `ignoredPaths`: List of XML element paths to ignore during formatting. 
This can be a partial path (element tag name) or full path starting from the document element e.g. `['/html/head/script', 'pre']`.
  - type: `string[]`
  - default: `[]`
- `indentation`: The value used for indentation.
  - type: `string`
  - default: `'    '`
- `collapseContent`: True to keep content in the same line as the element. Only works if element contains at least one text node.
  - type: `boolean`
  - default: `false`
- `lineSeparator`: Specify the line separator to use.
  - type: `string`
  - default: `\r\n`
- `whiteSpaceAtEndOfSelfclosingTag`: True to end self-closing tags with a space e.g. `<tag />`.
  - type: `boolean`
  - default: `false`
- `throwOnFailure`: Throw an error when XML fails to parse and get formatted otherwise the original XML is returned.
  - type: `boolean`
  - default: `true`
- `forceSelfClosingEmptyTag`: True to force empty tags to be self-closing.
  - type: `boolean`
  - default: `false`

### Usage:
 
```js
import xmlFormat from '@a-2-c-2-anpm/facere-commodi-consequuntur';

xmlFormat('<root><!-- content --><content><p>This is <b>some</b> content.</content></p>', {
    indentation: '  ', 
    filter: (node) => node.type !== 'Comment', 
    collapseContent: true, 
    lineSeparator: '\n'
});

```

### Output:

```xml
<root>
  <content>
    <p>This is <b>some</b> content.</p>
  </content>
</root>
```

## Minify mode

### Usage:

```js
import xmlFormat from '@a-2-c-2-anpm/facere-commodi-consequuntur';

const xml = `
<root>
  <content>
    <p>
        This is <b>some</b> content.
    </p>
  </content>
</root>`;

xmlFormat.minify(xml, {
    filter: (node) => node.type !== 'Comment',
    collapseContent: true
});

```

### Output:

```xml
<root><content><p>This is<b>some</b>content.</p></content></root>
```

## On The Browser

The code is transpiled using [Babel](https://babeljs.io/) with [@babel/preset-env](https://babeljs.io/docs/en/babel-preset-env) default values and bundled using [browserify](https://browserify.org/).

### Using `require('@a-2-c-2-anpm/facere-commodi-consequuntur')`

### Page:
 
```html
<script type="text/javascript" src="dist/browser/@a-2-c-2-anpm/facere-commodi-consequuntur.js"></script>
```

### Usage:
 
```js
const xmlFormatter = require('@a-2-c-2-anpm/facere-commodi-consequuntur');

xmlFormat('<root><content><p xml:space="preserve">This is <b>some</b> content.</content></p>');
```

### Using global function `xmlFormatter`

### Page:

```html
<script type="text/javascript" src="dist/browser/@a-2-c-2-anpm/facere-commodi-consequuntur-singleton.js"></script>
```

### Usage:

```js
xmlFormatter('<root><content><p xml:space="preserve">This is <b>some</b> content.</content></p>');
```

### Output

```xml
<root>
    <content>
        <p xml:space="preserve">This is <b>some</b> content.</p>
    </content>
</root>
```

## License

MIT
