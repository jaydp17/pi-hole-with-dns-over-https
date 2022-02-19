# pi-hole-with-dns-over-https

pi-hole launch configuration with DNS over HTTPS using ~[cloudflared](https://github.com/cloudflare/cloudflared)~ [dnscrypt-proxy](https://github.com/DNSCrypt/dnscrypt-proxy).

The change from cloudflared to dnscrypt-proxy was made because cloudflared stops serving dns queries once internet fluctuates. More info in the following links

- https://discourse.pi-hole.net/t/automatically-restarting-cloudflared-when-internet-is-restored/21828
- https://www.reddit.com/r/pihole/comments/myy2ae/cloudflared_not_restarting_after_an_internet/

## Post install configuration

Pi hole has a default rate limit of 1000 reqs per 60s. And if all of our network queries are going through the router to the pi-hole, there's a chance that pi-hole might ratelimit queries from the router's IP with a REJECTED status.

This can be trouble shooted using the Tools -> Pi-hole diagnosis page.

To increase the rate-limit update the following config

```sh
docker exec -it <pi_hole_container> bash
echo "RATE_LIMIT=2000/60" >> /etc/pihole/pihole-FTL.conf
```
