**[Keller Williams Scraper](https://apify.com/dz_omar/kw-scraper?fpr=smcx63)** extracts **Keller Williams (kw.com) listings** — homes **for sale, for rent and sold** — from a pasted kw.com search or property link or a typed place. Every listing comes with its price, size, features, photos, HOA, schools, agent and brokerage contacts and neighborhood statistics.

Perfect for **real estate investors**, **agents and brokers**, **market analysts** and **proptech teams** who need Keller Williams listing data in a spreadsheet, a database or an API without copying listings by hand.

## What does Keller Williams Scraper do?

- **Paste a kw.com link** — a **search link** (map area, price, bedrooms, bathrooms, property types, living area, lot size, year built, features, keywords, open house, price reduced and sort are all read from the link) returns that search exactly as kw.com shows it; a **property link** returns that listing with its full record.
- **Search any place** — cities, ZIP codes, counties, neighborhoods, school zones or a whole state: `Austin, TX`, `78701`, `Travis County, TX`, `Zilker`, `Texas`.
- **Sale, rent and sold** — pick the listing type per run; for sale can include pending and coming soon.
- **20+ filters** — price, bedrooms, bathrooms (or exactly N), property type, living area, lot size, year built, pool / pond / hot tub / deck / porch / gated entry / garage / parking / garden / fireplace, new construction, foreclosure, short sale, description keywords, open house, price reduced.
- **Go beyond 10,000 results** — large searches are read in price bands automatically, so a whole state or metro area is reachable.
- **Full or summary** — the complete record, or the search-result fields only for fast, small exports; optional tax and sales history.
- **Sorted your way** — recently updated, price, living area, price per living area or days on site.
- **Resumable** — an interrupted run continues where it left off, without duplicates.

### What data can you extract from Keller Williams?

| Category | Fields |
|---|---|
| Listing | listing ID, link, status, category (sale / rent / sold), MLS number and source, listing and close dates |
| Price | sale, rent and sold amounts, price history with percent change |
| Property | type and subtype, bedrooms, bathrooms, living area, lot size, year built, stories, heating and cooling, appliances, utilities, roof, parking, interior and exterior features (pool, deck, fireplace…), structure details |
| Location | address parts, coordinates, neighborhood, city, ZIP and county areas with walkability and market statistics (listings for sale, days on market, average prices) |
| Costs | HOA fee and what it includes, buyer and seller commission details, tax history and recorded sales (optional) |
| Schools | assigned public schools with type, grades, student-teacher ratio and ranking score |
| Agents | listing agent name, license, phone numbers, email, photo; brokerage line and MLS compliance text |
| Media | all photos, virtual tours, open houses |
| Activity | views, shares and saves of the listing on kw.com |

Records keep kw.com's own field names and structure, and empty values stay as `null`.

### Why use Keller Williams Scraper on Apify?

Running it on Apify gives you **API access**, **scheduling**, **monitoring**, **webhooks**, **integrations** (Make, Zapier, n8n, Google Sheets) and **proxy rotation** without managing infrastructure. Export the dataset as JSON, CSV, Excel or HTML, or read it over the API.

## How to scrape Keller Williams listings

1. Open **Keller Williams Scraper** in Apify Console.
2. Either paste kw.com **search or property links** (Option A), or type **places to search** (Option B) and choose For sale, For rent or Sold.
3. Add filters if you typed places (a pasted link already carries its own filters).
4. Set **Maximum results per search** (start small: `10`) and, for a first look, **Detail level** `Summary`.
5. Click **Start**, wait for the run to finish, then download the results as JSON, CSV or Excel, or fetch them over the API.

## How much does it cost to scrape Keller Williams?

Pay per result: one event per listing delivered (full record or summary), plus a small start fee per run. Accounts without a paid Apify plan pay the Bronze price.

| Event | Bronze | Silver | Gold |
|---|---|---|---|
| **Listing** — full record | $0.0015 | $0.0012 | $0.0009 |
| **Listing (summary)** — search-result record | $0.0006 | $0.0005 | $0.0004 |
| Run start (per GB of memory; this Actor runs at 1 GB) | $0.003 | $0.003 | $0.003 |

- **1,000 full records** cost **$1.50** (Bronze), **$1.20** (Silver) or **$0.90** (Gold), plus the run start.
- **1,000 summary records** cost **$0.60**, **$0.50** or **$0.40**.
- A listing that could not be loaded in full is delivered without a full-record charge.
- Set a **maximum cost per run** and the Actor stops at that limit, keeping everything collected so far. Results are saved to the dataset as they are found, so you can watch them arrive while the run is still going.

## Input and output examples

### Input

```json
{
    "startUrls": [{ "url": "https://kw.com/search/sale?viewport=30.2859%2C-97.7524%2C30.2409%2C-97.8187&bedrooms=1%2Cnull&price=350000%2C750000&sort=price" }],
    "locations": ["Austin, TX"],
    "listingType": "sale",
    "priceMin": 300000,
    "priceMax": 900000,
    "bedroomsMin": 3,
    "propertyTypes": ["house"],
    "features": ["pool"],
    "maxItems": 100,
    "sortBy": "price",
    "sortDirection": "asc",
    "detailLevel": "full"
}
```

| Input | What it does |
|---|---|
| `startUrls` — `https://kw.com/search/sale?viewport=…&price=…` | Reads that search as kw.com shows it (area, filters and sort come from the link); limited by *Maximum results per search* |
| `startUrls` — `https://kw.com/property/…/2044070089496910` | Delivers that listing with its full record |
| `locations` — `78701`, `Travis County, TX`, `Texas` | One search per place, each limited by *Maximum results per search* |
| `maxItems` — `0` | Reads every match of each search (large searches are split into price bands) |

### Output

A summary record (`detailLevel: summary`; `primaryImage` is the first photo, shown as a picture in the table views):

```json
{
    "id": "2122614481591966",
    "listingCategory": "sale",
    "listingStatus": "active",
    "pricing": { "sale": { "amount": 550000, "currency": "USD" }, "rent": { "amount": 550000, "currency": "USD" }, "sold": { "amount": null, "currency": "USD" } },
    "address": { "displayAddress": "2422 N 37TH Street, Phoenix, AZ 85008", "city": "Phoenix", "state": "AZ", "zipcode": "85008" },
    "facets": { "bedrooms": 5, "bathrooms": 2, "homeSize": { "value": 1823, "unitType": "SQ_FT" }, "lotSize": { "value": 0.14, "unitType": "ACRES" } },
    "propertyType": "Single Family Detached",
    "listingDate": "2026-06-03T21:00:26.169Z",
    "primaryImage": "https://storage.googleapis.com/…/1.jpg",
    "urlPath": "/property/2422-N-37TH-Street-Phoenix-AZ-85008/2122614481591966",
    "source_url": "https://kw.com/property/2422-N-37TH-Street-Phoenix-AZ-85008/2122614481591966"
}
```

The full record adds the photos, features, HOA, schools, agent and brokerage, open houses, neighborhood statistics and the listing text.

## Frequently asked questions

### Is it legal to scrape Keller Williams listings?

The Actor reads listing information that kw.com shows to any visitor. You are responsible for how you use it: follow Keller Williams' and the listing MLS's terms, and applicable data-protection law when you use agent contact details. This is not legal advice.

### Do I need a Keller Williams account?

No. No login, cookies or API key are needed — links and places are enough.

### Why did a place search return nothing?

The run still succeeds and returns one row that names the filters which, left out one at a time, would bring listings back (for example *Price range (212)*). Nothing is charged for that row.

### Why did a run return fewer results than I asked for?

| Situation | What you see | What to do |
|---|---|---|
| Fewer matches than your limit | `"…: 37 listings match"` in the log | Loosen the filters or add places |
| Listings share one price beyond 10,000 | a log line about identical prices | Narrow the search (type, area) |
| Link is not a property or search page | skipped and listed in the log | Paste a `…/property/<address>/<number>` or `…/search/sale?…` link, or use *Places to search* |
| Search link has no map area | skipped, the row says so | Open the search on kw.com, move the map, copy the link again |
| Your maximum cost was reached | `"Your maximum cost for this run is reached"` | Raise the maximum cost per run |

### Can I use Keller Williams Scraper in Make, Zapier, n8n or my own code?

Yes. Start it from the Apify API or any client library, schedule it, or trigger it with a webhook, then read the dataset as JSON, CSV or Excel.

### What happens if a run is interrupted?

The Actor saves its progress and resumes where it left off — no duplicate records and no repeated charges.

## Support

- 🌐 **Website:** [flowextractapi.com](https://flowextractapi.com)
- 📧 **Email:** [flowextractapi@outlook.com](mailto:flowextractapi@outlook.com)
- 💬 **GitHub:** [FlowExtractAPI](https://github.com/FlowExtractAPI)
- 💼 **LinkedIn:** [flowextract-api](https://www.linkedin.com/in/flowextract-api/)
- 🐦 **X (Twitter):** [@FlowExtractAPI](https://x.com/FlowExtractAPI)
- 📱 **Facebook:** [flowextractapi](https://www.facebook.com/flowextractapi)
- 🎵 **TikTok:** [@flowextractapi](https://www.tiktok.com/@flowextractapi)

## Legal & compliance

- **Public data only** — processes publicly available data.
- **Rate limiting** — respects source-service limits and terms of use.
- **Data protection** — no storage of personal information or unauthorized data collection.
- **Commercial use** — suitable for business intelligence and research.
- No affiliation with or endorsement by Keller Williams Realty, Inc. is implied.

---

*Keller Williams Scraper — by FlowExtract API. Turn any website into structured data.*
