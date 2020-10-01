# HTML Extractor API - C#

## Getting Started

1. Create a new console solution through `dotnet new console -o ./` (this will create a new solution in the current repository)
2. [Get an API key on the Scraper.AI dashboard](/en-us/extractor/api_key.md)

## Creating our Code

We are now set to create our code that will fetch the HTML for any website we want! In the created `Program.cs` file, put the following code:

**Program.cs**

```csharp
using System;
using System.IO;
using System.Net;

namespace dotnet
{
  class Program
  {
    static void Main(string[] args)
    {
      var apiKey = args[0];
      var url = args[1];

      // Create a Request for the URL
      WebRequest request = WebRequest.Create($"https://proxy.scraper.ai?url={url}&is_render=true&api_key={apiKey}");

      // Get the response
      WebResponse response = request.GetResponse();

      // Get the stream containing content returned by the server.
      // The using block ensures the stream is automatically closed.
      using (Stream dataStream = response.GetResponseStream())
      {
        // Open the stream using a StreamReader for easy access.
        StreamReader reader = new StreamReader(dataStream);

        // Read the content.
        string responseFromServer = reader.ReadToEnd();
        
        // Display the content.
        Console.WriteLine(responseFromServer);
      }

      // Close the response.
      response.Close();
    }
  }
}
```

## Running

Once this is done, we can run the example above through `dotnet run <YOUR_TOKEN> <YOUR_URL>` which will get the HTML from the Proxy Server and display it in the terminal.