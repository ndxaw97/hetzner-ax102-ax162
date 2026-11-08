# Hetzner Dedicated Server pricing: is the €259 AX102 enough, or do you need the €614 AX162? (specs, setup fees, the unlimited-traffic exception, cancellation terms)

Hetzner's dedicated line currently has two models you can configure and price on the product pages: the **AX102 at €259.00/month** and the **AX162 at €614.00/month**. The AX102 is a 16-core Ryzen 9 7950X3D with 128 GB of DDR5 ECC memory that cannot be expanded; the AX162 is a 48-core EPYC 9454P whose memory scales to 512 GB. Three details decide more purchases than the CPU choice does: there is **no minimum contract term**, cancellation is **immediate**, and traffic is unlimited **except on servers with the 10G uplink add-on**.

Below is what each model is actually for, what the €355 monthly difference buys, where the bill can grow past the headline price, and what you are committing to when you order.

> **Quick pick**
>
> - Game server, one database, a handful of VMs, a CI runner, a crawler, or a single busy application that fits in 128 GB of RAM → **AX102, €259.00/month**
> - More than 128 GB of RAM, or work that genuinely needs 48 parallel cores (VM farms, build and render batches, databases with heavy concurrency) → **AX162, €614.00/month**
> - 👉 [See the AX102 and AX162 configurations and current monthly prices](https://bit.ly/Spinservers)

## AX102 vs AX162: the two models with published specs

Both are single-tenant bare metal with the same feature set and the same two locations. What separates them is core count, memory ceiling and storage ceiling.

| Model | Processor / cores | RAM | Storage | Price (€/month) | Order |
| --- | --- | --- | --- | --- | --- |
| **AX102** | AMD Ryzen 9 7950X3D, 16 cores (8 with 3D V-Cache, 8 for higher clocks) | 128 GB DDR5 ECC, **128 GB maximum** | 2×1.92 TB up to 2×7.68 TB Gen4 NVMe DC-Edition | **€259.00** | [AX102 configuration and price](https://bit.ly/Spinservers) |
| **AX162** | AMD EPYC Genoa 9454P, 48 cores | 128 GB up to **512 GB DDR5 ECC registered** | 2×1.92 TB up to 2×15.36 TB NVMe DC-Edition | **€614.00** | [AX162 configuration and price](https://bit.ly/Spinservers) |

Two caveats about that table. It is **not the whole Hetzner dedicated line-up**: the official price list also includes AX42, EX63, EX131, SX65, SX135, SX295 and GEX131 tiers, but I could not verify their configurations against product pages, so I am not publishing specs or recommendations for them. If you want the full menu, check the order page rather than trusting a spec table someone assembled from model names.

The second caveat is specific to the AX162. Its spec table says storage goes up to 2×15.36 TB NVMe Datacenter Edition, while the description paragraph on the same page mentions 4×3.84 TB Gen4 NVMe. The table is the figure to plan around, but confirm the exact drive configuration in the configurator before you order.

## What both servers include

The shared platform is identical across the two models, which matters if you are comparing against a cheaper bare-metal provider that charges extra for basics.

| Parameter | Value |
| --- | --- |
| Port / guaranteed bandwidth | 1 Gbit/s / 1 Gbit/s |
| Traffic | Unlimited and free (one exception, below) |
| Locations | FSN1 (Falkenstein) and HEL1 (Helsinki) |
| Network availability | min. 99.9% |
| Backbone | 50.12 TBit/s total bandwidth, redundant network, Juniper routing |
| Minimum contract term | None |
| Cancellation period | Immediately |
| Payment | Bank transfer, credit card, PayPal, SEPA direct debit (EUR only, SEPA-country accounts) |

Standard features on both:

- Full root access, one dedicated IPv4 address (listed as optional), IPv6 /64 subnet
- DDoS protection plus a stateless firewall you configure in the Robot admin interface, with rules on IPv4 source addresses and TCP/UDP source ports
- vSwitch, which connects your dedicated servers across locations over VLAN
- Rescue system, VNC installation, image installer, 24-hour reset service via the web interface, traffic statistics, reverse DNS management, Domain Registration Robot
- Webmin available for LAMP setups
- Free phone and email support, 24/7 on-site service in the data centres

Optional add-ons are where costs start to move: Remote Hands (billed in quarter-hour units), additional single IPs, additional IP subnets, Failover-IP and failover subnets, and Storage Box volumes of 1, 5, 10 or 20 TB billed monthly or hourly.

## What the extra €355 a month actually buys

€355 × 12 = **€4,260 a year**. That is the real size of the decision, so it is worth being precise about where the money goes.

**Cores: 48 versus 16.** The EPYC 9454P is built for parallel workloads, and that is the phrase Hetzner uses on the AX162 page. Forty-eight cores pay off when you are running many virtual machines or containers at once, compiling large codebases, rendering or transcoding in batches, or serving a database with a lot of simultaneous connections. The Ryzen 9 7950X3D is an asymmetric chip: eight cores carry AMD's 3D V-Cache for low-latency, cache-hungry work, and the other eight are tuned for higher clock speeds. That profile suits game servers, a single application with a hot working set, a moderately sized database, or a build box that runs one job at a time and wants it finished quickly. Sixteen fast cores beat 48 slower ones whenever the workload cannot be split.

**Memory: a ceiling versus a limit.** The AX102 tops out at 128 GB and there is no upgrade path; memory is not a line item you can add later. The AX162 starts at 128 GB and goes to 512 GB of registered DDR5 ECC. If your project is at 90 GB today and growing, the AX102 is a dead end and migrating later costs you a move, not an upgrade. If you know you will sit at 64 to 128 GB for the next two years, paying for expandability you never use is €4,260 a year for nothing.

**Storage: 7.68 TB versus 15.36 TB per drive pair.** Both start at 2×1.92 TB. The AX162's NVMe ceiling is twice as high, which only matters if you are storing datasets, media or backups locally rather than on a Storage Box.

The decision rules that fall out of this:

- Under 128 GB of RAM and a workload that fits 16 cores → **AX102**, and keep the €4,260
- Any chance of crossing 128 GB in the next year, or a workload that scales with core count → **AX162**, because the AX102 has no intermediate step
- Storage above roughly 7 TB usable on local NVMe → **AX162**, or budget for a Storage Box instead
- 👉 [Compare the AX162 configuration at €614 per month](https://bit.ly/Spinservers)

## Where the monthly price stops being the whole bill

**The setup fee is charged per order.** Hetzner's official price list (German edition, which includes 19% VAT) lists a one-time setup fee of €153.51 for the AX102-1 and €361.76 for the AX162-1, roughly €129 and €304 net of VAT. The product pages show a "once-off Setup" line without an amount. Because the fee is per order, ordering, cancelling a week later and reordering costs you that fee each time. It is the closest thing this product has to a minimum spend.

**Unlimited traffic does not apply to the 10G uplink.** This is the clause that turns a fixed monthly bill into a variable one. On the standard 1 Gbit/s port, traffic is unlimited and free. Add the 10G uplink and the unlimited policy stops applying: usage above **20 TB is billed per TB**, calculated on **outgoing traffic only**, with incoming and internal traffic excluded. There is no bandwidth cap, so nothing throttles you; the meter simply runs. A seedbox, a media mirror or a backup target on 10G is exactly the case where this bites.

**Extra IPs need a reason and a primary.** Additional single IPs and subnets all require a primary IPv4 first, and subnet allocation follows RIPE guidelines. Sizes run from /29 (6 usable addresses) through /28, /27, /26 and /25 up to /24 (254 usable), each billed monthly or hourly plus a setup charge. If you are planning a mail server, a proxy pool or per-customer IPs, price the subnet into the first month rather than discovering it after deployment.

**Remote Hands runs on the clock.** On-site hands-on work is billed in quarter-hour increments. Hetzner runs 24/7 on-site service as part of the package, but anything beyond a standard intervention is a metered request.

One billing detail worth knowing: the price list quotes servers "excluding IPv4" because the dedicated IPv4 is listed as an optional feature. The €259.00 and €614.00 figures are the standard configuration with one address; run IPv6-only and the server line drops a little below the headline.

## You are not signing up for a year

No minimum contract term, and the cancellation period is "immediately". There is no annual discount to chase and no lock-in to weigh against one, and the price list shows no annual pricing tier for these models. You can order a server for a two-week migration window and cancel it when the migration ends, which is a useful way to test whether 16 cores are enough before committing to a monthly line item.

Payment is by bank transfer, credit card, PayPal or SEPA direct debit (EUR only, SEPA countries). If you handle personal data for EU customers, Hetzner offers an optional Data Processing Agreement under Article 28 of the GDPR, which most budget bare-metal providers do not put in front of you.

👉 [Order the AX102 at €259 per month, cancel any time](https://bit.ly/Spinservers)

## Cheaper and larger options in the same line-up

The AX102 is not the cheapest way into Hetzner's dedicated range. The current price list puts the AX42-1 at €115.79/month including 19% VAT, about €97 net, so there is an entry tier below the AX102 for workloads that do not need a 16-core Ryzen. I am deliberately not quoting its configuration, because the model pages I could verify cover only the AX102 and AX162.

Hetzner's own documentation also points customers at the **server auction**, where older models are sold at prices set by a Dutch-style auction and availability depends on what has been cancelled. Setup fees on auction hardware are typically lower and sometimes absent, which makes the auction the standard answer for a cheap lab box or a short-term build machine. The trade-off is older silicon and no guaranteed supply of a specific configuration.

## Questions that come up before ordering

**Is traffic really unlimited?** On the 1 Gbit/s port, yes: unlimited and free, with no bandwidth limitation. With the 10G uplink add-on, usage above 20 TB of outbound traffic is charged per TB.

**Can I upgrade the AX102's memory later?** No. 128 GB is the maximum. The AX162 goes to 512 GB of DDR5 ECC registered, so memory growth is a reason to pick the larger model even if 48 cores is more than you need today.

**Where are the servers?** FSN1 in Falkenstein, Germany, and HEL1 in Helsinki, Finland. Both are EU locations, which keeps GDPR paperwork simple and gives you a choice between central European latency and a northern European site.

**Do I get full control of the hardware?** Yes, full root access, your own kernel, Rescue System and VNC installation. Nothing is virtualised underneath you, and using 4 vCPU's worth of the machine does not reduce the bill.

**What does the network look like in practice?** Minimum 99.9% availability, redundant network with Juniper routing, and 50.12 TBit/s of total bandwidth across the backbone.

## How to decide in one minute

Fits in 128 GB and 16 fast cores handle it → **AX102 at €259.00/month**. Needs more than 128 GB, or scales with core count, or needs more than about 7 TB of local NVMe → **AX162 at €614.00/month**. Neither case requires a contract longer than the month you are paying for.

Two things to settle before you click order. First, whether you need the 10G uplink: if yes, budget for the 20 TB outbound allowance and per-TB charges above it, because "unlimited" no longer applies. Second, whether you need extra IPs or a subnet: those require a primary IPv4, follow RIPE allocation rules, and add both a monthly charge and a setup fee.

👉 [Start with the AX102, or step up to the AX162](https://bit.ly/Spinservers)
