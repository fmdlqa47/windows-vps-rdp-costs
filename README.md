# Windows VPS RDP: What It Really Costs, Which Plan Fits, and How to Connect (Full SpinServers Plan Table)

SpinServers sells two things you can put Windows on: a KVM VPS line that runs from 2 vCPU / 2 GB up to 32 vCPU / 32 GB, and dedicated servers from about **$79/month** with Windows auto-install and IPMI access. Both are priced without a Windows licence, because SpinServers sells Windows on a bring-your-own-licence basis. That one detail decides whether the monthly figure you see is a bargain or half the story, and it's the part most "cheap RDP VPS" articles skip.

What follows is every KVM plan on the current page, what a licence actually adds to the bill, which Windows build makes sense to install now, and the exact steps to open an RDP session plus the fixes when it refuses.

> **For most readers, a Windows box for RDP means one desktop, or a desktop two or three colleagues share.** On SpinServers that's an entry KVM tier or an entry dedicated machine, plus a licence you supply. If you want the OS bundled into a single monthly price with no BYOL paperwork, a turnkey Windows host will suit you better, because BYOL only pays off when you already hold a legitimate licence.
>
> 👉 [See the current SpinServers KVM VPS tiers and what each one costs](https://bit.ly/Spinservers)

## What the SpinServers setup gives you

The company runs its own space in San Jose, California and Dallas, Texas, which matters if your users or the platforms you connect to are in North America. The VPS line ships with a 1 Gbps port, RAID-10 SSD storage, one IPv4 and one IPv6 address, and sits behind a DDoS-filtered network. The dedicated line adds 10 Gbps ports, an IPv6 /64, VPC networking, and IPMI/iKVM remote management, with auto-install for Linux, Windows and ESXi.

That IPMI access is worth more than it sounds. It's the out-of-band console you fall back on when a firewall rule or a bad driver kills RDP and you have no other way in. On a VPS you get whatever console the platform exposes; on a dedicated box you get the same view a technician standing in the rack would have.

One operational detail catches people out: **port 25 is closed by default on every VPS**, and opening it requires a support ticket with a justification, which the provider reserves the right to refuse. If your Windows machine is meant to send mail, budget for an external SMTP relay instead of assuming it will work out of the box.

## Every KVM VPS plan currently listed

All seven plans share the same base: 1 Gbps network port, RAID-10 SSD, 1 IPv4 + 1 IPv6, DDoS protection, port 25 closed by default.

| Plan (vCPU / RAM) | Storage | Monthly traffic | Price | Order |
| --- | --- | --- | --- | --- |
| 2 vCPU / 2 GB DDR4 | 40 GB RAID-10 SSD | 4 TB | Priced at checkout | [Order](https://bit.ly/Spinservers) |
| 4 vCPU / 4 GB DDR4 | 80 GB RAID-10 SSD | 8 TB | Priced at checkout | [Order](https://bit.ly/Spinservers) |
| 6 vCPU / 8 GB DDR4 | 120 GB RAID-10 SSD | 8 TB | Priced at checkout | [Order](https://bit.ly/Spinservers) |
| 8 vCPU / 8 GB DDR4 | 160 GB RAID-10 SSD | 10 TB | Priced at checkout | [Order](https://bit.ly/Spinservers) |
| 12 vCPU / 12 GB DDR4 | 160 GB SSD | 10 TB | from **$62.00/mo** | [Order](https://bit.ly/Spinservers) |
| 16 vCPU / 16 GB DDR4 | 320 GB RAID-10 SSD | 15 TB | Priced at checkout | [Order](https://bit.ly/Spinservers) |
| 32 vCPU / 32 GB DDR4 | 500 GB SSD | 20 TB | Priced at checkout | [Order](https://bit.ly/Spinservers) |

Only the 12 vCPU tier carries a starting figure in the plan list, from $62.00/month. The rest show their total on the order form, and that total is where you find out whether a Windows image is available on the plan and whether a licence line has been added. Read it before you pay rather than after.

Notice the shape of the ladder: cores and RAM climb faster than storage. The 32 vCPU plan has 500 GB, which is generous for a database and tight if you plan to host several users' profile data plus a mail archive. Storage is the resource to watch if your workload is file-heavy rather than compute-heavy.

## The Windows licence is the line item that changes the maths

SpinServers has sold its Windows dedicated servers on a BYOL basis: you bring the licence, you don't rent it from them month to month. That's a deliberate cost model, and it's the same model behind a lot of cheap-looking Windows infrastructure.

Compare it with how turnkey Windows VPS hosts price the same thing. One US provider's current price list shows Windows Server 2019 Standard as a **$19.99/month** add-on, with Server 2016 at the same rate, Server 2022 quoted on request, and additional RDP user licences (CALs) also quoted separately. On a $12.99 base plan, the licence nearly doubles the monthly bill, and over a year that add-on alone is roughly **$240**.

So the comparison isn't "SpinServers at $X versus someone else at $Y". It's:

- **You own a licence** (retail copy, volume agreement, a Visual Studio or similar subscription entitlement) and the terms allow it on rented hardware. BYOL is cheaper, and the delivery speed and bandwidth of a bare-metal box come free with it.
- **You don't own one.** Add the cost of a legitimate licence to whatever SpinServers quotes before you compare anything. A $62/month server plus a licence is a different proposition from $62/month.

There's a third path people forget: run Windows Server on the box and connect with RDP, but keep the licence question with your reseller or Microsoft partner. It's paperwork either way. Do it before you order, not after the machine is live.

👉 [Price the server first, then add the licence you already hold](https://bit.ly/Spinservers)

## Confirm the plan can run Windows before you pay

Two things get confused here. A virtualisation platform can *technically* boot a Windows ISO and still be sold as Linux-only, and budget KVM tiers sometimes exclude Windows outright, either because the licence situation is messy or because the plan's disk is too small for a comfortable install.

SpinServers advertises auto-install of Linux, Windows and ESXi on the dedicated line. On the VPS line, Windows availability is a per-plan question, so ask sales in writing before ordering: which Windows editions the plan supports, whether the image is a clean ISO install you license yourself, and how much disk the install consumes. A 40 GB system disk fits Server with room for updates but not much else; 80 GB and up is where a working desktop with applications lives.

While you're asking, confirm the cancellation terms. Published reviews of the dedicated line note that month-to-month service generally comes without a refund window, so treat the first invoice as final and test the machine properly in week one.

## Which Windows version to install

**Windows 10 is no longer a sensible default.** Microsoft ended support for it on **14 October 2025**, and hosting providers still selling Windows 10 RDP images position them for compatibility cases: software validated only on Windows 10, or internal tools never tested on Windows 11. If you're standing up a new machine to run a desktop application remotely, start from a Server build.

- **Server 2016** is the oldest of the set and the least interesting for a new deployment.
- **Server 2019** is the safe middle ground and still the edition most application vendors list as supported.
- **Server 2022 and 2025** are where new builds should go, provided your line-of-business software supports them. Check the vendor's matrix before you pick, because rolling back means a reinstall.

SpinServers' own published list of supported Windows versions tops out at Server 2019 plus Windows 10, and that list is old. If you need 2022 or 2025, confirm availability with them directly. On a dedicated box you can also mount your own ISO through IPMI, which sidesteps the question entirely.

## Open an RDP session from Windows, macOS, Linux or a phone

Once the machine is provisioned, the IP address and administrator credentials arrive by email or in the client area. From there:

1. Open **Remote Desktop Connection** on Windows (search `mstsc`). It's been preinstalled since XP.
2. Click **Show Options** so you can see the fields that matter.
3. Put the server IP in **Computer** and your username in **User name**.
4. Under **Connection settings**, click **Save**, then **Connect**. Saving means you don't retype the IP every time.
5. Enter the password. When the certificate warning appears, accept it; the self-signed certificate is normal on a fresh install.
6. To disconnect, click the **x** in the connection bar. Your session keeps running on the server.

On macOS, iOS and Android, use Microsoft's own remote desktop app (now branded Windows App). On Linux, Remmina or FreeRDP both work. One caveat for managed or fully managed servers: administrator access may need to be enabled in the control panel before RDP will accept you at all.

## When RDP won't connect

Work through these in order, because each one rules out a layer:

- **Open the console.** IPMI/iKVM on a dedicated server, or the VPS console in the client area, shows you the actual screen. If Windows is sitting at a login prompt, the problem is network or credentials, not the OS.
- **Check the firewall.** A misconfigured Windows Firewall rule is the most common cause of a box that was working an hour ago and isn't now. Undo the last rule from the console and reconnect.
- **Check that RDP is enabled.** Control Panel → System and Security → System → Allow remote access → tick "Allow Remote Assistance connections to this computer" on the Remote tab. On a fresh manual install this is sometimes off.
- **Try a different network.** Corporate networks and some ISPs block outbound 3389. Tethering to a phone settles it in thirty seconds.
- **Recheck the credentials.** Caps lock, the wrong account, or an expired password all produce the same generic failure message.

That console access is the reason to care about IPMI before something breaks. A server you can't see the screen of is a server you can only fix by opening tickets.

## More than one user changes the sizing

A Windows Server licence includes two sessions, and those are for administration, not for a team to work in. Serving several people concurrently requires the Remote Desktop Services role plus RDS CALs, purchased per user or per device. That's a licensing task, not a configuration checkbox, and it's the step where "we'll just share the admin login" turns into a compliance problem.

Resource-wise, budget roughly 1 to 2 GB of RAM per concurrent user on top of what the OS and your applications need. The 2 GB and 4 GB tiers are single-user machines. A team of five running an ERP client wants 16 GB and a plan with real cores behind it, or a dedicated server.

👉 [Compare the larger SpinServers configurations if you're sizing for a team](https://bit.ly/Spinservers)

## Dedicated servers, when a VPS is too small

Pricing checked in September 2026 put the entry dedicated configuration at **$79/month**: a 4-core Xeon E3-1280 v5, 32 GB RAM, 1 TB NVMe, 30 TB of traffic on 2 × 10 Gbps ports. Above that, listings show a dual-processor machine with 256 GB RAM and 2 × 1.6 TB SSD in RAID-1 around **$149/month**, and a quad-processor box with 768 GB RAM and 8 × 2 TB SSD in RAID-10 at **$679/month**.

Configurations and prices shift with location, hardware availability and stock, so treat those as the shape of the range rather than a fixed catalogue. What you get at every tier is the same thing a VPS can't give you: your own kernel, your own RAID, IPMI, and a 10 Gbps pipe. For a database that has outgrown shared storage, or a trading setup where latency and a stable US IP matter, that's the jump to make.

## Which plan to pick

- **One person, one desktop, a trading terminal or browser automation.** The 2 vCPU / 2 GB tier boots Server, but 4 GB is the honest minimum once a desktop application is running. Go one step up.
- **A small team of three to five.** 6 to 8 vCPU with 8 to 12 GB, plus RDS CALs. The 8 vCPU / 8 GB tier is the natural starting point if the workload is office software rather than a database.
- **SQL Server, .NET, or anything memory-hungry.** 16 vCPU / 16 GB and up on the VPS line, or step into a dedicated box where you control the disk layout.
- **You already own a Windows licence and need bandwidth.** SpinServers is built for exactly this case, and the 10 TB to 20 TB traffic allowances are the reason to look at it over a $15/month turnkey plan with a metered port.

Two things to confirm before you pay: that the exact plan you chose offers the Windows edition you want, and what the cancellation terms are for the billing cycle you selected. Get both in writing in the sales ticket, keep it, and the rest is a straightforward build.

👉 [Start with the SpinServers plan list and match a tier to your workload](https://bit.ly/Spinservers)
