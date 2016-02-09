# deskbot: How to add presets and automations to your BuzzFeed SF standing desk

The code in this repo is drawn from TJ Hunter's very great [photon-desk repo](https://github.com/Hypnopompia/photon-desk) which tells you how to convert your [V3 GeekDesk](http://www.geekdesk.com/geekdesk-v3-frame-only) into a desk with pre-sets. He even has [nifty controllers you can order](https://www.tindie.com/products/TJ_Hunter/photon-geekdesk-controller/) but this one just uses a [Photon](https://docs.particle.io/datasheets/photon-datasheet/) and [Photon Relay Shield](https://docs.particle.io/datasheets/photon-shields/#relay-shield) that you can buy from [the Particle store](http://store.particle.io). We're also going to show you how to use IFTTT to hook your desk pre-sets up to your phone.

You will need:

**Hardware**
- Photon
- Photon Relay Shield
- Ultrasonic ping sesnor, like [this one](http://www.amazon.com/SainSmart-HC-SR04-Ranging-Detector-Distance/dp/B004U8TOE6/ref=sr_1_1?ie=UTF8&qid=1455050855&sr=8-1&keywords=hc+sro4)
- 4 Male-to-Female jumper wires
- USB-to-micro-USB cable, preferably pretty long
- Outlet USB brick (optional)
- 3D printed case for the deskbot
- Long screws (like 3 inches)
- Your standing desk

**Software**
- A [Particle Build](http://build.particle.io) account
- An [IFTTT](https://ifttt.com) account
- The [IFTTT "Do" app](https://ifttt.com/products/do/button)
- A Google account with Google Calendar

## Step 1: Start Printing This Thing

First, print the 3D case for the deskbot. The `.stl` file is in this repo. We used a MakerBot M2 with PLA filament.

## Step 2: Claim Your Photon

You're going to need to unbox your Particle Photon and claim it to the Particle Build account you made. Info on how to do that is [here](https://docs.particle.io/guide/getting-started/start/photon/#connect-your-photon).

## Step 3: Add Code

Copy the text of deskbot.ino into a new app called "deskbot" in Particle Build. Then go to the libraries button (bookmark in the lower left corner) and add the RelayShield library to the deskbot app. This will automatically add a new line of code at the top of your file-- that's good! Save your app, make sure your Photon is plugged in and online, and hit the lightning bolt to flash the code to your Photon. The RGB LED will be purple for a little while (especially if it is the first time you're flashing code to this device), and then it will flash green, then cyan again.

## Step 4: Assembly

Is your case done printing? Good! Time for assembly.

(NOTE: Depending on the width of your screws, you might need to widen the holes on the Relay Shield using a drill press. If you work at BuzzFeed SF, ask one of the OpenLab Fellows for help with this.)

Reference the awesome post we have on this to see how to put it all together. Basically, you line up the first two relays with the holes. Make sure you unplug your desk (that's super important) before plugging anything from your desk into the relay shield. The order is roughly:

1) Plug the Photon into the Relay Shield, being careful to line up the Photon with the outline on the shield.

2) Use the jumper wires to connect the ping sensor to the headers on either side of the Photon. You should connect:

`Vcc` to `VIN`

`Trig` to `D1`

`Echo` to `D2`

`Gnd` to `GND`

I looped the wires underneath the Photon to make it a bit cleaner. You can do this if you want, or just squish them into the box later.

3) Plug in the micro-USB cable to the micro-USB port on your Photon.

4) UNPLUG YOUR DESK FROM THE WALL. I cannot stress this enough.

5) Unscrew the black controller from your desk and open it up. You'll see a particular arrangement of wires in there. This is sort of a crazy arrangement, just take my word for it and wire it like this:

Yellow wire: Connects NO of Relay 1 to NO of Relay 2

Blue wire: Connects NC of Relay 1 to NC of Relay 2

Ground sides of the black wire: One on either side of the blue wire (NC and NC)

Power sides of the black wire: One on either side of the yellow wire (NO and NO)

6) Flip the whole relay over and put it in the bottom part of the deskbot case. You can wrap the ping sensor around the back of the relay shield so that it is technically above the shield, facing downward into the two large holes exposing its sensors. Center the wires in the exit tracts cut in front of relays 1 and 2 and close the box.

## Step 5: Turn it on and test it!
Set the box on your desk with the ping sensor facing down and pointing towards the ground, off the edge of your desk. This is how your deskbot "sees," so make sure there isn't anything obscuring its view of the floor.

Plug the USB cable into your power brick or into your computer. This will turn on your deskbot.
If you have the Particle CLI, you can test this quickly by using the command `particle call [NAME OF YOUR DEVICE] set 90` to make it raise up to about 90 cm.

I guess if you don't have the CLI, wellllll.... if I really loved you I'd have some code here you could use to test it. But I don't love you that much, so just make an IFTTT account and see if you can get it working that way.

## Step 6: Making an IFTTT DO recipe

Follow the steps on the IFTTT DO app to create a recipe for Particle. You'll need to authenticate your Particle account with the same email and password you used for Particle Build. Once this is done, tell IFTTT you want it to use your recipe to call a function. The fuction is "set" and the data the desired height of your desk in centimeters. Mine is 65 for sitting and 95 for standing. You can adjust yours as necessary. Make one recipe for sitting and one for standing. When you press the button, your desk should go to the desired height!

## Step 7: Google Calendar

Create a Google Calendar called "deskbot" or "standing desk" or something. It doesn't matter, as long as you can recognize it. Go into your IFTTT account through the web interface and create a recipe with Google Calendar as the trigger. What I like to do here is hook up the deskbot calendar to IFTTT and have it trigger the Particle function "set" with data "95" when it encounters an event with the word "up" in it. Similarly, it triggers "set" with the data "65" when it encounters an event with the word "down." Now you can schedule the ups and downs of your desk!

## Step 8: Attach to Desk

Screw the box into your desk, with the ping sensor facing down. Make sure that the ping sensor isn't pointing at anything. Enjoy.
