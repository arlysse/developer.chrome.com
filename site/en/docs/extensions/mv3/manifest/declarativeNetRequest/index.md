---
layout: "layouts/doc-post.njk"
title: "Manifest - declarativeNetRequest"
date: 2022-12-13
updated: 
description: Reference documentation for the declarativeNetRequest property of manifest.json.
---

An optional Manifest key enabling the use of the [declarativeNetRequest API](/docs/extensions/reference/declarativeNetRequest/). Using `declarativeNetRequest`, you can block or modify network requests by specifying declarative rules. This lets extensions modify network requests without intercepting them and viewing their content, providing more privacy. The manifest key accepts a dictionary with a single key called `"rule_resources"`, containing a list of static ruleset dictionaries. The "declarativeNetRequest" and "declarativeNetRequestFeedback" permissions must also be added, as well as the list of specified  "host_permissions" URLs.

```json
{
  "name": "My extension",
  ...

  "declarative_net_request" : {
    "rule_resources" : [{
      "id": "ruleset_1",
      "enabled": true,
      "path": "rules_1.json"
    }, {
      "id": "ruleset_2",
      "enabled": false,
      "path": "rules_2.json"
    }]
  },
  "permissions": [
    "declarativeNetRequest",
    "declarativeNetRequestFeedback",
  ],
  "host_permissions": [
  "http://www.blogger.com/",
  "http://*.google.com/"
],
  ...
}
```

It must be noted that extensions cannot clear the browser's Cache Storage or Service Worker registrations automatically. When enabling an extension using `declarativeNetRequest` rules to block certain sites, the rule may be ignored depending on if the site is cached. This caching can persist after browser restarts. You use the chrome.browsingData API to clear the browser memory manually to ensure specified `declarativeNetRequest` rules are followed. 