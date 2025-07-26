# [SpeculationRuelsAPI supports addtional headers]

## Authors:

- [aohui-wan] ([ArkWeb])

## Introduction

The proposal adds an additional_headers field to the Speculation Rules API to add additional headers to preload resources.

## User-Facing Problem

Websites implement features such as traffic splitting, version routing, full-link tracing, and client platform identification by adding custom headers to HTTP requests.
For mainstream hybrid development scenarios—such as those using WKWebView/UIWebView on iOS or WebView on Android  provide native interfaces for injecting custom headers.
However, the Speculation Rules API, currently lacks support for setting custom headers during resource prefetching.
This limitation prevents the use of the Speculation Rules API in specific scenarios where prefetching version-specific or conditionally required resources is necessary.

## Proposed Approach

The proposal is to add an additional_headers field to the speculation rules API to allow developers to add custom headers (excluding sensitive headers) based on their actual business needs.

### Examples

```
<script type="speculationrules">
{
  "prerender": [
    {
      "urls": ["two.html"],
      "additional_headers": [
             {"Cr-Prerender-Id": "2"}, 
             {"Cr-Prerender-Version":"1002"}, 
             {"Cr-Prerender-Region": "China"}
         ]
    }
  ]
}
</script>
```

When pre-rendering two.html, the request headers for the main document resource will include the fields added in additional_headers.

### Other activities to consider / security consideration

To prevent the addition of sensitive HTTP headers, it is recommended to only allow custom headers with the prefix Cr-Prerender or Cr-Prefetch.