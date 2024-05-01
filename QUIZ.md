### How does the DevBoard handle received serial messages? How does this differ from the naïve approach?

When a byte is sent over serial it triggeres 'on_receive' which checks if the received byte is a valid high or low LED state. If updating the LED state is a succsess, it states S_OK if not valid S_ERR. When we use the event driven commpared to the naïve approach, it only triggers the code when its necessary rather than continuosly checking the port.

### What does `detached_callback` do? What would happen if it wasn't used?

Makes the function run in a new thread rather than the main thread which allows the function to execute independently of the main GUI. This is important because long running operations make the GUI unresponsive.

### What does `LockedSerial` do? Why is it _necessary_?

In multithreaded applications like the one we have, it makes sure that access to serial ports are serialized. This is necessary particularly in GUI applications when actions might trigger serial opperations from different threads. If this does happen it will result in data conflicts/corruption.