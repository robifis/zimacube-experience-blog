# OPNsense Might Be the Best Use Case for the ZimaCube Yet

I did not buy my ZimaCube 2. I got it through the [Pioneer programme](../meta/disclaimer.md), and that still matters because it would be very easy to get carried away talking about hardware like this and pretend price is irrelevant.

It is not irrelevant.

That said, this might be the cleanest use case I have found for the machine so far.

If you have read [why I moved the box to Proxmox full time](../homelab-journal/proxmox-primary-os.md), you already know where my head is at with this hardware. I do not want the ZimaCube acting like an expensive little NAS with good manners. I want it doing real work. Running OPNsense on it feels like exactly that.

## The port layout makes this make sense.

A lot of homelab ideas sound clever right up until the physical hardware gets involved.

This one does not.

The ZimaCube 2 Standard has dual 2.5 gigabit Ethernet on the back, and that is the whole reason this works so well. Most people still are not getting multi-gig internet into the house anyway, which means those two ports are already enough to make it a very believable firewall and router box without resorting to USB dongles, adapters, or whatever other crimes people commit to get a second network connection.

That is the bit I love.

One port for WAN. One port for LAN. Done.

If you want the broader hardware picture, read the [hardware overview](../hardware/overview.md). The short version is simple: the ZimaCube has more than enough I/O and more than enough headroom for this job.

## Proxmox is what makes it interesting.

Installing OPNsense itself was not the interesting part.

That bit is easy.

You download the DVD image, throw the ISO into Proxmox, create a VM, pass both network adapters through at the bridge level, boot it up, and go through the install. The only part you really need to pay attention to is making sure your WAN and LAN adapters are assigned properly. Get that wrong and you are just manufacturing your own misery.

Everything else is normal.

What makes the setup good is that it is living inside Proxmox on the same machine I am already using properly elsewhere. That matters because it means I can still take advantage of the internal drives, the rest of the platform, and the same virtualisation workflow I am already sold on from [the Proxmox setup](../homelab-journal/proxmox-primary-os.md).

That is where this stops being "router in a VM for the sake of it" and starts becoming a genuinely sensible homelab decision.

## The ISP router was the weak link.

This is where the whole thing gets annoying.

My internet provider gave me a Nokia Beacon 3.1, and it is one of those ISP routers that reminds you you do not really own your own network. You are allowed to use it. You are not really allowed to shape it.

I had to put the thing into bridge mode just to get out of its way.

That is frustrating, because the whole point of running your own network gear is control. DHCP, DNS, routing, plugins, remote access, firewall rules, the lot. If the ISP box is still acting like the adult in the room, it never quite feels like your setup.

OPNsense fixes that.

Not perfectly, because the bridge mode nonsense still exists, but enough that the network finally feels like mine again.

## A router VM is not automatically a stupid idea.

Some people hear "router in a VM" and stop thinking.

I get it.

It sounds like the sort of sentence that should end in a forum thread full of regret. If this was the only machine in the house, if there were no backups, no rollback path, and no fallback hardware, I would agree with them.

That is not what this is.

I am already [backing the environment up properly](../homelab-journal/backups.md). The router VM is cloned. I can template it. I can roll it back if I break something. The old physical router is still sitting there configured in the house. If everything goes wrong, I unplug one cable, plug another back in, and the network is back.

That is not reckless.

That is a recovery plan.

Half the internet is held together by worse decisions than this.

## The hardware is barely breaking a sweat.

This is the part that really makes me smile.

I have given the OPNsense VM one core and 2GB of RAM. That is already more than enough RAM for a router VM, and the ZimaCube itself has plenty of CPU thanks to the i3-1215U sitting underneath it all. Most consumer routers are doing this sort of work on hardware that feels like it was pulled from a drawer in 2014.

This is not that.

This is a proper x86 machine with DDR5 memory and enough headroom to run infrastructure without sounding like it is begging for mercy. Even the Standard model is overqualified for the job. If I had the Pro with 10 gig on top, it would be even more ridiculous in the best possible way.

Ridiculous is fine when it works.

## OPNsense gives you room to grow.

This is the real reason I like it.

A lot of home network gear wants you to stay inside the lines. OPNsense feels like a blank canvas. You install it, set your interfaces, get the core network online, and then you can shape the rest around how you actually want your lab to work.

That flexibility is the whole appeal.

I can run DHCP and DNS the way I want. I can add the Tailscale plugin and get secure remote access into the network without doing anything stupid. I can start layering in proper firewall rules, monitoring, and extra services without having to beg a plastic ISP box for permission.

I am also planning to spend more time with curated blocklists and feeds, because that is another area where OPNsense starts to justify itself very quickly. Once you realise you can harden the edge of the network properly, going back to a locked-down ISP interface starts to feel a bit pathetic.

## The all in one box argument is stronger than people admit.

A lot of the so-called proper way to build a homelab really just means buying more little boxes.

More power bricks.

More mess.

More things to fail.

There is obviously a point where separating roles makes sense. I am not pretending every service in the world should be collapsed into one chassis. That would be silly. Yet the ZimaCube has the horsepower, the storage options, and the port selection to make this specific consolidation feel smart rather than cheap.

That is the difference.

This is not me trying to force a tiny machine to do too much. This is me looking at a machine that has plenty of CPU, more than enough RAM for a router VM, internal storage flexibility, and dual 2.5 gigabit, then giving it a job that actually suits it.

That feels correct.

## It is not perfect.

The setup itself has been solid.

The annoyances are mostly external.

The ISP bridge mode nonsense is still annoying. The fans are a little louder than I would like, and after a few hours in the room you do notice them. That is not a deal-breaker, but it is real. I will probably try a low-noise adapter from Noctua and calm it down a bit.

I am also already thinking about what comes next.

A Pro upgrade with 10 gig would be very tempting. More networking options would be even better. I have a couple of ideas in mind there that I am not going to spoil just yet.

## My honest take

This is one of the first setups that makes the ZimaCube feel fully justified.

Running OPNsense on it does not feel like a gimmick. It feels like the sort of job this hardware was built for. Dual 2.5 gigabit on the back, Proxmox underneath, internal drives available, rollback options in place, backups already handled, and a fallback router still on standby if I really need to bail out.

That is not overkill.

That is a clean homelab design with a safety net.

If you buy a machine like this and only let it sit there doing cautious little NAS duty, I think you are leaving a lot on the table. I said in my [ZimaOS write-up](../homelab-journal/zimaos-review.md) that the stock software started to feel like a ceiling. This is the other side of that argument. Once you put the ZimaCube on Proxmox and start giving it proper jobs, the hardware finally starts making sense.

This is one of those jobs.

---

**Related Posts:**
- [Why Proxmox Is the Only OS That Makes Sense for the ZimaCube](../homelab-journal/proxmox-primary-os.md)
- [The Most Exciting Topic in Tech: Backups](../homelab-journal/backups.md)
- [ZimaOS: Good at What It Does, Just Not for This](../homelab-journal/zimaos-review.md)
- [Hardware Overview](../hardware/overview.md)
- [Would I Buy the ZimaCube 2 With My Own Money?](../hardware/would-i-buy-it.md)

*Written: June 2026*
