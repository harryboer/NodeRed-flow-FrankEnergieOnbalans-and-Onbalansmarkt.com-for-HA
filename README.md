You need to already have NodeRed in HomeAssistant and also the NodeRed Companion integration: https://github.com/zachowj/hass-node-red

Furtermore, sensors in HomeAssistant of 1. combined SoC 2.Combined Daily kWh Charge 3.Combined Daily kWh Discharge

Register on Onbalansmarkt.com and get the API token


Load the flow.json file into NodeRed in HomeAssistant, the flow is from my 3 Sessy batteries, adjust accordingly.

![Schermafbeelding 2025-01-05 om 13 55 29](https://github.com/user-attachments/assets/d5d01df7-a731-4e9a-a1b8-6183addc0b00)


In Noderedflow:

Adjust contents in 'credentials' with your own details

The 3 blue Nodes that get the data from HomeAssistant ('SoC combined', 'Daily kWh charged' and 'Daily kWh discharged') need to be edited with your sensors from HomeAssistant. These values can't be obtained from FrankEnergy datapull so you can provide them yourself for publishing to Onbalansmarkt.com

Deploy flow, add more debug items as required to see outputs. The result should now be processed and posted to Onbalansmarkt.com 


To get the data into HomeAssistant:

The 6 blue sensor Nodes (or how ever many batteries you have (x2))  that send the Trade data to HomeAssistant need to be edited, and also the Switch nodes feeding into the sensor node:

![Schermafbeelding 2025-01-05 om 16 27 39](https://github.com/user-attachments/assets/28ca8992-ace7-4fdb-9b43-36126b56b33b)


In Debug 17 (output from 'Handle SmartBatteryResponse' node) you should see your batteries:

![Schermafbeelding 2025-01-05 om 15 41 26](https://github.com/user-attachments/assets/99c0534a-78f7-4e6a-8283-c928fa346391)

copy from each battery the 'id' field, you need tich if you want to add results into HomeAssistant. This is de id that FrankEnergie gives to every battery.

Use them in these in the Switch nodes:

![Schermafbeelding 2025-01-05 om 15 43 23](https://github.com/user-attachments/assets/1fcd38df-38dc-4e65-ae5d-208fd0c3030e)

leave the '_period' or '_total' part in the filter!

Edit all the blue HomeAssistant Sensor nodes accordingly, or adjust to however many batteries you have. Edit the 'Entity Config' in properties. 

Per battery there is a Period (daily trade results) and Total (Total trade results) sensor

When succesful they should appear as sensors in HomeAssistant
