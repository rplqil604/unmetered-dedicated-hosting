# unmetered dedicated server hosting: what 1Gbps–100Gbps plans really cost, and how to tell true unmetered from throttled "unlimited"

Unmetered dedicated server hosting changes what you're actually paying for. Instead of a monthly transfer quota — typically 5 to 100 TB, with per-TB overage after that — you pay a flat rate for a dedicated port, and the port speed is the only ceiling. A 1Gbps port pushed at line rate moves roughly 324 TB in a 30-day month, and the invoice looks identical whether you use 2 TB or 200 TB of it.

The practical rule of thumb that falls out of current provider pricing: below about 20 TB a month, a metered plan can still be cheaper. Above it, unmetered almost always wins. This article covers the math behind that number, what entry plans cost right now, the fine print that separates genuine unmetered offers from throttled ones, and a decision path for picking between them.

> **Quick pick:** if you mainly want the cheapest sensible entry point and don't need more than 1Gbps, start with a budget-focused host — RackNerd built its reputation at exactly that end of the market. For comparison, verified entry pricing elsewhere currently starts at $93/mo (Cenmax, USA) and €129/mo (NexonHost, Europe). [👉 Check RackNerd's current dedicated server lineup and pricing](https://bit.ly/my-rn)

## What "unmetered" actually means

An unmetered dedicated server is bare metal with a dedicated network port billed at a flat monthly rate, where nobody counts your terabytes. You can run the port flat out, 24/7, and the price stays the same as a quiet month. There's no per-TB rate in the price list because nothing is being measured against one.

The real ceiling is the physics of the port itself. Every server connects through a physical port with a finite speed, which is exactly why "unlimited bandwidth" as a marketing claim usually hides fair-use clauses or quiet throttling. Unmetered plans state the actual limit up front: the port speed you bought.

Two details matter more than most buyers expect:

- **Inbound counts too — in your favor.** On NexonHost's builds, neither direction is metered, so replication traffic and backups arriving at the server cost nothing extra. Some metered plans count inbound against your quota, which stings if you run nightly offsite backups.
- **Bursting is legitimate use, not an abuse flag.** NovoServe states plainly that it doesn't throttle legitimate use of the port you purchased — buy a 10Gbps port and that bandwidth is yours to saturate. The only hard line, at every provider, is illegal activity and network abuse.

## The bandwidth math

A full 1Gbps port moves 125 MB/s. Multiply that across a month and you get the real capacity hiding inside an "entry-level" unmetered plan:

| Port speed | Sustained throughput | Per day | Per 30-day month |
| --- | --- | --- | --- |
| 1Gbps | 125 MB/s | ~10.8 TB | ~324 TB |
| 10Gbps | 1.25 GB/s | ~108 TB | ~3.2 PB |
| 100Gbps | 12.5 GB/s | ~1.08 PB | ~32 PB |

Nobody saturates a port around the clock, and that's the point of the billing model. The question "how much did I transfer this month?" disappears entirely. The only variable left is whether your average throughput fits inside the port.

So when does unmetered actually beat metered? NexonHost publishes a concrete break-even figure: below roughly 20 TB a month, a metered plan can win; above it, unmetered almost always does. Metered plans pair a quota with per-TB overage, which means a viral launch or a strong campaign week lands as a line item on next month's invoice — and "forecast the traffic, then forecast the mistake" becomes part of your budgeting. Unmetered collapses all of that into one fixed number per server.

## What people actually run on these servers

The common thread is egress measured in terabytes, where a good month would be an expensive month on metered billing:

- **Streaming and IPTV** — HD and 4K delivery where sustained outbound throughput is the product itself; Server Room builds specifically for radio, IPTV and video platforms.
- **File distribution and mirrors** — game patches, package mirrors, model weights, software downloads. Any workload where a popular release can multiply egress overnight.
- **Seedboxes** — continuous, outbound-heavy seeding that burns through metered allowances faster than almost anything else.
- **CDN origin and cache fill** — edge nodes re-pull from your origin every time a cache expires, and that background traffic grows with your audience.
- **Backup and replication** — nightly dumps and cross-site sync move the same terabytes every day, limited only by port speed.
- **Game and voice servers** — player counts swing by the hour and by season, and community growth shouldn't outrun the invoice.

## What unmetered dedicated hosting costs right now

Entry pricing from the providers with public plan pages, as currently listed on each one's own site:

| Provider | Entry build (as listed) | Entry price | Port options | Locations |
| --- | --- | --- | --- | --- |
| Cenmax | Quad Core Xeon, 16 GB RAM, 250 GB SSD, unmanaged | $93/mo (USA) · $100/mo (Germany) | 1Gbps unmetered | USA, Germany |
| NexonHost | 2x Xeon E5-2630 v3 (20c/40t), 128 GB RAM, 240 GB SSD | €129/mo | 1Gbps standard; 20Gbps on Intel builds, up to 200Gbps on EPYC | 11 European countries + Ashburn, VA |
| Maple-Hosting | 16 GB RAM, 2x 240 GB SSD or 2x 2 TB SATA | $209/mo | Unmetered 1G dedicated port | Amsterdam (AMS-IX) |
| NovoServe | Configured per build; 1–10Gbps standard tiers | Quoted at configuration | Up to 50Gbps on webshop; custom 100Gbps+ | Amsterdam, New York |
| Server Room | 10Gbps tier: Xeon, 32–64 GB RAM, SSD/NVMe | Quoted at configuration | 10 / 20 / 100Gbps unmetered | New York, Miami, San Francisco, Amsterdam, Bucharest |

A few notes that affect the comparison:

- Cenmax's US plans include 5 usable IPv4 addresses plus an optional /64 IPv6 block; German plans include 1 IPv4 + 1 IPv6. The same hardware is available managed (MaxPanel, monitoring, daily backups) from $186/mo in the US.
- Server Room includes 1 IP and sells up to 256 more at $6 each, provisions typical unmetered servers within 2–4 hours after verification, and refunds payment in full if it can't deliver the server you ordered.
- Maple-Hosting's listed unmetered builds were marked out of stock when these prices were collected; annual billing there takes 15% off.
- NexonHost deploys its Intel builds automatically within minutes, but AMD EPYC builds carry an estimated two-week delivery.

RackNerd isn't in that table for a simple reason: dedicated-server stock and pricing move constantly — one of the hosts above already had flagship builds out of stock at collection time — so a snapshot of a configurator goes stale fast. The current configurator is the only reliable source for what's actually available today. [👉 See what RackNerd has in stock right now](https://bit.ly/my-rn)

## The fine print that separates good unmetered deals from bad ones

Before comparing two "10Gbps unmetered" listings side by side, three things change the real-world experience more than the number on the plan page.

### How the provider measures "unmetered"

Two models exist in the market, and they behave differently under load. The first is a flat dedicated port: no quota, no measurement, port speed is the ceiling — that's how NexonHost and Cenmax describe their builds. The second is a 95th-percentile plan: Maple-Hosting deliberately sets your physical port higher than the plan you pay for, so short spikes and live events ride the headroom for free, and you only move up a tier when *sustained* usage genuinely grows. Prefer zero chance of ever upgrading? They'll cap the port to your plan on request.

Neither model is a trick, but they suit different traffic shapes. Spiky workloads — streaming, game servers, campaign traffic — benefit from the percentile model's free burst headroom. Sustained line-rate workloads like seeding or replication fit a flat port more cleanly. It's worth one email to sales before ordering either way.

### What the network behind the port can actually deliver

This is the part most listings hope you won't ask about. Two hosts can advertise the same 10Gbps unmetered port and deliver completely different real-world throughput depending on total network capacity, carrier mix and peering — which is why the cheapest unmetered offer is so often the slowest in practice. The concrete detail to look for: NovoServe, for instance, advertises an 18+ Tbps backbone with 10+ Tier-1 transit providers and 800+ peering partners behind its plans, and publishes looking glass plus speedtest nodes in Amsterdam and New York so you can benchmark from your own region before paying. Most established providers offer equivalents; use them.

### Attack protection and deploy time

A DDoS flood aimed at an unmetered port can fill everything you're paying for, so mitigation placement matters. NexonHost includes network-edge DDoS mitigation on every build, dropping floods upstream before they consume your port. Not every provider spells this out on the plan page — confirm it. Deploy time is the other variable: 2–4 hours after verification (Server Room) and 12–24 hours (Cenmax USA) sit at the fast end, while custom EPYC builds on NexonHost run about two weeks. If you need the box this week, filter by that first.

## How to choose

Map your monthly transfer and traffic shape to a plan type:

- **Under ~20 TB/month and predictable** — a metered plan is often cheaper. Don't pay for port capacity you won't fill.
- **Steady heavy egress in the hundreds of TB** — a flat unmetered 1Gbps port is the sweet spot. Move to 10Gbps only after you've actually measured saturation.
- **Spiky audiences — streaming, launches, seasonal campaigns** — unmetered for cost predictability; a 95th-percentile plan adds free burst headroom.
- **Need 10Gbps and beyond** — NexonHost scales Intel builds to 20Gbps and EPYC builds to 50–200Gbps; NovoServe sells up to 50Gbps on its webshop and designs custom 100Gbps+ topologies; Server Room builds custom 100Gbps designs for CDNs and IPTV platforms.
- **Cheapest possible entry in the USA or Germany** — Cenmax's $93/mo Quad Core tier, unmanaged.
- **EU-heavy audiences** — Maple-Hosting's AMS-IX-connected Amsterdam network or NovoServe's Amsterdam nodes.

If price is the primary filter, RackNerd is the logical first stop — it's a host whose entire reputation was built on low pricing, and its configurator will tell you immediately whether current stock beats the fixed plans listed above. [👉 Open RackNerd's dedicated server configurator](https://bit.ly/my-rn)

## FAQ

**Is unmetered the same as unlimited bandwidth?**

No. "Unlimited" is a marketing label that usually hides fair-use clauses or quiet throttling. Unmetered is a billing model that states the real limit up front — the port speed — and never counts your terabytes.

**How much data can a 1Gbps unmetered port actually transfer?**

About 324 TB in a 30-day month at full saturation: 125 MB/s sustained, roughly 10.8 TB per day. Your real-world number will be lower, but your bill stays flat either way.

**Do unmetered servers come with a fair use policy?**

It depends on the provider, and this is worth confirming before you pay. NovoServe explicitly enforces no throttling fair-use policy for legitimate high-bandwidth use on its premium plans; Maple-Hosting measures sustained usage at the 95th percentile instead of billing overage. Illegal activity and network abuse are prohibited everywhere.

**What happens to my invoice during a traffic spike?**

Nothing, on an unmetered plan — that's the core of the model. The same invoice as a quiet month, whether the spike lasts an afternoon or a full week.

**Can I get faster than 10Gbps?**

Yes. NovoServe offers 50Gbps unmetered ports through its webshop and designs custom setups to 100Gbps and beyond; NexonHost's EPYC builds scale to 100–200Gbps; Server Room builds custom 100Gbps designs for content networks.

## Before you order

Three checks that take ten minutes and prevent the most common regrets:

1. **Run the provider's speedtest or looking glass from your region.** Port speed is a promise; throughput is the proof.
2. **Ask how "unmetered" is measured.** Flat port or 95th percentile, and does inbound count? The answers determine which plan fits your traffic shape.
3. **Confirm DDoS mitigation and deploy time** if either matters for your launch deadline.

Then match the plan to your situation. Predictable light traffic doesn't need unmetered at all; steady terabyte-scale egress wants a flat 1Gbps port; spiky workloads want burst headroom; anything past 10Gbps moves you into the EPYC and custom-build tier, where delivery times stretch to weeks. And when the deciding factor is the number on the invoice, start at the budget end of the market — [👉 compare RackNerd's current dedicated server deals](https://bit.ly/my-rn) — then pick by traffic shape rather than sticker price alone.
