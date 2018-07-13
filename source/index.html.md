---
title: API Reference

# language_tabs: # must be one of https://git.io/vQNgJ
#   - shell
#   # - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - chat
  - structures
  - references
# - errors

search: true
---

# Introduction

Welcome to the osu!api. You can use this API to get information on various circles and those who click them.

You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right (eventually).

# Endpoint

## Base URL

The base URL is: `https://osu.ppy.sh/api/[version]/`

## API Versions

This is combined with the base endpoint to determine where requests should be sent.

Version | Status
------- | ---------------------------------------------------------------
v2      | current
v1      | _legacy api provided by the old site, will be deprecated soon_

# Authentication

```shell
# With shell, you can just pass the correct header with each request
curl "https://osu.ppy.sh/api/[version]/[endpoint]"
  -H "Authorization: Bearer {{token}}"
```

> Make sure to replace `{{token}}` with your OAuth2 token.

<aside class="warning">
Public access is not yet available, thus this section is incomplete.
</aside>

osu!api uses OAuth2 to grant access to the API. You can register for access `[somewhere eventually]`.

osu!api requires a valid token to be included with all API requests in a header that looks like the following:

`Authorization: Bearer {{token}}`

<aside class="notice">
You must replace <code>{{token}}</code> with your OAuth2 token.
</aside>
