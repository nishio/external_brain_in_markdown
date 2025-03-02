
`Error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:5000 -> 0.0.0.0:0: listen tcp 0.0.0.0:5000: bind: address already in use`

:

```
% lsof -i :5000
COMMAND   PID   USER   FD   TYPE            DEVICE SIZE/OFF NODE NAME
ControlCe 646 nishio   19u  IPv4 0xd262a94b56389b9      0t0  TCP *:commplex-main (LISTEN)
ControlCe 646 nishio   20u  IPv6 0xd262a94b562b041      0t0  TCP *:commplex-main (LISTEN)
```

[[lsof]]

:

```
% ps -ax | grep 646
  646 ??        27:10.74 /System/Library/CoreServices/ControlCenter.app/Contents/MacOS/ControlCenter
```


[Why is Control Center on Monterey … | Apple Developer Forums](https://developer.apple.com/forums/thread/682332)
> Why is Control Center on Monterey listening to port 5000 and port 7000? I have used these ports for years for local development, but now find them in use by Control Center. Is this worth filling a Feedback about?

> This is apparently due to the new AirPlay functionality. Control Center stops listening to those ports when I turn off “AirPlay Receiver” in the “Sharing” System Preference:

