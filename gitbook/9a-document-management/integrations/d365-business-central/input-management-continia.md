---
description: >-
  Raptor can be integrated with Continia Document Capture, ensuring that all
  incoming documents are stored correctly in Raptor.
---

# Input Management: Continia

## 9A Raptor Integration Setup

Makes sure 'Enable Input Management' is on to enable the different Raptor-fields dealing with Continia on the document categories pages. It partially switches off certain Continia functionalities and uses Raptor document warehouse in replacement.&#x20;

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

## Document categories&#x20;

### 1. Document input

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

* Save ... in Raptor - toggle&#x20;
* Raptor template for...: choose a template for the related document, attachment or mail
* Raptor Tag for Continia Documents Code&#x20;
  * All documents from Continia will get this tag

### 2. Templates: template card

On the document category page go to the Customizable Colums fasttab, select the right template and  edit the template card.&#x20;

<figure><img src="../../.gitbook/assets/image (166).png" alt=""><figcaption></figcaption></figure>

**! Do this for EVERY master template that you use.**&#x20;

Most common are:&#x20;

* PURCHASE master template ; type PDF
* EBILLING master template ; type XML

Go to the Code Units fasttab on this template card.&#x20;

* After Step 1: fill in NAL DocMgtDocCaptureStep1 (object ID = 2057804)

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

## Register to make a purchase invoice

Attachments, invoices and emails get the Continia tags and the right template that you set up&#x20;

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

## CDC document number

Every invoice you receive through Continia is given a CDC document number. This number is a unique ID for documents within Continia Document Capture.

<figure><img src="../../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>

This number now also appears as a tag on the Continia incoming documents.

<figure><img src="../../.gitbook/assets/image (182).png" alt=""><figcaption></figcaption></figure>

### 1. Business Central: add the CDC document number to (posted) purchase invoice

9A Raptor API Setup&#x20;

* EndPointAPI: Purchase invoice&#x20;
* Look for the API field 'D-number'

<figure><img src="../../.gitbook/assets/image (190).png" alt=""><figcaption></figcaption></figure>

9A Raptor Integration Scenarios

* Scenario: Purchase Invoice&#x20;
* Link field 2057801 (NAL CDC Document No.) with the API field 'D-number'.
* Make sure you check the box in the column 'Integrate with 9A Raptor'

<figure><img src="../../.gitbook/assets/image (191).png" alt=""><figcaption></figcaption></figure>

Do the same for the entity 'posted purchase invoice'

### 2. Raptor: make sure the D-number is added as a tag and field&#x20;

Entity configuration: purchase invoice&#x20;

<figure><img src="../../.gitbook/assets/image (192).png" alt=""><figcaption></figcaption></figure>

Templates: Continia Incoming Mail, Continia Attachments, Continia Incoming Document

<figure><img src="../../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>

