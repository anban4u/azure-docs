---
title: Azure API Management transformation policies | Microsoft Docs
description: Learn about the transformation policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''

ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
---
# API Management transformation policies
This topic provides a reference for the following API Management policies. For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a> Transformation policies  
  
-   [Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.  
  
-   [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.  
  
-   [Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.  
  
-   [Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.  
  
-   [Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.  
  
-   [Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.  
  
-   [Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.  
  
-   [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.  
  
-   [Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.  
  
-   [Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.  
  
##  <a name="ConvertJSONtoXML"></a> Convert JSON to XML  
 The `json-to-xml` policy converts a request or response body from JSON to XML.  
  
### Policy statement  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### Example  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|json-to-xml|Root element.|Yes|  
  
### Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|apply|The attribute must be set to one of the following values.<br /><br /> -   always - always apply conversion.<br />-   content-type-json - convert only if response Content-Type header indicates presence of JSON.|Yes|N/A|  
|consider-accept-header|The attribute must be set to one of the following values.<br /><br /> -   true - apply conversion if JSON is requested in request Accept header.<br />-   false -always apply conversion.|No|true|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound, on-error  
  
-   **Policy scopes:** global, product, API, operation  
  
##  <a name="ConvertXMLtoJSON"></a> Convert XML to JSON  
 The `xml-to-json` policy converts a request or response body from XML to JSON. This policy can be used to modernize APIs based on XML-only backend web services.  
  
### Policy statement  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### Example  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|xml-to-json|Root element.|Yes|  
  
### Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|kind|The attribute must be set to one of the following values.<br /><br /> -   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.<br />-   direct - the converted JSON reflects the original XML document's structure.|Yes|N/A|  
|apply|The attribute must be set to one of the following values.<br /><br /> -   always - convert always.<br />-   content-type-xml - convert only if response Content-Type header indicates presence of XML.|Yes|N/A|  
|consider-accept-header|The attribute must be set to one of the following values.<br /><br /> -   true - apply conversion if XML is requested in request Accept header.<br />-   false -always apply conversion.|No|true|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound, on-error  
  
-   **Policy scopes:** global, product, API, operation  
  
##  <a name="Findandreplacestringinbody"></a> Find and replace string in body  
 The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.  
  
### Policy statement  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### Example  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|find-and-replace|Root element.|Yes|  
  
### Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|from|The string to search for.|Yes|N/A|  
|to|The replacement string. Specify a zero length replacement string to remove the search string.|Yes|N/A|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound, backend, on-error  
  
-   **Policy scopes:** global, product, API, operation  
  
##  <a name="MaskURLSContent"></a> Mask URLs in content  
 The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway. Use in the outbound section to re-write response body links to make them point to the gateway. Use in the inbound section for an opposite effect.  
  
> [!NOTE]
>  This policy does not change any header values such as `Location` headers. To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.  
  
### Policy statement  
  
```xml  
<redirect-content-urls />  
```  
  
### Example  
  
```xml  
<redirect-content-urls />  
```  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|redirect-content-urls|Root element.|Yes|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound  
  
-   **Policy scopes:** global, product, API, operation  
  
##  <a name="SetBackendService"></a> Set backend service  
 Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation. This policy changes the backend service base URL of the incoming request to the one specified in the policy.  
  
### Policy statement  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### Example  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
 In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.  
  
 Initially the backend service base URL is derived from the API settings. So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.  
  
 When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter. For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
 If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used. For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|set-backend-service|Root element.|Yes|  
  
### Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|base-url|New backend service base URL.|Yes|N/A|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, backend  
  
-   **Policy scopes:** global, product, API, operation  
  
##  <a name="SetBody"></a> Set body  
 Use the `set-body` policy to set the message body for incoming and outgoing requests. To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.  
  
> [!IMPORTANT]
>  Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression. To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message. If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.  
>   
>  Please note the following considerations when using the `set-body` policy.  
>   
>  -   If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.  
> -   Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.  
> -   Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.  
> -   If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.  
  
 For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.  
  
### Policy statement  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### Examples  
  
#### Literal text example  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### Example accessing the body as a string  
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### Example accessing the body as a JObject  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### Filter response based on product  
 This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product. For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30. Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|set-body|Root element. Contains the body text or an expressions that returns a body.|Yes|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound, backend  
  
-   **Policy scopes:** global, product, API, operation  
  
##  <a name="SetHTTPheader"></a> Set HTTP header  
 The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.  
  
 Inserts a list of HTTP headers into an HTTP message. When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service. When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.  
  
### Policy statement  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### Examples  
  
#### Example  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### Forward context information to the backend service  
 This example shows how to apply policy at the API level to supply context information to the backend service. For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30. At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|set-header|Root element.|Yes|  
|value|Specifies the value of the header to be set. For multiple headers with the same name add additional `value` elements.|Yes|  
  
### Properties  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|exists-action|Specifies what action to take when the header is already specified. This attribute must have one of the following values.<br /><br /> -   override - replaces the value of the existing header.<br />-   skip - does not replace the existing header value.<br />-   append - appends the value to the existing header value.<br />-   delete - removes the header from the request.<br /><br /> When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.|No|override|  
|name|Specifies name of the header to be set.|Yes|N/A|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound, backend, on-error  
  
-   **Policy scopes:** global, product, API, operation  
  
##  <a name="SetQueryStringParameter"></a> Set query string parameter  
 The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter. Can be used to pass query parameters expected by the backend service which are optional or never present in the request.  
  
### Policy statement  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### Examples  
  
#### Example  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### Forward context information to the backend service  
 This example shows how to apply policy at the API level to supply context information to the backend service. For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30. At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|set-query-parameter|Root element.|Yes|  
|value|Specifies the value of the query parameter to be set. For multiple query parameters with the same name add additional `value` elements.|Yes|  
  
### Properties  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|exists-action|Specifies what action to take when the query parameter is already specified. This attribute must have one of the following values.<br /><br /> -   override - replaces the value of the existing parameter.<br />-   skip - does not replace the existing query parameter value.<br />-   append - appends the value to the existing query parameter value.<br />-   delete - removes the query parameter from the request.<br /><br /> When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.|No|override|  
|name|Specifies name of the query parameter to be set.|Yes|N/A|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, backend  
  
-   **Policy scopes:** global, product, API, operation  
  
##  <a name="RewriteURL"></a> Rewrite URL  
 The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.  
  
-   Public URL - `http://api.example.com/storenumber/ordernumber`  
  
-   Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service. This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority). This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.  
  
> [!NOTE]
>  You can only add query string parameters using the policy. You cannot add extra template path parameters in the rewrite URL.  
  
### Policy statement  
  
```xml  
<rewrite-uri template="uri template" />  
```  
  
### Example  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|rewrite-uri|Root element.|Yes|  
  
### Attributes  
  
|Attribute|Description|Required|Default|  
|---------------|-----------------|--------------|-------------|  
|template|The actual web service URL with any query string parameters.|Yes|N/A|  
|copy-unmatched-params|Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template|No|true|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound  
  
-   **Policy scopes:** product, API, operation  
  
##  <a name="XSLTransform"></a> Transform XML using an XSLT  
 The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.  
  
### Policy statement  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
    	<xsl:output method="xml" indent="yes" />  
    	<xsl:param name="User-Agent" />  
    	<xsl:template match="* | @* | node()">  
    		<xsl:copy>  
    			<xsl:if test="self::* and not(parent::*)">  
    				<xsl:attribute name="User-Agent">  
    					<xsl:value-of select="$User-Agent" />  
    				</xsl:attribute>  
    			</xsl:if>  
    			<xsl:apply-templates select="* | @* | node()" />  
    		</xsl:copy>  
    	</xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### Example  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
      	<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
    		<xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
    		<!-- Copy all nodes directly-->  
    		<xsl:template match="node()| @*|*">  
    			<xsl:copy>  
    				<xsl:apply-templates select="@* | node()|*" />  
    			</xsl:copy>  
    		</xsl:template>  
      	</xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|xsl-transform|Root element.|Yes|  
|parameter|Used to define variables used in the transform|No|  
|xsl:stylesheet|Root stylesheet element. All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)|Yes|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound  
  
-   **Policy scopes:** global, product, API, operation  
  
## Next steps
For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).  
