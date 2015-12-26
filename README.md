# RTNiFiStreamProcessors - GetMQTTSensorProcessor and GetMQTTVideoProcessor for Apache NiFi

### Introduction

These two processors can be used to capture MQTT streams generated by RTMQTT (https://github.com/richards-tech/RTMQTT). Sensor data is pushed into a flowfile by GetMQTTSensorProcessor while GetMQTTVideoProcessor generates two streams. The first is the actual MJPEG stream, the second is a metadata stream. Normally the sensor and metadata streams would be pushed into Kafka while the video stream would be save to a local file. GetMQTTVideoProcessor generates a timestamp-based filename attribute for use by the PutFile processor.

This was tested with NiFi 0.4.1. The PutFile processor needs to be patched to support append mode - see this page for a patch: https://issues.apache.org/jira/browse/NIFI-958. When this is applied, the video will cycle through intervals on a basis that can be configured in GetMQTTVideoProcessor (second, minute, hour, day).

### Build

Clone the repo:

    git clone gitL//github.com/richards-tech/RTNiFiStreamProcessors

and build using Maven:

    cd RTNiFiStreamProcessors
    mvn clean install
    
This will generate a file ./nifi-richardstech-nar/target/nifi-richardstech-nar-1.0-SNAPSHOT.nar. This should be copied into NiFi's lib directory. The processors will then be available for selection.

