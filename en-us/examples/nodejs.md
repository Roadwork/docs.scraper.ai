# HTML Extractor API - Node.JS

## Getting Started

1. Create a new `package.json` with `npm init -y`
2. Create an empty `index.js` file
3. Install `node-fetch` through `npm i node-fetch --save`
4. [Get an API key on the Scraper.AI dashboard](/en-us/extractor/api_key.md)

## Creating our Code

We are now set to create our code that will fetch the HTML for any website we want! In the created `index.js` file, put the following code:

**index.js**

```javascript
const fetch = require('node-fetch');
const fs = require('fs');

const apiToken = process.argv[2];
const url = process.argv[3];

async function start() {
  const req = await fetch(`https://proxy.scraper.ai?url=${url}&is_render=true&api_key=${apiToken}`);
  const html = await req.text();

  fs.writeFileSync('index.html', html);
}

start().catch(e => console.error(e));
```

## Running

Once this is done, we can run the example above through `node index.js <YOUR_TOKEN> <YOUR_URL>` which will get the HTML from the Proxy Server and put it in an `index.html` file where the process is started.