# webrtc tryout

## Projects for tryouts

### janus (https://github.com/meetecho/janus-gateway)

1. Not so hard to deploy, but there's some problems with docker
2. Existing html webpage & restful JSON API

    # Create A transaction Room
    POST http://172.3.100.102:8088/janus 
        {"janus":"create","transaction":"gaxirHKaEnI7"}
    
    # Get transaction detail / check the status of this video room Change the transaction into videoroom / multi camera
    GET http://172.3.100.102:8088/janus/{transaction_id}?maxev=10

    # Change the transaction into videoroom / multi camera
    POST http://172.3.100.102:8088/janus/6963204288983649
        {"janus":"attach","plugin":"janus.plugin.videoroom","opaque_id":"videoroomtest-c8u5m0B6msmR","transaction":"gaxirHKaEnI7"}

    # Join the video group
    POST http://172.3.100.102:8088/janus/6963204288983649/7273951142925917
        {"janus":"message","body":{"request":"join","room":1234,"ptype":"publisher","display":"123"},"transaction":"gaxirHKaEnI7"}

3. This system is using http keep-alive to make sure that server could notice client immediately that some one is disconnect
4. It could maintain 6 clients, keep-alive
5. Must via https on Chrome, Mobile(safari) not support VP8 publisher

--- Question ---
1. How to push video by C++/Golang/Python or Docker?
2. How to maintain the session/cookie
3. Could it be secure by hashing the room number?


###  alfalfa (https://github.com/excamera/alfalfa)

1. hard to secondary development, it's code by C/C++
2. 1 sender, 1 receiver, 1 port
3. currently I could just get videos without colors
4. not so clear where it change the transaction layer(as it said in their website: Video is better when the codec and transport work together.)
5. it seems it could not reconnect after the program crashed
6. it could only use its own FramePlayer (on ubuntu desktop)
7. it's hard to deploy
8. it has own encoder/decoder, maybe it's much more fast then normal webRTC by browser
9. the sender could be called by python or other higher programing language and maintaince by supervisord, but we should turn on several processes

--- Question ---
1. It seems hard to fix bugs (even though I fix one, thanks for google)
2. because it's connect by process, if our binary is safe enough, may be we can secure it by some hash code (because it realize decoder, not normal webRTC)
