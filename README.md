# nifi-iot-demo

# Flow

NiFi on Mac --> MiNiFi on RPi --> LED + Other devices etc. 

Operations 
- NiFI polls MiNiFi to check on the status of LED and other devices
- MiNiFi runs those commands and sends the info back to NiFi 
- NiFi stores the info in HBase, which is queried by Ambari to show the current status of LED and other device. 
- NiFi also exposes an API that can be used by Ambari Views. The API will send DNP message to MiNiFi to take action on LED and change its status.
