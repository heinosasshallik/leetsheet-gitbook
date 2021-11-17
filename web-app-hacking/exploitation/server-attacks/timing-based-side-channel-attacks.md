# Timing-Based Side-Channel Attacks

If a correct password/cookie/token/whatever takes longer to process than an incorrect one, then you can infer the correctness of the token based on the time it takes to get a reply from the server. For example, this can happen if the auth cookie is checked with a for-loop for whatever reason.



[Web Timing Attacks made practical](https://www.youtube.com/watch?v=KirTCSAvt9M):

* Look at data at the network layer (tcp data packets, don’t measure handshakes)
* To determine a if there’s a timing attack, send two requests at the same time - a correct one and an incorrect one. If there’s a time difference, then there’s probably a timing attack
* You can do statistics based on those request pairs. You can use a Kalman filter and L-estimators to filter out noise and get a better estimate.
* Nanown is a tool that automates this

\
[You can also put javascript on your page that makes conclusions based on the size of returned resources](https://tom.vg/2016/08/browser-based-timing-attacks/). For example a social network with users on the “light side” and “dark side”. If you make a GET request (through img tag) to socialnetwork.com/darkside and the returned resource size is large, then the request went though and he’s on the dark side. If the resource size is small, then he’s on the light side. The way you measure resource size is by the time it takes to process it client-side (after it’s been downloaded). But this can mostly just be used for making conclusions, not any real exploitation.
