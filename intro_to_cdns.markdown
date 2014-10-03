## Crushing your competition with speed

### How to use CDNs to create lighting fast websites

Eric Koslow

@ekosz1

---

## Agenda

- Learn about HTTP Caching
- Add Rack::Cache to our project
- Add a Cloudfront CDN to our project

---

## Get the code!

## github.com/ekosz/calhacks\_demo

---

## View the site

### calhacks-speed.herokuapp.com

---

## Look at this site, this site is amazing...

but maybe a little slow.

---

## HTTP Caching <sup><small>([?](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching))</small></sup>

- Etag
- Cache-Control

---

## Etag

```
➜  ~  curl -I http://teespring.com
HTTP/1.1 200 OK
Content-length: 29276
Content-Type: text/html; charset=utf-8
Etag: "0dcbf3922e7fb4ac74a518735268cd95"
...
X-Runtime: 0.017336
```

- The fingerprint for this webpage is '0dcbf3922e7fb4ac74a518735268cd95'

---

## Etag

```
➜  ~  curl -I http://teespring.com -H 'If-None-Match: 0dcbf3922e7fb4ac74a518735268cd95'
HTTP/1.1 304 Not Modified
Content-length: 0
...
X-Runtime: 0.014281
```

- Yep keep using the content you got.  It hasn't changed

---

## Lets add some Etags!

The cache key is the hardest part

---

## Cache-Control

```
➜  ~  curl -I http://teespring.com
HTTP/1.1 200 OK
Cache-Control: max-age=1800, public
Content-length: 29276
Content-Type: text/html; charset=utf-8
...
X-Runtime: 0.020358
```

- `max-age=1800`: Cache this page for 1800 seconds (1 hour)
- `public`: Hey men in the middle, feel free to cache this as well

---

## Cache-Control

```
➜  ~  curl -I 'https://teespring.com/dashboard/campaigns' -H 'Cookie: _teespring_session_2=...;'
HTTP/1.1 200 OK
Cache-Control: max-age=0, private, must-revalidate
Content-length: 44290
Content-Type: text/html; charset=utf-8
...
X-Runtime: 0.238420
```

- `max-age=0`: Don't cache me bro
- `private`: Hey men in the middle, please DON'T cache this request
- `must-revalidate`: Don't serve any 'stale' content, check with me for new stuff

---

## The fastest request, is the one thats never sent

Lets quickly set some cache-control headers

---

## What about all the requests that aren't cached?

---

## Rack::Cache to the rescue!

[github.com/ekosz/calhacks_demo/compare/cache_control...rack_cache](http://github.com/ekosz/calhacks_demo/compare/cache_control...rack_cache)

---

## No mater how fast we make our site, latency is still getting in the way

Lets fix that too, using CDNs

---

## What does it mean?

## C<span class='fragment' fragment-index='1'>ontent</span>
## D<span class='fragment' fragment-index='2'>elivery</span>
## N<span class='fragment' fragment-index='3'>etwork</span>

---

<iframe style="width: 100%; height: 800px" src="http://batchgeo.com/map/daace363a2d1f693125c3fe70bec4fe5"></iframe>

Amazon's Cloudfront Network

---

# Final Demo

