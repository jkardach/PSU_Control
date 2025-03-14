## PSU_Control
This macOS program is used to control two KIMRIM DC310pro combination power 
supply/meters. It uses SCPI commands over the USB/Serial interface, and so 
should work on other combination power supply/meters (like the OWON SPM Series.

These power supplies/meters are very cheap ($140 on Amazon). The OWON SPM6103 is
slightly more expensive ($161), but might be a better choice. They appear to be the
same hardware design, but different firmware. The KIPRIM folks seem to think limits
should be set to 10% lower than the programmed value (if your current limit is set
to 1A, then the over protection trips at 0.9A, the support person explains that you
never want to hit the limit, so they put a buffer in. Having said that, KIPRIM
support is very good in that they fixed some bugs at my request (didn't ask to
fix the limit issues, I just won't use limits).

I have not used the OWN PSU, but might purchase one just to see if the firware 
and operation make sense.

I mainly used the example program that is provided by SerialGate, but modified the 
swiftUI to support additional commands and multiple serial interfaces (intend to 
have three eventually). I highly recommend the SerialGate library, only complaint
the documentation is not great, but that seems to be a very common issue.

The disable for the ports button is commented out as it gives an error (Swift bug), 
hopefully it can be uncommented someday.
I did add an additional view that is basically the layout of the serial ports, but 
allows the serial ports to be extended to two (or three) extreamly easily by making 
another instance of vModel.

Also modified the vModel to allow the textField to activate with a CR (don't have
to use the send button). and added some generic commands in the sendPort method.

The example had all of the serial reads into a group task, but I changed this
because the power supply needs to associate a response with a command. You can't
really distinguish the responses as many of them just return a number (current, 
voltage, ...) so I send a command, then then get the response).
