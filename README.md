You need to already have NodeRed in HomeAssistant and also the NodeRed Companion integration: https://github.com/zachowj/hass-node-red

Furtermore, sensors in HomeAssistant of 1. combined SoC 2.Combined Daily kWh Charge 3.Combined Daily kWh Discharge

Register on Onbalansmarkt.com and get the API token


Load the NodeRed_Frankonbalansmarkt.json file into NodeRed in HomeAssistant, the flow is from my 3 Sessy batteries, adjust accordingly.


![Schermafbeelding 2025-02-01 om 21 32 39](https://github.com/user-attachments/assets/3ff7427d-3976-4238-a1c8-3e6c9265ea56)




In NodeRed flow:

Adjust contents in 'credentials' with your own details

The 4 blue Nodes that get the data from HomeAssistant ('SoC combined', 'Daily kWh charged', 'Daily kWh discharged' and 'Zelfconsumptie Plus') need to be edited with your sensors from HomeAssistant. These values can't be obtained from FrankEnergy datapull so you can provide them yourself for publishing to Onbalansmarkt.com. For the 'Zelfconsumptie Plus' you can create an Input Boolean and name this 'frank energie zelfconsumptie plus' to manually indicate if your batteries are in 'Zelfconsumptie Plus':
 ![Schermafbeelding 2025-03-25 om 11 57 01](https://github.com/user-attachments/assets/2064c204-c5f0-46b4-bfef-d77334b57fb7)

If you don't want this then disconnect this nodes and the function node that it feeds into, this way you can easily reconnect in future if required. Also edit the node 'Prepare for Onbalansmarkt.com' and change the line:

     selfConsumptionMode: selfConsumption

to: 

     selfConsumptionMode: null


Deploy flow, add more debug items as required to see outputs. The result should now be processed and posted to Onbalansmarkt.com 



To get the data into HomeAssistant: (if you don't want this, delete these nodes from the flow)

The 18 blue sensor Nodes (or how ever many batteries you have (x6)) that send the Trade data to HomeAssistant need to be edited, and also the Switch nodes feeding into the sensor node:

![Schermafbeelding 2025-02-01 om 22 34 00](https://github.com/user-attachments/assets/6c8547bf-3c4a-4c2b-8117-ef4412320e5e)



In Debug 17 (output from 'Handle SmartBatteryResponse' node) you should see your batteries:

![Schermafbeelding 2025-01-05 om 15 41 26](https://github.com/user-attachments/assets/99c0534a-78f7-4e6a-8283-c928fa346391)

copy from each battery the 'id' field, you'll need these if you want to add results into HomeAssistant. This is the unique id that FrankEnergie gives to each battery.

Use them in the Switch nodes, per battery there is a Period Trade (daily trade results), a Total Trade (Lifetime trade results), Period EPEX (daily EPEX correction), PeriodFrankSlim (daily Frank Slim discount), PeriodImbalance (daily imbalance trade result) and PeriodTotalResult (Daily Discount Invoice result)  switch node followed by a sensor node:

![Schermafbeelding 2025-01-05 om 15 43 23](https://github.com/user-attachments/assets/1fcd38df-38dc-4e65-ae5d-208fd0c3030e)

Make sure to leave these values in the switch nodes: (but add the unique battery ID in front of them) 
'_period_trading' 
'_total' 
'_period_epex'
'_period_frank_slim'
'_period_imbalance'
'_period_total'

Edit all the blue HomeAssistant Sensor nodes accordingly, or adjust to however many batteries you have. Edit the 'Entity Config' in properties. 



When succesful they should appear as sensors in HomeAssistant
