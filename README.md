# Project Name

Raspberry Pi as leaf node connects to edge translate gateway.

## Getting Started

### Prerequisites

(ideally very short, if any)

- OS
- Library version
- ...

### Installation

(ideally very short)

- npm install [package name]
- mvn install
- ...

### Quickstart
Pick a devbox or laptop or lattepanda as edge gateway, any device that could run docker, start edge runtime works 
Make sure that your gateway and leaf node connect to the same network 
Generate all necessary certs in gateway following this document https://docs.microsoft.com/en-us/azure/iot-edge/how-to-create-transparent-gateway  
Briefly in windows powershell:  
 
git clone https://github.com/azure/azure-iot-sdk-c 
 
cd azure-iot-sdk-c\tools\CACertificates 
 
powershell in admin mode: . ./ca-certs.ps1 
 
Test-CACertsPrerequisites 
 
New-CACertsCertChain 
 
New-CACertsEdgeDevice myGateway 
 
Go to Azure portal Azure IoT Hub and navigate to Certificates. Add a new certificate, providing the root CA file when prompted (RootCA.pem  for powershell, ./certs/azure-iot-test-only.root.ca.cert.pem in Bash) 
 
Generate .crt from pem and install it to Raspberry Pi 
commands: 
openssl x509 -in RootCA.pem -inform PEM -out RootCA.crt 
 
sudo cp RootCA.crt /use/local/share/ca-certificates/RootCA.crt 
 
sudo update-ca-certificates 
 
Follow this document to setup you Raspberry PI 
Follow the steps to git clone the python sample from https://github.com/azure-samples/iot-hub-python-raspberrypi-client-app 
Follow the instructions to run setup.sh to get python sdk to work since python sdk has issues with RaspBian https://github.com/Azure/azure-iot-sdk-python/issues/81 
 
Run the app.py with connectionstring appended with GatewayHostName 
e.g.  
HostName=qisun-iothub.azure-devices.net;DeviceId=pi;SharedAccessKey=XXXXX;GatewayHostName=<gateway machine name> 
Verify the gateway receives the messages with dockers log –f edgeHub 
Verify messages goes to iothub 
 
 

## Demo

A demo app is included to show how to use the project.

To run the demo, follow these steps:

(Add steps to start up the demo)

1.
2.
3.

## Resources

(Any additional resources or related projects)

- Link to supporting information
- Link to similar sample
- ...
