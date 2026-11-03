---
description: The Kickstart Configuration Package can be used as a base for configuration.
---

# Kickstart: configuration

## Prerequisites&#x20;

The Kickstart only contains configuration. Before importing this package, you will need to set up the integration between Raptor and Business Central: [Set up integration Raptor - BC](https://app.gitbook.com/o/bqSIsQqz4U4PqAwwBN3A/sites/site_10ySw/s/Kfypi8e8luNHtfjQhy6p/~/edit/~/changes/285/integrations/d365-business-central/set-up-integration-raptor-bc)&#x20;

## Kickstart Configuration Package

* Import the Kickstart as a configuration package into the right company.&#x20;
* This configuration package contains all setup, API fields and scenarios. It consists of the following tables:&#x20;
  * 2057741: NAL Raptor API Call Setup
  * 2057743 : NAL Rapt. API Call Setup Field
  * 2057745 : NAL Raptor Setup (Package)
  * 2057747 : NAL Raptor Setup (Package/API)
  * 2057754 : NAL Rapt. Integration Scenario
  * 2057757 : NAL Raptor Integration Field
* The purpose of the configuration package is to import all possible scenarios. Afterwards you can customise as desired (e.g. enable/disable certain scenarios, event management, ...).&#x20;

Business Central: Configuration Packages - page&#x20;

* 1\. Import package&#x20;
  *

      <figure><img src="../../.gitbook/assets/image (731).png" alt=""><figcaption></figcaption></figure>
* 2\. Adjust the fields on the table 'NAL Raptor Integration Field'
  *

      <figure><img src="../../.gitbook/assets/image (732).png" alt=""><figcaption></figcaption></figure>
* 3\. Deselect 'Validate Field' boxes for this table only
  *

      <figure><img src="../../.gitbook/assets/image (733).png" alt=""><figcaption></figcaption></figure>


* 4\. Apply the package&#x20;
  *

      <figure><img src="../../.gitbook/assets/image (734).png" alt=""><figcaption></figcaption></figure>
