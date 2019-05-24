# w251_hw3

Thomas Drage <draget@berkeley.edu>

Cloud storage output:

http://s3.au-syd.cloud-object-storage.appdomain.cloud/hw3draget

- detect.py - Run in Ubuntu container on TX2
- forward.py - Run in Alpine container on TX2
- sav.py - Run in Ubuntu container on cloud VM

In addition an Alpine container with MQTT broker (Mosquitto) was present on both TX2 and cloud VM (host name "mosquitto" on a Docker bridge network). On the cloud VM, 1883 from the VM is mapped to the container to accept incoming connections.

The topic "faces" was used throughout for this prototype - a more fully defined topic name could be used if there was more than one data stream in some hierarchy. QoS was set to 0 - this means that delivery is not guaranteed. In this case a lot of frames are generated, the completeness is not guaranteed anyway (due to classifier performance) and there is no use-case requiring reliability yet, so this simple method is used. If it was critical not to miss any frames, QoS of 1 could be used.

Some next steps for this project would include authentication to the cloud broker and verification that the received payloads do indeed contain PNG images (and not a virus!) and are from a reputable source prior to saving to object storage.
