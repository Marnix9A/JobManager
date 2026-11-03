# Adobe Acrobat for PDF Printing

When printing PDF documents through the Document Routing Agent, Adobe Acrobat DC must be installed on the same server where the Document Routing Agent client is running.

To ensure uninterrupted operation, the Adobe Acrobat sign-in prompt should be disabled. Otherwise, the sign-in dialog may appear periodically and interfere with automated document processing.

To disable the sign-in prompt, add the following **DWORD** registry values under the **FeatureLockDown** registry key:

* **bSuppressSignOut** = `1`
* **bToggleAdobeSign** = `1`

These registry changes take effect immediately; restarting the server is not required.

<figure><img src="../../../.gitbook/assets/image (681).png" alt=""><figcaption></figcaption></figure>

Add the cServices folder and value bUpdater - DWORD

<figure><img src="../../../.gitbook/assets/image (682).png" alt=""><figcaption></figcaption></figure>
