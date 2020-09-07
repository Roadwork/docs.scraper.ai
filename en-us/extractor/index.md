# Scraper.AI HTML Extractor

At Scraper.AI we offer the tools you need to extract data from any website successfully! That's why we exposed our HTML extraction engine that is powering our no-code engine as well for developers to use! 

## Core Features

* Gather the Full HTML of any website page
  * Single-Page Application (SPA) supported
  * Javascript (JS) rendering supported
  * XHR requests supported
* Captcha solving
* Proxy rotating
* Identity masking
* Authenticated Page support
* Custom headers support
* Complex cookie support
* Await selectors to make sure you get the content you want

## Usage

Utilizing the extractor is as simple as [requesting an API key](/en-us/extractor/api-key.md) and sending a simple GET request to the endpoint `extract.scraper.ai` with the query parameters related to your request.

Example:

```bash
curl "https://extract.scraper.ai/api_key=<YOUR_API_KEY>&url=<YOUR_URL>
```

## Advanced Usage

Next to the simple extraction method, you are definitely able to utilize this API to extract more complex pages. For this you can find several use cases below:

### Custom Headers

Custom headers are supported (e.g. User Agent, Cookies, ...), to utilize this, just simply pass any of the headers as you would pass them in a normal request.

```bash
curl -i -H 'hello: "world"' "https://extract.scraper.ai/?api_key=<YOUR_API_KEY>&url=https://httpbin.org/anything&is_render=true"
```

### SPA / JS Rendering

For dynamic webpages you can simple append the `is_render=true` query parameter to extract these pages.

```bash
curl "https://extract.scraper.ai/api_key=<YOUR_API_KEY>&url=<YOUR_URL>&is_render=true
```

### Authenticated Pages Support

Authenticated pages are a complex use case that is not a simple as passing the `document.cookie` value from a website! That's why we added a customer header flag that allows you to pass more complex cookies to extract authenticated pages.

```bash
curl -i -H 'scraper-ai-cookie: [{"domain":".httpbin.org","expirationDate":1662550207,"hostOnly":false,"httpOnly":false,"name":"example_cookie","path":"/","sameSite":"unspecified","secure":false,"session":false,"storeId":"0","value":"scraper_ai_example_value"}]' "https://extract.scraper.ai/?api_key=<YOUR_API_KEY>&url=https://httpbin.org/anything&is_render=true"
```

### Wait for Selector

Next to all of the above, you sometimes also have to wait for a selector to come in view. This because some websites perform an XHR call later, or its something not supported by trivial browser, or you simply want to make sure that the selector exists on the page. That's why we have as well incorporated the `scraper-ai-waitfor` header that does just this for any amount of `CSS Paths` you pass through it in an array shape, e.g. `[ "body > div" ]`.

**Example 1 : Successful Load**

```bash
curl -i -H 'scraper-ai-waitfor: [ "#swagger-ui > div > div:nth-child(2) > div.information-container.wrapper > section > div > hgroup > h2" ]' "https://extract.scraper.ai/?api_key=<YOUR_API_KEY>&url=https://httpbin.org&is_render=true"
```

Which will load correctly and show the HTML

**Example 2 : Selector Not Found**

```bash
curl -i -H 'scraper-ai-waitfor: [ "body > div:nth-of-type(1) > div > div > div:nth-of-type(2) > main > div > div > div > div:nth-of-type(1) > div > div:nth-of-type(4) > div > div > section > div > div > div > div > div > article > div > div > div > div:nth-of-type(2) > div:nth-of-type(2) > div:nth-of-type(1) > div > div > div:nth-of-type(1) > div:nth-of-type(1) > a > div > div:nth-of-type(1) > div:nth-of-type(1) > span > span:nth-of-type(1)" ]' "https://extract.scraper.ai/?api_key=<YOUR_API_KEY>&url=https://httpbin.org&is_render=true"
```

Which will not load and show an empty response with a timeout