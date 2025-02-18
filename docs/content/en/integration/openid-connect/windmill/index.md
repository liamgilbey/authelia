---
title: "Windmill"
description: "Integrating Windmill with the Authelia OpenID Connect 1.0 Provider."
lead: ""
date: 2023-12-10T10:52:22+11:00
draft: false
images: []
menu:
  integration:
    parent: "openid-connect"
weight: 620
toc: true
community: true
---

## Tested Versions

- [Authelia]
  - [v4.37.5](https://github.com/authelia/authelia/releases/tag/v4.37.5)
- [Windmill]
  - [1.224.0](https://github.com/windmill-labs/windmill/releases/tag/v1.224.0)

## Before You Begin

{{% oidc-common %}}

### Assumptions

This example makes the following assumptions:

* __Application Root URL:__ `https://windmill.example.com/`
* __Authelia Root URL:__ `https://auth.example.com/`
* __Client ID:__ `windmill`
* __Client Secret:__ `insecure_secret`

### Authelia

Authelia configuration.yml

```yaml
identity_providers:
  oidc:
    ## The other portions of the mandatory OpenID Connect 1.0 configuration go here.
    ## See: https://www.authelia.com/c/oidc
    clients:
    - id: 'windmill'
      description: 'Windmill'
      secret: '$pbkdf2-sha512$310000$c8p78n7pUMln0jzvd4aK4Q$JNRBzwAo0ek5qKn50cFzzvE9RXV88h1wJn5KGiHrD0YKtZaR/nCb2CJPOsKaPK0hjf.9yHxzQGZziziccp6Yng'  # The digest of 'insecure_secret'.
      authorization_policy: 'two_factor'
      redirect_uris:
        - 'https://windmill.example.com/user/login_callback/authelia'
      scopes:
        - 'openid'
        - 'profile'
        - 'email'
        - 'groups'
      userinfo_signed_response_alg: none
```

## Budibase

### Core configuration

**Superadmin settings > Core**

- Base Url: https://windmill.example.com

{{< figure src="windmill_core.png" alt="Windmill" >}}

> ⚠️ **Don't forget to press save.**

### Auth configuration

**Superadmin settings > SSO/OAuth**

- Config URL: https://auth.example.com
- Client Id: Windmill
- Client Secret: insecure_secret

{{< figure src="windmill_sso.png" alt="Windmill" >}}

> ⚠️ **Don't forget to press save.**

## See Also

- [Windmill OpenID Connect Documentation](https://www.windmill.dev/docs/misc/setup_oauth)

[Authelia]: https://www.authelia.com
[Windmill]: https://www.windmill.dev
[OpenID Connect 1.0]: ../../openid-connect/introduction.md
