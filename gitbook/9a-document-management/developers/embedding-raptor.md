# Embedding Raptor

The 9A Raptor DWH can be embedded in any application, either by loading in an iframe and sending context over JavaScript messages, or simply by passing the context in the URL.

## Embed using URL parameters

To embed Raptor via URL, you can use query parameters "exa-auth-plugin" and "exa-plugin-context", and "tenant-id"

<details>

<summary>exa-auth-plugin</summary>

This parameter contains the authentication token used to identify the user.

**Usage Guidelines**

* ✅ **Required** when:
  * Embedding Raptor inside an iframe
  * The user is already authenticated in the host application
* ⚠️ **Important considerations**:
  * Without this token, authentication inside an iframe may fail due to browser and sandbox restrictions.
  * The token enables seamless single sign-on (SSO)-like behavior.

**Security Warning**

* ❌ **Do NOT include this parameter** in links that are shared externally (e.g., via email).
  * The token is user-specific and sensitive.
  * Sharing it could allow others to impersonate the authenticated user.

**Fallback Behavior**

* If no authentication token is provided:
  * The user may be directed to a default or different tenant.
  * Your application should support tenant switching to handle this case.

</details>

<details>

<summary>exa-plugin-context</summary>

This parameter provides contextual information to Raptor about the target record or dataset.

**Supported Content**

* Target record identifiers
* Tags
* Filters
* Other contextual metadata

This allows Raptor to open with the correct data and preconfigured state.

</details>

<details>

<summary>tenant-id</summary>

This parameter can be used to define the entended raptor tenant in case no exa-auth-plugin parameter is present. The reason for this is that without an explicit token the user has to login with his personal account, and we do not (yet) know what tenant is being targeted. So the user would end up in his or her default tenant. This could be a different tenant then the one the link was intended for. And that coud cause problems when we then resolve a context tag.

Technically this is optional, but you should always have one or the other in the URL.

If you have both a plugin auth token, and the tenant id set, both should reference the same tenant.

</details>

Example on how to create the url:

```javascript
//1. The external system token (see /api/user/getusertoken)
var authToken = "xxxxx"; 
var tenantId = "xxxxxxx-xxxx-xxxx-xxxxxx";

//2.The business context
//Use parameters "source", "type", "fields" and "legalEntity" to resolve a context tag
//using entity configuration (see /api/integration/resolvecontext)

//Use the "options" to toggle various options when embedding Raptor

//Use the "documentFilter" to preload Raptor using a fixed query

var context = { 
   "tenantId": tenantId ,
   "source": "D365-FO",
   "type": "VENDVENDORV2ENTITY",
   "fields": {
      "VENDORACCOUNTNUMBER": "V00001",
      "VENDORORGANIZATIONNAME": "Spotmeyer's Furnishings"
   },
   "options": {
      "mode": undefined, //use "compact" for compact mode
      "disable-context-detach": false,
      "disable-upload": false,
      "disable-download": false,
      "disable-view": false,
      "disable-email": false,
      "disable-copy": false,
      "disable-delete": false,
      "disable-external-src": false,
      "disable-documenttriggers": false,
      "disable-tenantname": false,
      "disable-useroptions": false,
      "disable-search-bar": false,
      "readonly-mode": false
   },
   "documentFilter": {
      "name": "My documents",
      "query": { "operator":"document.uploader.self" }
   }
};

var url = new URL('https://raptor.9altitudes.com')
url.searchParams.append('exa-plugin-context', JSON.stringify(context));
url.searchParams.append('exa-auth-plugin', authToken);
url.searchParams.append('tenant-id', tenantId );

url.toString();
```

