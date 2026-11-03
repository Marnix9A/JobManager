---
description: >-
  Raptor can be integrated with Jobmanager, ensuring that people on the
  shopfloor have access to important documents when executing a job.
---

# JobManager

## 9A Raptor Integration Setup <a href="#id-9a-raptor-integration-setup" id="id-9a-raptor-integration-setup"></a>

Makes sure 'Enable JobManager Management' is on to enable the integration with JobManager.

<figure><img src="../../.gitbook/assets/image (735).png" alt=""><figcaption></figcaption></figure>

## JobManager Integration

### 1. 9A Raptor Integration Scenarios

Two integration scenarios are available to ensure the integration with Jobmanager.&#x20;

#### JobMan Job

JobManager operates on the same underlying records as Production Orders, Assembly Orders, Service Orders, and Projects. To avoid the need for separate entity configurations, the JobManager integration uses static impersonation. This allows JobManager pages to reuse the existing Raptor integration of the underlying Business Central document, ensuring that the correct documents are displayed without additional configuration. As a result, the 9A Raptor viewers displayed within JobManager automatically inherit the context of the originating document (Production, Assembly, Service, or Project).&#x20;

To enable this integration, you need to set up the JobMan Job integration scenario. It is not necessary to set up new API fields and integration. When the JobMan Job scenario is enabled, this will just activate the viewer on Jobmanager and refer to the correct integration scenario connected to the page.&#x20;

**When the JobMan Job integration scenario is enabled, the JobManager job lists are mapped to the following Raptor entities:**

Production Job list: productionOrderRouting

Project Job list: projectPlanningLines

Service Job list: serviceLines

Assembly Job list: assemblyOrderLines

<figure><img src="../../.gitbook/assets/image (722).png" alt=""><figcaption></figcaption></figure>

#### JobMan Stamp Journal

The JobMan Stamp Journal refers to the 9A Viewer on the Active Jobs tile. This scenario also uses static impersonation, and reuses the existing Raptor integration.&#x20;

<figure><img src="../../.gitbook/assets/image (723).png" alt=""><figcaption></figcaption></figure>

## JobManager Comment Factbox&#x20;

9A Raptor Document Warehouse integrates directly with the JobManager Comment FactBox. This works in both directions.&#x20;

Raptor -> Comment Factbox: When a document is added to the Raptor viewer on a JobManager page (Production Jobs, Project Jobs, Service Jobs, Assembly Jobs, or Active Jobs), a corresponding linked record is automatically created in the JobManager Comment FactBox.

Comment Factbox -> Raptor: When a user adds a document through the JobManager Comment FactBox using the Add Image action, the document is automatically uploaded to Raptor Document Warehouse. The document is created with the correct metadata and tags based on the current context.&#x20;

<figure><img src="../../.gitbook/assets/image (725).png" alt=""><figcaption></figcaption></figure>

### 1. Setup

#### Comments Setup List

To enable the integration with the JobManager Comment FactBox, additional setup is required on the Comments Setup List page.

For each relevant job type, a line must be created that links the job type to the codeunit responsible for synchronizing documents with the Comment FactBox (codeunit = 2112963).

<figure><img src="../../.gitbook/assets/image (726).png" alt=""><figcaption></figcaption></figure>

#### 9A Raptor Integration Scenarios&#x20;

On the JobMan Job integration scenario, it is important that the toggle 'Save attachments to Raptor Side' is enabled.&#x20;

<figure><img src="../../.gitbook/assets/image (727).png" alt=""><figcaption></figcaption></figure>
