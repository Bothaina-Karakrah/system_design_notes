## Functional Requirements
Functional requirements are the features that the system must have to satisfy the needs of the user.
1. Users can submit a long URL and receive a unique short URL.
2. Visiting the short URL redirects to the original URL.
3. (Optional) Support custom aliases and basic analytics.

## Non-Functional Requirements
Non-functional requirements refer to specifications about how a system operates, rather than what tasks it performs.
1. Short URLs must be globally unique.
2. The system should prioritize availability over strong consistency.
3. Support up to 1B stored URLs.
4. Redirection latency should be <100ms at P99.
5. The system should be horizontally scalable.
