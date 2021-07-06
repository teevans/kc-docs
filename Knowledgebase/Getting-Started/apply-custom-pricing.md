Apply Custom Pricing 
========

Update `values.yaml` file to define custom pricing and set `customPricesEnabled` to `true`:

```
defaultModelPricing: 
    CPU: 00.1
    spotCPU: 00.1
    RAM: 5.00
    spotRAM: 0.65
    GPU: 693.50
    spotGPU: 225.0
    storage: 0.04
    zoneNetworkEgress: 0.01
    regionNetworkEgress: 0.01
    internetNetworkEgress: 0.12
    enabled: true
customPricesEnabled: true  
```

Use cmd  `helm upgrade` to deploy the configuration change: 

```
$ helm upgrade kubecost kubecost/cost-analyzer --namespace kubecost -f values.yaml
```

Rebuild the ETL data pipeline by visiting or pinging the following endpoints:

```
/model/etl/assets/rebuild?commit=true&window=all
/model/etl/allocation/rebuild?commit=true&window=all
```

Example: 

```
$ curl -Lk 'http://localhost:9090/model/etl/assets/rebuild?commit=true&window=all'
{"code":200,"data":"Rebuilding Asset ETL"}
```
