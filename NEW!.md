
--------------------
01-02-2025: Nodes that are updated are:

- Prepare Get SmartBatterySessions Request (correcting timestamp and adding periodTotalResult item)
- Handle SmartBatterySessions Response (processing the new data)
- Prepare for Onbalansmarkt.com (streamlining payload with new data to publish on Onbalansmarkt)

and then extra blue nodes that send the data 'Period Total Result' (=kortingsfactuur vandaag) to HomeAssistant

--------------------
29-01-2025: Nodes that are updated are:

- Prepare Get SmartBatterySessions Request (adding new datalabels to retrieve from Frank)
- Handle SmartBatterySessions Response (processing the new data)
- Extract Sessy Trade Results (Adding new data for HomeAssistant)

and then all the extra blue nodes that send the data to HomeAssistant, also update the period trading switch node because the filter 'period' is changed to 'period_trading'


One extra item is the node 'Zelfconsumptie plus' this is input from HomeAssistant where I made a boolean helper to indicate the batteries are running in Zelfconsumptie mode in de FE app. This is then also published on Onbalansmarkt.com
For this you need to set up this boolean helper in HA and add the relevant nodes in NodeRed to import the state of the hekper and also use the updated code in node 'Prepare for Onbalansmarkt.com'
