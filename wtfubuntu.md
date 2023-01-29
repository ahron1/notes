# WTF Ubuntu

I use Ubuntu as my daily driver on my laptop. I have done so for many years. Largely, it works well. From time to time, I end up with what would in QC terms, be considered unmitigated disasters. Train wrecks of software development.

This is why I can never, in good faith, advise anyone to use Ubuntu. This is also why I will go to considerable length and trouble to *avoid* using Ubuntu on production servers - despite millions of people using it. Despite the large ecosystem, involving K8s, and what not.

## Audio

From time to time, usually after an update, audio magically stops working. After spending some time on the various stackexchange sites, and trying out different things, it works again. Major annoyance, but not a deal breaker. Certainly not a train wreck. That's up next.

## Screen Sharing

The year is 2022. Literally, the entire professional world has gotten used to remote work, video calls, and screen sharing. I upgrade to Ubuntu 22.04 - thinking it'll be more stable and reliable, being the "LTS" release. I am on a Zoom call with a prospective customer and offer to show a demo via screen sharing. The usual. Unexpectedly, and rather shockingly, it doesn't work. WTF is going on. I double check, the permissions are all kosher. I'm in the middle of talking to someone who might pay us. I am supposed to be technical. I can't get screen sharing to work. Sheepishly, I get the other party to switch to Meet. Same problem. The exact same problem. Switch to different browser. Still the same. WTF is going on, seriously. The error message in either case was the same, which led me to believe the issue might be deeper that Zoom or Meet. An awkward chat later, I share some screenshots and reschedule the call.

Turned out, as it should have, I was not special. [There is a question on askUbuntu with 100+ upvotes on this exact problem](https://askubuntu.com/questions/1407494/screen-share-not-working-in-ubuntu-22-04-in-all-platforms-zoom-teams-google-m). The solution is as simple as changing the default display server. When was the last time you "needed" to do that, as a user?

Earlier releases of Ubuntu used `xorg` as the display server. This worked well. Ubuntu 22.04 chucked out `xorg` and defaulted to *Wayland*. Screen sharing under Wayland is not a solved problem. Lots of workarounds, plugins, and dependencies. Not the sort of stuff you get right in the first attempt. This is fine, lots of software are yet to fully support different features out-of-the-box.

The real question is, how did Ubuntu devs actually package this with their OS and make it the default? A Red Hat engineer, around the end of 2022, [wrote that Wayland Screen Sharing is not enabled by default on Chromium](https://jgrulich.cz/2022/11/21/webrtc-chromium-year-end-report/). So why do the folks at Ubuntu think it worth guinea-pigging their users with it? Who makes these decisions at Ubuntu? Is there any rhyme or reason to it? Does someone oversee these half-baked decisions? Do they even use their own OS? Is there any testing at all? What could convince an otherwise competent, intelligent, talented bunch of individuals to bin something that has been working nicely and build in a replacement that's not yet fully functional?

Would I ever trust an entity with this sort of development process / cycle to build a production OS that I wanted to be as stable and reliable as possible? Are there conceivable situations where I want a production system that needs to be babysat for inane incompatible unannounced breaking changes on critical features?

## Yarn


