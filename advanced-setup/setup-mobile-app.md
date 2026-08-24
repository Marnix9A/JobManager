# Setup Mobile App

**Note the App below is deprecated and replaced by [this solution](../daily-use/mobile-role-center.md).** Business Central 19 is **LAST** version where the following is supported.

## For all JobManager version _(see below for additional steps regarding older versions)_

1.  Activate the _JobManager_ **SOAP** Web Services _6182750 JobManWebService_ within the NAV/BC page _Web Service_.
2.  Open _Dynamics NAV Administration_ on the NAV Server and change the following values:
    1.  Tick **Enable SOAP Services**.
    2.  **Max Message Size** under **SOAP Services** should be set to minimum _20480_.
3.  The port for **SOAP Services** should set up in the firewall with forward to the NAV Server. _On request we can disclose the IP-address of the APP Server._
4.  Check the **SOAP** connection from a browser on another computer (if SSL change http to http**s**):
    *   Syntax: `http://MyPublicIP:MySoapPort/MyNavService/WS/MyNavCompany/services`
    *   Sample without company: `http://navdemo9999.cloudapp.net:7047/NAV/WS/services`
    *   Sample with company: `http://navdemo9999.cloudapp.net:7047/NAV/WS/Cronus%20Danmark%20A%2fS/services`
    *   Sample with Tenant: `http://navdemo9999.cloudapp.net:7047/NAV/WS/services?Tenant=Ten999`
    *   Result: Should be able to login and see list of services.
5.  The following information should be used to setup the APP. Setup the APP can be done at [this site](https://jmgapp.dk/Account/Login.aspx).
    1.  Information about the customer.
    2.  Information about the NAV partner.
    3.  The NAV Servers **public IP-address**. This must be a **fixed IP-addresses**.
    4.  The name of the NAV _Instance_.
    5.  The name of the NAV _Company_ - **Remarks regarding _Company_:**
        *   The name _should_ be _without_ space and special characters
        *   The name _should_ only contain these letters _a..z, A..Z og 0..9_
        *   The name _CAN'T_ contain local letters (eg. danish, german letters) or other regional special letters
    6.  Optionally the name of the NAV _Tenant_.
    7.  The port for **SOAP Services**.
    8.  Domain, User name and password for a valid NAV user.
        *   The User must have _JOBMAN-ADMINISTRATOR_ or _SUPER_ permissions.
    9.  Perhaps an _Employee Number_ for our test of the connection.
6.  If you want to upload images from within the app:
    1.  Setup the [Path for new links](../general-setup/path-for-new-links.md) on [JobManager setup](../general-setup/jobmanager-setup.md).
    2.  Enable for relevant lines with [Add links/image](../other-setup/add-links-image.md) on [Comments setup](../other-setup/comments-setup.md).

**Setup the APP is be done by the BC/NAV partner at [this site](https://jmgapp.dk/Account/Login.aspx). Contact support@jobmanager.dk to be created as user and usage instructions.**

## JobManager version 01.25 and older, the following _also applies_

The following must be done for JobManager versions **earlier** than **01.26**

1.  Open _Dynamics NAV Administration_ on the NAV Server and change the following values:
    1.  **Service Default Time Zone** should be set to _Server Time Zone_, and the Servers Time Zone should be the same as the the Companys main location.

## JobManager version 01.16 and older, the following _also applies_

The following must be done for JobManager versions **earlier** than **01.17** - after any upgrade _to_ **01.17** the following can be **reversed**:

**Note:** If the customer has special code adjustments to their JobManager APP, then these may still depend on **Odata**.

1.  Activate all _JobManager_ **OData** Web Services within the NAV/BC page _Web Service_.
2.  Open _Dynamics NAV Administration_ on the NAV Server and change the following values:
    1.  Tick **Enable OData Services**.
    2.  **Max Page Size** under **OData Services** should be set to minimum _9999_.
    3.  **Services Language** under **General** should be set to _en-US_.
    4.  **Services Option Text Source** / **Services Option Format** under **General** should be set to _OptionCaption_.
3.  Add/Edit the following entry to the _CustomSettings.config_ file for each relevant instance:
    *   `<add key="EnableODataStrictFiltering" value="false"/>`
    *   By default, the files are located in either:
        *   _C:\\Program Files\\Microsoft Dynamics NAV\\##\\Service\\Instances\\<instancename>_
        *   _C:\\Program Files\\Microsoft Dynamics NAV\\##\\Service_.
        *   _C:\\Program Files\\Microsoft Dynamics 365 Business Central\\##\\Service\\Instances\\<instancename>_
        *   _C:\\Program Files\\Microsoft Dynamics 365 Business Central\\##\\Service_
4.  The port for **OData Services** should set up in the firewall with forward to the NAV Server. _On request we can disclose the IP-address of the APP Server._
5.  Check the **OData** connection from a browser on another computer (if SSL change http to http**s**):
    *   Syntax: `http://MyPublicIP:MyODataPort/MyNavService/OData`
    *   Sample: `http://navdemo9999.cloudapp.net:7048/NAV/OData`
    *   Sample with Tenant: `http://navdemo9999.cloudapp.net:7048/NAV/OData?Tenant=Ten999`
    *   Result: Should be able to login and see list of services.

## See also

[Choose device](../get-started-guide/choose-device.md)  
[Mobile Role Center](../daily-use/mobile-role-center.md)  
[Mobile Registration Client App](../mobile-registration-client-app/README.md)  
[Get started with App](../mobile-registration-client-app/get-started-with-app.md)  
[Q&A (App)](../q-and-a-questions-and-answers/q-and-a-app.md)
