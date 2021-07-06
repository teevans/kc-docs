Implement a New Cloud Provider
=====================

To add a new cloud provider to Kubecost you must implement the provider interface-- and even then only a subset. A good place to start for understanding the minimal set to implement would be to look at the methods implemented by the CSVProvider, which simply takes a pricing sheet of nodes/persistentvolumes and matches them based on the ProviderID() field in kubernetes.

https://github.com/kubecost/cost-model/blob/develop/pkg/cloud/csvprovider.go

In particular, the most important functions to implement are:

DownloadPricingData() -- a threadsafe method for fetching your prices

NodePricing() -- the only requirement is to fill out the "Cost" field in returned Node. CPU/RAM/GPU breakdowns if they do not exist in the cloud provider will get set based on a ratio computed from a survey of other cloud providers.

PVPricing() -- the only requirement is to fill out the "Cost" field in the returned PV
(These costs fields are all hourly)

To beging start with an implementation of DownloadPricingData(), NodePricing(), and PVPricing() functions. 