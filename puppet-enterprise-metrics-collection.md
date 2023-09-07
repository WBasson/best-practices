# ⚠ WARNING ⚠

This repository is no longer mantained since ~ 2019. While some of these documentation might still be useful, much of it is obsolete or out of date.

For a maintained collection of similar information, please see [Patterns and Tactics](https://www.puppet.com/docs/patterns-and-tactics/latest/patterns-and-tactics.html).
# Puppet Metrics Collection

## Summary

To ensure the information needed to troubleshoot performance issues is available when needed, it is recommended that Puppet users set up a metrics gathering tool.  This standard defines how to gather, retain, and graph metrics for Puppet components in a format that is easily shareable with Puppet Support.  

## Expectations

This is a standard that applies to all Puppet customers.  

This standard assumes no existing performance monitoring infrastructure and the modules will configure influxdb and grafana for the user.  If there is desire to use existing tools for storing and graphing metrics then that will be left to the user to deduce from our examples.  

## Standard Details

### Preferred Option


#### Collecting metrics 

We recommend using the [puppet_metrics_collector](https://github.com/puppetlabs/puppetlabs-puppet_metrics_collector) module to collect metrics.  By default, the module stores metrics in `/opt/puppetlabs/puppet-metrics-collector`, and the data can be easily archived and shared with Support.

#### Storing and visualizing metrics 

If permanent visualization of metrics is desired, we recommend the [puppetlabs-puppet_metrics_dashboard](https://forge.puppet.com/puppetlabs/puppet_metrics_dashboard) module to store historical metrics in influxDB and visualize metrics with Grafana.  This option requires an additional server to run influxDB and Grafana.  After configuring influxDB with the module you will configure *puppet-metrics-collector* to directly export metrics into InfluxDB.

For temporary visualization of metrics we recommend [puppet-metrics-viewer](https://github.com/puppetlabs/puppet-metrics-viewer).  This option uses a docker container to allow visualizing the metrics on an ad-hoc basis but no data is permanently stored.

Both options use a set of example dashboards with the most useful metrics for troubleshooting scaling and performance issues.  

### Alternate Options

While the preferred option allows for long term analysis of the performance data, the PuppetDB developer dashboard can be used before long term solutions have been configured. The [PuppetDB dashboard](https://puppet.com/docs/puppetdb/5.2/maintain_and_tune.html#monitor-the-performance-dashboard) provides a real time view of the current state of the PuppetDB service. This can be helpful in troubleshooting issues, but does not provide historical data. 

*Note*: The PuppetDB dashboard negatively impacts performance and should not be left open. Instead use it for troubleshooting specific incidents when you don't yet have longer term metrics gathering and visualization set up. 

### Discouraged Options

It is possible to collect metrics from JMX or direct export of graphite metrics from puppetserver.  These options are discouraged for their complexity and because the output is not readily shareable with Puppet Support or 3rd parties.  

## Feedback / Ideas for Improvement

Please submit issues to the projects below if you have ideas for improvement:

[puppet_metrics_collector](https://github.com/puppetlabs/puppetlabs-puppet_metrics_collector)  
[puppet_metrics_dashboard](https://github.com/puppetlabs/puppet_metrics_dashboard)  
[puppet-metrics-viewer](https://github.com/puppetlabs/puppet-metrics-viewer)  
