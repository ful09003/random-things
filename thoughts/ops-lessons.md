(see warcs/03-21-23/ops-lessons)

Overall, I mostly agree with the takes from this post (younger me probably would have argued a few, thankfully I'm not
him any longer). Thoughts I have are 

> Email is the worst monitoring and alerting mechanism except for all the others.
> 
> Absence of a signal is itself a signal.
> 
> The severity of an incident is measured by the number of rules broken in resolving it.
* Or _how many rules are created as a result of resolving it_
> The mobile hotspot you're paying for so you can leave your house while you're oncall only works at home and in the office.
* This pains me, living in an area where the evil network overlords I pay are prohibited from operating, due to those
  pesky non-compete clauses
> The only other person who knows how this works is also on vacation.
* And you'll likely spend longer asking a million followup questions than you will bandaging the problem :)
> If a post-mortem follow-up task is not picked up within a week, it's unlikely to be completed at all.
* I'd also suggest "If a project has to be punted twice in a row, it's unlikely to be completed at all.". Both claims leave
  some wiggle room though, as organizational politics play some part
> That janky script you put together during the outage -- the one that uses expect(1) and 'ssh -t -t' -- now is the foundation of the entire team's toolchest.
* Yes, until one or more of your colleagues use completely different tools, shells, etc. (this pains me almost weekly)
> NTP being off may not be a root cause, but it sure didn't help.
> 
> UTC or GTFO.
> 
> Your infrastructure uses a lot more self-signed certificates than you think. A lot more. In places that make you weep.
> 
> Self-signed certificates beget long lived certs, which beget lack of certificate validity monitoring, which begets curl -k, which begets a lack of certificate deployment automation, which begets self-signed certificates.
> 
> For any N applications, at most N/2+1 use the same certificate bundle.
> 
> The system you're troubleshooting doesn't use the one the tool you're troubleshooting it with does.
* It seems a lesson that I have to share several times (especially in container-land): **bake in tools like dig and mtr**.
  You will absolutely at some point need to exec into a container and do something that will make you thank past-you for installing a little toolbox.
> An API without a reference implementation and command-line client is called a gray box.
> 
> Restricted shells are not as restricted as you think.
> 
> Very few operations are truly idempotent.
* Nothing unique here, other than this this THIS
> "Asserting state" beats "monitoring for compliance" any day.
> 
> One in a Million is next Tuesday.
> 
> People give talks at conferences not to convince others that their work is awesome and totally worth the time and effort they put in, but themselves.
> 
> It's ok to use shell for complex stuff; it often times is easier, faster, and still less of a mess than juggling libraries and dependencies.
* Absolutely agree, with the caveat that as soon as you allow your team to install and use whatever shell they'd like, it all fails spectacularly.
> There's nothing wrong with Perl.
> 
> Ok, we all at times keep adding $, {, }, and @ in random places trying to make things work, but still.
> 
> Serverless isn't.
> 
> Y38K is already here, it's just not evenly distributed.
> 
> If you determine "human error" as the root cause, then you're doing it wrong.
* I'd add that many companies who need to announce "we are blameless!" are in-fact, not.
> Your network team has a way into the network that your security team doesn't know about.
> 
> And don't even as much as mention the serial console and IPMI networks, but boy are you glad you have 'em.
* One particularly "fun" scenario is when console logins via root are disabled, and a filesystem fills up. Systems built
  by (probably salty) ex-sysads will have an answer for "what to do" which does not involve booting into a recovery
  environment, and your security team likely keeps a respectable distance.
> Blocking TCP port 53 traffic leads to very strange failures. Don't.
> 
> Somewhere in your infrastructure a service you didn't know uses DNS for endpoint discovery in a very surprising way.
* Not me with several `local.$domain.$tld` A records :)
> Do. Not. Monkey. Around. With. /etc/hosts.
>
> If you break it, you own it - for now; if you fix it, you own it - forever.
> 
> Turning it off and on again is actually quite a reasonable way to fix many things.
* This took me a while to come back to. It's a cycle, the inexperienced admin will reboot first; the somewhat-experienced 
  admin  will dig and dig _and then reboot_, and the experienced admin will reboot first :) 
> A README.md in git is no substitute for a manual page that's shipped with your tool.
* This one was a bit eye-opening to me, I dig it but alas I find the general approach is that manual pages are a thing
  of the past (and for some reason, Go developers love to shove entire manuals into their `--help` output)
> A search for a document you know exists will only turn up links to documents referencing but not actually linking to the one you're looking for.
* \>:(
> The document you're looking for was marked as obsolete and not migrated to the new content management solution.
> 
> Sure, your current content management system sucks, but it's still better than the one you're moving to.
> 
> Nobody knows how git works; everybody simply rm -fr && git checkout's periodically.
* Every year I feel I find new nuggets of joy (and sorrow) when using `git`
> There are very few network restrictions creative and determined use of ssh(1) port forwarding can't overcome.
> 
> This is both incredibly useful and concerning.
> 
> It is tempting to jump right into implementing a solution when the right thing may well be to not do the thing that requires the solution in the first place.
* This has (as of 2023) been a predominant theme for me professionally, and I notice is often driven by folks afraid or outright hostile
  of the other musings in the original post (and copied here). Intepretation of that is left to the reader.
> Turning things off permanently is surprisingly difficult.
* "No, I don't know why I am called out in the MOTD for this system, I no longer have access to it, and have not for 3 years"...
> "Ancient" is a very relative term when it comes to software and protocols.
> 
> "Obsolete" doesn't mean it's not in use and relied on.
> 
> The sets of systems online before and after a data center power outage only intersect. Some of the old systems coming online will immediately cause a different outage.
> 
> Some of your most critical services are kept alive by a handful of people whose job description does not mention those services at all.
* Locations of some of your most disturbing skeletons are only known by an often separate set of people. Competent leaders
  will respect these groups. 
> After the initial "down for everybody or just me ermahgehrd Slack is down" drop, productivity increases linearly throughout the duration of the outage.
> 
> You're bound by the CAP theorem much more often than you may think. Halting Problem's a bitch, too.
> 
> Eventual consistency doesn't help when the system you're debugging hasn't converged yet.
> 
> The source you're looking at is not the code running in production.
> 
> strace(1)/ktrace(1) doesn't lie.
* Similar to my addition of toolkits baked into container images, please make sure these are installed :)
> Unless somebody's been playing LD_PRELOAD games.
> 
> Schrödinger's Backup -- "The condition of any backup is unknown until a restore is attempted." -- is overly optimistic.
> 
> There's an xkcd for the precise situation you find yourself in. (There's also one for at least half of these.)
> 
> At some point in your career you will implement half of kerberos. Poorly.
* I'm still waiting for this moment, myself
> Any sufficiently successful product launch is indistinguishable from a DDoS; any sufficiently advanced user indistinguishable from an attacker.
> 
> Debugging any sufficiently complex open source product is indistinguishable from reverse engineering a black box.
> 
> "We've always done it this way." is not a good reason by itself, but there's bound to be one for why.
* Sadly, I find that more often than not it's not a reason you'll know until you break things terribly (as the original
  implementer is long gone)
> That reason may or may not be valid any longer, however.
> 
> A junior engineer asking "why" and pointing out the docs don't reflect reality is at least as valuable as the senior engineer working blindly off tribal knowledge.
* Asking "why" is at once the most powerful and least-correctly-used approach in this industry, in my experience.
> Your herculean efforts to upgrade the OS across your entire fleet completed just in time for the EOL announcement of the version you upgraded to.
> 
> This phenomenon was first described in Dante's Inferno as the Ninth Circle of Hell, Ring Four, aka RedHat Canto XXXIV.
> 
> Containers create at least as many problems as they solve.
> 
> The most ninja move the expert you hired for that third party black box product you rely on is to say "Let me ping the support team".
> 
> Somewhere, somebody ran into this exact problem, but they never bothered to post a solution.
* And I can't blame them, having done this plenty myself. At best I can hope to share with my team in our chosen communication
  platform, at worst I could post on stackoverflow (:
> That completely automated solution you set up requires at least three manual steps you didn't document.
* I won't say I'm adverse to bold claims of "let's automate X" and "this is too toilsome", but I find that it's often suggested
  by folks with glaring ignorance to what the manual process details in the first place, or _why it's done manually_
> CAPEX budget always increases, OPEX budget always decreases.
* Some day I'll find a company that doesn't subscribe to this belief.. Surely they're out there, right?
> CAPEX costs can be reasonably estimated, OPEX costs can only be ballparked.
* Some day the business-types will stop categorizing "human toil brought about by debt" as OPEX, and realize that "HUMANEX" vastly
  outweighs CAPEX and OPEX
> Doubling your time estimate in the hopes of beating expectations won't work because your manager takes your estimate, has a hardy laugh, and then resets it back to what they already promised upchain.
* Find yourself a manager who does not do this lol
> Your quarterly planning means bubkes when the next re-org rolls around.
> 
> Most of your actual work is not covered by your OKRs.
> 
> Recursively applying the Pareto Principle is a surprisingly accurate way to gauge your low hanging fruit, determine your high impact objectives, and ballpark your required effort.
> 
> Although, to be honest, it only works in about 80% of cases.
> 
> Management will always happily spend $$$ on outside consultants to tell them what you've been saying for years.
* They will pay 5x that to be told what they want to hear
> Management will much rather invest in inventing a new, square wheel than fixing an old round one.
> 
> In any organization practicing continuous integration, half of all commits are to fake out CI tests.
> 
> Good software development practices do not always translate well to ops and friends.
> 
> Mandatory code reviews do not automatically improve code quality nor reduce the frequency of incidents.
> 
> Every new paradigm tends to mostly add layers of abstractions; cutting through them and identifying what basic principles continue to apply is half the battle.
> 
> Real change can only be implemented above layer 7.
> 
> "Prod" is just another name for "staging".
> 
> Your source of truth lies.
> 
> Also: it's incomplete.
> 
> pcap or it didn't happen.
> 
> grep(1) > Splunk (there, I said it)
* `grep(1) + awk(1)` > many log ETL and UIs
> Multithreading is rarely worth the added complexity.
> 
> Parallelism is not Concurrency.
> 
> Simplicity is King.
> 
> Nobody knows what exactly it is you do.
* If you're being told or advertised continuously about what someone does, _and_ you're in a company where roles are usually
  well-defined, there's a non-zero chance that the person's position is completely bullshit 