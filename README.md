# MechBoard16
MechBoard16 is a mechanical keyboard for the Commodore 16.

![Board](https://raw.githubusercontent.com/SukkoPera/MechBoard16/master/img/render-top.png)

## Summary
This project was born out of my dream of being able to build a complete Commodore 16 computer from scratch. While you can already build <a href="...">the full circuit board</a> from off-the-shelf-components only (almost...) and put that in a case <a href="xxx">you can buy new on the market</a>, you would then have to complete that by stealing a keyboard from an original machine (and no, VIC-20/C64 keyboards won't work and there isn't much we can do in that regard, unless we patch the KERNAL and a ton of software). So I just set to rectify that.

Now, while I'm not too fussy when it comes to keyboards, give me anything that works and I'll be happy (although you probably wouldn't want to be one of the witnesses of the third time I typed *rep* on a keyboard with a misworking <kbd>G</kbd>....), making the new C16 keyboard a mechanical one looked to be the best choice for a number of reasons:
- Some good soul has already done that for the C64: he did the basic design, took all the relevant measurements, thought about all the parts needed and - best of all - he openly shared all of his notes and materials about the process. Since his original project fits the Breadbin C64 and the C16 case is basically the same, this means that, in principle, I could recycle 90% of his work and just design a new PCB featuring the C16 keyboard matrix. So all hail to MtnBuffalo and his <a href="https://www.breadbox64.com/mechboard64-2/">MechBoard64 project</a>, this wouldn't be a reality without his job, isn't openness great?
- Well, designing a membrane keyboard would actually be harder for an amateur (all membranes are custom, how do I design and get one produced?) and lead inferior results.
- There is an incredible variety of mechanical keyswitches and keycaps around, yielding endless customization possibilities.
- I didn't know anything about mechanical keyboards, so it would just be fun to learn about them and finally own one at last.

## Assembly
The documentation from MtnBuffalo is pretty detailed, so please refer to that but first have a look at the following notes from myself.

### Circuit Board
The **circuit board** is the electrical heart of the keyboard and is the only component that needs to be different from the one used in MechBoard64 since the C16 and C64 use different keyboard matrices, despite the nearly identical key layout.

The MechBoard64 PCB was made in Sprint Layout, which is a non-open format, so I redid it all in KiCad and while I was at it, I decided to add some improvements:
- I added a diode for every key. In theory, this allows for every key to be read properly, without *ghosting* issues. Still, the KERNAL applies a *blocking* algorithm so, in practice, nothing will change in this regard.
- BUT I also added a microcontroller with USB capabilities (ATmega32U4) and connected it to all the keyboard rows and columns. This mean the whole thing can be a *N-Key Rollover* USB keyboard, which will probably be useful for those people who want to use it with emulators. And keep in mind that since you have full control on the software, it can also appear as a VIC-20/C64 keyboard over USB!
- MechBoard64 has a version with LEDs, but all LEDs are driven in parallel, resulting in a huge current draw. I don't particularly care about LEDs but I decided to throw them in while I was at it, and since I would have a microcontroller onboard anyway, I decided to drive them through a MAX7219/7221 chip: this allows for individual LED control, much reduced power draw (the LEDs are multiplexed), brightness control and maximum brightness setting through a single resistor.

I realize not everyone might be interested in the above and in fact **it is all optional**! If you are not interested in USB and/or LEDs, just mount the key switches and bridge every diode (yes, this is annoying, sorry), ignoring all the extra components: basic keyboard functionality will still be there.

The PCB is what this GitHub project is all about and let me reinstate that it's only component that you need to change to make a MechBoard64 work on a C16. If you are already familiar with it, just grab the new PCB and go ahead with the build!

### Metal Bracket
The board will need to be fastened to the top part of the case somehow, and this is done through a **metal bracket** which doubles as a keyboard plate.

I have designed my own bracket (coming soon...) but since I strived to maintain the same position for all of the key and screw holes, you should be able to use this board with the plate that was designed for the MechBoard64: you can get it through a Chinese company as MtnBuffalo recommends or ask other manufacturers.

### Screws
To fasten the two things together, you will need **screws**: MtnBuffalo recommends *six plastic M3 x 10 mm screws, six plastic M3 bolts and six plastic M3 x 3mm spacers (ø=6 mm)*. I used *metal* screws of the same dimensions and plastic spacers with an outside diameter of 5 mm.

### Key Switches
At this point you will have a nice keyboard prototype without keys, so you will need to solder exactly 66 **key switches** into it. This is the point where your customization options start: MtnBuffalo used Gateron Yellow switches as he thought they yield a very similar experience to the original keys. While I have never tried those, I don't think we should necessarily aim at replicating the original experience, so I'd recommend feeling free to use different switches.

Although, it's easy to get lost for those like me who might not be too much into keyboards, so here's some help: first of all, you need *standard/normal profile* switches, don't get *low profile* ones.

Second: speaking of "pressing experience", there are 3 main types of switches: the most common type is *linear* and the original keys are of this type. It means that the key can be pressed with a constant pressure until it comes to a halt. Some people prefer to feel a "bump" when the key triggers, so they'd better look for keys of the *tactile* type. Finally, I have a thing for *clicky* switches, which make a rather high-pitched click when they trigger. I'm well aware most people find these annoying, but when your ordinary keyboard is a 122-key "battlecruiser" Model M...

Finally, while the keyboard was designed for Cherry MX keyswitches, these days maaaany manufacturers make compatible ones: I think the most respected alternative manufacturers are Gateron and Kailh. Durock is another well-known brand and, even though I don't think it's a particularly smart idea to save 10€ on a project that will cost you around 100€ anyway, there are also cheaper options: Outemu is a Chinese brand that seems to have its fans, while Redragon is the cheapest I could find (less than 10€ for 150 keyswitches - more than enough for 2 keyboard - shipped to Europe!) and their Black switches look definitely decent to me, for the price.

MX-compatible key switches can have two different mounting styles, *PCB* or *plate*: the former are for keyboard that do not use a plate and come with two extra side prongs that help positioning the key switch correctly and securing it in place. Plate-mount switches lack these prongs, since their job will be done by the hole in the plate. MechBoard64 requires plate-mount switches or that you cut the extra prongs (it's just plastic), while MechBoard16 has extra holes and will thus accept both types.

One final tip is that there is a tendency to use stiffer switches for the spacebar, since it is generally pressed with more force. So if you chose MX Red switches, you might want to use an MX Black for the spacebar. Due to my clicky thing, I used Gateron Blues but I went for a Gateron Green for my spacebar.

### Keycaps
The key switches look all boringly the same, so you'll probably want to stick some **keycaps** on their *stems*. I was quite surprised when I found out that almost all the keycaps ever made are the same size, so in principle you could use any keycaps having MX connection style. In reality, you are bound to the original Commodore keycaps: this is because most of the wider keycaps (<kbd>CTRL</kbd>, <kbd>CLEAR/HOME</kbd>, <kbd>SHIFT</kbd> and the Function keys) on the original keyboard have their stem receptacles off-center while contemporary keycaps, on the contrary, have the receptacles centered.

There are more problems in using modern keycaps by the way: for instance, the original Commodore spacebar is 9U, while contemporary spacebars are much shorter (I think they don't go over 7U). Most modern keycaps also have different profiles for different rows (the originals are all the same) and not all sizes are available for all rows: as an example, for the Function keys you'll need 1.5U keycaps, one per row, but modern keycaps only come in 1.5U for rows 1 and 3.

Since working around all these issues requires more thought and since the Mechboard64 simply used the original Commodore placement, for the first MechBoard16 release I decided to follow suit but things might change in the future, once I'm sure all the rest is correct.

The bottom line is that **at the moment you still need to recover the keys from an original C16 keyboard**. Keys from a VIC-20 or C64 keyboard should work just as well, despite having some labeling differences (<kbd>RESTORE</kbd> is <kbd>CLEAR/HOME</kbd>, the arrow keys are missing, etc.). Some people have actually produced new C64 keys but they didn't plan alternative labeling for us C16 users and apparently those keys were even only sold through Kickstarter-style initiatives and are not on regular sale (yet?).

### Keycap Adapters
It looked easy after all, didn't it? Unfortunately, the original Commodore keycaps do not have MX-style stems, so you'll need some **adapters**. These must be 3D-printed, use the STL file provided by MechBoard64.

### Stabilizers
The wider keys (<kbd>RETURN</kbd> and <kbd>SPACE</kbd>) are too large for a single keyswitch and would *bind* (get stuck) unless hit close to the center. In order to avoid that, thin metal bars are used to attach them to the keyboard plate for the whole length. These are called **stabilizers** and again, come in different styles. Mechboard64 went for the so-called *Costar stabilizers*: these can be bought on the market and come as a kit of plastic clips that must be inserted in the slots available on the plate, a set of key inserts and some bent metal wire that goes inbetween.

Unfortunately, the original Commodore spacebar is too wide for the insert kits that are currently available commercially so, while you can use the clips and inserts, you will need to bend some metal wire with the correct proportions. MtnBuffalo used 1 mm steel wire bent with a tool named EZ Bender and I was able to buy both things at a model shop (I was told they are commonly used by model airplane enthusiasts, if that helps). The EZ Bender was about 30€ and the wire is inexpensive (buy it straight, not in a spool!).

### Cables
This is the easy part: just get a bunch of those *Dupont wires* people use for Arduino projects: you'll need 20 female-to-female, they're cheap and you can find them everywhere. You'll probably find them with individual connectors only but oh well... As for the length, 20 cm should be fine.

The above assumes that a 90-degree male pin header is soldered at CN1, but you can also solder a female header and use a male-to-female wires.

Oh, and while we're at it, CN2 on the board allows for connection of the keyboad to a Plus/4 computer: while this makes little sense, as the Plus/4 has a totally different form factor in which the keyboard cannot fit, it could still be useful for temporary use or whatever. Maybe someone will relayout the board in the proper format? ;)

### LEDs
If you want LEDs, you can solder one per each key. The required diameter is 3 mm. I'd recommend using high-brightness ones.

Remember to tune R207 according to the LEDs you choose and brightness you like.

R208, 209, 210, 211 and 212 TBD

## Mainboard Modification
TBD

Please note that I am in no way endorsed by any of the above-mentioned companies, shops or websites. I am only suggesting them for practical needs and to save you time.
