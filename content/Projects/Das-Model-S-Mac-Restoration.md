+++
title = "Das Model S Mac Restoration"
description = "I found a Das Model S keyboard in bad shape at the campus surplus store and decided to fix it up (and take a look inside). Be warned, some of the pre-restoration images are pretty disgusting."
date = 2018-09-16
draft = false
+++

{{% alert theme="info" %}} I found a Das Model S keyboard in bad shape at the campus surplus store and decided to fix it up (and take a look inside).{{% /alert %}}

For the past few weeks, I’ve been visiting the surplus store on campus regularly. Normally they have some interesting vintage boards in stock: so far I’ve seen buckling spring, “space invaders”, and a wide variety of Alps and Alps clones. The only Cherry board I’ve encountered so far has been a Das Model S Mac keyboard, which I bought for $2.

{{< figure src="DasKeyboard/IMG_20171023_163841" type="jpg" width="55%">}}

Here it is with a few caps removed. The V key was stuck when I got it. Although I was able to reset the switch after opening it, the weighting was still wrong and the contact wasn’t reliable. That would need to be replaced. The caps were quite shiny but otherwise in decent shape, and the plate underneath was filthy.

{{< figure src="DasKeyboard/IMG_20171023_171640" type="jpg" width="55%">}}

With the keycaps removed, it was time to wash them. I put them all in a plastic container, gave them a good amount of soap and warm water, then shook, rinsed, and repeated. By that point most of the grime and oil had come off. For good measure, I hand-scrubbed each cap with a paper towel before setting them out to dry, though I doubt this was necessary.

{{< figure src="DasKeyboard/IMG_20171023_210622" type="jpg" width="55%">}}

Keycaps out of the way, I then set about disassembling the board. A total of five screws hold the board together on the bottom: one under each foot, two at the bottom corners, and one under the warranty sticker. I removed all of the feet to be cleaned later.

{{< figure src="DasKeyboard/IMG_20171024_161124" type="jpg" width="55%">}}
<!-- {{< figure src="DasKeyboard/IMG_20171024_161213" type="jpg" width="55%">}} -->

From there, it was a matter of running my fingers along the edges to remove the top plastic shell. I managed to break a few of the tabs holding the two shells together in the process. Luckily the tabs aren’t really necessary since the screws connect both halves of the case.

<!--{{< figure src="DasKeyboard/IMG_20171024_162130" type="jpg" width="55%">}}-->
{{< figure src="DasKeyboard/IMG_20171024_162513" type="jpg" width="55%">}}

The insides of the shell were just as dirty as the top of the plate. A combination of brushing and compressed air took care of the larger pieces, leaving only the oil underneath. With the worst of the grime dislodged, I was then able to examine the electronics more closely.

{{< figure src="DasKeyboard/IMG_20171024_162529" type="jpg" width="55%">}}

Dislodging the USB cable strain relief from the hole in the plastic shell and the removal of two additional screws from the USB daughterboard allows for the removal of the entire PCB.

{{< figure src="DasKeyboard/IMG_20171028_143506" type="jpg" width="55%">}}

The USB hub uses a Genesys GL850G. This is a single-TT hub chip, so while normal peripherals should function fine, combinations of multiple 12Mbps devices (such as some DACs) could potentially have issues. As the cable has two USB connectors, the keyboard itself shouldn’t share this pipeline with devices connected to the hub.

The other IC is a Holtek HT82K94E keyboard encoder.

{{< figure src="DasKeyboard/IMG_20171028_143312" type="jpg" width="55%">}}

At this point I desoldered the bad switch and replaced it with a spare from a switch tester. I didn’t have a desoldering pump on hand, so I had to resort to melting the solder and pulling the switch by hand. Luckily I had a switch puller from one of my E-element boards to help me remove it from the plate.

{{< figure src="DasKeyboard/IMG_20171028_151700" type="jpg" width="55%">}}

After replacing the broken switch, I finally got to removing the more difficult grime. Although I was able to apply IPA liberally to the PCB, I had to be a bit more careful with the plate since the alcohol can etch ABS. I’m not sure what plastic the switches themselves are made of, but might as well use caution.

{{< figure src="DasKeyboard/IMG_20171029_143402" type="jpg" width="55%">}}

The plastic casing was then washed thoroughly under normal water. After being dried with a microfiber cloth, it shined quite nicely. A couple of scratches here and there from the previous owner are here to stay, but the end result still looks far better than it did before.

{{< figure src="DasKeyboard/IMG_20171029_144925" type="jpg" width="55%">}}

With the keycaps, PCB, plate, and case all clean, it was time for reassembly.

On the bottom of the case, I used superglue to reattach the rubber feet.

{{< figure src="DasKeyboard/IMG_20171029_172744" type="jpg" width="55%">}}{{< figure src="DasKeyboard/IMG_20171029_173052" type="jpg" width="55%">}}


Finally, I started installing the keycaps. After a few false starts, I realized that the stabilized keys needed to be attached first, since Costar stabilizers need a bit of wiggle room to put on.

{{< figure src="DasKeyboard/IMG_20171029_174212" type="jpg" width="55%">}}

The finished board is quite nice, but not entirely to my tastes. I'm not a big fan of clicky MX style switches (I prefer the cleaner-feeling actuation of most vintage switches). On top of that, I think the cheap Outemu blues are better than the Cherries since they're just as consistent but are smoother and crisper until just before bottoming out.

Thanks to the thick plate, the switches feel surprisingly solid, a bit better than the E-elements and without the drawback of loud resonances through the chassis. Even though the keycaps are fairly thin and etched, they still feel quite nice and aren't as loud as the more brittle feeling cheap caps found on most entry-level boards. Oddly enough, I think I like the amount of smoothing the caps have seen; it reminds me a bit of high-end ABS caps, which I much prefer to the cheap textured ones.

{{< figure src="DasKeyboard/IMG_20180112_160531" type="jpg" width="55%">}}

I do like the Costar stabilizers. The spacebar feels like a single uniform key rather than a tilted one when struck off-axis; it's far better than the cheap rattly messes found on Corsair boards and even a decent bit better than the genuine Cherries and whatever knockoff the E-element boards use. If I were to make a custom board, I think Costars would be worth it; the keycaps aren't much harder to remove but the typing experience is appreciably improved.
