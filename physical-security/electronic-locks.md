# Electronic Locks

## Door Contact Sensors <a href="#docs-internal-guid-cd7371e0-7fff-8786-f4dd-1743a887c310" id="docs-internal-guid-cd7371e0-7fff-8786-f4dd-1743a887c310"></a>

{% embed url="https://youtu.be/LS5OQHUJaJE?t=3102" %}
Timestamped explanation
{% endembed %}

Door contact sensors are sensors which detect if a door is open or not. Let’s say there’s a reader on one side and a request-to-exit (REX) sensor on the other. If neither the reader or the sensor are triggered, then the sensor assumes a forced entry and triggers an alarm.&#x20;

So one thing you could do is trigger the REX sensor with a can of compressed air so that the sensor doesn’t go off, and then slip the latch using a traveler hook or slim jim.

To find contact sensors, you can use a magnet on a stick.

{% embed url="https://youtu.be/LS5OQHUJaJE?t=3211" %}
Timestamped demo about finding contact sensors
{% endembed %}

It’s also possible to bypass these with a magnet&#x20;

{% embed url="https://youtu.be/LS5OQHUJaJE?t=3265" %}
Timestamped demo on door contact bypassing
{% endembed %}

## Snooping credentials

[https://www.redteamtools.com/support/ESPKey%20Tool%20Manual%20v1.0.0.pdf](https://www.redteamtools.com/support/ESPKey%20Tool%20Manual%20v1.0.0.pdf)

An ESPKey can be installed on an RFID reader, which uses the Wiegand protocol (most commonly used protocol) to snoop credentials.

### Prevention

Use a secure protocol like OSDPv2.&#x20;

Also, readers can have tamper sensors, which are supposed to detect if a reader is dismounted from the wall. However, these aren’t commonly installed. The tamper sensors can be either a physical switch or a light sensor.

## Credential Cloning

RFID cards can be cloned, for example using a long-range card reader. Low-frequency cards are extremely easy to clone, but high-frequency cards protect the credentials with a secret, and there’s a handshake between the reader and the card to unlock the credentials.&#x20;

One thing you can try is to find out the secret to decrypt the credentials, somehow. Or, if you have snooped wiegand credentials from a reader, and if readers support both high-frequency and low-frequency cards, then you can clone the credentials onto a low-frequency card.

Note that the extremely popular HID iClass cards have a **known** master encryption key, which makes them easy to clone. The huntpad that is used by DeviantOllam and Babak Javadi is [set up to clone these types of cards](https://youtu.be/Qt2Gn2CoJ74?t=225).

## Bypassing electronic locks

### **Battery**

You can just drill into the lock, connect a 9V battery to the solenoid, then the lock should open.

### **Magnet**&#x20;

There are some locks that open if you put a magnet next to them. &#x20;

{% embed url="https://www.youtube.com/watch?v=58MiE_mUDBA" %}

DeviantOllam carries around magnets and also a tool which shows the direction of a magnetic field (magnetic search pole), indicating where the magnet should be placed:\


{% embed url="https://youtu.be/TjyXwgSzs6k?t=280" %}

### **Removing power**

Magnetic locks need power to keep the doors closed. If the power goes out, then the magnetic lock doesn’t work anymore. You might be able to disassemble to junction box for the magnetic lock and simply remove the power.

## Request to Exit Sensor attack

If there’s a sensor which opens the door when someone’s on the other side, then you can get a can of compressed air, turn it the other way around and spray the liquid through an opening in the door. If the sensor is a sensitive enough motion-detecting or heat change detecting sensor, then the door will open.&#x20;

If the sensor is more advanced and **detects thermal**, then if you can try to get a hand warmer on a piece of wire through, then it might open

{% embed url="https://youtu.be/_4jmnun4pTU?t=2569" %}
Timestamped
{% endembed %}

Though actually, babak said that the request to exit sensors are commonly PIR (passive infrared sensors), which detect changes in heat. The compressed air method only works because they’re set to be extremely sensitive to changes so users don’t run into the door.

{% embed url="https://youtu.be/LS5OQHUJaJE?t=689" %}
Timestamped
{% endembed %}

In fact, you can just vape or spray liquid from your mouth through a gap at the sensor, and it might open.

There are better sensors which aren’t susceptible to this, though. RCR (range controlled radar) sensors detect a change in distance, and they’re usually dual sensors, both infrared and microwave, so you need to activate both in order for it to fire. But passive infrared is the most common.

## Keypad PIN code theft

If there’s a keypad with a PIN code, then it would be useful if you could find out someone’s pin code

### **Button Press Traces**

If you put some sort of substance on the keypad (like a powder that glows under UV light), then when someone presses the buttons, they’ll leave a mark on the powder. You can later examine the marks to find out the numbers they pressed (though not the exact combination).

Alternatively, you can just film the keypad with an infrared camera, and the pressed buttons should be a different color due to the heat of the finger that pressed them.

### **Video**

If you set up a video camera, then you might be able to make out the exact numbers from the video. If not, you might still see the motion of the hand and figure out the rough positions of the numbers. This method can be combined with another method, like button press traces.
