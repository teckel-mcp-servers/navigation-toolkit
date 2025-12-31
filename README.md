# navigation toolkit
This MCP server gives LLM/AI/Agents the ability to provide accurate navigation information. There are three main application areas (all can be combined): time &amp; place, road-trips, and general aviation.

## Time and Place
Accurate determination of local time and sun position at any place in the world, taking into account time zones and daylight savings corrections.
### LLM prompt examples using these tools:

_“How many hours of daylight will there be on the Isle of Man on June 15th this year?”_

_“What time is it in Hong Kong right now, and what are the light conditions (daylight, twilight, or darkness)?”_

_“What time is sunrise and sunset in Hamburg, Germany tomorrow?”_

_“My flight is departing for San Francisco from London at 3 hours from now. The flight will take ten hours. What time will it be when I arrive in San Francisco, and what will the lighting conditions be?”_

## Roadtrips
Accurate determination of driving distances and times anywhere in the world, taking into account current traffic (and allowing for ferry trip times if water crossing required). Computation of latitude and longitude for any place specified by address, postal code, name, landmark, etc. Search for hotels, restaurants, or any other typical feature, within a specified range of any location.
### LLM prompt examples using these tools:

_“What is the distance, and how long will it take, to drive from Joshua Tree to Oakland CA?”_

_“Find me 10 hotels within 20 miles of Prestwick Airport, UK”_

_“What is the latitude and longitude of UK postcode IM4 7BN?”_

_“If I drive from Berlin to Munich tomorrow, departing at 9am local time, will it be dark when I arrive?”_

## General Aviation
Accurate computation of distances between points on Earth using the World Geodetic System 1984 (WGS84), the geodetic reference system that defines the Earth’s shape and size as an oblate spheroid, the standard for the Global Positioning System (GPS). The distances can be computed either as great-circles (i.e., shortest distance between the two points) or rhumblines (i.e., the distance measured along a straight line drawn on a mercator projection map).
Accurate computation of the end-point for a given start-point, bearing, and range. The bearing can be referenced to either true or magnetic north (if magnetic, the magnetic variation is automatically calculated and corrected for), and the track can be specified as a great circle or rhumbline.

Search for airports within a specified range from any location in the world, with multiple optional filters (such as “must have AVGAS” etc). For the US only, can also search for navaids, fixes, features, and obstacles.
Obtain the latest aviation weather report (METAR) and forecast (TAF) for any worldwide ICAO designated weather station (in raw and decoded formats). Find the nearest ICAO designated weather station to a given location, or multiple stations within a specified range of that location.

Computation of aviation-pertinent atmospheric parameters (versus altitude) given the measured temperature and pressure (from METARs).
Perform VFR (Visual-Flight-Rules) flight route calculations between specified origin and destination airfields, plus up to ten optional intermediate waypoints (when not routing direct). Automatically computes wind corrections (using latest METARs along the route, and assuming a power-law extrapolation from METAR measured winds at 10m AGL to wind aloft), magnetic variation, and sunlight conditions (e.g., if daylight, twilight, or night-time at each waypoint plus direction (azimuth and zenith) to the sun relative to flight track (to assess if glare will be an issue). For the origin and departure airfields, gives essential information for each runway (surface, dimensions) plus the crosswind and headwind/tailwind components (computed from latest METARs), plus, where the information is available, details on runway lighting, visual approach aids, and instrument approach aids. Also provides the communication frequencies for the origin and departure airfields, plus where the information is available, telephone contact details, operating hours, and whether PPR is required. Utilizes current atmospheric conditions (from latest METAR data) to model the atmosphere (and its deviations from the International Standard Atmosphere) in order to compute for example, density altitude at the departure airfield, true airspeed (TAS), Mach number, and estimated cloud-base and freezing altitude along the route, and pressure altitude at each waypoint (i.e., the altitude displayed on the altimeter when set at standard pressure setting, useful for flight level determination). All navigation timings are presented in UTC as well as in local time (taking account of timezone and Daylight-Savings corrections). As well as providing a route summary (total distance, flight time, fuel consumption), all relevant data is provided per leg to facilitate the generation of a navlog (e.g., groundspeed, distance, timings, magnetic heading and true track, fuel used, etc). Aircraft Performance and route profile data (indicated airspeed, altitude, fuel flow rate) can be specified or default values (100kts, 2500ft 8 USgal/hour) are used if omitted. The latest METAR (current weather) and TAF (forecasts) reports are provided for each waypoint. A URL is also provided which enables the route to be viewed on skyvector.com (via any web browser). From there, the route can be exported to popular pilot apps such as Garmin Pilot, ForeFlight etc.

### LLM prompt examples using these tools:

_“What is the great-circle distance between Prestwick Airport and Goodwood Airfield in the UK?”_

_“What is the latitude and longitude of the location 25 nautical miles on a true bearing of 335 degrees from EGNS?”_

_“What is the latitude and longitude of the location 45 nautical miles on a magnetic bearing of 85 degrees from the Daventry VOR (DTY) in the UK?”_

_“What is the nearest METAR report for Wolverhampton Airport, UK?”_

_“Perform the flight route calculations for a VFR flight from Wolverhampton Airport, UK, to EGTK, with intermediate waypoint 15 nautical miles on a magnetic bearing of 210 degrees from Wolverhampton. Indicated airspeed will be 95 kts, altitude 2000 ft, departing Wolverhampton 45 minutes from now. Provide details for the navlog, plus a skyvector URL.”_

Then,
_“How long is the drive from EGTK to Chipping Norton?”_

_“Perform the flight route calculations for a VFR flight from Palo Alto Airport, CA, to Half Moon Bay airport, CA, with an intermediate waypoint overflying Stanford University. Indicated airspeed will be 100 kts, altitude 3000 ft, departing Palo Alto two hours from now. Provide details for the navlog, plus a skyvector URL.”_

Then,
_“Are there any Mexican restaurants within 10 miles of Half Moon Bay airport?”_

## How to Use the teckel Toolkits

### First generate an API key using the teckel App.

Do the following:

1. Install the teckel App and create (or import) an Ethereum Account.

2. Navigate to the Accounts page by tapping on the wallet icon in the upper right corner of the App home screen. Access the API Key Manager for the created or imported Ethereum Account by tapping “Manage API Key” on the Accounts page.

3. Use the API key when making calls to the endpoints. All the available endpoints are available via the teckel App, incorporating the actual API key for the given Ethereum Account.

4. For illustrative purposes, we will use the following fake key d1e12345-c234-45a6-9b76-1234567891ff in the examples presented below. You would substitute your actual API key in place of this fake key.

### Next, decide if you are using the MCP servers or RESTful (API) to access the tools.

# Using the MCP Servers
## Configure your MCP client-of-choice
Whatever the client, the configuration is essentially the same. Namely, provide the client with the MCP server endpoint and access credentials. These are typically in the form of a configuration JSON snippet, using your API key as the “Bearer” token in the “Authorization” tag. For example, here is the precise configuration for use with the Cursor desktop app (navigate within the Cursor app to the Cursor Settings -> Tools & MCP -> + New MCP server and enter these details using your actual teckel API key to replace this fake one).
### MCP JSON configuration (example for use with Cursor)
```
{
 "mcpServers": {    
    "teckel-navigation-toolkit": {
      "url": "https://mcp-servers.bh.tkllabs.io:9780/navigation-mcp",
      "headers": {
        "Authorization": "Bearer d1e12345-c234-45a6-9b76-1234567891ff"
      }
    }   
  }
}
```
NOTE: This configuration assumes the HTTP(streamable) protocol. If your client requires the older (now legacy) SSE protocol, replace “navigation-mcp” with “navigation-sse”.

### MCP JSON Configuration (example for use with n8n)
Similarly, for use with n8n, below is the JSON code snippet for a sample workflow which accesses the teckel Ethereum and Navigation Toolkits MCP servers. (Save this entire snippet to a .json file; then import the file to your n8n workflow.) You will need to replace the credentials with your own “Bearer Auth” credential within n8n (using your teckel API key as the “Bearer token”). 
```
{
  "name": "Teckel Tools MCP Example",
  "nodes": [
    {
      "parameters": {
        "endpointUrl": "https://mcp-servers.bh.tkllabs.io:9780/ethereum-mcp",
        "authentication": "bearerAuth",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.mcpClientTool",
      "typeVersion": 1.2,
      "position": [
        -16,
        640
      ],
      "id": "569bf922-b8cb-40a0-beb8-2da890dab925",
      "name": "Teckel Tools MCP server: ethereum",
      "credentials": {
        "httpBearerAuth": {
          "id": "zPHt516IS5uuS2S5",
          "name": "TECKEL APIKEY"
        }
      }
    },
    {
      "parameters": {
        "modelId": {
          "__rl": true,
          "value": "gpt-5",
          "mode": "list",
          "cachedResultName": "GPT-5"
        },
        "messages": {
          "values": [
            {
              "content": "Perform a VFR flight route calculation from EGNS to EGPK, departing 60 minutes from now. Include an intermediate waypoint on magnetic bearing 320 degrees at 20 nm from EGNS, followed by another on true bearing 355 for 15 nm from the previous waypoint.\n"
            }
          ]
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.openAi",
      "typeVersion": 1.8,
      "position": [
        -496,
        368
      ],
      "id": "5c9a94cd-71a4-4d77-84f5-664ef14871af",
      "name": "Message a model",
      "credentials": {
        "openAiApi": {
          "id": "EvoF3L2GoYTtESR3",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "endpointUrl": "https://mcp-servers.bh.tkllabs.io:9780/navigation-mcp",
        "authentication": "bearerAuth",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.mcpClientTool",
      "typeVersion": 1.2,
      "position": [
        192,
        640
      ],
      "id": "016dae90-92b4-4eed-9120-f8531bafbd10",
      "name": "Teckel Tools MCP server: navigation",
      "credentials": {
        "httpBearerAuth": {
          "id": "zPHt516IS5uuS2S5",
          "name": "TECKEL APIKEY"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "Teckel Tools MCP server: ethereum": {
      "ai_tool": [
        [
          {
            "node": "Message a model",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "Teckel Tools MCP server: navigation": {
      "ai_tool": [
        [
          {
            "node": "Message a model",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "626e0784-a43b-4857-bf54-91e7f1c32c59",
  "meta": {
    "templateId": "self-building-ai-agent",
    "templateCredsSetupCompleted": true,
    "instanceId": "3c7702199c1f42229c256ae3782d70f8576bc5028e557d0903826477f97e032b"
  },
  "id": "rAm1XjSle8lYmOcT",
  "tags": []
}
```
# Using the RESTful API Servers
The benefit of using the MCP servers is that the connected LLMs can parse the natural language in the user prompts, populate the required parameters for calling the toolbox API functions, then likewise unravel the returned JSON structure into natural language for presentation to the user. However, if you wish to utilise the teckel toolkits at a lower level (e.g., in your own app), you can call the functions directly using the RESTful (POST) API protocols. You are then responsible for populating the input parameters, and handling the returned JSON output.

The base API URL endpoint is identical to the MCP server endpoint:
```
https://mcp-servers.bh.tkllabs.io:9780/
```
The desired function name must be appended to this URL, and the function arguments must be added as query-string parameters. The teckel API key must be added as a Bearer Token in the Authorization header. The POST protocol must be used (rather than GET), but the body can be empty since the parameters are passed in the query-string.  Below is an example curl request for calling the _perform_sun_calculations_ from the Navigation Toolkit with the required parameters:
### Curl Request
```
curl -X POST \   'https://mcp-servers.bh.tkllabs.io:9780/perform_sun_calculations?latitude=54&longitude=-4.4861228&altitudeMetres=100&dateTimeUTCstr=25-Oct-2025%2014:18:39' \
  -H 'Authorization: Bearer d1e12345-c234-45a6-9b76-1234567891ff' \
  -H 'Content-Type: application/json'
```
### JSON Response
```
{"results":{"sunElevation":17.66329058182842,"sunAzimuth":215.1455213675287,"sunriseUTC":"25-Oct-2025 07:04:51","sunriseAzimuth":109.78189990283305,"sunsetUTC":"25-Oct-2025 16:58:17","sunsetAzimuth":249.96470561181022,"middayUTC":"25-Oct-2025 12:01:38","middaySunElevation":23.75305488041259,"daylightHours":"09:53:26"}}
```
## Functions (tools) list
The full suite of functions available in the toolkit can be found at https://teckel.io/ai-mcp-services/

## Pricing
Pricing (via _teckel credits_ purchased within the teckel App) for usage of each function in the toolkit can be found at https://teckel.io/ai-mcp-services/

## Rate Limiting
All MCP/API calls are subject to rate-limiting per API key. The thresholds are not published, but if a given API key has exceeded the rate limit, a 429 error code will be returned on the given call.

## Errors
If the MCP/API call fails due to user error resulting in a 4xx error code, the user is charged one Base Call Fee (see https://teckel.io/ai-mcp-services/). If the API call fails due to server error resulting in a 5xx error code, the user is not charged. If the given call is part of a cascade of nested calls, the above rules apply to the “outer” call: In other words, if the outer call fails with a 4xx error code, the user is charged one Base Call Fee (for the failed outer call), and there will be no charge for any of the cascaded calls (whether they succeeded or not). Likewise, if the outer call fails with a 5xx error code, the user is not charged at all (even if the cascaded calls succeed).
 
## Note on API Key Security
Should you have concerns that your API key has been compromised (and someone else may be consuming your teckel credits by using your key), simply replace the key via the API Key Manager → Replace API key in the teckel App. The old key will then be immediately disabled.
