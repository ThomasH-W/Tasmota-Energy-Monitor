# Tasmota-Energy-Monitor
Energy monitor using NodeRED, InfluxDB and Grafana

This project is using power monitoring devices like Gosund SP111, SONOFF POW to measure the energy consumption.
Data is collected by NodeRED and pushed to a Influx database.
Finally Grafana is used to provide a dashboard.

## Grafana Monitoring

![3825759A-FF9F-4E9A-95C6-94841B3EACC9](https://user-images.githubusercontent.com/3676469/219877600-6ac0cc8c-290d-4fbb-97d5-d5a57ec5e824.jpeg)


![4B077E85-3864-49A2-B832-98EFC162FBA3](https://user-images.githubusercontent.com/3676469/219877607-be316b8c-6ac5-4018-b540-90394a17c36b.jpeg)


## NodeRED

![EE548C94-9332-4D77-9C91-5CADC5A79EF2_4_5005_c](https://user-images.githubusercontent.com/3676469/219877613-3afb5971-c4bb-4841-bc5d-ee5ea3281302.jpeg)

The flow is kept very generic. You do not need to manually create flows for each devices.
Instead of using discovery, NodRED is listening to all SENSOR messages and creating automatically a list of devices. 

The fiedls pushed to the influx database are
*    device: myDevice,
*    event: 'tele',
*    power: msg.payload.ENERGY.Power,
*    today: msg.payload.ENERGY.Today,
*    yesterday: msg.payload.ENERGY.Yesterday,
*    total: msg.payload.ENERGY.Total

At the end of each day at 11.58 p.m. the value of today is pushed to another measurement in influx.
