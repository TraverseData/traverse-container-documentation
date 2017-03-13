# Traverse Container Documentation v1.2:

## Contents

  * [Overview](#overview)
  * [Resource URL](#resource-url)
  * [`User` object](#user-object)
  * [`Start` method](#start-method)
  * [Example](#example)
  * [Best practices](#best-practices)

## Overview

To use the Traverse Container, load it from the [resource URL](resource-url) and then call the [`start` method](#start-method).

Please see the [example](#example) and [best practices](#best-practices), below.

## Resource URL

The Container is hosted at the following URL:

<a href="">http(s)://static.traversedlp.com/v1/container/traverse-container.js?clientId=`clientId`</a>

| Parameter    | Description | Required |
| ------------ |------------ | -------- |
| `clientId` | Your 36-character client ID (includes hyphens). | Yes |

## `Start` method

Initialize the Container by passing a [`user` object](#user-object) to the `start` method.

| Parameter    | Description | Required |
| ------------ |------------ | -------- |
| `user` | A [user](#user) object | Yes |

## `User` object

A `user` object is written as a [Javascript Object Literal](http://www.dyn-web.com/tutorials/object-literal/) and may contain any of the following fields:

| Parameter   | Description | Required |
| ----------- | ----------- | -------- |
| `email`     | Plaintext (non-hashed) email address. *The Container will normalize and hash the email address client-side, and it will not be transmitted*.<sup id="a1">[1](#f1)</sup> | Yes |

### Hashed Data

The Container automatically handles the normalization and hashing of potentially sensitive fields. The plaintext values never leave the user's browser. You may also set these hashes manually using the following the naming convention: {parameter name}{hash type}{original character casing}. E.g. `emailMd5Upper`, `emailSha1Lower`, etc. If you choose to do this, we require all three of Md5, Sha1, and Sha256 hashes for both upper and lower-case input values, so 6 total for each field that is passed hashed.


## Example

Load the container and initialize with some user data:

```
<script src="https://static.traversedlp.com/v1/container/traverse-container.js?clientId=YOUR-CLIENT-ID-HERE" type="text/javascript"></script>
<script type="text/javascript">
TraverseContainer.start({
  email:     "john.doe@example.com", /* The Container will normalize and hash the email address. */
});
</script>
```

Initializing with hashed email addresses:

```
TraverseContainer.start({
  emailMd5Lower:     "8eb1b522f60d11fa897de1dc6351b7e8",
  emailMd5Upper:     "61cad946c746dae396d1eeb795c3fa30",
  emailSha1Lower:    "73ec53c4ba1747d485ae2a0d7bfafa6cda80a5a9",
  emailSha1Upper:    "a22f248ad84acf5c54dab0036bf5ebed3958fbb6",
  emailSha256Lower:  "836f82db99121b3481011f16b49dfa5fbc714a0d1b1b9f784a1ebbbf5b39577f",
  emailSha256Upper:  "540c78e61f7b5440c1a229e4ccccb651bfbbec672939f573e0870d290bfcc54e"
});
```


Best practices
--------------

1. The Container is asynchronous, so always load it from the *target* of a form submit, rather than *on* submit, or it will not have time to record the [data](#user-object) before the user navigates to the next page!
2. For best compatibility with your page, load the Container from the HTML `body` section rather than the `head`.
3. To avoid affecting page-load time, load the Container from the bottom of your HTML.
