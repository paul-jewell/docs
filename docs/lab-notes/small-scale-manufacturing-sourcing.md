Title: Small Scale Manufacturing Stories: Sourcing Parts
Summary: Bar
Date: January 23, 2018

# Small Scale Manufacturing Stories: Sourcing Parts

*10 July 2020, [@OmerK](https://twitter.com/omerk)*

This lab note is equal parts a cautionary tale in sourcing parts for small scale manufacturing projects and a product defect notice for one of the Electrolama projects, the [zzh](/projects/zig-a-zig-ah/).

**tl;dr**: If you’ve bought a zzh from the Electrolama Tindie store on June 20, 2020 and you’re seeing bad RF performance, you might have received a board that has a counterfeit component installed. _This only applies to a subset of all zzh boards sold so please read the [“Identifying faulty boards”](#identifying-faulty-boards) section below for clarification_. An email with a link to this note has been sent to all Tindie customers who purchased a zzh on June 20, 2020.

Follow along for the details of how this issue happened and what we will do to make things right. I am documenting this here in hopes that it will serve as a warning and a reminder to folks interested in getting things manufactured.

## Unexpected Demand

[zzh](/projects/zig-a-zig-ah/) is a little USB stick form-factor wireless MCU development board that I developed as I was getting frustrated by the older-generation dongles used for Open-Source Zigbee Home Automation when I was rebuilding my smart home setup. With no real commercial plans for selling boards and purely as a weekend project, I pushed [the design files up on Github](https://github.com/electrolama/zig-a-zig-ah) in January and got an unexpected number of queries asking when these boards would be put up for sale. Thinking maybe this was a small group of enthusiasts, I ordered some boards and a stencil and hand populated a small number of boards, 5 at a time, that pretty much instantly sold out [on Tindie](https://www.tindie.com/stores/electrolama/) the day I listed them.

![](/_assets/zzh-lab-desk.jpg)

![](/_assets/zzh-panel5.jpg)

With the waitlist getting longer and longer and no real chance of being able to hand-populate the number of boards required, I reached out to one of the factories I contracted in the past for a small trial batch of production. At the same time, I continued hand populating smaller panels in London and the combination of both the Shenzhen and London batches became the second set of boards that I put up on Tindie June 20, 2020.

When I sent the order for this batch to be produced in Shenzhen, I sourced most of the components directly from LCSC. Items that were not available from LCSC were sourced from a parts vendor from the Duhui Market in Huaqiangbei. I’ve met this vendor in person and ordered from him many times with no problems over the last few years.

PCBs and components were delivered to the factory, boards were tested with the “blink test” program to ensure MCU was running after assembly and then packaged and sent to me in London. I individually plugged them all in, ensured that the LED was blinking and erased the program before packing them in the ESD bags along with antennas and the plastic enclosure.

I do not have RF testing facilities in my tiny home lab in London so to test the radio functionality, I picked a handful of samples and plugged them into my home server that runs my zigbee2mqtt and HomeAssistant setup. I ran them for about half a day each, every single dongle worked fine with my set of devices and that gave me the confidence to deem this batch acceptable to go for sale on Tindie.


## The Problem

The RF section of zzh is very simple, just an integrated filter/balun (LFB182G45BG5D920 from Murata) and a 0R link for the unused pi-filter before the SMA connector where the antenna plugs in:

![](/_assets/zzh-rf.png)

A full reel of LFB182G45BG5D920 is 4000 pieces, given that this was a trial batch I did not order a full reel but instead sourced the quantity required (plus a safety margin) as “cut tape” from an existing reel. This is common practice for small/trial runs and as long as you trust your parts vendor/distributor this shouldn’t really cause issues. I also asked the vendor to take a photo of the reel these were cut from, just in case.

When working with a new CEM and procuring parts from different vendors, one should always be vigilant and ask for samples for approval before production starts. Given my history with both the CEM and the parts vendor, I skipped this approval step and gave the go ahead for production against my better judgement, in order to deliver boards as quickly as possible.

Following several tickets on Github and a few support queries over email, I realised something was not exactly right with the signal quality. Upon in-depth investigation, I discovered a component issue for part FL1:

![](/_assets/FL1_samples.jpg)

The board on the left is from CEM “S” (see “Identifying Faulty Boards” section below) with parts procured in Shenzhen and the one on the right is a board I hand-populated in London with parts from Mouser. 

Sample A (sourced in Shenzhen) has a slightly different colour than Sample B (sourced from Mouser). Upon noticing this, admittedly far too late, I asked the parts vendor for that photo of the reel the parts were cut from:

![](/_assets/FL1_label.jpg)

...and contacted Murata to ask if this difference in colour could be explained by different material sources or even different manufacturing plants. The answer I got back, in verbatim, is as follows:

> Thanks for contacting us.  Our quality dpt replied as below :
> 
> We, muRata, have not change ceramic material after mass production.
> 
> We checked lot number of below taping _ Sample A, but there is no history of below lot number to make a shipment to market.
> 
> We kindly recommend to contact the Sale point of the product / distributors of sample A.
> 
> If this sample A comes from our authorized distributors, we will receive notice from them and  we can investigate this further.
> 
> We have been aware of cases where counterfeit products are sold as Murata products by using copied packaging, product labels, and Murata logo.
> 
> Please understand that we are not in the position to provide any support for products that have not been purchased through authorized channels

Doesn’t leave much room for interpretation, FL1 parts sourced in Shenzhen have a dodgy label and are counterfeit, which explains the poor RF performance.

Strange though it may seem, counterfeit components are very prevalent in all areas of manufacturing, from military to toys with shocking numbers of horror stories. Sadly, this is yet another one of those stories…



## Testing and why there is never enough of it

Of course the first question to ask in a situation like this is “How was this not caught during testing?”. Well, this is a story on how testing can fail even with the best of intentions.

Testing can be a real cost-adder and how much testing can be performed on a product is determined by a few factors, key ones being safety and cost. zzh is a hobby project that graduated from a few prototypes to a small production run of boards in a period of time that is considered fast in manufacturing world standards. By the time I released the manufacturing datapack to the CEM in Shenzhen, we had a number of people using the boards I hand populated and provided useful feedback confirming that the design was functional so my testing strategy revolved around making sure we could run a simple program on the MCU (the blink test), relying on the AOI for part placement/values checking and a random selection of boards picked out of the batch for functional testing.

First testing step that failed was AOI, after SMD assembly. The general idea here is that you train the AOI machine with a “golden sample” and subsequent boards are checked against that for any manufacturing defects or potential discrepancies in part placement/orientation/value/colour. So why didn’t the AOI flag the discrepancy in colour? Three possible causes:

  - The factory didn’t deem the difference in colour a failure and merely used the AOI to check SMD placement and orientation.
  - The factory didn’t actually use the “golden sample” I provided to them as it was panelised differently and instead used a sample they deemed correct (with the problematic FL1) from the first panel they assembled.
  - The colour difference between the genuine and counterfeit components was not distinct enough.

While I did write a custom tool that the factory used to burn the blink program and verify it visually, this was not doing any RF tests as the assumption was that AOI would catch it.


![](/_assets/zzh-testsw.png)

(the custom tool that the factory used to test boards)

With AOI not catching the problem part and the “samples approval” process being skipped in the interest of speeding things up, the functional test would have been the next line of defence against possible RF problems. I performed what I assumed to be “real life” functional tests where I picked a handful of samples and used them on my home automation setup which didn’t flag any issues. I live in a typical London flat (i.e: small space) and have a lot of routers in my Zigbee network so those probably clouded the results of this practical test.

No in-depth RF testing was performed either at the factory or in my tiny home lab, as setting up the necessary RF test environment is not exactly realistic and prohibitively expensive for a project of this hobby/enthusiast nature.


## Lessons (Re-)learned

There is nothing super special here, unfortunately counterfeit components are a real problem in manufacturing and there is a very valid reason why manufacturing operations are very “process heavy”.

I have spent the last few years of my life setting up and dealing with volume production of electromechanical products and I have worked with and implemented processes to catch exactly these types of issues creeping into products. There are established and proven systems in place to keep counterfeit parts out of production lines.

Electrolama projects are what I work on over weekends and evenings, I have a regular day job. As such, I didn’t treat this run of zzh boards with the attention to detail it required as the constant notifications of tweets/emails asking for availability of stock badly influenced my decision making ability. In the interest of getting boards out to the hands of the enthusiastic hackers as soon as possible, I bypassed systems that would have prevented this mistake from happening.

But of course, hindsight is 20/20. I am documenting this here in hopes that it will serve as a warning and a reminder to folks interested in getting things manufactured. This is most certainly not a China-only problem. No matter how trusted a parts vendor is, always perform your own tests before you approve any volume of production if you have a new source for your parts. Even if you’ve worked with them for years and historically they have supplied you with genuine parts worth thousands of dollars...


## What Comes Next

This is a hardware issue so unfortunately the fix either involves reworking or replacing the boards. 

I've emailed everyone who *might* be affected, offering either a shipment of a new FL1 for rework (quicker option) or a replacement board from the new batch (slower option).

Components and boards are sitting in another factory (that has more stringent quality control!) for the next batch but I am holding off production until samples can be tested by folks who kindly offered help out and who have access to all the fancy RF gear that I don't have in my home lab. Once these independent tests are approved, production can continue and we will have new stock available in a few weeks time. Safety over speed for this new batch.


## Identifying Faulty Boards

**Please note that the issue discussed in this note only applies to a subset of boards sold through the Electrolama Tindie shop.** There could be a plethora of reasons why you have bad RF performance (from positioning of coordinator to RF interference to bad Zigbee topography), replacement boards will only be sent to customers affected by this manufacturing issue.

The faulty boards have the mark “S” (code for the CEM used) at back, next to the USB plug: 

![](/_assets/zzh-mfg-s.jpg)

...and they were only sold through the Tindie shop on July 20, 2020.

If you have an affected board or need help identifying, please contact support@(this-domain) with your Tindie Order ID and photos of your boards and we will help diagnose your issue.


## Contact

support@(this-domain) for any Tindie order related queries.

hello@(this-domain) for everything else.
