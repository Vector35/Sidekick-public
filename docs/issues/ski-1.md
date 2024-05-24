# Sidekick Issue 1: API Key Stored in Binary Ninja Database (BNDB)

## Affected Versions: < 1.1

## Issue Summary

In versions of Sidekick below 1.1, the user's Sidekick API key was unintentionally stored inside of any BNDB when it was saved. No customer data or private information can be accessed with this API key and Sidekick does not have metered billing for API usage. But, because this API key can be leaked without the user's knowledge if a BNDB is shared with another person, we are revoking all API keys that have been used with these older versions of the Sidekick plugin out of an abundance of caution.

## Required Actions

If you are a Sidekick user with an active API key, you will not be able to access the Sidekick service again until you:

* Update your Sidekick plugin to 1.1 or greater via the Plugin Manager
* Log into your [Sidekick account](https://sidekick.binary.ninja/account) and navigate to your [API Keys](https://sidekick.binary.ninja/account#api-keys) to retrieve your new API key
* Update your `sidekick.api_key` setting in Binary Ninja to use the new API key

At this point, Sidekick functionality should be restored. If this is not the case, [contact us](mailto:sidekick@vector35.com).

## Other Information

To ensure users don't wind up in the same situation after this update, we will be taking the following actions with any API key used with these older versions:

* Denying any requests
* Revoking the API key included in the request
* Automatically generating a new API key

As a reminder, if you need to generate a new API key at any point, [contact us](mailto:sidekick@vector35.com).