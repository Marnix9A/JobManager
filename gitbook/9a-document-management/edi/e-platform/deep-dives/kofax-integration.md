# Kofax integration

The kofax integration allows easy configuration of some advanced tasks that would otherwise require multiple calls and endpoints. + It is the only way to send documents to the raptor document warehouse from inside E-Platform.

## Basic configuration

Configuration is done via a JSON object:

<pre class="language-json"><code class="lang-json">{
    "SourceEndpoint": <a data-footnote-ref href="#user-content-fn-1">111</a>,
    "RaptorConfig":{
        "ApiGatewayUrl": "<a data-footnote-ref href="#user-content-fn-2">https://raptor.adultimagroup.com/apigateway</a>",
        "ExternalSystemId": "<a data-footnote-ref href="#user-content-fn-3">7c9e6679-7425-40de-944b-e07fc1f90ae7</a>",
        "Secret": "<a data-footnote-ref href="#user-content-fn-4">xxxxx</a>",
        "RunAs": "<a data-footnote-ref href="#user-content-fn-5">SYSTEM</a>"
    },
    "UploadStage": {
        "ResponseEndpointId": <a data-footnote-ref href="#user-content-fn-6">112</a>,
        "<a data-footnote-ref href="#user-content-fn-7">tags</a>": [
            "<a data-footnote-ref href="#user-content-fn-8">0f8fad5b-d9cb-469f-a165-70867728950e</a>",
            ...
        ]
    },
    "EnrichStage": {
        "ResponseEndpointId": <a data-footnote-ref href="#user-content-fn-9">113</a>,
        "<a data-footnote-ref href="#user-content-fn-10">AfterEndpoints</a>": [<a data-footnote-ref href="#user-content-fn-11">112</a>, <a data-footnote-ref href="#user-content-fn-12">115</a>]
        "<a data-footnote-ref href="#user-content-fn-13">TagTransformations</a>": [
            { "TransformationId": <a data-footnote-ref href="#user-content-fn-14">10</a>, "Source": <a data-footnote-ref href="#user-content-fn-15">115</a> },
            {
              "TransformationId": 11,
              "<a data-footnote-ref href="#user-content-fn-16">sources</a>": [
                { "EndpointId": <a data-footnote-ref href="#user-content-fn-17">115</a>, "Key": "<a data-footnote-ref href="#user-content-fn-18">header</a>" },
                { "EndpointId": 111, "Key": "kofax" }
              ]
            }
        ],
        "<a data-footnote-ref href="#user-content-fn-19">Templates</a>": [
            { "code": "<a data-footnote-ref href="#user-content-fn-20">purchase\\invoice</a>" }
        ],
        "<a data-footnote-ref href="#user-content-fn-21">Fields</a>": [
            { "<a data-footnote-ref href="#user-content-fn-22">code</a>": "comments" }
        ]
    }
}
</code></pre>

Example of responses made available in the response endpoints:

{% tabs %}
{% tab title="Upload Stage" %}
```xml
<UploadStage sagaId="4cb6d94e-0000-0000-0000-000000000000">
  <DocumentId>c7f45dc6-0000-0000-0000-000000000000</DocumentId>
  <Tags />
</UploadStage>
```
{% endtab %}

{% tab title="Enrich Stage" %}
```xml
<EnrichStage sagaId="4cb6d94e-0000-0000-0000-000000000000">
  <Tags>
    <Tag id="9ba4150e-0000-0000-0000-0000000000000000" linked="true" />
  </Tags>
  <Templates>
    <Template id="a41f127b-0000-0000-0000-000000000000" />
  </Templates>
  <Fields />
  <Messages />
</EnrichStage>
```
{% endtab %}
{% endtabs %}

Example of a tag transformation:

{% tabs %}
{% tab title="Input" %}
Note: this example contains a multi source input; from endpoints 57 & 60

```xml
<root>
  <source type="xml" isNull="false" key="input" endpoint="57">
    <Kofax>
      <Batches xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
        <Batch>
          <Id>a2eb46b512f340ef81461aac0bfbfef5</Id>
        </Batch>
      </Batches>
    </Kofax>
  </source>
  <source type="xml" isNull="false" key="upload-stage" endpoint="60">
    <UploadStage sagaId="4cb6d94e-0000-0000-0000-000000000000">
      <DocumentId>DOCX</DocumentId>
      <Tags>
        <Tag id="5a23845d-0000-0000-0000-000000000000" />
        <Tag id="7f5dc63b-0000-0000-0000-000000000000" />
        <Tag id="c7f45ddd-0000-0000-0000-000000000000" />
      </Tags>
    </UploadStage>
  </source>
</root>
```
{% endtab %}

{% tab title="Transformation" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:output method="xml" encoding="UTF-8" omit-xml-declaration="no" indent="yes"/>

  <xsl:template match="/">
    <Root>
      <entityName>EXAMPLE</entityName>
      <legalEntity>NONE</legalEntity>
      <source>E-PLATFORM</source>
      <fields>
        <xsl:variable name="batchId">
          <xsl:value-of select="/root/source[@key='input']/Kofax/Batches/Batch/Id"/>
        </xsl:variable>
        <xsl:variable name="numberOfSources">
          <xsl:value-of select="count(/root/source[@key])"/>
        </xsl:variable>
        <STATUS>
          <xsl:choose>
            <xsl:when test="$batchId != '' and $numberOfSources &gt; 1">
              <xsl:text>SUCCESS</xsl:text>
            </xsl:when>
            <xsl:otherwise>
              <xsl:text>FAILURE</xsl:text>
            </xsl:otherwise>
          </xsl:choose>
        </STATUS>
        <TEST>MULTI-SOURCE-TAG-TRANSFORM</TEST>
      </fields>
    </Root>
  </xsl:template>
</xsl:stylesheet>

```
{% endtab %}

{% tab title="Result" %}
```xml
<Root>
  <entityName>EXAMPLE</entityName>
  <legalEntity>NONE</legalEntity>
  <source>E-PLATFORM</source>
  <fields>
    <STATUS>SUCCESS</STATUS>
    <TEST>MULTI-SOURCE-TAG-TRANSFORM</TEST>
  </fields>
</Root>
```

And as json:

```json
{
    "entityName": "EXAMPLE",
    "legalEntity": "NONE",
    "source": "E-PLATFORM",
    "fields": {
        "STATUS": "SUCCESS",
        "TEST": "MULTI-SOURCE-TAG-TRANSFORM"
    }
}
```
{% endtab %}

{% tab title="Entity Config" %}

{% endtab %}
{% endtabs %}

[^1]: ID of the input endpoint that receives the data from kofax. (triggered by a document export)\
    This is the official "kick off" for the Kofax Integration.

[^2]: The Api Gateway that should be used to communicate with the document warehouse. This will only differ from the example value if the documents should be send to an internal test environment.

[^3]: ID of the external system in the document warehouse. Create a new one for "E-Platform" if it does not yet exist.

[^4]: Secret linked to the external system id.

[^5]: The "External User Name" of a user linked to the external system. Typically a system account.

[^6]: Id of an endpoint where details of the upload will be placed in. These can be used by other endpoints for example to get the document Id, or to delay execution untill the document is uploaded in the warehouse.

[^7]: optional; allows to add fixed tags to a document during while uploading the document. For example a tag "Processing" could be added.

[^8]: Id of a tag. Multiple ids can be added.

[^9]: Id of an endpoint where details of the enrich stage will be placed in. Can be used by other endpoints for example to get the details of actions performed; or to wait for all the tags & templates to be added on the document.

[^10]: Defines which endpoints must have finished before starting the enrichment stage. Can be important if data is required from other calls that may not have finished yet.

[^11]: In this case the enrichment stage has explicitly stated that the document must be uploaded before it can be enriched.

[^12]: The tag transformation uses the output of endpoint 115, so it the enrichment stage can not start before this output is available.

[^13]: optional; if used each tag transformation must result in a valid body for the 'Resolve Context" call in the api gateway. This call can create or return the id of a tag if there is a matching entity configuration.

[^14]: The (first) transformation to run. Note that multiple transformations can be chained. This by setting the "Next Transformation" on the transformation definition itself.

[^15]: Runs the transformation on the "output" of this endpoint.

[^16]: Multiple sources can be used as well. Sources are combined in the same way that they would for endpoints that have configured multiple sources.

[^17]: Define the ID of the endpoint

[^18]: Define a unique key for the endpoint.

[^19]: optional; allows to define a template which should be added to the uploaded document. Note: only one template can be configured.

[^20]: The code of the template to assign to the document.

[^21]: Optional; allows to add fields (without value) to a document. Note that fields which are part of the template are already added.

[^22]: Fields are added by code.
