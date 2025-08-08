# Using Ball Endmills and V bits

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

\
\
In the image above, the top two rows are the end of ball endmills, the bottom one is a vbit\
\
When working with ball endmills and vbits you are always going to leave a series of small grooves on the part. When you are machining you set your stepover to minimize this value to an acceptable amount.\
The larger the tip of the endmill, the smoother the sides of the grooves created, making them less noticeable, at the cost of losing the ability to make smaller features.\
Generally you want to use the largest size endmill that will create the features that you want as you can use larger stepovers for the same surface finish. In the example above see how the top set of circles is further apart, but the ridges are less pronounced than the middle ones.\
V bits tend to make sharper ridges more like threads as well.

the soft edges of ball endmills are also better for sloped surfaces as there is not the hard corner, it hides transitions better and is easier on the bit\
V bits are easier to make smaller sizes on, so they will be more common for very small details

For a project with a lot of 3d detail, I would use a large ball endmill to get the majority of the shape, clean up the small details with a smaller ball endmill, and finish any super sharp engraving with a v-bit if needed.

Since ball endmills do not have a flat bottom, they are less good at flat horizontal surfaces. If you want a bit that can do flat surfaces with decent finishes on sloped surfaces, bull nosed endmills have a flat bottom with radiused corners.

When using endmills with a radius, it is a good practice to rough out the part with a flat or bull nosed endmill to get a stepped approximation of the final shape, do a semi-finishing pass with the ball endmill to get an even thickness of material to remove for the finishing pass (you can use a larger stepover than you would for a finish pass as the ridges will be removed in the finish), and then finish with the smaller stepover.

It is also best practice to cut with the side of a ball endmill and not the bottom face. This is often accomplished by making the toolpath start at the bottom of a surface and move to the top

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

See in this image, if you start at the bottom and move up the surface, most of the cutting is happening on the side of the ball, whereas if you started from the top and moved down you would always be cutting with the center
