# jbpm-kafka-feeder
[![Build status](https://travis-ci.org/Jiri-Kremser/jbpm-kafka-feeder.svg?branch=master)](https://travis-ci.org/Jiri-Kremser/jbpm-kafka-feeder)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0)

jBPM listener that feeds the data into Apache Kafka

## Usage

deploy jBPM into openshift:

```bash
# image streams
oc create -f https://raw.githubusercontent.com/jboss-container-images/rhpam-7-openshift-image/7.0.1.GA/rhpam70-image-streams.yaml

# import template
oc create -f https://raw.githubusercontent.com/jboss-container-images/rhpam-7-openshift-image/7.0.1.GA/templates/rhpam70-trial-ephemeral.yaml

# instantiate the template
oc new-app -l app=jbpm --template=rhpam70-trial-ephemeral -p IMAGE_STREAM_NAMESPACE=`oc project -q`
```

Then in the jBPM UI do:

1. upload listener jar into artifact repository (settings top right -> artifact, upload)
1. create example project (it orders for instance)
1. go to its settings and add the listener jar as a dependency, whitelist everything
1. add event listener, id = classname, resolving mechanism = reflection
1. create new process instance
1. check the logs if the listener got triggered
