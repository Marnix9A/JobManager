# Concepts

## Routes

Every message that passes via the E-Platform does so under the umbrella of a Route. This is just a name, and contains a collection of calls to be invoked.

## Endpoints

An endpoint represents one of:

* A single call to an other system (= output)\
  Usually a HTTP POST.
* A input / entry point\
  Every route should have at least one input endpoint; a message that is received must find a matching input endpoint in order to be accepted. Although technically possible multiple entry endpoints can be configured; but this is rare.
* A representation of a complex action\
  There are some "specialized" integrations that combine multiple calls into a single "action" in which case the result of those calls will be converted to a XML message that is made available on the endpoint. An example would be the "uploading of the kofax document to the raptor document warehouse".

Routes are a combination of endpoints, which are chained to each other.

When one endpoint is finished, multiple endpoints can be chained to it. (aka parallel tasks) Although most implementations choose to invoke calls sequentially because this makes the system more predictable.

Endpoints support "retries". If an endpoint detects a problem, the action will be invoked again with up to 10 retries. After 10 failures the endpoint itself is goes into the "failed" state, usually blocking the message.

### Distribution List

The distribution list links endpoints to each other. It basically says after endpoint 1, invoke endpoint 2. In order to include an endpoint in a route, it either has to be the entry endpoint, or linked to and endpoint already in the route.

If one endpoint has multiple other endpoints linked to it, then those endpoint can run in parallel.

Important rules:&#x20;

* loops are not allowed
* Every (output) endpoint that must be invoked must be triggered via the distribution list.
* Every endpoint should be triggered only once.
* Every endpoint will result in a call; so conditions are not possible.

Note: consider an example where you want to make a call that links an order to an invoice. Should there be no order information available, you still need to make a call. Because you can't skip the call based on some condition. Not only do you have to make a call, the call should also be successfull, else the action will be retried.

Note: consider an example where you want to add multiple orders to a single invoice. Because it is not possible to configure loops, and conditions, you have to do this in a single call. The kickstart routes provided by 9Altitudes use o-data batch calls to D365-FO to accomplish just this. However this has the drawback that a failure in one or more of the batch jobs will not be detected, and will not result in retry attempts since the batch call itself did in fact succeed.

**Exception**

Some endpoints are "managed" by special actions, such as uploading and enriching documents in the document warehouse. These actions are not triggered by the distribution list, but use special hooks to be triggered.

### Endpoint Sources

Endpoint sources allow one endpoint to use the output (= response) from multiple other endpoints as input data. When sources are configured; all those endpoints must be finished before the 'target' endpoint will be invoked.

So sources can be used to wait for multiple other calls to be finished; and to get access to the responses of all those calls.

Note: if sources are configured, the "input message" will be an XML containing all the outputs of the selected source endpoints into a single merged xml object.

Important:

A source endpoint must still be added to a "main branch" (via the distribution list.) Adding a source endpoint without adding it to a distribution list will result in a stuck message; because the endpoint will never be triggered.

### Message Types

An endpoint must define a message type, however message types are mostly informative. Meaning they just indicate what kind of message is being used. Message types are defined once, and can then be used in many endpoints.&#x20;

An example of a message type could be "D365-FO Invoice Header", or even "unknown".

### Protocol

A protocol is a combination of a Name and a Version, and is mostly informative.

An example would be (name) "UBL" , and (version) "2.0"

## Sagas

When a message arrives and finds an entry endpoint into a route, it is assigned a Saga Id. Each action (/endpoint) that is triggered as a result will have access to this Saga Id , and can use it to read responses of other endpoints that were triggered before. Saga's are also used to link logs related to the same message.

Endpoints can also store data into saga variables, which can then be used in subsequent tasks.

## Transformations

Transformations can be used for several purposes; but the most important one is to modify the "source message" of an endpoint to create the body of the message that is send by that endpoint.

Types of transformations

* XML to JSON
* JSON to XML
* XSLT (Xml Transformation.)

A normal use case would be:

1. Convert the json response of a invoice creation from JSON to XML
2. Create a XML file that represents an "order total line" with the same amount as the invoice, and the same ID as the invoice.
3. Convert the XML to JSON, so it can be posted to a REST endpoint that accepts only JSON data.

Transformations can be very powerfull because they can also extract data from an XML and place it in a saga variable. Basically any logic that is part of the e-platform must be encoded in a transformation.
