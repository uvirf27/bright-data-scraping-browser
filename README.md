# bright data scraping browser: Pricing, Per-GB Cost Math, and When a Credit-Based API Is the Smarter Buy

Bright Data's Scraping Browser (now marketed as Browser API) is a hosted headless browser with unblocking built in: you run your existing Puppeteer, Playwright, or Selenium scripts on Bright Data's infrastructure, and every session comes with CAPTCHA solving, proxy rotation, and browser fingerprinting handled for you. It ranked #1 in an independent AIMultiple benchmark of 8 remote browser providers, with a 95% success rate across 160 automated real-world tasks.

The catch is the billing unit. Since late August, the product is billed per gigabyte of traffic at $8/GB on pay-as-you-go, with a free tier of 5,000 credits and 1 GB per month and a Scale plan starting at $499/month for 71 GB. Whether that's cheap or expensive depends almost entirely on how heavy your page loads are — a number most reviews quote but almost none actually break down. This article does the math, covers the details hiding outside the pricing page, and looks at when a credit-based scraping API like ScraperAPI will cost you less for the same job.

> **Quick verdict:** If your target site needs clicking, scrolling, or multi-step interaction behind tough bot protection, Bright Data's Scraping Browser is a strong pick — start with its free 1 GB tier and keep an eye on your traffic meter. If you mainly need pages fetched and parsed (even JS-heavy ones) without interactive automation, a credit-based API is usually cheaper and simpler. 👉 Try ScraperAPI free — 7-day trial with 5,000 API credits, no credit card required

## What Bright Data's Scraping Browser actually is

It's a fully managed browser running on Bright Data's servers, headless by default, and controlled through the automation libraries you already use. You point Puppeteer or Playwright at a single `wss://` endpoint on port 9222 (Selenium uses an HTTPS endpoint on port 9515), and from there your code works like a normal browser session — except the proxy management, CAPTCHA solving, user agent handling, cookie management, and automatic retries all happen under the hood.

Two practical details worth knowing before you commit:

- You can open a live view of any session through the Chrome DevTools debugger, which matters a lot when a scrape silently breaks and you need to see what the page actually did.
- The unblocking layer is the same engine behind Bright Data's Web Unlocker product. The difference is scope: Web Unlocker handles one-step requests (one API call in, clean HTML/JSON out), while Browser API handles full interaction — clicking, scrolling, filling forms, multi-step flows, and downloading files like CSVs and PDFs through the DevTools protocol.

On the headless question: Bright Data's product page makes the point that plain headless browsers paired with proxies are easier for bot-protection software to flag at scale, and that Browser API's fingerprinting layer is designed to make sites treat each session like a real user's browser. That's the product's core promise, and the AIMultiple benchmark (97% composite score, 100% speed score) is the best independent evidence currently available for it.

## Bright Data Scraping Browser pricing right now

The current pricing structure is newer than most articles you'll find. On August 28, Bright Data moved the Browser API off a four-tier per-GB ladder onto a Free / Pay-as-you-go / Scale / Enterprise shape — the same structure it had already given Web Unlocker, SERP API, and Web Scraper API earlier that summer.

| Plan | What you get | Price | Billing |
| --- | --- | --- | --- |
| Free tier | 5,000 credits + 1 GB traffic per month, no credit card | $0 | Monthly, recurring |
| Pay-as-you-go | No commitment | $8 per GB | Per GB used |
| Scale | Starts at 71 GB included, resizable via slider | From $499/month (~$7.03/GB effective) | Monthly commitment |
| Enterprise | Custom packages, account manager, premium SLA, SSO | Contact sales | Custom |

Three things about this table that deserve a second look:

**The free tier is genuinely new.** Before August, there was no free tier at all — you went straight to $8/GB pay-as-you-go or a $499/month commitment. Now you can test the product with 1 GB of real traffic before spending anything. For a product billed on bandwidth, 1 GB is roughly 300–500 full desktop page loads, which is enough to prototype against a real target.

**The old committed tiers have gone quiet.** Through July 2026, the page printed $6/GB at 166 GB ($999/month) and $5/GB at 399 GB ($1,999/month). Those price breakpoints no longer appear — the Scale plan uses a slider, and you have to drag it to see what larger commitments cost. If you're budgeting a serious volume, expect to talk to sales rather than read a rate card.

**The entry commitment hasn't moved.** The Scale slider starts where the old entry tier did: $499 a month with 71 GB included, an effective $7.03/GB. Pay-as-you-go is unchanged at $8/GB.

## The per-GB billing unit, explained with actual page weights

Bright Data bills by bandwidth, and browsers download everything. That single sentence explains most of this product's real-world cost.

HTTP Archive data puts the median desktop page at around 2,652 KB — roughly 1,054 KB of images and 613 KB of JavaScript — while the HTML you actually parse is a few tens of kilobytes. At $8/GB:

- A full page load costs about **$0.021**.
- The same page with images, fonts, and media blocked via request interception costs about **$0.002**.

That's a 10x swing from a rule you write once, and it dwarfs every plan discount on the pricing page. Going from PAYG to a $499/month commitment saves you about 12% per GB; blocking assets you never parse saves you 90%. If you use this product, the request-blocking setup is worth more than any negotiation with sales.

One comparison from an independent 2026 review is worth repeating: this per-GB model punishes long-running sessions. Competitors billed per browser hour — one lists $20/month for 100 hours, then $0.12/hour — win outright when your agent-style sessions run long and mostly idle, because wall-clock time is cheap but bandwidth keeps accumulating. Browserless-style providers that let you self-host (from $25/month) sit in a different corner entirely for teams that want infrastructure control.

## Details that don't show up on the pricing page

A few things only surface in help docs and third-party pricing trackers, and each one affects a buying decision.

The free tier's 5,000 credits are a shared pool. Pricing trackers that monitor Bright Data's pages report that these credits are shared across Bright Data's other APIs and don't roll over month to month. Fine for testing, but don't bank unused credits.

The cheap per-request path exists inside the same product family. If your target pages don't need interaction, Bright Data's own Web Unlocker charges about $1.50 per 1,000 successful requests, and it only bills successes — failures are free. For a static protected page, that can cost a fraction of loading the full page through the browser. The Browser API FAQ itself positions the two products this way: browser interaction is the trigger for choosing the browser.

Volume pricing is now opaque by design. As noted above, the $6/GB and $5/GB breakpoints disappeared from the public page in the August restructure. Budget accordingly.

## When the Scraping Browser is the right call — and when it's overkill

Honest answer first: for straightforward page collection, this product is expensive for what you get.

The Scraping Browser earns its price when the bottleneck is unblocking plus interaction — login-gated dashboards, infinite-scroll feeds, multi-step checkout flows, sites where you need to click a button and wait for a JS-rendered response behind Cloudflare or PerimeterX. There, the built-in unblocking and the #1 benchmark placement justify a per-GB premium.

But if your job is "fetch this URL, render the JavaScript, give me the HTML," a full remote browser is overkill. You're paying bandwidth rates for images and scripts you'll never parse, when a request-based API would do the same job at a per-request rate. This is exactly the gap where credit-based scraping APIs live.

## The credit-based alternative: ScraperAPI

ScraperAPI takes a different approach to the same problem. Instead of handing you a remote browser, it wraps proxy rotation, headless rendering, and CAPTCHA handling behind a single GET endpoint — you request a URL, it returns the HTML. All plans include JS rendering, premium residential and mobile IPs, JSON auto parsing, custom sessions, unlimited bandwidth, and a 99.9% uptime guarantee. Notably, unlimited bandwidth means the page-weight math above simply doesn't apply: a 2.6 MB page and a 200 KB page cost the same credits.

Here's the full current plan lineup (all prices in USD; annual billing takes 10% off every paid plan):

| Plan | Monthly credits | Concurrent threads | Price/month | Billed annually | Get started |
| --- | --- | --- | --- | --- | --- |
| Hobby | 100,000 | 20 | $49 | $44.10 | [ Get Hobby](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | 1,000,000 | 50 | $149 | $134.10 | [ Get Startup](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | 3,000,000 | 100 | $299 | $269.10 | [ Get Business](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | 5,000,000 | 200 | $475 | $427.50 | [ Get Scaling](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | 10,500,000 | 300 | $975 | $877.50 | [ Get Professional](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | 21,500,000 | 500 | $1,975 | $1,777.50 | [ Get Advanced](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | 22,000,000+ | 500+ | Custom | Custom | [ Contact sales](https://www.scraperapi.com/pricing?fp_ref=coupons) |

Before the trial, two things worth knowing about how credits actually get spent — the part the plan grid doesn't show you.

Credits are a difficulty meter, not a request counter. A standard page costs 1 credit, but JS rendering or premium proxies cost 10, the combination costs 25, and ultra-premium proxy plus rendering costs 75. Hard domains have fixed prices: Amazon, Walmart, and eBay cost 5 credits per request; Google and Bing SERPs cost 25; LinkedIn costs 30; and sites behind Cloudflare, Datadome, or PerimeterX add 10 credits when the bypass succeeds. The spread is huge — two users on the same 100,000-credit Hobby plan can get anywhere from about 1,333 to 100,000 actual scrapes depending on their settings. Use the Domain Cost Estimator in the dashboard before committing to a plan, and set a `max_cost` per scrape so no single request blows through your budget.

Overage handling differs by tier, and it matters. On Hobby, Startup, and Business, credits stopping means scraping stops until you upgrade (auto-upgrade is opt-in). Only Scaling and above get pay-as-you-go overage at a fixed per-credit rate, capped at a monthly limit you set. If your volume spikes unpredictably, that's a reason to start at Scaling rather than Business.

Entry is low-friction on both ends: a 7-day trial with 5,000 credits and no credit card, plus a free plan with 1,000 credits capped at 5 concurrent connections if you want to keep testing past the trial.

The honest cost comparison: at $0.021 per full page load on Bright Data PAYG, roughly $475 buys you about 22,600 full page loads per month. The same $475 on ScraperAPI's Scaling plan buys 5 million credits — about 100,000 standard pages, or 1,000,000 Amazon pages at the 5-credit rate, or 200,000 fully rendered Google SERP requests at the 25-credit rate. For non-interactive scraping, the arithmetic isn't close.

👉 See ScraperAPI's current plans and start the 5,000-credit free trial

## FAQ

**Is Bright Data's Scraping Browser headless or headful?**
Headless. The browsers run on Bright Data's infrastructure, and you control them through Puppeteer, Playwright, or Selenium. The unblocking and fingerprinting layers make sites treat sessions like real user browsers, and you can watch any session live via Chrome DevTools.

**How much does the Scraping Browser cost per page?**
At the $8/GB pay-as-you-go rate, a median desktop page (about 2.6 MB) costs roughly $0.021 per full load, dropping to about $0.002 if you block images and other assets you don't parse. Your actual number depends almost entirely on how aggressively you block requests.

**Is there a free trial?**
Yes, on both sides of this comparison. Bright Data added a free tier in August 2026: 5,000 credits and 1 GB of traffic monthly, no credit card. ScraperAPI offers a 7-day trial with 5,000 API credits, also with no credit card, plus an ongoing free plan with 1,000 credits.

**Do I need to rewrite my code to switch between these tools?**
Not entirely. Bright Data's Scraping Browser plugs into your existing Puppeteer/Playwright/Selenium code — you swap the connection endpoint. ScraperAPI is a different integration: an HTTP API call per request rather than a browser session, so it replaces browser-based scraping rather than relocating it. If your scripts depend on clicking and form-filling, ScraperAPI's model won't replicate that; if they just fetch and parse, the rewrite is usually trivial.

## Which one should you pick

Match the tool to the shape of the job:

- Login flows, clicking, scrolling, multi-step interaction behind hard bot protection → Bright Data's Scraping Browser. Start on the free 1 GB tier, write your request-blocking rules on day one, and only then look at the Scale slider.
- Static or JS-rendered pages fetched at volume, including Amazon, Google SERPs, and LinkedIn → the per-request economics favor ScraperAPI by a wide margin, with a 7-day trial to verify success rates on your specific targets before paying anything.
- Long-running, mostly-idle agent sessions → per-hour billing (as offered by providers like Browserbase) beats per-GB on wall-clock economics.

One last check before you spend anything on either route: run ten real URLs from your target site through the trial and record credits consumed or gigabytes transferred. Both vendors price optimistically for easy targets and expensively for hard ones — your own URLs are the only estimate that counts. 👉 Start the ScraperAPI free trial and run your first test batch today
