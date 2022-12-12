# Design a Rate Limiter

rate limiting can be for many reasons
ie.
- we rate limit trying passwords on a device to 5 wrong attempts per hour this
is for security reasons

- Youtube limits 20 video uploads per 24h this is so you can't load them with
  too many videos, so the reasoning here is to save cost of storing all those
  videos and to prevent people from crashing their site by spamming uploads.  So
  cost and availability are the main reasons.

Questions
Are we designing a rate limiter for a backend api?

is it for a single api or for multiple api servers?
The answer will most likely be for multiple because it is most useful for
distributed systems.  For single servers you could manage the rate limiting in
the server itself in memory using a hashmap but this isn't particularly useful.
Most rate limiters are external services that manage the rate limiting of
multiple api servers behind it.

If a user is hitting your rate limiter and the requests go through then you will
be served data from the rate limiter as it comes back from the api.

user -> rate limiter -> api-|
user <- rate limiter <- api-|


if you are being rejected by the rate limiter you will receive a 429 response
directly from it.

user -> rate limiter-|
user <- rate limiter-|

429 is the error code for rate you are being throttled.  This should return a
response of how long or why you are being throttled.

----
How do rate limiters identify the users? it could be by userId if you are
forcing them to be logged in, or by ip for the most general case.

---

Non-Functional requirements
minimize latency
maximize throughput

Storage- we probably don't care about how much storage it requires.  For storage
we would need to store the rules of the rate limiter.  Ie, 20 videos per 24h,
100 comments per 24h.

Number of users
Ip has 4 bytes
lets, over estimate and say it takes 128 byes to store the number of requests they have made

so it takes 132 bytes per user

so we have 132 billion bytes = 132GB of data.  This is feasible to put into
memory :o.  This is the purpose of this to check

----

If talking about availability we want to have the system fail open rather than
fail closed most likely.  This will allow the system to remain functional even
if the rate limiter isn't working.  For something like youtube if it was
fail-closed then the whole site would be down while the rate limiter is down.

----

A rate limiter acts as a reverse proxy