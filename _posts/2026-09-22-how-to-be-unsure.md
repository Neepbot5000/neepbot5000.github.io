---
layout: post
title: How to be unsure
date: 2026-09-22 13:18 +0100
tags: [physics, guide]
category: physics
---
Not in life, but in A-Level Physics.  

Uncertainties are probably the worst taught topic in the A-Level specification. There are a few reasons for this. First, it's already something that is taught at the GCSE level, and there's only a little that needs to be learned at A-Level - so some teachers just don't teach it - at least not properly. Factor this with that the actual maths with calculating uncertainties is really easy, and that it is often classed under practical and mathematical skills rather than actual content - many people just skip or gloss over it.  

### So what do you need to know?

There are **three** parts to it. If you have collected (or are given) data, you can calculate the uncertainty (spread) of the values. This is what is traditionally part of the GCSE specification.  
You can also calculate the uncertainty from a single point of data using the *resolution of your equipment*.  
However, if you *combine* two numbers with uncertainties (like in a formula), your result will have a *combined* formula, derived from the uncertainties in the numbers you used. Here's what I mean:  

> I want to calculate the resistance of a component in a circuit.
> Using an ammeter, I have calculated A = 3.00 ± 0.01 A 
> ...and V = 12.0 ± 0.05 V.
> Using V = IR, we can calculate the resistance to be about 4 Ω ± *Some uncertainty*

What is that uncertainty?

## But first, this is really important

Accuracy is how close the *average value* is to the **true value**.
Precision is how close your values are **to each other**.

#### (But that's not the important part)

It is important that you know the difference between absolute, fractional and percentage uncertainty.

**Absolute uncertainty** is probably what you are used to. It just means that the *uncertainty is independant from the value*. What does this mean?  
Let's go back to our previous example - `3.00 ± 0.01 A`. This means that the value lies somewhere between `2.99 A` and `3.01 A`.  
However, uncertainties are not always written this way.

**Fractional uncertainty** is where the uncertainty is expressed as a *fraction of the value*, and is sometimes expressed as a fraction.  
In the previous example, `± 0.01 A` could mean the true value could be up to 0.01 A above or 0.01 A below the states value. However, in fractional uncertainty, `± 1/100 A` means that the true value could be up to 1/100 bigger or smaller than the stated value. In this case, it could be up to `3.03 A`, or as low as `2.97 A`, as `3 * 1/100 = 0.03`.  

So what is **percentage uncertainty** then? It sounds like another type of uncertanty, but it is literally just the fractional uncertainty expressed as a percentage - essentially, the fractional uncertainty *divided by 100*.  

Don't get mixed up between them!

# Working out an uncertainty from a set of values

This is really easy. All you have to do is calculate the range of your data (high - low), and half this. This will be your uncertainty.   
Additionally, calculate the mean of your data. This will be your value.  

That's it! You should get something like `3.00 ± 0.01 A`.

# Working out the uncertainty from the resolution of the equipment

Mathmatically this is simple, but it's not the easiest thing to wrap your head around.  
You'll first need to know the resolution of the equipment you worked with. The resoultion of a piece of apparatus will be **the smallest quantity that will result in a perceptable change in the reading.** For an ammeter with two decimal points, this would be `0.01 A`. For a standard 30cm ruler, this would be `1 mm`, because that's the distance between the graduation lines.

![That's a ruler](https://bam.files.bbci.co.uk/bam/live/content/zqrdfcw/small)

*Here you can see the difference in resolution between each ruler.*  

Once you have your resolution, it might be tempting to just calculate the uncertainty by dividing the resolution by 2. And while you would be on the right track... **not so fast!** Because there is another thing you need to factor in...  

>Is the data you have just recieved from a *reading* or a *measurement*?  

This is really important, and while you might think they are both verbs for "reading something off an instrument", there is a key difference.  
#### Readings
A *reading* is when you record the length/weight/mass/etc *once*. A common example of this is reading off a digital instrument, like this ammeter.
![Your typical school ammeter.](https://ravencourtclocks.com/cdn/shop/files/story-sons-satz-digital-school-ammeter-38281913106602.jpg?v=1728289126)  
to calculate the uncertainty, divide the resolution by 2. In this case, `5.00 ± 0.005 A`.

#### Measurements
A meaurement is when you record the length/weight/mass/etc *twice*. You might think of never doing this, but whenever you record the length of an object on a ruler, you do this.  

 ![These Rubik's cubes are very small.](https://3dprintingindustry.com/wp-content/uploads/2015/02/worlds-smallest-rubiks-cube-3D-printed.jpg)

If we want to measure the length of the 2x2 Rubik's cube in the middle, we have to record the *start point* and the *end point* - because that minature definately isn't 5 cm!  

> "But what if I just place the object at zero (cm)?"  

You are still recording twice. The object is not *exactly* at 0 cm, you have just placed it according to the gradulation lines.  

Whenever you take a measurement, your uncertainty will be ± *resolution*. Do not divide by 2.

# Combining Uncertainties

Before reading this, make sure you know about absolute, fractional and percentage uncertainties - if you don't, scroll up.  

There are a few basic rules to follow:
1. When adding or subtracting data, add the *absolute uncertainties*.
2. When multiplying or dividing data, add the *fractional uncertainties*.
3. When raising to a power (squaring *and* square-rooting), multiply the *fractional uncertainties* by the power.

> Even when subtracting or dividing data, you *never* subtract or divide your uncertainties. You should add or multiply them.
{: .prompt-warning}

Remember that fractional and percentage uncertainties are essentially the same thing. So, if you wanted to, you can always use the percentage uncertainties instead of the fractional uncertanties.

## Let's use our example from earlier
> I want to calculate the resistance of a component in a circuit.
> Using an ammeter, I have calculated A = 3.00 ± 0.01 A 
> ...and V = 12.0 ± 0.05 V.
> Using V = IR, we can calculate the resistance to be about 4 Ω ± *Some uncertainty*  

We can calculate resistance using `V = IR` -> `R = V/I`. We are combining our uncertainties.  
> When multiplying or dividing data, add the *fractional uncertainties*.  

So we would *add* the voltage and ampere uncertainties. But before we do that, we need to convert them into *fractional uncertainties* - they're currently *absolute uncertainties*. 

`V = 12.0 ± 1/240`  
`A = 3.00 ± 1/300`  
Now we just need to add those fractions - giving us `R = 3/400`. But this is still a fractional uncertainty. We can convert by multiplying that fraction with our answer (4 Ω):  
`4 * 3/400 = 0.03` - that's our uncertainty, giving `4 ± 0.03 Ω` as the final ansewr.