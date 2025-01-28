You need to already have NodeRed in HomeAssistant and also the NodeRed Companion integration: https://github.com/zachowj/hass-node-red

Furtermore, sensors in HomeAssistant of 1. combined SoC 2.Combined Daily kWh Charge 3.Combined Daily kWh Discharge

Register on Onbalansmarkt.com and get the API token


Load the NodeRed_Frankonbalansmarkt.json file into NodeRed in HomeAssistant, the flow is from my 3 Sessy batteries, adjust accordingly.


![Schermafbeelding 2025-01-28 om 00 26 02](https://github.com/user-attachments/assets/b7688396-5193-489d-b664-1d29abb87648)




In NodeRed flow:

Adjust contents in 'credentials' with your own details

The 3 blue Nodes that get the data from HomeAssistant ('SoC combined', 'Daily kWh charged' and 'Daily kWh discharged') need to be edited with your sensors from HomeAssistant. These values can't be obtained from FrankEnergy datapull so you can provide them yourself for publishing to Onbalansmarkt.com

Deploy flow, add more debug items as required to see outputs. The result should now be processed and posted to Onbalansmarkt.com 



To get the data into HomeAssistant:

The 15 blue sensor Nodes (or how ever many batteries you have (x5))  that send the Trade data to HomeAssistant need to be edited, and also the Switch nodes feeding into the sensor node:

![Schermafbeelding 2025-01-28 om 01 03 54](https://github.com/user-attachments/assets/61814e22-9b91-44f3-b25e-345a422dc875)



In Debug 17 (output from 'Handle SmartBatteryResponse' node) you should see your batteries:

![Schermafbeelding 2025-01-05 om 15 41 26](https://github.com/user-attachments/assets/99c0534a-78f7-4e6a-8283-c928fa346391)

copy from each battery the 'id' field, you'll need these if you want to add results into HomeAssistant. This is the unique id that FrankEnergie gives to each battery.

Use them in the Switch nodes, per battery there is a Period (daily trade results) and a Total (Total trade results) switch node and sensor node:

![Schermafbeelding 2025-01-05 om 15 43 23](https://github.com/user-attachments/assets/1fcd38df-38dc-4e65-ae5d-208fd0c3030e)

leave the '_period' or '_total' part in the filter!

Edit all the blue HomeAssistant Sensor nodes accordingly, or adjust to however many batteries you have. Edit the 'Entity Config' in properties. 



When succesful they should appear as sensors in HomeAssistant
