### Block `integration`: third-party service

- A request the service refuses or times out on shows a message naming the service, and leaves no half-written data.
- Credentials for the service are stored server-side and never sent to a client.
- An incoming webhook or callback is verified as coming from the service; an unverified one is refused.
- A webhook delivered twice is processed once.
- When the service is down, the rest of the product keeps working and the affected feature says it is unavailable.
