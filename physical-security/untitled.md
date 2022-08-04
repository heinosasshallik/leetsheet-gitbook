# Mechanical Locks

## Lock picking <a href="#docs-internal-guid-6f52c207-7fff-7a95-e934-77aa286e0311" id="docs-internal-guid-6f52c207-7fff-7a95-e934-77aa286e0311"></a>

[This PDF](https://www.lysator.liu.se/mit-guide/MITLockGuide.pdf) seems detailed but I found it after I’d learned the basics.

Tensioning by LockpickingLawyer:&#x20;

{% embed url="https://www.youtube.com/watch?v=9O-CJEwcQnY" %}
Tensioning guide
{% endembed %}



High security lock picking:

* CaptainHookNumber1 on Youtube for picking european high security locks
* [This PDF](https://www.docdroid.net/nmZckmS/high-security-lockpicking.pdf) gives a good overview

**Swapping pick directions**

If you’ve picked the lock the wrong way (or it’s more difficult to pick the lock the right way than the wrong way), then you can use a plug spinner tool to spin the plug the right way after it’s been picked.

## Combination locks

Always apply pressure to the shackle.

_Note: This information applies to the combination lock I own. I haven’t been able to test it out on other combination locks yet_

A dial is correct when it turns freely even with extreme pressure from the shackle. It should turn pretty much exactly from one dividing line to another (on the combination wheel). If it turns more or less than that, then it’s probably not right. If you think you’ve found the right one, then you can try all the other numbers as well, since it might be a false gate (but a false gate means you’re close)

At first, all the dials turn freely. Except, when you rotate them 360 degrees, then there’s probably one spot that’s more difficult to turn than the rest. That’s the worst spot for the dial to be in, so you should turn the dial to where it moves the easiest. You might get a few dials pretty close (or even correct) right off the bat this way.

Now that a few dials are about right, the dials will start moving more rigidly. If a dial turns relatively freely (up until a point, where it gets blocked solidly), then that means it’s either in the right position, or in a false gate. If the dial turns very rigidly, then it’s in the wrong position. Try to get the dials to turn freely and brute-force your way out of the false gates. One way to detect false gates: If one dial moves pretty freely, but moving another dial still moves that first dial, then it might be in a false gate.

Another way to start is by setting them all to zero and moving them all by one until you find one that seems right. Then keep moving the rest. If for example you’re turning one wheel and at a point, all the dials start turning freely, then you’ve gone wrong (a dial that you thought was correct, is in fact not correct). Go back and try the other dials again.\


## **Safe-type combination padlocks**

{% embed url="https://www.youtube.com/watch?v=Fah-LJJaPWg" %}

The logic is pretty much exactly the same as for the normal combination locks. Except you need to apply as much pressure as possible. Then, when you move it to the correct gate, then you’ll feel a slight click/movement as it drops into the gate. When you start to move it out of the gate, then the resistance and the click will be much greater.

_Note: I haven't been able to pick a single safe-type combination padlock yet._

## Master keying privilege escalation

Deviant’s talks:

* [https://www.youtube.com/watch?v=aVPSaKLKHd4](https://www.youtube.com/watch?v=aVPSaKLKHd4)
* [https://www.youtube.com/watch?v=DKcL6zYZoRU](https://www.youtube.com/watch?v=DKcL6zYZoRU\&t=139s)
* [https://www.youtube.com/watch?v=NT7167wQtvk](https://www.youtube.com/watch?v=NT7167wQtvk)

## Key impressioning

### **Judging by scrape marks on the key**

{% embed url="https://www.youtube.com/watch?v=p0euhqTq_9o" %}

You don’t need the specific tool used in that video. What you can do is jiggle the key on the lock every day, inspecting the results and filing the key down each time according to the scratch marks. It might take a few weeks, but you’ll have a functioning key by the end of it, if you do it right.

### **Using photography**

{% embed url="https://www.youtube.com/watch?v=vxJ3Kovz-bo" %}

{% embed url="https://www.youtube.com/watch?v=AayXf5aRFTI" %}

The depth of a key is standard. You can use calipers to measure the depth and get the key bitting that way. Or, slightly sneakier - you can take a photo. Here are gridlines for common keys that will help you determine the bitting (use photoshop to get the angle and size right)

{% embed url="https://github.com/deviantollam/decoding" %}

The gridlines are under “Key Decoding”

And btw - some keys have the bitting written on the key itself (direct bitting code). If you see a number on your key, then that might be the bitting. Higher numbers usually mean deeper bitting, so you can easily verify this.

However, some locks have a “blind” code on the packaging  the key The manufacturer has a lookup table for that code. You may or may not have access to it (for example, for Masterlock there are resources online for it). If not, then if you see a thrown out lock packaging with a blind code, then you can just go to your local hardware store, find the same lock with the same blind code, and check what bitting it has.

Combination dial locks may have them written on the back as well.

There’s also locksmithing software for this, like InstaCode

## Overlifting attack

Common for wafer locks.

If you insert a blank key (or, for example, a popsicle stick) into a wafer lock, then it will overlift the wafers, forcing them to block on the opposite side they’re normally blocking at (therefore having the spring push them back into the original position). Therefore, if you keep rotational energy while slowly pulling the blank key back out, then the wafers will go from the opposite side into the middle, but will get stuck in the middle before they can get back into the original position. Therefore, when you’ve pulled the blank key out (keeping rotational energy), then all the wafers will be in the correct position, and you can open the lock.

This also occurs in cheaper pin-tumbler locks, and it’s commonly exploited using a comb rake.&#x20;

![](https://lh4.googleusercontent.com/E6o573JOehvCDOs2Y-AnOSbIHyzt7CaclkOcWYv7obHLeg8AOdgJUjeLwhAfEkhAMtaXrwbtFafpiKRt75wbQ4HWf-JHTONxe2io9Okjlfn2AgjYUWHeErfLHIUxd56BC7UtOzGx48PVwVToO7cptQ)

\


## Self-impressioning attack

Common for tubular locks.

When all the driver pins and springs are the same length, then if you push onto all the key pins with equal force, then all the driver pins will be at the same distance from the shear line. Therefore, since all the driver pins need to be at the shear line for the lock to open, and all the driver pins move to the same position when you apply x force onto all the key pins, it’s not very difficult to open the lock this way.

Essentially, if you push something soft into all the key pins, you’re automatically impressioning the lock. This is how the tubular lock impressioning tools work. Additionally, this is why you can open many tubular locks by shoving something soft into it (most famously, a soft bic pen)

If the springs are of different materials or have different lengths or the driver pins have different lengths, then it doesn’t work.

## Handcuff escaping

_Note: This does not work if the officer engages the double locking mechanism on the handcuffs._

If you can slide a thin piece of metal (like part of a beer can) between the teeth of the handcuffs (you will have to tighten it by one notch for it to slide in between) then the teeth will no longer be locker together and you can just pull it apart. Btw if the metal is too thin and the teeth are biting strong enough, then it will crimp the metal and it will get stuck. So thicker is better.

## Direct Locking Lug/Cam Attack

### **Padlocks**

If the locking lug of a padlock is not protected, then a lockpicking knife (or other object of a suitable shape) can be inserted into the lock and the locking lug can be unlocked without having to turn the key.&#x20;

&#x20;

![knife tool, which can be used to pry the locking lug](https://lh6.googleusercontent.com/H\_9mInP6LkA8C4bGfaPP4e08Mpjgf0K5vpVbeEjWxrYQHW0z2wzlSlFAEBmPlaltG2jNi4JXFNSNfnNpHP5wDfo0WzGE\_5eTQMUa\_XDciVmWA8gxwzvKj3fiAXGw3cBhOYyW0d94tbEE5yNkT5k9MA)

![Driver bypass tool](https://lh4.googleusercontent.com/aTdhAYASrClMMH97gRtKStT1fGTE9odL24bNmp627241owVIWoH6g3iVEJf-EwIYYLhL86HS2GfOQHtDSbp6wnkDEgPductFep4YHTnIEfPStohITFMmLm6LPN3FHrQrMRAqyQpu2ctcHulnj4BLzg)

The above driver bypass tool was used by lockpickinglawyer used to turn the locking lug:&#x20;

{% embed url="https://youtu.be/kJ1_P5oqf6Y" %}

Below: Adams Rite bypass tool, which can be used to directly manipulate the lock cam on some locks.

\


![](https://lh6.googleusercontent.com/hjEH\_8eXXh9kgOZgBbyvNBNKSQYAHXizGOhS8gk1dfNtKLHTZL-605s9S2T-RhN\_uRzfsj5MUZIOByFnnxRYVd2ep6VHtMiuKIxV2PSCl12aqiSvpcSi-3tsCo1PRk0\_WU0XPzAuosPu1hwGjGTivg)

\


**Combination locks**

A thin shim can go through the dial hole and operate the unlocking mechanism directly

[https://youtu.be/4YYvBLAF4T8?t=2210](https://youtu.be/4YYvBLAF4T8?t=2210)

\


**Shimming**

If a shim can be inserted between the shackle and the locking bar, then nothing is keeping the shackle closed anymore. Also works for handcuffs.

\
\


#### Latch Slipping Attacks

[https://www.go-rbcs.com/articles/the-deadlocking-plunger-weakness](https://www.go-rbcs.com/articles/the-deadlocking-plunger-weakness)

\


Doesn’t work for locks, where the deadbolt doesn’t move unless the key is turned. It works for locks, where the deadbolt can retract. The purpose of a deadlocking plunger is to prevent this type of attack, but if the strike plate is improperly installed, and the plunger is not depressed, then the vulnerability remains.

\


Latches can be slipped with credit cards, traveler hooks (aka shrum tool), piano wire, etc.

\
\


You can also try to use an air wedge to try to offset and disable a deadlatch

![](https://lh5.googleusercontent.com/se33ycNbQ-ci6y7tddiiCgoT2kDEXwQFHjyH7HQnBItXyEhL0URXMtTS1pQpKJrrFym-MU3Phd8md-jo2bTrADzJMswP18-T5d4MmqRTN5MndIvhcy9f543b1X7t5G-0mlVK2zAaBWB9UJ3-e5\_oJg)
