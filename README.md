# fluent-bit-prometheus-integration
Monitoring VM's resource with fluent-bit

fluent-bit is famous Log Processor and Forwarder which allows you to collect data/logs from different sources. fluent-bit 0.13 onwards it comes with the feature of monitoring system resource using its inbuilt http server, so no need of any other application like node-exporter to monitor resource.

## How to do this ?
configure fluent-bit in Vm.
Here I am using **vagrant** to setup VM. You can find simple CentOS vagrant in vagrant-file folder.

Bring the vm up
```
vagrant up
```
Configure fluent-bit using yum

add a new file called td-agent-bit.repo in /etc/yum.repos.d/ in the vm with the following content:
```
[td-agent-bit]
name = TD Agent Bit
baseurl = http://packages.fluentbit.io/centos/7
gpgcheck=1
gpgkey=http://packages.fluentbit.io/fluentbit.key
enabled=
```

Install td-agent-bit
```
yum install td-agent-bit
service td-agent-bit start
```
check fluent-bit running status
```
service td-agent-bit status
```
expose td-agents running port. I have exposed port in the vagrant file.

Add VM's IP and port in the kubernetes manifest file so that prometheus can pull the metrics.

apply manifest file
```
kubectl apply -f /manifest
```

