# MCP Server

## What is an MCP Server?

An **MCP (Model Context Protocol) Server** enables AI assistants and agents to securely interact with external systems through a standardised interface. Instead of requiring separate integrations for each AI platform, an MCP server exposes capabilities such as searching documents, retrieving data, executing actions, and interacting with business applications in a consistent manner.

For Raptor Document Management, the MCP Server enables compatible AI assistants and agents to access documents, manage metadata and templates, and interact with document management functionality while respecting the security permissions of the authenticated user.

#### Benefits

* Standard integration with modern AI assistants and agents
* Secure authentication and authorisation
* Direct access to document management capabilities from AI-powered tools
* Reduced need for custom integrations
* Consistent experience across different AI platforms

## Connection

Raptor Document Management provides an HTTP-based MCP Server that can be used to connect compatible AI assistants and agents.

<table data-header-hidden><thead><tr><th width="139.45458984375"></th><th></th></tr></thead><tbody><tr><td>Primary</td><td><a href="https://raptor.9altitudes.com/mcpservice/mcp">https://raptor.9altitudes.com/mcpservice/mcp</a></td></tr><tr><td>Alternative</td><td><a href="https://raptor.9altitudes.com/mcpservice/mcp-token">https://raptor.9altitudes.com/mcpservice/mcp-token</a></td></tr></tbody></table>

{% hint style="info" %}
Before the MCP Server can access your Raptor tenant, you have to enable the MCP Server. This can be done either in read only mode, or as full access.\
[https://raptor.9altitudes.com/configuration/tenant-settings](https://raptor-dev.adultimagroup.com/configuration/tenant-settings)

<p align="center"><br><img src="../.gitbook/assets/image (729).png" alt="" data-size="original"></p>

In **Read Only** mode the MCP Server will not allow any AI agent to make changes in your raptor tenant, this is a safe way to activate AI capabilities without risk.

In **Full Access** mode, the agent can do whatever the user can do.
{% endhint %}

{% hint style="info" %}
Required User Rights

You can limit the users who can use the MCP Server tools via roles. Add the _Use MCP Server data tools_ setting. Also note that Administrators can always do everything, that includes using MCP servers.

<p align="center"><img src="../.gitbook/assets/image (730).png" alt=""></p>
{% endhint %}

### Authentication

The Raptor MCP Server supports two authentication methods

<details>

<summary>OAuth 2.0 (recommended)</summary>

The primary endpoint uses OAuth 2.0 authentication. Compatible MCP clients will guide users through an interactive sign-in process. Access is granted using the permissions of the authenticated Raptor user.

{% hint style="warning" %}
when authenticating to a MCP server using OAuth all tenants linked to that user are accessible to the agent. It is the responsibility of the agent to make sure it connects to the correct tenant before calling any other tool.

Whenever for any reason a session is stopped and re-created, the agent is responsible to re-verify, and if needed switch again to the correct tenant. This could potentially happen during an active session if for example the session timeout is reached, and the server closed the session.
{% endhint %}

</details>

<details>

<summary>Access Token Authentication</summary>

The alternative endpoint supports token-based authentication. This option is primarily intended for environments where interactive sign-in is not available.\
All actions performed through the MCP Server are executed using the permissions associated with the authenticated user or access token.

Create the token via the procedure explained [here](https://app.gitbook.com/o/bqSIsQqz4U4PqAwwBN3A/s/Kfypi8e8luNHtfjQhy6p/~/edit/~/changes/270/developers/api-starting-guide#external-system-authentication). \
Then add the resulting token in a header with name: **exa-auth-plugin**

</details>

## Capabilities

The Raptor MCP Server provides access to the most commonly used document management functionality available to end users.

Supported capabilities include:

* Searching and retrieving documents
* Uploading and downloading documents
* Viewing document metadata
* Assigning and removing tags
* Assigning and removing templates
* Updating metadata fields
* Accessing document contents for AI-assisted processing

Administrative functionality is currently not exposed through the MCP Server. This includes configuration management, tenant administration, and other system-level operations.

### Available Tools

#### General tools

<details>

<summary><strong>Who Am I</strong></summary>

This tool returns information about the currently authenticated user and the active tenant.

For OAuth-based sessions, we strongly recommend that agents call this tool before performing any actions. This allows the agent to verify that it is connected to the expected tenant and operating under the correct user context.

When assigning tasks to an agent, consider providing the expected tenant name as part of the instructions. The agent can then use this tool to validate that it is connected to the correct environment before continuing.

For long-running sessions, it may be advisable to call this tool periodically. Some agent hosts may restart or reinitialise sessions automatically, potentially resulting in a different active context.

</details>

<details>

<summary><strong>Switch Tenant</strong></summary>

This tool lists the tenants available to the currently authenticated user and allows the active tenant to be changed.

It is typically used when the Who Am I tool indicates that the agent is connected to the wrong tenant, or when the user needs to work with a different tenant.

After switching tenants, it is recommended to run the Who Am I tool again to verify that the correct tenant is now active. Guidance for this verification step is also included in the tool response.

</details>

<details>

<summary><strong>Help</strong></summary>

This tool provides information about the tools available on the MCP Server, including detailed usage guidance and parameter descriptions.

Some MCP clients expose only a subset of available tools directly to the AI model. By using the Help tool, an agent can discover the full set of capabilities available through the server and obtain additional guidance on how individual tools should be used.

For complex workflows, it is often beneficial to instruct the agent to use this tool at the start of a session to familiarise itself with the available functionality.

</details>

<details>

<summary><strong>Run System Command</strong></summary>

This tool provides access to specialised system functions that support specific workflows within the MCP Server.

In most cases, agents should only use this tool when explicitly instructed to do so by another MCP tool. For example, a document search result may include guidance to execute a specific system command in order to retrieve additional information or perform a follow-up action.

The available system functions are intentionally exposed through this mechanism rather than being presented as standalone tools. This simplifies tool discovery, reduces the amount of context that must be provided to the agent, and helps ensure compatibility across a broad range of MCP clients and AI models.

Agents should not attempt to invoke this tool without explicit instructions on which system function to execute and which parameters to provide.

</details>

#### Document related tools

<details>

<summary><strong>Search Documents</strong></summary>

This tool accepts a natural language search request, similar to the search experience provided by the Copilot functionality within the Raptor user interface.

The search request is automatically translated into one or more document queries and executed against the document repository. The tool returns the matching documents, together with the total number of matching results.

When additional matching documents are available, paging information is included so that subsequent result pages can be retrieved.

{% hint style="info" %}
Search requests are interpreted using AI-assisted query generation. As a result, the same search terms may occasionally produce slightly different queries and therefore different results.

For example, a search for "invoices" may be interpreted as a search for documents tagged as sales or purchase invoices, while in another session it may be interpreted as a search for documents based on an invoice template. Both interpretations may be valid depending on the context provided to the AI model.
{% endhint %}

{% hint style="info" %}
To ensure a responsive experience and minimise token consumption, only a subset of matching results is returned initially. Additional result pages can be retrieved using the paging information included in the response. When additional pages are available, the response may include instructions to use the _Run System Command_ tool to retrieve subsequent results.
{% endhint %}

</details>

<details>

<summary><strong>File Upload</strong></summary>

This tool supports multiple methods of creating documents within Raptor Document Management. The most appropriate upload method depends on the capabilities available to the MCP client and AI agent.

**Direct File Upload**\
The preferred upload method is a direct file upload. When requested, the tool generates a one-time upload token and provides an endpoint to which the file can be uploaded using an HTTP POST request.

This method requires that the agent or MCP client is capable of performing HTTP requests. Depending on the network environment, the Raptor service endpoint may need to be added to an allowlist.

**URL-Based Upload**\
For documents that are already available online, a URL can be provided instead of uploading the file directly.\
Raptor will create a document record and store the provided URL as an external document reference.

**Text-Based Upload**\
As a fallback mechanism, text-based documents can be uploaded by providing their content directly through the MCP protocol.\
This option is primarily intended for smaller text-based files and scenarios where neither direct file uploads nor URL-based uploads are available.

{% hint style="warning" %}
Text-based uploads require the complete file contents to be transmitted through the MCP protocol. This can consume a significant number of tokens and is therefore recommended only for smaller text-based documents, such as simple XML files or UBL documents without embedded attachments.\
Whenever possible, Direct File Upload or URL-Based Upload should be preferred over Text-Based Upload.
{% endhint %}

</details>

<details>

<summary><strong>Download File</strong></summary>

This tool allows agents to download documents stored in Raptor Document Management.

The tool returns a unique, single-use download URL for the requested document. To retrieve the file, the agent or MCP client must perform a separate HTTP GET request against the provided URL.

{% hint style="info" %}
Downloading documents requires support for outbound HTTP requests. Agents or MCP clients that cannot perform HTTP GET requests will not be able to download document contents through this mechanism.
{% endhint %}

</details>

<details>

<summary><strong>OCR Document</strong> <em>(limited)</em></summary>

This tool extracts text from supported text-based documents, allowing AI agents to access document contents without downloading the original file.

For certain file formats, such as XML and UBL documents, additional processing may be performed to remove large embedded data sections that are not typically useful for AI processing, such as Base64-encoded attachments.

This tool can be particularly useful in environments where agents are unable to download documents directly due to network restrictions or limited HTTP capabilities.

{% hint style="info" %}
At present, this tool is primarily intended for text-based document formats. Support for OCR and text extraction from additional document types, such as PDF files and scanned documents, is planned for a future release.
{% endhint %}

</details>

#### Metadata related tools

<details>

<summary><strong>Search Tags</strong></summary>

This tool allows agents to search for tags within Raptor Document Management.

Tags can be located by name, or by navigating the tag hierarchy starting from the available root tags. The behaviour is similar to the tag selection experience available in the Raptor user interface.

</details>

<details>

<summary><strong>Assign Tag to Document</strong></summary>

This tool allows tags to be assigned to or removed from a document.

It is commonly used in combination with the **Search Documents**, **Upload File**, and **Search Tags** tools.

</details>

<details>

<summary><strong>Get Templates</strong></summary>

This tool returns the templates available within the current tenant.

In addition to listing available templates, the tool can provide detailed information about individual templates, including the metadata fields defined by the template.

</details>

<details>

<summary><strong>Assign or Remove Template</strong></summary>

This tool allows templates to be assigned to or removed from a document.

It is typically used together with the **Get Templates** tool to locate the desired template and the **Search Documents** or **Upload File** tools to identify the target document.

</details>

<details>

<summary><strong>Set Document Field</strong></summary>

This tool allows metadata fields to be added or updated on a document.

Fields that are part of an assigned template can be updated, as well as other supported metadata fields.

Example:

> Set the **Due Date** field on document _XXXX_ to _2029-12-31_.

</details>

## FAQ

<details>

<summary>My agent only accepts STDIO servers</summary>

Some AI agents and MCP clients only support MCP servers that communicate through STDIO and do not support direct HTTP-based MCP connections.

In these scenarios, a bridge or proxy can be used to expose the Raptor MCP Server as an STDIO-compatible MCP server. One commonly used solution is **mcp-remote**, which acts as an intermediary between an HTTP-based MCP server and an STDIO-based MCP client.

Project:

* [mcp-remote on GitHub](https://github.com/geelen/mcp-remote)

Please refer to the documentation of your MCP client for instructions on configuring external MCP servers and STDIO bridges.

{% hint style="info" %}
**Authentication considerations**

When using OAuth authentication through a bridge such as _mcp-remote_, a browser window may be opened during the initial connection or whenever an authentication token has expired.

The sign-in process can take several seconds to complete. Some MCP clients may incorrectly assume that the MCP Server is unavailable if the connection is not established immediately.

If this occurs, complete the sign-in process and restart the MCP client or AI agent. In most cases the authentication token will be stored and reused for future connections, allowing subsequent initialisation attempts to succeed without requiring another sign-in.
{% endhint %}

</details>

<details>

<summary>My agent supports OAuth 2.0, but the connection still fails</summary>

The Raptor MCP Server uses OAuth 2.0 with Dynamic Client Registration (DCR), which is the recommended authentication approach for HTTP-based MCP servers.

Although support for this protocol is becoming increasingly common, MCP client implementations vary and not all clients support every aspect of the specification. As a result, compatibility issues may occasionally occur even when a client advertises support for OAuth 2.0 authentication.

Raptor aims to follow the relevant MCP and OAuth specifications as closely as possible. However, compatibility with every MCP client or AI agent cannot be guaranteed.

If you encounter authentication or connection issues, please contact us at **support@9altitudes.com** and include:

* The name and version of the MCP client or AI agent
* Any relevant error messages
* Details about the authentication method being used

We will investigate whether the issue can be resolved through configuration changes or product improvements. Please note that in some cases, client-specific workarounds may not be feasible if they would negatively impact compatibility with other MCP clients.

</details>

