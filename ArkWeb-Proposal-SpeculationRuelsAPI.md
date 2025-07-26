# [SpeculationRuelsAPI supports addtional headers]

## Authors:

- [aohui-wan] ([ArkWeb])

## Participate
- [Issue tracker] https://issues.chromium.org/issues/434299387

## Table of Contents 

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Introduction](#introduction)
- [User-Facing Problem](#user-facing-problem)
  - [Goals [or Motivating Use Cases, or Scenarios]](#goals-or-motivating-use-cases-or-scenarios)
  - [Non-goals](#non-goals)
- [Proposed Approach](#proposed-approach)
  - [Solving add addtional headers for the prerendering/preloading request for main document with this approach](#solving-add-addtional-headers-for-the-prerenderingpreloading-request-for-main-document-with-this-approach)
- [Accessibility, Privacy, and Security Considerations](#accessibility-privacy-and-security-considerations)
- [References & acknowledgements](#references--acknowledgements)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Introduction

The proposal adds an additional_headers field to the Speculation Rules API to add additional headers when preload resources.

## User-Facing Problem

Websites implement features such as traffic splitting, version routing, full-link tracing, and client platform identification by adding custom headers to HTTP requests.
For mainstream hybrid development scenarios—such as those using WKWebView/UIWebView on iOS or WebView on Android  provide native interfaces for injecting custom headers.
However, the Speculation Rules API, currently lacks support for setting custom headers during resource prefetching.
This limitation prevents the use of the Speculation Rules API in specific scenarios where prefetching version-specific or conditionally required resources is necessary.

### Goals [or Motivating Use Cases, or Scenarios]

When prefetching or prerendering resources via the Speculation Rules API, set custom headers to be added to the main document request by configuring addition_headers.

### Non-goals

N/A

## Proposed Approach

The proposal is to add an additional_headers field to the speculation rules API to allow developers to add custom headers (excluding sensitive headers) based on their actual business needs.


### Solving add addtional headers for the prerendering/preloading request for main document with this approach

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

## Accessibility, Privacy, and Security Considerations

To prevent the addition of sensitive HTTP headers, it is recommended to only allow custom headers with the prefix Cr-Prerender or Cr-Prefetch.

## References & acknowledgements

Many thanks for valuable feedback and advice from:

- [YaoMing Liu]

Thanks to the following proposals, projects, libraries, frameworks, and languages
for their work on similar problems that influenced this proposal.

- [ArkWeb]
- [Huawei Browser]