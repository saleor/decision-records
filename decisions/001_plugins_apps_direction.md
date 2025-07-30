# 2025 Apps/Plugins direction

Status: accepted

Summary: What's our take on Plugins and Apps and the whole ecosystem of extending Saleor.


## Issue

Historically Saleor had Plugins as a way to implement third party integrations and customer solutions. At some point we moved towards Apps. We still have plugins in the codebase though. It's not always clear how we stand with the general direction.

### Plugins general direction

In general we do need and want to maintain the plugins we have in the codebase. This means:

- we do not build any new features in these plugins
- we fix bugs and port fixes to previous versions of saleor/saleor
- we treat it as normal functionality we have

### Apps general direction

Apps is our current preferred ecosystem of building new extensions. We also maintain our own App Store available in the Dashboard and a public facing one on [apps.saleor.io](http://apps.saleor.io).

We have apps that we host, we have example apps we do not intend to hos. We have open source apps and closed source apps intended for cloud users only.

General decision making around apps:

- app will be hosted and closed source if we think it’s important for us to maintain it for enterprise clients and an added value for money for our clients
- app will be hosted and open source if we think it’s critical for Saleor to have a specific integration or a specific app available for everyone
- app will be open source and not hosted in all other cases

The list of supported apps is up to date on Dashboard. [apps.saleor.io](http://apps.saleor.io) holds a list of both our hosted apps, open source apps and apps built by third party companies.


### Plugins list with the intended future

- Adyen - we have an app replacement for Cloud users, we want to remove the plugin as soon as possible
- Authorize.net - we have an app replacement example in [saleor/saleor-app-payment-authorize.net](https://github.com/saleor/saleor-app-payment-authorize.net)
- braintree - intended to be replaced by an app
- np_atobarai - intended to be replaced by an app
- razorpay - we do not intend to build a replacement, and we want to remove it as soon as possible
- stripe - we are building an open-source app replacement in [saleor/apps](https://github.com/saleor/apps/tree/main/apps/stripe)
- admin_email - will be folded into [saleor/saleor](https://github.com/saleor/saleor) code
- avatax/avalara - we have an app replacement available in [saleor/apps](https://github.com/saleor/apps/tree/main/apps/avatax)
- openid_connect - will likely be replaced by an External Auth API and folded into [saleor/saleor](https://github.com/saleor/saleor) core code
- sendgrid - there is an app replacement [saleor/apps](https://github.com/saleor/apps/tree/main/apps/smtp)
- user_email - there is an app replacement in [saleor/apps](https://github.com/saleor/apps/tree/main/apps/smtp)
