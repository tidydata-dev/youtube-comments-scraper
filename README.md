# YouTube Comments Scraper — Python, Node.js & cURL examples

Get **YouTube comments and replies** — text, author, likes, reply count, pinned and creator-hearted flags, date — from videos, Shorts, playlists, whole channels or search results. **$0.25 per 1,000 comments**, no YouTube API key or quota.

Hosted on Apify: **[YouTube Comments Scraper](https://apify.com/tidydata/youtube-comments-scraper?fpr=wtg6qt)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/youtube-comments-scraper").call(run_input={
    "sources": [
        "https://www.youtube.com/watch?v=NiCgcUTL9_Q"
    ],
    "maxCommentsPerVideo": 500,
    "sortBy": "newest",
    "includeReplies": True
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['author', 'likeCount', 'text']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/youtube-comments-scraper').call({"sources": ["@veritasium"], "maxVideosPerSource": 3, "maxCommentsPerVideo": 100});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~youtube-comments-scraper/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"sources": ["@veritasium"], "maxVideosPerSource": 3, "maxCommentsPerVideo": 100}'
```

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper?fpr=wtg6qt) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper?fpr=wtg6qt) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper?fpr=wtg6qt) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor?fpr=wtg6qt) · [Google News](https://apify.com/tidydata/google-news-scraper?fpr=wtg6qt) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper?fpr=wtg6qt) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets?fpr=wtg6qt) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.

---
<sub>Links to apify.com include our affiliate ID: if you start a paid Apify plan through them, Apify pays TidyData a commission at no extra cost to you.</sub>
