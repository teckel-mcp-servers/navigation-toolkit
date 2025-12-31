# navigation-toolbox
The main purpose of the Navigation Toolbox is to give LLM/AI/Agents the ability to provide accurate navigation information. There are three main application areas (all can be combined): time &amp; place, road-trips, and general aviation.

## Time and Place
Accurate determination of local time and sun position at any place in the world, taking into account time zones and daylight savings corrections.
LLM prompt examples using these tools:

“How many hours of daylight will there be on the Isle of Man on June 15th this year?”

“What time is it in Hong Kong right now, and what are the light conditions (daylight, twilight, or darkness)?”

“What time is sunrise and sunset in Hamburg, Germany tomorrow?”

“My flight is departing for San Francisco from London at 3 hours from now. The flight will take ten hours. What time will it be when I arrive in San Francisco, and what will the lighting conditions be?”

## Roadtrips
Accurate determination of driving distances and times anywhere in the world, taking into account current traffic (and allowing for ferry trip times if water crossing required). Computation of latitude and longitude for any place specified by address, postal code, name, landmark, etc. Search for hotels, restaurants, or any other typical feature, within a specified range of any location.
LLM prompt examples using these tools:

“What is the distance, and how long will it take, to drive from Joshua Tree to Oakland CA?”

“Find me 10 hotels within 20 miles of Prestwick Airport, UK”

“What is the latitude and longitude of UK postcode IM4 7BN?”

“If I drive from Berlin to Munich tomorrow, departing at 9am local time, will it be dark when I arrive?”

## General Aviation
Accurate computation of distances between points on Earth using the World Geodetic System 1984 (WGS84), the geodetic reference system that defines the Earth’s shape and size as an oblate spheroid, the standard for the Global Positioning System (GPS). The distances can be computed either as great-circles (i.e., shortest distance between the two points) or rhumblines (i.e., the distance measured along a straight line drawn on a mercator projection map).
Accurate computation of the end-point for a given start-point, bearing, and range. The bearing can be referenced to either true or magnetic north (if magnetic, the magnetic variation is automatically calculated and corrected for), and the track can be specified as a great circle or rhumbline.

Search for airports within a specified range from any location in the world, with multiple optional filters (such as “must have AVGAS” etc). For the US only, can also search for navaids, fixes, features, and obstacles.
Obtain the latest aviation weather report (METAR) and forecast (TAF) for any worldwide ICAO designated weather station (in raw and decoded formats). Find the nearest ICAO designated weather station to a given location, or multiple stations within a specified range of that location.

Computation of aviation-pertinent atmospheric parameters (versus altitude) given the measured temperature and pressure (from METARs).
Perform VFR (Visual-Flight-Rules) flight route calculations between specified origin and destination airfields, plus up to ten optional intermediate waypoints (when not routing direct). Automatically computes wind corrections (using latest METARs along the route, and assuming a power-law extrapolation from METAR measured winds at 10m AGL to wind aloft), magnetic variation, and sunlight conditions (e.g., if daylight, twilight, or night-time at each waypoint plus direction (azimuth and zenith) to the sun relative to flight track (to assess if glare will be an issue). For the origin and departure airfields, gives essential information for each runway (surface, dimensions) plus the crosswind and headwind/tailwind components (computed from latest METARs), plus, where the information is available, details on runway lighting, visual approach aids, and instrument approach aids. Also provides the communication frequencies for the origin and departure airfields, plus where the information is available, telephone contact details, operating hours, and whether PPR is required. Utilizes current atmospheric conditions (from latest METAR data) to model the atmosphere (and its deviations from the International Standard Atmosphere) in order to compute for example, density altitude at the departure airfield, true airspeed (TAS), Mach number, and estimated cloud-base and freezing altitude along the route, and pressure altitude at each waypoint (i.e., the altitude displayed on the altimeter when set at standard pressure setting, useful for flight level determination). All navigation timings are presented in UTC as well as in local time (taking account of timezone and Daylight-Savings corrections). As well as providing a route summary (total distance, flight time, fuel consumption), all relevant data is provided per leg to facilitate the generation of a navlog (e.g., groundspeed, distance, timings, magnetic heading and true track, fuel used, etc). Aircraft Performance and route profile data (indicated airspeed, altitude, fuel flow rate) can be specified or default values (100kts, 2500ft 8 USgal/hour) are used if omitted. The latest METAR (current weather) and TAF (forecasts) reports are provided for each waypoint. A URL is also provided which enables the route to be viewed on skyvector.com (via any web browser). From there, the route can be exported to popular pilot apps such as Garmin Pilot, ForeFlight etc.

LLM prompt examples using these tools:

“What is the great-circle distance between Prestwick Airport and Goodwood Airfield in the UK?”

“What is the latitude and longitude of the location 25 nautical miles on a true bearing of 335 degrees from EGNS?”

“What is the latitude and longitude of the location 45 nautical miles on a magnetic bearing of 85 degrees from the Daventry VOR (DTY) in the UK?”

“What is the nearest METAR report for Wolverhampton Airport, UK?”

“Perform the flight route calculations for a VFR flight from Wolverhampton Airport, UK, to EGTK, with intermediate waypoint 15 nautical miles on a magnetic bearing of 210 degrees from Wolverhampton. Indicated airspeed will be 95 kts, altitude 2000 ft, departing Wolverhampton 45 minutes from now. Provide details for the navlog, plus a skyvector URL.”

Then,
“How long is the drive from EGTK to Chipping Norton?”

“Perform the flight route calculations for a VFR flight from Palo Alto Airport, CA, to Half Moon Bay airport, CA, with an intermediate waypoint overflying Stanford University. Indicated airspeed will be 100 kts, altitude 3000 ft, departing Palo Alto two hours from now. Provide details for the navlog, plus a skyvector URL.”

Then,
“Are there any Mexican restaurants within 10 miles of Half Moon Bay airport?”

# How to Use the teckel Toolboxes

First generate an API key using the teckel App.

Do the following:

1. Install the teckel App and create (or import) an Ethereum Account.

2. Navigate to the Accounts page by tapping on the wallet icon in the upper right corner of the App home screen. Access the API Key Manager for the created or imported Ethereum Account by tapping “Manage API Key” on the Accounts page.

3. Use the API key when making calls to the endpoints. All the available endpoints are available via the teckel App, incorporating the actual API key for the given Ethereum Account.

4. For illustrative purposes, we will use the following fake key d1e12345-c234-45a6-9b76-1234567891ff in the examples presented below. You would substitute your actual API key in place of this fake key.

Next, decide if you are using the MCP servers or RESTful (API) to access the tools.

# Using the MCP Servers
## Configure your MCP client-of-choice
Whatever the client, the configuration is essentially the same. Namely, provide the client with the MCP server endpoint and access credentials. These are typically in the form of a configuration JSON snippet, using your API key as the “Bearer” token in the “Authorization” tag. For example, here is the precise configuration for use with the Cursor desktop app (navigate within the Cursor app to the Cursor Settings -> Tools & MCP -> + New MCP server and enter these details using your actual teckel API key to replace this fake one).
##MCP JSON configuration (example for use with Cursor)
{
 "mcpServers": {
    "teckel-ethereum-toolbox": {
      "url": "https://mcp-servers.bh.tkllabs.io:9780/ethereum-mcp",
      "headers": {
        "Authorization": "Bearer d1e12345-c234-45a6-9b76-1234567891ff"
      }
    },
    "teckel-navigation-toolbox": {
      "url": "https://mcp-servers.bh.tkllabs.io:9780/navigation-mcp",
      "headers": {
        "Authorization": "Bearer d1e12345-c234-45a6-9b76-1234567891ff"
      }
    }   
  }
}

