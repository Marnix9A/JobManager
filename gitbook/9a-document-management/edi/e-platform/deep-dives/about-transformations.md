# About Transformations

## General

Transformations are typically linked to an endpoint, and will transform the input into a message that will be send. Transformations can be chained, and are optional. (So instead of using NONE you can just not provide 0 transformations.)

Enumerations required for configuration:\
`0: NONE`\
[`1: XSLT`<br>](about-transformations.md#xslt)`2: DLL (obsolete)`\
[`3: XML to JSON`<br>](about-transformations.md#to-json)[`4: JSON to XML`](about-transformations.md#to-xml)

Technically at most 3 transformations should be required to create almost any reasonable result. (`TO XML` -> `XSLT` -> `TO JSON`) However it could be a good idea to chain multiple XSLT transformations. For example the first XSLT could just be the version from the D9A kit, followed by a second transformation that holds customer specific changes. This has 2 big advantages: 1) it is clear what the customizations are; and 2) it allows to upgrade the D9A transformation if a new version is available without having to redo the customizations to it. There is however also a drawback; only data that is still available in the output from the first XSLT can still be used in the 2nd XSLT.

## XSLT

The most important transformation is the XSLT because it allows custom logic.\
Only XSLT version 1.0 is supportd.

The code for this transformation = 1

A simple example of an XSLT would be:

{% tabs %}
{% tab title="XSLT" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
	<xsl:output method="xml" encoding="UTF-8" omit-xml-declaration="no" indent="yes" />
	<!-- 
	Created by: 9Altitudes 
	
	History:
	15/03/2023 XXX Initial Version
	
	Notes:
	Used for: demo purpose / documentation
	-->
	<xsl:variable name="smallCase" select="'abcdefghijklmnopqrstuvwxyz'"/>
	<xsl:variable name="upperCase" select="'ABCDEFGHIJKLMNOPQRSTUVWXYZ'"/>

	<xsl:template match="/book">
		<output>
			<name>
				<xsl:value-of select="author/firstName"/>
				<xsl:text> </xsl:text>
				<xsl:value-of select="translate(./author/familyName, $smallCase, $upperCase)"/>
			</name>
			<description>Transformed output.</description>
		</output>
	</xsl:template>

</xsl:stylesheet>
```
{% endtab %}

{% tab title="Input" %}
```xml
<book>
	<author>
		<firstName>Yuval</firstName>
		<firstName>Noah</firstName>
		<familyName>Harari</familyName>
	</author>
	<title>Sapiens: A brief history of humankind</title>
	<releaseDate>10-02-2015</releaseDate>
	<isbn>9780062316097</isbn>
</book>
```
{% endtab %}

{% tab title="Result" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<output>
  <name>Yuval HARARI</name>
  <description>Transformed output.</description>
</output>
```
{% endtab %}
{% endtabs %}

This example converted an input to a different format. Note that the transformation can only add fixed "extra" data, but can not invent data. So all the real data should either come from the input, or be encoded in the XSLT itself.

### Special Functions

There are a few helper functions available that assist with problems that are difficult to solve with the XSLT 1.0 functions available. List of currently available functions:

In namespace `e-platform:helpers/v1`

* `Increment()`\
  Returns a new number every time it is called. Incrementing the previous number with 1.
* `Increment('<<counter>>')`\
  Creates a "counter" with key <\<counter>> and returns an incremented value each time it is called.
* `GetCounterValue('<<counter>>')`\
  Returns the current value of the counter with name <\<counter>>.

To use a special function the namespace must be referenced in an xmlns:xxx="namespace" attribute at the top of the file. See the example below that creates a "scripts" which is then used to call the functions.

{% tabs %}
{% tab title="XSLT" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet
  xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0"
  xmlns:scripts="e-platform:helpers/v1"
  >
  <xsl:output method="xml" encoding="UTF-8" omit-xml-declaration="no" indent="yes"/>

  <xsl:template match="/">
    <TRANSFORMATION-RESULT>
      <xsl:call-template name="TestCounter"/>
    </TRANSFORMATION-RESULT>
  </xsl:template>

  <xsl:template name="TestCounter">
    <TEST-COUNTER>
      <xsl:choose>
        <xsl:when test="function-available('scripts:Increment')">
          <invoke method="Increment()">
            <result expect="1">
              <xsl:value-of select="scripts:Increment()"/>
            </result>
          </invoke>
          <invoke method="Increment()">
            <result expect="2">
              <xsl:value-of select="scripts:Increment()"/>
            </result>
          </invoke>
          <invoke method="Increment('')">
            <result expect="3">
              <xsl:value-of select="scripts:Increment('')"/>
            </result>
          </invoke>
          <invoke method="GetCounterValue('')">
            <result expect="3">
              <xsl:value-of select="scripts:GetCounterValue('')"/>
            </result>
          </invoke>
          <invoke method="Increment('XX')">
            <result expect="1">
              <xsl:value-of select="scripts:Increment('XX')"/>
            </result>
          </invoke>
          <invoke method="GetCounterValue('XX')">
            <result expect="1">
              <xsl:value-of select="scripts:GetCounterValue('XX')"/>
            </result>
          </invoke>
          <invoke method="GetCounterValue('YY')">
            <result expect="0">
              <xsl:value-of select="scripts:GetCounterValue('YY')"/>
            </result>
          </invoke>
        </xsl:when>
        <xsl:otherwise>
          <xsl:text>FAILURE: Script "e-platform:helpers/v1:Increment()" is not available.</xsl:text>
        </xsl:otherwise>
      </xsl:choose>
    </TEST-COUNTER>
  </xsl:template>
</xsl:stylesheet>

```
{% endtab %}

{% tab title="Input" %}
```
<root></root>
```
{% endtab %}

{% tab title="Result" %}
```xml
<TRANSFORMATION-RESULT>
  <TEST-COUNTER>
    <invoke method="Increment()">
      <result expect="1">1</result>
    </invoke>
    <invoke method="Increment('')">
      <result expect="2">2</result>
    </invoke>
    <invoke method="Increment('')">
      <result expect="3">3</result>
    </invoke>
    <invoke method="GetCounterValue('')">
      <result expect="3">3</result>
    </invoke>
    <invoke method="Increment('XX')">
      <result expect="1">1</result>
    </invoke>
    <invoke method="GetCounterValue('XX')">
      <result expect="1">1</result>
    </invoke>
    <invoke method="GetCounterValue('YY')">
      <result expect="0">0</result>
    </invoke>
  </TEST-COUNTER>  
</TRANSFORMATION-RESULT>
```
{% endtab %}
{% endtabs %}

In namespace: e-platform:core-integration/v1

* HasSagaId\
  Indicates if a saga id is available, and the result of other saga related functions can be used.
* GetSagaId\
  Returns the saga id related to the current messag.
* StoreSagaParameter('<\<name>>', '<\<value>>')\
  Sets the value of a saga parameter. The variable is automatically created if it did not yet exist.

Example

{% tabs %}
{% tab title="XSLT" %}
<pre class="language-xml"><code class="lang-xml">&#x3C;?xml version="1.0" encoding="utf-8"?>
&#x3C;xsl:stylesheet
  xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0"
  xmlns:<a data-footnote-ref href="#user-content-fn-1">core-integration</a>="<a data-footnote-ref href="#user-content-fn-2">e-platform:core-integration/v1</a>"
  >
  &#x3C;xsl:output method="xml" encoding="UTF-8" omit-xml-declaration="no" indent="yes"/>

  &#x3C;xsl:template match="/">
    &#x3C;TRANSFORMATION-RESULT>
      &#x3C;xsl:call-template name="TestSagaVariables"/>
    &#x3C;/TRANSFORMATION-RESULT>
  &#x3C;/xsl:template>

  &#x3C;xsl:template name="TestSagaVariables">
    &#x3C;TEST-SAGA-VARIABLES>
      &#x3C;xsl:variable name="sagavar-value" select="'example'" />
      &#x3C;xsl:choose>
        &#x3C;xsl:when test="function-available('core-integration:HasSagaId')">
          &#x3C;SagaId>
            &#x3C;xsl:attribute name="hasSagaId">
              &#x3C;xsl:value-of select="<a data-footnote-ref href="#user-content-fn-3">core-integration</a>:<a data-footnote-ref href="#user-content-fn-4">HasSagaId</a>()"/>
            &#x3C;/xsl:attribute>
            &#x3C;xsl:value-of select="core-integration:GetSagaId()"/>
          &#x3C;/SagaId>
          &#x3C;StoredSagaParameter>
            &#x3C;name>selfcheck-param&#x3C;/name>
            &#x3C;value>
              &#x3C;xsl:value-of select="$sagavar-value"/>
            &#x3C;/value>
            &#x3C;result>
              &#x3C;xsl:value-of select="core-integration:StoreSagaParameter('selfcheck-param', $sagavar-value)"/>
            &#x3C;/result>
          &#x3C;/StoredSagaParameter>
        &#x3C;/xsl:when>
        &#x3C;xsl:otherwise>
          &#x3C;xsl:text>FAILURE: Script "e-platform:core-integration/v1:HasSagaId()" is not available.&#x3C;/xsl:text>
        &#x3C;/xsl:otherwise>
      &#x3C;/xsl:choose>
    &#x3C;/TEST-SAGA-VARIABLES>
  &#x3C;/xsl:template>
&#x3C;/xsl:stylesheet>

</code></pre>
{% endtab %}

{% tab title="Input" %}
```xml
<root></root>
```
{% endtab %}

{% tab title="Result" %}
```xml
<TRANSFORMATION-RESULT>
  <TEST-SAGA-VARIABLES>
    <SagaId hasSagaId="true">7c9e6679-7425-40de-944b-e07fc1f90ae7</SagaId>
    <StoredSagaParameter>
      <name>selfcheck-param</name>
      <value>example</value>
      <result>true</result>
    </StoredSagaParameter>
  </TEST-SAGA-VARIABLES>
</TRANSFORMATION-RESULT>
```
{% endtab %}
{% endtabs %}

### To JSON

This transformation can be used if the input message, or the output of the previous stage in the transformation chain is an XML, and it has to be converted to a JSON object.

One special case is to be mentioned, output that should be transformed to a number must be indicated as such by wrapping the number in \`TONUMBER(...)\` text.

{% tabs %}
{% tab title="Input" %}
```xml
<author>
  <name>Yuval Noah Harari</name>
  <date>10-02-2015</date>
  <books>TONUMBER(10)</books>
  <numberZero>TONUMBER(000.00)</numberZero>
  <numberText>1234.5<numberText>
</author>
```
{% endtab %}

{% tab title="Output" %}
```json
{
  "name": "Yuval Noah Harari",
  "date": "10-02-2015",
  "books": 10,
  "numberZero": 0,
  "numberText": "1234.5"
}
```
{% endtab %}
{% endtabs %}

### To XML

Converts a json object into an XML structure.

Example

{% tabs %}
{% tab title="Input" %}
```json
{
  "name": "Yuval Noah Harari",
  "date": "10-02-2015",
  "books": 10,
  "numberZero": 0,
  "numberText": "1234.5"
}
```
{% endtab %}

{% tab title="Output" %}
```xml
<root>
  <name>Yuval Noah Harari</name>
  <date>10-02-2015</date>
  <books>10</books>
  <numberZero>0</numberZero>
  <numberText>1234.5</numberText>
</root>
```
{% endtab %}
{% endtabs %}

[^1]: This is an alias which you can choose; as long as it is unique within the transformation.

[^2]: The namespace. Fixed value.

[^3]: Name of the alias.

[^4]: Name of the function.
