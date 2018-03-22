# ha-node-red-automations
Home Assistant Node-RED Automations

## About

These are my personal automations and utilities for Home Assistant, using the node-red-contrib-homeassistant plugin. See the screenshots for quick visual representations of the flows or import ha-flows.json into your Node-RED or a test Node-RED project to see the logic. 

## Node-RED Tabs

A quick run down of the flows broken down into the tabs they are located in the project. 

### Home Automation 

This handles all the lighting and heating and cooling needs. We use door sensors on a majority of doors and a few motion sensors alond with prescence detection and bayesian inference for sleeping. The end goal is for all the lighting to be pretty much automatic all the time. 

### Location Tracking

Here we handle notifications on on location updates. It uses some logic to try to determine if my wife and I are together, and if so it won't notify us of each other's location. It also tries to eliminate false positives as you just pass through a zone but don't stay -- and it speaks the locations and exits/enters on the home Google Minis if we are home. 

Finally here we have everyone's favorite feature which is the WWE inspired entrance announcment and theme song when we return home. 

### Security 

If we see any events on the motion or door sensors when we are away, we will be notified. We also handle doors that are open too long here. 

### Utilities 

This houses all the crazy little things like reformatting MQTT state messages for Sonoffs so the state in Home Assistant is always correct, monitoring our email for days when school is cancelled, automatically turning on guest mode if in laws are at our house, and some crazy flows trying to automatically retry any Zigbee/ZHA errors for our lighting. (We have way too many bulbs now)

### Dashboard

Creates a node-red dashboard for some basic graphing and metrics.

### Dev 

Where are the flows are created and tested until they graduate into one of the other tabs. 

## Requirements

The full list of packages that are required:

        "node-red-contrib-bigtimer": "1.8.0",
        "node-red-contrib-counter": "0.1.4",
        "node-red-contrib-home-assistant": "0.3.0",
        "node-red-contrib-looptimer": "0.0.8",
        "node-red-contrib-moment": "2.0.7",
        "node-red-contrib-stoptimer": "0.0.7",
        "node-red-contrib-time-range-switch": "0.5.1",
        "node-red-contrib-traffic": "0.2.1",
        "node-red-dashboard": "2.8.1",
        "node-red-node-email": "0.1.24",
        "node-red-node-random": "0.1.0",
        "node-red-node-rbe": "0.2.1"
        
## Produced

The ha-flows.json was was produced with the command:

cat ha-flows.json | json_pp | sed -f patterns

Where patterns is a file containing:

s/sensitive-password/your-password/g

s/yourdomain/exampledomain/g
