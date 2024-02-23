---
hide:
  - toc

title: Basic Automatic Configuration
---

If you have a paid Apple Developer account, the easiest way to create the provisioning profile is
to use the automatic configuration strategy. There are two ways to do this:

* Use the `xcodeOrgId` and `xcodeSigningId` [capabilities](../reference/capabilities.md):
    ```json
    {
      "appium:xcodeOrgId": "<Team ID>",
      "appium:xcodeSigningId": "Apple Developer"
    }
    ```
* Create a `.xcconfig` file somewhere on your file system and add the following to it:
  ```ini
  DEVELOPMENT_TEAM = <Team ID>
  CODE_SIGN_IDENTITY = Apple Developer
  ```
  Then use the `xcodeConfigFile` capability to specify the path to this file:
  ```json
  {
    "appium:xcodeConfigFile": "/path/to/xcconfig/file"
  }
  ```

Note that these are mutually exclusive strategies; use _either_ the `xcodeConfigFile` capability
_or_ the combination of `xcodeOrgId` and `xcodeSigningId`.

* `xcodeOrgId` / `DEVELOPMENT_TEAM` is a unique 10-character string generated by Apple that is
  assigned to your team.
    * To find this string (your Team ID), sign in to [developer.apple.com/account](https://developer.apple.com/account),
      and click Membership in the sidebar. Your Team ID appears in the Membership Information
      section under the team name. You can also find your Team ID listed under the "Organizational
      Unit" field in your iPhone Developer certificate in your keychain.
* `xcodeSigningId` / `CODE_SIGN_IDENTITY` is usually either `Apple Developer` or `iPhone Developer`.

Once this configuration is done, you should specify your real device UDID with the `udid` desired
capability, after which you should be able to start your test. Proceed with
[Validating the WDA Install](./real-device-config.md#validating-the-wda-install) for the next steps.