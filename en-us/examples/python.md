# HTML Extractor API - Python

## Getting Started

1. Create a `main.py` file that will contain all our content required
2. Install the requests library with `pip install requests`
3. [Get an API key on the Scraper.AI dashboard](/en-us/extractor/api_key.md)

## Creating our Code

We are now set to create our code that will fetch the HTML for any website we want! In the created `main.py` file, put the following code:

**main.py**

```python
import sys
import asyncio
import requests

async def start():
  api_key = sys.argv[1]
  url = sys.argv[2]

  res = requests.get(f"https://proxy.scraper.ai?url={url}&is_render=true&api_key={api_key}")
  print(res.text)

if __name__ == "__main__":
  import time
  s = time.perf_counter()
  asyncio.run(start())
  elapsed = time.perf_counter() - s
  print(f"{__file__} executed in {elapsed:0.2f} seconds.")
```

## Running

Once this is done, we can run the example above through `python main.py <YOUR_TOKEN> <YOUR_URL>` which will get the HTML from the Proxy Server and display it in the terminal.