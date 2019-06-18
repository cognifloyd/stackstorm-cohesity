# Cohesity Pack for StackStorm

Cohesity pack provides integration with Cohesity DataPlatform

## Pre-requisites

- Cohesity Cluster running version 6.0 or higher
- StackStorm

## Setup

### Install Cohesity pack on StackStorm

```bash
# Install Cohesity Pack
st2 pack install cohesity

# Check installation
st2 action list -p cohesity
```

### Configuration

Copy the example configuration in [cohesity.yaml.example](./cohesity.yaml.example) to `/opt/stackstorm/configs/cohesity.yaml` and edit as required. It must contain:
* `hostname` - Hostname or IP address of the Cohesity Cluster
* `username` - The username to login to the Cohesity Cluster
* `password` - The password to login to the Cohesity Cluster
* `domain`   - The domain to login to the Cohesity Cluster

#### Example

```yaml
---
hostname: "cohesity-cluster.example.com"
username: "EXAMPLE_USER"
password: "EXAMPLE_PASSWORD"
domain:   "example.com"
```

## Sensors

### CohesityAlertSensor
This is a sensor that senses new alerts generated on the Cohesity Cluster.

A trigger called `new_alert` is emitted when a new Cohesity alert is detected.

An example of the trigger payload is shown below:

```json
{
  "status": "processed",
  "occurrence_time": "2019-05-08T16:42:18.000000Z",
  "trigger": "cohesity.new_alert",
  "id": "5cd3695a40c8e015610d334c",
  "payload": {
    "category": "kCluster",
    "code": "CE00301012",
    "name": "UpgradeStarted",
    "description": "Upgrade started on the node 1270179007222379 with ip 10.2.148.29.",
    "state": "kOpen",
    "alert_type": 1012,
    "cause": "Started upgrade to 6.2_release-20190508_073c4a45.",
    "id": "317979:1557358953619257",
    "severity": "kInfo"
  }
}
```

## Actions

Once you have installed the cohesity pack you can run the command below to get a list of all available actions.

```bash
st2 action list -p cohesity
```

To get information on a specific action (say `resolve_alert`), please run:

```bash

[root@stackstorm ~]# st2 action get cohesity.resolve_alert
+---------------+--------------------------------------------------------+
| Property      | Value                                                  |
+---------------+--------------------------------------------------------+
| id            | 5cbd4f1d40c8e03a3f6a4adb                               |
| uid           | action:cohesity:resolve_alert                          |
| ref           | cohesity.resolve_alert                                 |
| pack          | cohesity                                               |
| name          | resolve_alert                                          |
| description   | Resolves the specified Cohesity alert.                 |
| enabled       | True                                                   |
| entry_point   | resolve_alert.py                                       |
| runner_type   | python-script                                          |
| parameters    | {                                                      |
|               |     "alert_id": {                                      |
|               |         "position": 0,                                 |
|               |         "required": true,                              |
|               |         "type": "string",                              |
|               |         "description": "Alert id to resolve."          |
|               |     },                                                 |
|               |     "description": {                                   |
|               |         "position": 2,                                 |
|               |         "required": true,                              |
|               |         "type": "string",                              |
|               |         "description": "Alert resolution description." |
|               |     },                                                 |
|               |     "summary": {                                       |
|               |         "position": 1,                                 |
|               |         "required": true,                              |
|               |         "type": "string",                              |
|               |         "description": "Alert resolution summary."     |
|               |     }                                                  |
|               | }                                                      |
| metadata_file | actions/resolve_alert.yaml                             |
| notify        |                                                        |
| output_schema |                                                        |
| tags          |                                                        |
+---------------+----------------------------------------------------
```
