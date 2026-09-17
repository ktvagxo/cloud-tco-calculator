# cloud tco: how to calculate the real cost of cloud, catch hidden fees, and lower your monthly bill

Most people search "cloud tco" for one of two reasons: a cloud invoice came in higher than expected, or they're building a business case for a migration and need numbers that hold up in front of a budget owner. Either way, you're in the right place, because the whole problem with cloud TCO is that the sticker price is only the beginning of the story.

TCO stands for total cost of ownership — the full cost of running a workload somewhere over its lifecycle, not just the monthly line item on the invoice. The gap between those two numbers is where budgets go to die. This piece walks through what belongs in a real cloud TCO calculation, which costs tend to get forgotten, and how providers with transparent resource pricing (we'll use Sharktech's OpenStack-based cloud as a concrete example, with its current plan prices) change the math.

## What cloud TCO actually covers

A useful cloud TCO calculation buckets costs into six groups. Skipping any of them makes the final number fiction.

- **Compute and storage**: the VMs, volumes, and object storage you actually provision. This is the part everyone quotes.
- **Data movement**: traffic in and out of the platform, between regions, and to your users. The part almost nobody prices correctly before signing up.
- **People costs**: engineering time to build, operate, patch, and monitor the environment. Often the single biggest line in year one.
- **Migration and exit costs**: moving workloads in — and, just as importantly, the cost of getting them *out* later.
- **Add-ons and small fees**: extra IPv4 addresses, snapshots, load balancers, support tiers.
- **Risk and compliance overhead**: audits, certifications, and the cost of downtime if the provider's uptime doesn't hold up.

If your current comparison is "this VM costs $X here vs $Y there," you've covered bucket one and are ignoring five others. That's also why cloud TCO comparisons so often end in arguments — two teams can be looking at completely different subsets of the cost.

## The costs that quietly wreck your TCO

### Egress fees are the classic silent killer

The math is not subtle. On AWS, outbound data transfer starts at **$0.09 per GB** for the first 10 TB per month, dropping to $0.085 for the next 40 TB, $0.07 for the next 100 TB, and $0.05 beyond 150 TB. Inbound is free. So a service pushing out an extra 1 TB a month pays roughly $90/month in egress alone — on top of compute.

Compare that with Sharktech's published rates: unlimited inbound, 5,000 GB outbound included with cloud services, and **$0.002 per GB** for additional outgoing traffic. That same extra 1 TB costs about $2. For any workload that serves a lot of data to the outside world — media, backups, APIs, CDN origin — egress can swing the total bill more than compute choice does.

This is also why egress pricing doubles as a lock-in mechanism: the more expensive it is to move data out, the more your data stays put regardless of whether the service still fits you.

### Overprovisioned and idle resources

The average deployment is sized for peak load and runs at average load. If you provision for the 30th of the month but live at the 15th, you're paying for capacity you never touch. Every serious cloud cost guide lands on the same advice: measure actual utilization before you size anything.

### Small fees that add up

IPv4 addresses are a good example. At Sharktech you get one public IPv4 free with activation and pay $1.50/month for each additional one — cheap, but listed. At hyperscalers, IP and load balancer charges arrive on the bill the same way, just often discovered later. The TCO lesson: enumerate everything you'll attach to the environment, not just the VM.

### Exit costs

The last line of a real TCO calculation is "what does it cost to leave?" If you can't export your machine images and data at reasonable cost, you don't own your TCO — the provider does. Sharktech makes a point of this on its cloud pages: you can download your server disk images at any time, via the portal or API, which keeps the exit scenario priced at approximately the cost of the bandwidth to move it (at $0.002/GB, that's cheap).

## How to run your own cloud TCO calculation

Here's a process that holds up in a budget meeting:

1. **Inventory the workload.** Peak vs average CPU, RAM, storage volume, and — critically — actual monthly inbound and outbound traffic in GB.
2. **Price the target environment in unit terms.** Hourly or monthly rates for the resources you need. With transparent providers this is arithmetic; with bundled hyperscaler pricing you'll want their calculators and a healthy margin of error.
3. **Add data movement, both directions.** Migration-in traffic, steady-state egress, and inter-region traffic if applicable.
4. **Add people time.** Setup effort, ongoing operations, and whether you need the provider's support. Note: Sharktech publishes 24/7 phone support on all cloud plans, which is rarer than it should be and directly reduces the "waiting for a ticket" cost.
5. **Price the exit.** Can you export your images and data? At what per-GB cost?
6. **Compare 1-year and 3-year totals, not month one.** Year-one pricing comparisons are one of the most common ways cloud TCO gets undercounted — commitments expire, traffic grows, and egress compounds.

Run the same six steps for each provider you're comparing and the ranking usually sorts itself out.

## Where the hyperscaler premium comes from — and when it's worth paying

AWS, Azure, and GCP aren't expensive by accident. You're paying for a global region footprint, enormous managed service catalogs, compliance certifications, and deep integrations. If your business genuinely needs AWS-specific services or 30 regions of presence, that premium buys something real.

But if your workload is straightforward — VMs, storage volumes, private networks, load balancing, snapshots — the premium mostly buys brand. A mid-size deployment of standard virtual machines doesn't become cheaper because the provider is famous. Sharktech's own FAQ frames it bluntly, guaranteeing "at least 40% cost savings compared to hyperscalers" for its quality tier, and its public cloud pricing page claims 50–80% savings. Vendor claims deserve skepticism in general, but in this case you can check the underlying unit prices yourself, because they're published.

## A concrete example: transparent resource pricing at Sharktech

Sharktech runs an OpenStack-based cloud in five locations — Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam — with a resource-pool model: instead of rigid VM presets, you get a pool of CPU, RAM, and storage to carve up across as many VMs as you like. Published unit rates:

| Resource | Rate |
| --- | --- |
| CPU | $0.0025 per core-hour |
| RAM | $0.0035 per GB-hour |
| NVMe storage | $0.00009 per GB-hour |
| SSD storage | $0.00006 per GB-hour |
| HDD storage | $0.00002 per GB-hour |
| Extra IPv4 | $1.50 per month |
| Extra outbound bandwidth | $0.002 per GB (inbound free, 5 TB out included) |

Those aren't overage penalties — they're the actual metered rates, which is what makes a TCO calculation honest: you can compute your bill before you receive it. Storage is tiered by performance (per-volume vendor estimates: NVMe around 1.2 GB/s and ~18,000 IOPS, SSD around 350 MB/s and ~6,000 IOPS, HDD around 120 MB/s), so you can put hot data on NVMe and archives on HDD instead of paying NVMe rates for everything.

The network comes with DDoS protection built in — Sharktech has been a DDoS-protected hosting specialist since 2003 — so protection doesn't show up as a separate TCO line the way it does when you bolt on a scrubbing service elsewhere. Private networking, virtual routers, floating IPs, load balancing, and an integrated VPN for hybrid setups are included features rather than add-on SKUs.

If your TCO spreadsheet wants concrete numbers, 👉 [grab Sharktech's current public cloud pricing and plans here](https://bit.ly/SharKTech) and drop them straight into the unit-cost columns.

## Full plan comparison: every current Sharktech cloud option

Sharktech splits its cloud into two billing models on the same infrastructure: **Public Cloud** (a committed base with hourly metered usage above it, capped to prevent surprise bills on everything except Enterprise) and **Dedicated Cloud** (you prepay a fixed allocation and get exactly that, no more, no less). Here is every plan currently displayed on the official store, starting from the Los Angeles location, billed monthly:

| Plan | vCPU (base–max) | RAM (base–max) | SSD storage (base–max) | Bandwidth | Price (from) | Billing | Link |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Public Cloud Small | 4–16 | 8–32 GB | 300–2,400 GB | 20 TB included, then $0.002/GB | $39.00/mo | Monthly | [ View Small plan](https://bit.ly/SharKTech) |
| Public Cloud Medium | 8–32 | 16–64 GB | 800–6,400 GB | 20 TB included, then $0.002/GB | $79.00/mo | Monthly | [ View Medium plan](https://bit.ly/SharKTech) |
| Public Cloud Large | 32–128 | 64–256 GB | 1,500–12,000 GB | 20 TB included, then $0.002/GB | $249.00/mo | Monthly | [ View Large plan](https://bit.ly/SharKTech) |
| Public Cloud Enterprise | 64+ (uncapped) | 128 GB+ (uncapped) | 5,000 GB+ (uncapped) | 20 TB included, then $0.002/GB | $499.00/mo | Monthly | [ View Enterprise plan](https://bit.ly/SharKTech) |
| Dedicated Cloud (XS–3XL) | Fixed allocation, your choice | Fixed | Fixed | Per quote | Custom | Flat monthly | [ Request a Dedicated Cloud quote](https://bit.ly/SharKTech) |

Notes that matter for TCO math: every plan includes 1 free public IPv4 (extra addresses $1.50/mo each), optional NVMe and HDD storage tiers are available up to each plan's caps, and non-Enterprise public plans carry a hard maximum resource ceiling so a runaway workload can't produce a runaway invoice. Dedicated Cloud is quote-based through sales — you tell them the resource pool, they price it flat monthly. If you want a bigger uncapped setup, that conversation covers it too.

## Which plan fits which workload

Some judgment, based on the published specs:

- **Small ($39/mo, 4 vCPU / 8 GB base)** fits staging environments, internal tools, small web stacks. The base allocation is modest, but the pool model means you can split it into four small VMs instead of one bigger one.
- **Medium ($79/mo, 8 vCPU / 16 GB)** is a sensible first stop for small production — a web tier plus a database VM with headroom.
- **Large ($249/mo, 32 vCPU / 64 GB)** handles heavier applications, multiple services, real databases. This is where hyperscaler comparisons start showing four-figure monthly gaps.
- **Enterprise ($499/mo, uncapped)** is for workloads that legitimately don't fit in a box — note it drops the billing cap, so utilization discipline matters here.
- **Dedicated Cloud** is the right call when predictability beats flexibility: a fixed monthly number, resources exclusively allocated, and it's also how you get GPU-ready setups.

The practical test: take last month's actual utilization (not your aspiration), match it to the smallest base allocation that covers it, and let the metered rates handle the spikes. If you do it the other way around — buy for the dream, get billed for the dream — that's a self-inflicted TCO problem no provider can fix.

## Cutting TCO no matter who hosts you

Switching providers is one lever. These are the others, and they work everywhere:

1. **Right-size before you optimize anything else.** Downscale anything running below ~40% CPU consistently.
2. **Tier your storage.** Databases on NVMe, logs and archives on HDD. At Sharktech the rate difference is roughly 4.5x between NVMe and SSD and 45x between NVMe and HDD per GB-hour — so putting cold data on NVMe is just donating money.
3. **Prefer fixed allocations for predictable workloads.** Steady-state demand is cheaper as a commit; spiky demand is cheaper metered. Public vs Dedicated Cloud is literally this choice.
4. **Watch egress monthly.** Set an alert. Egress creep is silent.
5. **Keep the exit cheap.** Exportable disk images and cheap data-out rates are a TCO feature, not a nicety.

## Quick answers on the Sharktech-specific angle

**Is the cheap price subsidized by bad uptime?** The vendor guarantees 99.999% uptime on public cloud, and an independent 2026 review from HostAdvice reported measured uptime above 99% and fast ticket responses. For balance: Trustpilot shows a middling 3.5/5 across a small sample of 13 reviews — too few to be conclusive either way, but worth knowing. The honest read is that the transparent pricing and published uptime guarantee give you verifiable claims, and the review record is thin rather than damning.

**Why does OpenStack matter for TCO?** Two reasons: no per-VM licensing fees baked into your rate, and open standards that keep migration tooling compatible. Open source infrastructure prices as infrastructure, not as infrastructure plus a software tax.

**What if my needs are unusual?** That's what the custom/Enterprise path is for — the same portal, uncapped resources, and a sales team that builds private and dedicated clouds for a living. 👉 [You can reach the full plan lineup and the sales contact through this link](https://bit.ly/SharKTech).

## The bottom line

Cloud TCO isn't a number — it's a discipline. The teams that pay least are the ones who count egress, add-ons, people time, and exit costs, then compare year-one *and* year-three totals across providers with transparent unit pricing. The teams that pay most compare one monthly VM price and call it done.

If your workload is standard VMs, storage, and networking — and especially if it pushes data outbound — a resource-metered OpenStack provider like Sharktech can cut the recurring bill dramatically, with published rates you can audit before you commit. If you need hyperscaler-specific services or global region sprawl, you're paying for things you actually use, and that's a different conversation. Either way: run the six-step calculation, and let the numbers make the case.
