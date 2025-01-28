Nodes that are updated are:

- Prepare Get SmartBatterySessions Request
- Handle SmartBatterySessions Response
- Extract Sessy Trade Results

and then all the extra blue nodes that send the data to HomeAssistant.

One extra item is the node 'Zelfconsumptie plus' this is input from HomeAssistant where I made a boolean helper to indicate the batteries are running in Zelfconsumptie mode in de FE app. This is then also published on Onbalansmarkt.com
For this you need to set up this boolean helper in HA and add the relevant nodes in NodeRed to import the state of the hekper and also use the updated code in node 'Prepare for Onbalansmarkt.com'
