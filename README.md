# realtime-stats-monitor
Detect Performance Issues with real time monitoring - Demo

This module consists of a Vagrantfile to easyly spin up the services needed to do realtime moniting of Nodejs services.

This requires a VM installed.  By default it uses [VirtualBox](https://www.virtualbox.org) .

Setup

``` git clone https://github.com/nearform/realtime-stats-monitor.git ```

``` cd realtime-stats-monitor ```


``` make ```

Verify:

Open browser to http://localhost:5601/


This VM will clone the following repos and install autocannan and concurenlty

- [https://github.com/nearform/stats](https://github.com/nearform/stats)
- [https://github.com/nearform/stats-to-elasticsearch](https://github.com/nearform/stats-to-elasticsearch)
- [https://github.com/nearform/create-stats-dashboard](https://github.com/nearform/create-stats-dashboard)
- [https://github.com/nearform/slow-rest-api.git](https://github.com/nearform/slow-rest-api.git)


You can find the source here:

```vagant ssh```

``` cd /usr/share/realtime-monitor ```


