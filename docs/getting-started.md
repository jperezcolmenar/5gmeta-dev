# Requirements for interfacing your application

# Software requirements

* Ubuntu, preferrably 20.04
* python3


# Registering into the application

First step to start using 5GMETA platform will be registering on it.

Please go to [Registration web page](https://5gmeta-platform.eu/identity/realms/5gmeta/protocol/openid-connect/auth?client_id=account-console&redirect_uri=https%3A%2F%2F5gmeta-platform.eu%2Fidentity%2Frealms%2F5gmeta%2Faccount%2F%23%2F&state=e663b644-ad9e-4099-8ef5-a01f0b96113b&response_mode=fragment&response_type=code&scope=openid&nonce=8fe4af95-2960-4091-8291-f0b938ecb71b&code_challenge=q1YJn1i-HV4Bk695CxlzYXIrLedunlS7TBafxCULGCQ&code_challenge_method=S256) and fill the form with the data.


Once you have registered you will be able to access the platform and start consuming data. Next you will be guided with some instructions to get that purpouse.

# Extra packages to be installed
First of all, you will need to install some dependencies (apt-get):

* python3-avro
* python3-confluent-kafka
* gstreamer1.0-plugins-bad (only if you are going to consume video)
* gstreamer1.0-libav (only if you are going to consume video)
* python3-gst-1.0 (only if you are going to consume video)

Also install with pip3:

* kafka-python
* numpy
* python-qpid-proton

Also find easy installation for all the required packages(Be careful of your environment compatibility):

* ```pip3 install -r examples/requirements.txt```

