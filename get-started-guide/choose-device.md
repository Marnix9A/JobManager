# Choose device

JobManager can be run on all the platforms that Microsoft supports for Business Central.

# Time registration inside the company

## Shared _terminals_

The best experience is achieved by using real PCs or Windows tablets with a keyboard and preferably a mouse.

JobManager contains a specially designed [Role Center](../other-setup/role-center.md) **JOBMANREG** for this purpose.

\*See the installation guide for help creating the most optimal shortcut to BC/NAV for time registration.

**LICENSE for BC/NAV:** A _Device_ license should be used here, but a _Full User_ or _Team Member_ (X) can technically also be used.

## Personal access

If the employee already has access to BC/NAV with a user, then the time registration could take place with that normal access.

**LICENSE for BC/NAV:** A _Team Member_ (X) or _Full User_ can be used.

# Time registration outside the company

## Personal access

If the employee _is on the go_, there are several solutions. The _device_ used determines which solution provides the best experience.

### Smart Phone

JobManager contains a specially designed [Role Center](../other-setup/role-center.md) **JOBMANMOBILE** for this purpose. Optimized with specially designed pages for mobile smart phones running [Microsofts APP for mobile devices](https://docs.microsoft.com/en-us/dynamics365/business-central/install-mobile-app). Read more [here](../daily-use/mobile-role-center.md).

**LICENSE for BC / NAV:** A _Team Member_ (X) or _Full User_ can be used.

### Tablets, iPads and PCs

JobManager contains a specially designed [Role Center](../other-setup/role-center.md) **JOBMANREG** for this purpose.

**LICENSE for BC/NAV:** A _Team Member_ (X) or _Full User_ can be used.

# License

If a _Team Member_ license is used all JobManager tables count as "free" writes. _This applies to Customer License is downloaded after 7th of March 2020._

24.  If a _Team Member_ license is used [Update In Progress (Production)](./update-in-progress-production.md) under [JobManager Setup](../general-setup/jobmanager-setup.md) should be disabled.

**IPO ONLY**

If the parameter on the JobManager employee table "only IPO" is used, a job must be selected during JobManager setup under the tab system jobs. Used to obtain a cheaper license

# Shortcuts

Shortcut to open the Registration Cockpit:

*   **OnPrem:** _http://TheServer:8080/BC/?Page=6182710&Mode=Edit_
*   **SaaS:** _https://businesscentral.dynamics.com/4a70d1ca-9ef5-4b36-ba64-d3a72571ed44/Production/?Page=6182710&Mode=Edit_

Info for Windows clients can be found in the _JobManager\_NAV\_InstallationGuide\_V0XXX.pdf_ within the installation ZIP-file.

# Recommended setting for the BC server instance

This unfortently only applies to OnPremise installations, as SaaS solutions are more _locked_ in settings.

We recommend all registration users login to a specific BC instance, which is only used for JobManager time registration.

Hide the _search icon_ in upper right corner, to limit the user from mistakenly opening other pages. Search for `ShowPageSearch` in [this page](https://docs.microsoft.com/pt-pt/dynamics365/business-central/dev-itpro/administration/configure-web-server) to read more.

The Web Clients timeout could be changed (raised) with _Business Central Administration Shell_. Go to [this page](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/administration/understanding-session-timeouts) to read more. The example below set _1 hour and 30 minuts_:

`Set-NAVWebServerInstanceConfiguration -WebServerInstance YourBC -KeyName SessionTimeout -KeyValue "01:30:00"`

## See also

[Role Center](../other-setup/role-center.md)  
[License for JobManager](./license-for-jobmanager.md)
