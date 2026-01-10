# Aligning Square Stock on the 4th axis with the wireless probe

{% hint style="info" %}
### If you have a 3D Probe you can instead use the [M465](../firmware/supported-commands/mcodes/probing.md#m465-probe-axis-angle) macro <a href="#figure-out-what-numbers-you-need-to-use" id="figure-out-what-numbers-you-need-to-use"></a>
{% endhint %}

### Figure out what numbers you need to use <a href="#figure-out-what-numbers-you-need-to-use" id="figure-out-what-numbers-you-need-to-use"></a>

Calculate the y axis offset for your stock by taking the width of the part in mm, dividing by 2 and then subtracting at least 3mm.\
So for a 25mm wide part you would get 25mm/2 = 12.5 ; 12.5 - 2 = 9.5mm which for simplicity I will round down to 9.\
In the future I will refer to this value as **{Y offset}** and use the example of 9mm\
\
\
\
\
&#x20;

### &#x20;Set up your origin <a href="#set-up-your-origin" id="set-up-your-origin"></a>

<figure><img src="https://wiki.makera.com/knowledge-sharing/align-stock-to4-th-axis-with--probe/4thaxisoriginsetting.png" alt=""><figcaption></figcaption></figure>

Upload the Allow4ThAxisOriginSetting.cnc file onto your machine and select it.[/knowledge-sharing/align-stock-to4-th-axis-with--probe/allow4thaxisoriginsetting.cnc](https://wiki.makera.com/knowledge-sharing/align-stock-to4-th-axis-with--probe/allow4thaxisoriginsetting.cnc)\
\
With the file open, go to the manual control tab and hit set origin. Set the origin to 4th axis origin at 0,0\
\
\
\
Switch to the probe tool with the tool dropdown and make sure it is calibrated. Make sure your machine is ready to move and leave it at the clearance height.\
\
Now you want to align your machine to the centerline of the A axis. To do this, go to the main screen and click the button in the bottom left that says MDI. This will open a terminal. In the terminal type in \
\
G90 G01 X0 Y0

\
and then hit the send button. This will move the carvera to be above the centerline of the 4th axis on X and above the headstock on Y

\
<br>

<figure><img src="https://wiki.makera.com/knowledge-sharing/align-stock-to4-th-axis-with--probe/align4thaxismoveto00.png" alt=""><figcaption></figcaption></figure>

\
\
\
Using the manual move tab, roughly align the stock in the a axis so that the top flat face is horizontal. Then move along Z and X until the probe is about 30mm over the center of the stock and clear of the chuck like in the image below. The exact distance above the stock is not important. \
&#x20;

<figure><img src="https://wiki.makera.com/knowledge-sharing/align-stock-to4-th-axis-with--probe/align4thaxisstocksetorigin2.png" alt=""><figcaption></figcaption></figure>

\
Probing Commands

Back into the MDI again type in:\
\
G90 G01 X0 Y9\
\
and hit send. This will move the probe over the first position. Change Y9 to whatever your  **{Y offset}** value was

G38.2 Z-150 F100 G4 P1

This will probe along the z axis and stop when it hits the stock. In the controller, write down the current Z position. We will call this **{Z1}** and I will use 2mm for this value\
\
&#x20;G91 G0 Z10

This will move up along the Z axis away from the stock

G90 X0 Y-9

This will move the probe over the second position. Change Y-9 to whatever your  **{Y offset}** value was with a minus sign in front of it

G38.2 Z-150 F100 G4 P1

This will probe along the z axis and stop when it hits the stock. In the controller, write down the current Z position. We will call this **{Z2}**&#x54;his will probe along the z axis and stop when it hits the stock. In the controller, write down the current Z position. For the example I will use 1mm for this value

Open a scientific calculator and do the following math.&#x20;

inverse tan( ( **{Z1}** - **{Z2} ) / (**&#x32;\* **{Y offset}** ))

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

In our example the values look like this:

&#x20;inverse tan(  (2\*9)  / (2-1) ) =  inverse tan(18) =  3.18 degrees.&#x20;

&#x20;

### &#x20;Move the A Axis and zero <a href="#move-the-a-axis-and-zero" id="move-the-a-axis-and-zero"></a>

\
Start by moving your probe to a safe location. The easiest way to do this is to use the goto - clearance command in the manual control tab.

Make sure the A axis is clear to spin and then type the following into the MDI\
\
G90 A 3.18 &#x20;

replacing 3.18 with whatever your calculated value is. This should level the A axis.

Then type in&#x20;

G10 L20 P0 A0

and hit send to zero the a axis (or use the axis dropdown A = 0)\
\
Deskproto generally starts with the stock level like this, however, if you need the stock in a different orientation you can use the manual controls or \
\
G90 A {value}

in the MDI to align it how you need for your operation and then once again zero the a axis.&#x20;
