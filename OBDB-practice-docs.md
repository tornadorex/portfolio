# The Open Brewery Database API
Welcome to the unofficial documentation for the [Open Brewery Database API](https://www.openbrewerydb.org/). I'm doing this to keep up on practicing API documentation. This is not meant to replace the existing docs, but to supplement them in a slightly different format.

**Endpoints and Contents**

- `/breweries`
	- [Getting Information on a Single Brewery](#single)
	- [Getting a List of Breweries](#list)
- `/random`
	- [Getting a Random Brewery](#random)
- `/search`
	- [Searching for Breweries by Term](#search)
- `/autocomplete`
	- [Fetching an Abbreviated List for Autocomplete](#autocomplete)

-----

<span id="single"></span>
## Getting Information on a Single Brewery
Gets the information for the specified brewery.

### URL
`GET https://api.openbrewerydb.org/breweries/{obdb-id}`
where {obdb-id} is the brewery's identifier in the databaseS

### Sample Request
`GET https://api.openbrewerydb.org/breweries/deschutes-brewery-bend`

### Response
<table><tr><th>Element</th><th>Description</th><th>Type</th><th>Notes</th></tr>
<tr><td><code>id</td><td>Open Brewery DB identifier</td><td>string</td><td /></tr>
<tr><td><code>name</td><td>Name of the brewery</td><td>string</td><td /></tr>
<tr><td><code>brewery_type</td><td>Type of brewery</td><td>string</td><td>See the <a href="#query-params">query parameters</a> for <code>by_type</code> for valid values</td></tr>
<tr><td><code>street</td><td>Street address of the brewery</td><td>string</td><td /></tr>
<tr><td><code>address_2</td><td>Extended address of the brewery</td><td>string</td><td>If empty/not applicable, returns null</td></tr>
<tr><td><code>address_3</td><td>Extended address of the brewery</td><td>string</td><td>If empty/not applicable, returns null</td></tr>
<tr><td><code>city</td><td>City where the brewery is located</td><td>string</td><td /></tr>
<tr><td><code>state</td><td>State where the brewery is located</td><td>string</td><td /></tr>
<tr><td><code>county_province</td><td>County or province where the brewery is located</td><td>string</td><td>If empty/not applicable, returns null</td></tr>
<tr><td><code>postal_code</td><td>Postal code for the brewery's address</td><td>string</td><td>Formatted as ##### or #####-####</td></tr>
<tr><td><code>country</td><td>Country where the brewery is located</td><td>string</td><td /></tr>
<tr><td><code>longitude</td><td>Brewery's geolocation, east/west</td><td>string</td><td /></tr>
<tr><td><code>latitude</td><td>Brewery's geolocation, north/south</td><td>string</td><td /></tr>
<tr><td><code>phone</td><td>Phone number for the brewery</td><td>string</td><td /></tr>
<tr><td><code>website_url</td><td>Brewery website's address</td><td>string</td><td /></tr>
<tr><td><code>updated_at</td><td>Date and time that the brewery entry was last updated</td><td>string</td><td>Follows ISO-8601 formatting</td></tr>
<tr><td><code>created_at</td><td>Date and time that the brewery entry was created</td><td>string</td><td>Follows ISO-8601 formatting</td></tr>
</table>

#### Sample Response

    {
        "id": "deschutes-brewery-bend",
        "name": "Deschutes Brewery",
        "brewery_type": "regional",
        "street": "901 SW Simpson Ave",
        "address_2": null,
        "address_3": null,
        "city": "Bend",
        "state": "Oregon",
        "county_province": null,
        "postal_code": "97702-3118",
        "country": "United States",
        "longitude": "-121.3246184",
        "latitude": "44.04780638",
        "phone": "5413858606",
        "website_url": "http://www.deschutesbrewery.com",
        "updated_at": "2022-08-20T02:56:08.975Z",
        "created_at": "2022-08-20T02:56:08.975Z"
    }

---

<span id="list"></span>
## Getting a List of Breweries
Gets a list of brewery entries that can be filtered by various parameters. All parameters are optional. Returns the first 20 entries if no query parameters are specified.

### URL
`GET https://api.openbrewerydb.org/breweries`

<span id="query-params"></span>
#### Query Parameters
##### Filters
<table><tr><th>Parameter</th><th>Description</th><th>Type</th><th>Notes</th></tr>
<tr><td><code>by_city</td><td>Filter breweries by city</td><td>string</td><td /></tr>
<tr><td><code>by_name</td><td>Filter breweries by name</td><td>string</td><td>You can use underscores or URL encoding for spaces</td></tr>
<tr><td><code>by_state</td><td>Filter breweries by state</td><td>string</td><td>The full state name is required; no abbreviations. You can use underscores or url encoding for spaces.</td></tr>
<tr><td><code>by_postal</td><td>Filter breweries by postal code</td><td>string</td><td>May be filtered by basic (5 digit) postal code or more precisely filtered by postal+4 (9 digit) code.
<p><strong>Note:</strong> If filtering by postal+4 the search must include either a hyphen or an underscore.</td></tr>
<tr><td><code>by_type</code></td><td>Filter by type of brewery</td><td>string</td><td>Valid values: <ul><li><code>micro</code> - Most craft breweries. For example, Samuel Adams is still considered a micro brewery.</li>
    <li><code>nano</code> - An extremely small brewery which typically only distributes locally.</li>
    <li><code>regional</code> - A regional location of an expanded brewery. Ex. Sierra Nevada’s Asheville, NC location.
    <li><code>brewpub</code> - A beer-focused restaurant or restaurant/bar with a brewery on-premise.
    <li><strike><code>large</code> - A very large brewery. Likely not for visitors. Ex. Miller-Coors. (deprecated)</strike>
    <li><code>planning</code> - A brewery in planning or not yet opened to the public.
    <li><strike><code>bar</code> - A bar. No brewery equipment on premise. (deprecated)</strike>
    <li><code>contract</code> - A brewery that uses another brewery’s equipment.
    <li><code>proprietor</code> - Similar to contract brewing but refers more to a brewery incubator.
    <li><code>closed</code> - A location which has been closed.</td></tr>
<tr><td><code>page</td><td>The offset or page of breweries to return</td><td>integer</td><td /></tr>
<tr><td><code>per_page</td><td>Number of breweries to return each call</td><td>integer</td><td>Default per page is 20. Max per page is 50.</td></tr>
</table>

##### Sorting
<table><tr><th>Parameter</th><th>Description</th><th>Type</th><th>Notes</th></tr>
<tr><td><code>by_dist</td><td>Sort the results by distance from a specified origin point in <code>latitude,longitude</code></td><td>string</td><td /></tr>
<tr><td><code>sort</td><td>Sort the results by one or more fields</td><td>string</td><td><code>by_dist</code> does not work with this query parameter.
<ul><li><code>asc</code> - Sort in ascending order<li><code>desc</code> - Sort in descending order</ul></td></tr>
</table>

### Sample Request - Filtering by City & State
`GET https://api.openbrewerydb.org/breweries?by_city=portland&by_state=oregon&per_page=3`

### Response
#### Sample Response

    [
        {
            "id": "10-barrel-brewing-co-portland",
            "name": "10 Barrel Brewing Co",
            "brewery_type": "large",
            "street": "1411 NW Flanders St",
            "address_2": null,
            "address_3": null,
            "city": "Portland",
            "state": "Oregon",
            "county_province": null,
            "postal_code": "97209-2620",
            "country": "United States",
            "longitude": "-122.6855056",
            "latitude": "45.5259786",
            "phone": "5032241700",
            "website_url": "http://www.10barrel.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        },
        {
            "id": "13-virtues-brewing-co-portland",
            "name": "13 Virtues Brewing Co",
            "brewery_type": "brewpub",
            "street": "6410 SE Milwaukie Ave",
            "address_2": null,
            "address_3": null,
            "city": "Portland",
            "state": "Oregon",
            "county_province": null,
            "postal_code": "97202-5518",
            "country": "United States",
            "longitude": "-122.6487531",
            "latitude": "45.4762536",
            "phone": "5032393831",
            "website_url": "http://www.13virtuesbrewing.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        },
        {
            "id": "alameda-brewing-co-portland-1",
            "name": "Alameda Brewing Co",
            "brewery_type": "micro",
            "street": "4736 SE 24th Ave",
            "address_2": null,
            "address_3": null,
            "city": "Portland",
            "state": "Oregon",
            "county_province": null,
            "postal_code": "97202-4787",
            "country": "United States",
            "longitude": "-122.6412495",
            "latitude": "45.48882655",
            "phone": "5034609025",
            "website_url": null,
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        }
    ]


### Sample Request - Sorting by Type and Name
`GET https://api.openbrewerydb.org/breweries?by_state=oregon&sort=type,name:asc&per_page=3`

### Response
#### Sample Response

    [
        {
            "id": "1188-brewing-co-john-day",
            "name": "1188 Brewing Co",
            "brewery_type": "brewpub",
            "street": "141 E Main St",
            "address_2": null,
            "address_3": null,
            "city": "John Day",
            "state": "Oregon",
            "county_province": null,
            "postal_code": "97845-1210",
            "country": "United States",
            "longitude": "-118.9218754",
            "latitude": "44.4146563",
            "phone": "5415751188",
            "website_url": "http://www.1188brewing.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        },
        {
            "id": "13-virtues-brewing-co-portland",
            "name": "13 Virtues Brewing Co",
            "brewery_type": "brewpub",
            "street": "6410 SE Milwaukie Ave",
            "address_2": null,
            "address_3": null,
            "city": "Portland",
            "state": "Oregon",
            "county_province": null,
            "postal_code": "97202-5518",
            "country": "United States",
            "longitude": "-122.6487531",
            "latitude": "45.4762536",
            "phone": "5032393831",
            "website_url": "http://www.13virtuesbrewing.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        },
        {
            "id": "7-devils-brewing-co-coos-bay",
            "name": "7 Devils Brewing Co",
            "brewery_type": "brewpub",
            "street": "247 S 2nd St",
            "address_2": null,
            "address_3": null,
            "city": "Coos Bay",
            "state": "Oregon",
            "county_province": null,
            "postal_code": "97420-1642",
            "country": "United States",
            "longitude": "-124.2147508",
            "latitude": "43.36654751",
            "phone": "5418083738",
            "website_url": "http://www.7devilsbrewery.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        }
    ]



---
<span id="random"></span>
## Getting a Random Brewery

Returns one or more random breweries from the database.

### URL
`GET https://api.openbrewerydb.org/breweries/random`

### Query Parameters
<table><tr><th>Parameter</th><th>Description</th><th>Type</th><th>Required</th><th>Notes</th></tr>
<tr><td><code>size</td><td>The number of breweries to return with each call</td><td>integer</td><td>Optional</td><td>Default is 1. Max per page is 50.</td></tr>
</table>

### Sample Request
`GET https://api.openbrewerydb.org/breweries/random?size=3`

### Response
#### Sample Response

    [
        {
            "id": "big-tupper-brewing-tupper-lake",
            "name": "Big Tupper Brewing",
            "brewery_type": "brewpub",
            "street": "12 Cliff Ave",
            "address_2": null,
            "address_3": null,
            "city": "Tupper Lake",
            "state": "New York",
            "county_province": null,
            "postal_code": "12986-1719",
            "country": "United States",
            "longitude": "-74.46576367",
            "latitude": "44.223293",
            "phone": "5183596350",
            "website_url": "http://www.bigtupperbrewing.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        },
        {
            "id": "iron-horse-brewery-ellensburg",
            "name": "Iron Horse Brewery",
            "brewery_type": "regional",
            "street": "1621 Vantage Hwy",
            "address_2": null,
            "address_3": null,
            "city": "Ellensburg",
            "state": "Washington",
            "county_province": null,
            "postal_code": "98926-9001",
            "country": "United States",
            "longitude": "-120.52000035450321",
            "latitude": "47.00287945234483",
            "phone": "5099333134",
            "website_url": "http://www.ironhorsebrewery.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        },
        {
            "id": "taylor-house-brewing-co-catasauqua",
            "name": "Taylor House Brewing Co",
            "brewery_type": "micro",
            "street": "76 Lehigh St",
            "address_2": null,
            "address_3": null,
            "city": "Catasauqua",
            "state": "Pennsylvania",
            "county_province": null,
            "postal_code": "18032",
            "country": "United States",
            "longitude": "-75.46805342",
            "latitude": "40.64817832",
            "phone": null,
            "website_url": "http://www.taylorhousebrewing.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        }
    ]

---

<span id="search"></span>
## Searching Breweries by Term
Searches for and returns breweries that match the search term.

### URL
`GET https://api.openbrewerydb.org/breweries/search?query={search}`
where {search} is the search term.

#### Query Parameters
<table><tr><th>Parameter</th><th>Description</th><th>Type</th><th>Required</th><th>Notes</th></tr>
<tr><td><code>per_page</td><td>Number of breweries to return each call</td><td>integer</td><td>Optional</td><td>Default per page is 20. Max per page is 50.</td></tr>
<tr><td><code>query</code></td><td>The search term to return breweries</td><td>string</td><td>Required</td><td>You can use underscores or url encoding for spaces.</td></tr>
</table>

### Sample Request
`GET https://api.openbrewerydb.org/breweries/search?query=dog&per_page=3`

### Response
#### Sample Response

    [
        {
            "id": "barrel-dog-brewing-evergreen",
            "name": "Barrel Dog Brewing",
            "brewery_type": "micro",
            "street": null,
            "address_2": null,
            "address_3": null,
            "city": "Evergreen",
            "state": "Colorado",
            "county_province": null,
            "postal_code": "80439",
            "country": "United States",
            "longitude": "-105.321458",
            "latitude": "39.6361637",
            "phone": "5599176846",
            "website_url": null,
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        },
        {
            "id": "boss-dog-brewing-cleveland",
            "name": "Boss Dog Brewing",
            "brewery_type": "brewpub",
            "street": "2179 Lee Rd",
            "address_2": null,
            "address_3": null,
            "city": "Cleveland",
            "state": "Ohio",
            "county_province": null,
            "postal_code": "44118-2907",
            "country": "United States",
            "longitude": "-81.56529555",
            "latitude": "41.50030645",
            "phone": "2163212337",
            "website_url": "http://www.bossdogbrewing.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        },
        {
            "id": "diving-dog-brewhouse-oakland",
            "name": "Diving Dog Brewhouse",
            "brewery_type": "micro",
            "street": "1802 Telegraph Ave",
            "address_2": null,
            "address_3": null,
            "city": "Oakland",
            "state": "California",
            "county_province": null,
            "postal_code": "94612-2110",
            "country": "United States",
            "longitude": "-122.2698881",
            "latitude": "37.807739",
            "phone": "5103061914",
            "website_url": "http://www.divingdogbrew.com",
            "updated_at": "2022-08-20T02:56:08.975Z",
            "created_at": "2022-08-20T02:56:08.975Z"
        }
    ]

---
<span id="autocomplete"></span>
## Fetching an Abbreviated List for Autocomplete
Returns a list of names and ids of breweries based on a search term. This endpoint is typically used for a drop-down selection. It returns a maximum of 15 results.

### URL
`GET https://api.openbrewerydb.org/breweries/autocomplete?query={search}`
where {search} is the search term.

#### Query Parameters
<table><tr><th>Parameter</th><th>Description</th><th>Type</th><th>Required</th><th>Notes</th></tr>
<tr><td><code>query</code></td><td>The search term to return breweries</td><td>string</td><td>Required</td><td>You can use underscores or url encoding for spaces.</td></tr>
</table>

### Sample Request
`GET https://api.openbrewerydb.org/breweries/autocomplete?query=dog`

### Response
#### Sample Response

    [
        {
            "id": "barrel-dog-brewing-evergreen",
            "name": "Barrel Dog Brewing"
        },
        {
            "id": "boss-dog-brewing-cleveland",
            "name": "Boss Dog Brewing"
        },
        {
            "id": "diving-dog-brewhouse-oakland",
            "name": "Diving Dog Brewhouse"
        },
        {
            "id": "dog-days-brewing-bremerton",
            "name": "Dog Days Brewing"
        },
        {
            "id": "dog-money-restaurant-leesburg",
            "name": "Dog Money Restaurant"
        },
        {
            "id": "dog-tag-brewing-bozeman",
            "name": "Dog Tag Brewing"
        },
        {
            "id": "dreaming-dog-brewery-elk-grove",
            "name": "Dreaming Dog Brewery"
        },
        {
            "id": "flying-dog-brewery-frederick",
            "name": "Flying Dog Brewery"
        },
        {
            "id": "island-dog-brewing-south-portland",
            "name": "Island Dog Brewing"
        },
        {
            "id": "laughing-dog-brewing-ponderay",
            "name": "Laughing Dog Brewing"
        },
        {
            "id": "lead-dog-brewing-reno",
            "name": "Lead Dog Brewing"
        },
        {
            "id": "running-dogs-brewery-saint-helens",
            "name": "Running Dogs Brewery"
        },
        {
            "id": "sea-dog-brewing-camden",
            "name": "Sea Dog Brewing"
        },
        {
            "id": "spotted-dog-brewery-las-cruces",
            "name": "Spotted Dog Brewery"
        },
        {
            "id": "tin-dog-brewing-seattle",
            "name": "Tin Dog Brewing"
        },
        {
            "id": "alpine-dog-brewing-co-denver",
            "name": "Alpine Dog Brewing Co"
        },
        {
            "id": "big-dogs-brewing-co-las-vegas",
            "name": "Big Dog's Brewing Co"
        },
        {
            "id": "bike-dog-brewing-co-west-sacramento",
            "name": "Bike Dog Brewing Co"
        },
        {
            "id": "dingo-dog-brewing-co-carrboro",
            "name": "Dingo Dog Brewing Co"
        },
        {
            "id": "dog-rose-brewing-company-saint-augustine",
            "name": "Dog Rose Brewing Company"
        },
        {
            "id": "dueling-dogs-brewing-company-lincoln",
            "name": "Dueling Dogs Brewing Company"
        },
        {
            "id": "little-dog-brewing-co-neptune-city",
            "name": "Little Dog Brewing Co."
        },
        {
            "id": "pub-dog-brewing-company-westminster",
            "name": "Pub Dog Brewing Company"
        },
        {
            "id": "river-dog-brewing-co-ridgeland",
            "name": "River Dog Brewing Co"
        },
        {
            "id": "sea-dog-brewing-co-conway",
            "name": "Sea Dog Brewing Co"
        },
        {
            "id": "sleepy-dog-brewing-co-tempe",
            "name": "Sleepy Dog Brewing Co"
        },
        {
            "id": "thirsty-dog-brewing-company-akron",
            "name": "Thirsty Dog Brewing Company"
        },
        {
            "id": "trail-dog-brewing-co-novato",
            "name": "Trail Dog Brewing Co."
        },
        {
            "id": "triple-dog-brewing-company-havre",
            "name": "Triple Dog Brewing Company"
        },
        {
            "id": "white-dog-brewing-boise-boise",
            "name": "White Dog Brewing Boise"
        },
        {
            "id": "white-dog-brewing-company-bozeman",
            "name": "White Dog Brewing Company"
        },
        {
            "id": "old-dog-alehouse-and-brewery-delaware",
            "name": "Old Dog Alehouse & Brewery"
        },
        {
            "id": "sea-dog-brewing-co-bangor-bangor",
            "name": "Sea Dog Brewing Co - Bangor"
        },
        {
            "id": "sea-dog-brewing-co-clearwater-clearwater",
            "name": "Sea Dog Brewing Co - Clearwater"
        },
        {
            "id": "wet-dog-cafe-and-brewery-astoria",
            "name": "Wet Dog Cafe & Brewery"
        },
        {
            "id": "dog-and-pony-alehouse-and-grill-renton",
            "name": "Dog & Pony Alehouse and Grill"
        },
        {
            "id": "hair-of-the-dog-brewing-co-portland",
            "name": "Hair of the Dog Brewing Co"
        },
        {
            "id": "sea-dog-brewing-co-s-portland-s-portland",
            "name": "Sea Dog Brewing Co - S. Portland"
        },
        {
            "id": "foy-enterprises-llc-dba-dog-river-brewery-barre",
            "name": "Foy Enterprises LLC DBA Dog River Brewery"
        }
    ]

---
## Status Codes and Errors

This table lists the returned HTTP status codes.

<table>
<tr><th>Code</th><th>Description</th></tr>
<tr><td>200</td><td>OK</td></tr>
<tr><td>404</td><td>Not Found</td></tr>
</table>
