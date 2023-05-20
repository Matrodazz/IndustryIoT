# IndustryIoT

### RaspberryPI
https://azure-samples.github.io/raspberry-pi-web-simulator/

### AnomalyDetection
```
WITH AnomalyDetectionStep AS
(
SELECT
EVENTENQUEUEDUTCTIME AS time,
CAST(humidity AS float) AS humid,
AnomalyDetection_SpikeAndDip(CAST(humidity AS float), 99, 120, 'spikesanddips') OVER(LIMIT DURATION(second, 120)) AS
SpikeAndDipScores
FROM IoTHubInput
where humidity is not null )
SELECT
time,
humid,
CAST(GetRecordPropertyValue(SpikeAndDipScores, 'Score') AS float) AS Score,
CAST(GetRecordPropertyValue(SpikeAndDipScores, 'IsAnomaly') AS bigint) AS IsAnomaly
INTO PowerBIOuput
FROM AnomalyDetectionStep
```

### PowerBI
https://app.powerbi.com/
