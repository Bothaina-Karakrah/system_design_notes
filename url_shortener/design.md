## Requirements
### Functional Requirements
Functional requirements are the features that the system must have to satisfy the needs of the user.
1. Users can submit a long URL and receive a unique short URL.
2. Visiting the short URL redirects to the original URL.
3. (Optional) Support custom aliases and basic analytics.

### Non-Functional Requirements
Non-functional requirements refer to specifications about how a system operates, rather than what tasks it performs.
1. Short URLs must be globally unique.
2. The system should prioritize availability over strong consistency.
3. Support up to 1B stored URLs.
4. Redirection latency should be <100ms at P99.
5. The system should be horizontally scalable.

## Core Entities
1. **Original URL**: The original long URL submitted by the user.
2. **Short URL**: The shortened version of the original URL.
3. **User**: The person or system creating the shortened URL.
4. **Analytics (optional)**: Click counts, timestamps, referrer info.

## API Design
RESTful APIs will be used for client-facing communication, since each endpoint returns exactly the expected resource and does not introduce overfetching or underfetching.

### Endpoints

**1. Shorten a URL**  
`POST /urls`  

**Request Body**
```json
{
  "long_url": "https://www.example.com/some/very/long/url",
  "custom_alias": "optional_custom_alias",
  "expiration_date": "optional_expiration_date"
}
```
**Response**
```json
{
  "short_url": "http://short.ly/abc123"
}
```

**2. Redirect to the Original URL**
`GET /{short_url}` -> -> HTTP 302 Redirect to the original long URL

**3. Get URL Analytics**
`GET /analytics/{short_url}`
**Response**
```json
{
  "short_url": "http://short.ly/abc123",
  "click_count": 120,
  "last_visited": "2026-03-02T12:45:00Z",
  "referrers": [
    "https://google.com",
    "https://twitter.com"
  ]
}
```
