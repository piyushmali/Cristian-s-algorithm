# Cristian-s-algorithm

Cristianʼs algorithm: The simplest algorithm for setting the time would be to simply issue a remote procedure call to a time server and obtain the time. That does not account for the network and processing delay. We can attempt to compensate for this by measuring the time (in local system time) at which the request is sent (T0) and the time at which the response is received (T1). Our best guess at the network delay in each direction is to assume that the delays to and from are symmetric (we have no reason to believe otherwise). The estimated overhead due to the network delay is then (T1- T0)/2. The new time can be set to the time returned by the server plus the time that elapsed since the server generated the timestamp: 
 
Suppose that we know the smallest time interval that it could take for a message to be sent between a client and server (either direction). Let's call this time Tmin. This is the time when the network and CPUs are completely unloaded. Knowing this value allows us to place bounds on the accuracy of the result obtained from the server. If we sent a request to the server at time T0, then the earliest time stamp that the server could generate the timestamp is T0 + Tmin. The latest time that the server could generate the timestamp is T1 - Tmin, where we assume it took only the minimum time, Tmin, to get the response. The range of these times is: T1 - T0 - 2Tmin, so the accuracy of the result is:
 
Errors are cumulative. If machine A synchronizes from a server B and gets an accuracy of ±5 msec but server B in turn got its time from server C with an accuracy of ±7 msec, the net accuracy at machine A is ±(5+7), or ±12 msec.

Several time requests may be issued consecutively in the hope that one of the requests may be delivered faster than the others (e.g., it may be submitted during a time window when network activity is minimal). This can achieve improved accuracy. 

Cristian's algorithm suffers from the problem that afflicts all single-server algorithms: the server might fail and clock synchronization will be unavailable. It is also subject to malicious interference.
