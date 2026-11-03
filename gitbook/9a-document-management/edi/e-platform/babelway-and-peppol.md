# Babelway & Peppol

The E-Platform service can be used to forward messages to Babelway, or receive messages from Babelway.

Babelway is our partner to access the Peppol network which is required to send and receive invoices to the goverment.

The babelway platform is completly managed by 9altitudes, and customers do not have access to its monitoring or configuration interface. However, it should be possible to setup email notifications when errors occure in Babelway.

When babelway is used, it is preferred to do all the transformations and routing there. And when possible you can send and receive messages without "E-Platform" itself.

However there are situations where this is not directly possible:

* When the ERP server runs "on-prem" and is not publicaly accessable.
* When Babelway cannot easily access the ERP services (mostly due to authentication issues.)&#x20;

In these cases a very basic E-Platform setup should be made which just passes on the messages without doing any transformation, or adding any logic.

