# ha-node-red-automations
Home Assistant Node-RED Automations

## UPDATED 4/4/2018

Added tab for notifications flows, set up vacation flows in Security tab - If family is outside of geozone, input boolean gets switched on  and then regular home automations flows are disabled and random lighting is turned on. Added Thermostat UI from /u/twitchy_fingers on Reddit to HA Dashboard. Finally a lot of small bug fixes to the logic in various flows. Thanks all for the feedback.

## About

These are my personal automations and utilities for Home Assistant, using the node-red-contrib-homeassistant plugin. See the screenshots for quick visual representations of the flows or import ha-flows.json into your Node-RED or a test Node-RED project to see the logic. 

## Node-RED Tabs

A quick run down of the flows broken down into the tabs they are located in the project. 

### Home Automation 

![home-automation-1](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/home-automation-1.png)
![home-automation-2](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/home-automation-2.png)
![home-automation-3](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/home-automation-3.png)
![home-automation-4](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/home-automation-4.png)

This handles all the lighting and heating and cooling needs. We use door sensors on a majority of doors and a few motion sensors alond with prescence detection and bayesian inference for sleeping. The end goal is for all the lighting to be pretty much automatic all the time. 

### Location Tracking

![location-tracking](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/location-tracking.png)

Here we handle notifications on on location updates. It uses some logic to try to determine if my wife and I are together, and if so it won't notify us of each other's location. It also tries to eliminate false positives as you just pass through a zone but don't stay -- and it speaks the locations and exits/enters on the home Google Minis if we are home. 

Finally here we have everyone's favorite feature which is the WWE inspired entrance announcment and theme song when we return home. 

### Notifications

![notifications](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/notifications-1.png)

All flows where Home Assistant is conveying information only. This includes text to speech alerts that play on Google Home Minis and push alerts to family iphones. 

Calendar alerts get spoken via the Home Assistant caldav component, trash pickup days we get an audible reminder when we are home. This also checks the calendar to handle holidays when the schedule changes. Finally, mail and package notification.

### Security 

![security](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/security.png)

If we see any events on the motion or door sensors when we are away, we will be notified. We also handle doors that are open too long here. 

### Utilities 

![utilities-1](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/utilities-1.png)
![utilities-2](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/utilities-2.png)
![utilities-3](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/utilities-3.png)

This houses all the crazy little things like reformatting MQTT state messages for Sonoffs so the state in Home Assistant is always correct, monitoring our email for days when school is cancelled, automatically turning on guest mode if in laws are at our house, and some crazy flows trying to automatically retry any Zigbee/ZHA errors for our lighting. (We have way too many bulbs now)

### Dashboard

![dashboard](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/dashboard.png)

Creates a node-red dashboard for some basic graphing and metrics. Also using ThermoStat UI from /u/twitch_fingers on Reddit to start creating a control dashboard for the system. 

### Dev 

![dev](https://raw.githubusercontent.com/walthowd/ha-node-red-automations/master/dev.png)

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
        "node-red-contrib-vacation-timer": "2.2.8"
        
## Produced

The ha-flows.json was was produced with the command:

cat ha-flows.json | json_pp | sed -f patterns

Where patterns is a file containing:

s/sensitive-password/your-password/g

s/yourdomain/exampledomain/g
