---
title: CORS
author: Pulkit Agrawal
description: "Understand CORS once and for all."
pubDate: 2025-12-11
tags: ["cors", "web", "learning in public"]
---

# CORS: Cross-Origin Resource Sharing

CORS is a browser security feature, not a server security feature.

Your browser has a feature that helps protect you from malicious websites. It prevents the page you are viewing from making JavaScript based requests to other web domains.

The browser has another feature, which allows web servers to disable this protection.

When a script loaded from abc.com makes a request to xyz.com, the browser will make an http (method: OPTIONS) request to xyz.com, asking the server at xyz.com if it would like to permit the cross domain request. If it says yes, then the browser makes the request. If it says no, the browser will throw a cross origin request error.

If you would like to permit cross origin requests on your webpage, you must write a request handler on the server that responds to the OPTIONS request with affirmation that the requestors domain should be permitted to make cross origin requests. Most server frameworks have a simple way to enable this behavior. 
