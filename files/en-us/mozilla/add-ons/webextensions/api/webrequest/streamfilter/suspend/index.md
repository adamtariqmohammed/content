---
title: webRequest.StreamFilter.suspend()
slug: Mozilla/Add-ons/WebExtensions/API/webRequest/StreamFilter/suspend
page-type: webextension-api-function
browser-compat: webextensions.api.webRequest.StreamFilter.suspend
sidebar: addonsidebar
---

Suspends a request. After this is called, no more data will be delivered until the request is resumed with a call to {{WebExtAPIRef("webRequest.StreamFilter.resume()", "resume()")}}.

You can't call this function until after the {{WebExtAPIRef("webRequest.StreamFilter.onstart", "onstart")}} event has fired.

## Syntax

```js-nolint
filter.suspend()
```

### Parameters

None.

### Return value

None.

## Examples

This example uses suspend/resume to delay a web request.

```js
function listener(details) {
  let filter = browser.webRequest.filterResponseData(details.requestId);

  filter.onstart = (event) => {
    filter.suspend();

    setTimeout(() => {
      filter.resume();
      filter.disconnect();
    }, 1000);
  };
}

browser.webRequest.onBeforeRequest.addListener(
  listener,
  { urls: ["https://example.org/"], types: ["main_frame"] },
  ["blocking"],
);
```

{{WebExtExamples}}

## Browser compatibility

{{Compat}}
