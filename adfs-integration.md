## Setting up SSO with ADFS and your web application using OpenID Connect and OAuth2

Here's how to set up SSO between your web application and ADFS using OpenID Connect and OAuth2, with an example scenario and sample configurations:

**Prerequisites:**
	* Your ADFS server should be configured and accessible.[[1]](https://www.browserstack.com/docs/enterprise/single-sign-on/adfs)
	* Your web application should be running in a Docker container on your client's web server VM.

**Example scenario:**
	* You have a web application called "MyWebApp" that needs to be accessible to users in your organization.
	* You have an ADFS server configured with user accounts from your organization.

**Sample configurations:**

**ADFS configuration:**

1. **Register your web application as a relying party trust:**
    * Open the ADFS Management console.
    * Navigate to **Relying Party Trusts** > **Add Relying Party Trust**.
    * Choose **Web application** as the type of relying party.
    * Enter **MyWebApp** as the **Display name**.
    * Select **OpenID Connect and OAuth 2.0 implicit grant** as the **Profile**.
    * Click **Next** and configure the following settings:
        * **Relying party identifier:** Enter the URL of your web application (e.g., https://mywebapp.example.com).
        * **Access Control Policies:** Choose the appropriate access control policy for your application (e.g., Permit all users).
        * **Client secrets:** Generate a client secret and add it to your application's configuration.
        * **Redirect URIs:** Add the redirect URI for your application (e.g., https://mywebapp.example.com/auth/callback).
    * Click **Next** and review the settings.
    * Click **Close** to complete the registration.

2. **Configure claims issuance:**
    * Open the ADFS Management console.
    * Navigate to **Relying Party Trusts** > **MyWebApp**.
    * Select the **Issuance Transform Rules** tab.[[2]](https://plugins.miniorange.com/adfs-single-sign-on-wordpress-sso-oauth-openid-connect)
    * Click **Add Rule** and choose **Send Claims Using a Custom Rule**.[[2]](https://plugins.miniorange.com/adfs-single-sign-on-wordpress-sso-oauth-openid-connect)
    * Enter a rule name (e.g., Send User Claims).
    * In the **Custom rule** box, enter the following rule:

```xml
c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"] => issue(claim = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress", type = "http://www.w3.org/2001/XMLSchema#string", value = c.Value);
```

    * Click **Finish** to save the rule.

**Web application configuration:**

1. Install the necessary OpenID Connect and OAuth2 libraries for your web application framework.
2. Configure your application to use the following settings:
    * **Client ID:** The client ID you generated in ADFS.
    * **Client secret:** The client secret you generated in ADFS.
    * **Authorization endpoint:** The authorization endpoint of your ADFS server (e.g., https://adfs.example.com/adfs/oauth2/authorize).
    * **Token endpoint:** The token endpoint of your ADFS server (e.g., https://adfs.example.com/adfs/oauth2/token).
    * **Redirect URI:** The redirect URI you configured in ADFS.
3. Implement the OpenID Connect and OAuth2 flows in your application to authenticate users and access resources on their behalf.

**Additional notes:**

* You may need to configure additional settings in ADFS, such as claims issuance and token lifetime.
* If your web application has multiple components or services, you may need to register them as separate relying parties in ADFS.
* For detailed instructions and sample configurations, refer to the official documentation for ADFS and your web application framework.

**Disclaimer:** This information is based on the provided sources and may not be up-to-date. Please refer to the official documentation for ADFS and your web application framework for the latest information.


---
Learn more:
1. [BrowserStack SSO with ADFS | SAML](https://www.browserstack.com/docs/enterprise/single-sign-on/adfs)
2. [ADFS Single Sign-On (SSO) WordPress OAuth & OpenID Login - Plugins - miniOrange](https://plugins.miniorange.com/adfs-single-sign-on-wordpress-sso-oauth-openid-connect)

![server_inject_icon](https://pfst.cf2.poecdn.net/base/image/0e8698a6e80a985ec6d5f4d175c17866cee4b502ac78ccea3d02bb90fdca0b9f?w=100&h=33)
Related searches:
+ [## Setting up SSO with ADFS and your web application

Here's how to set up SSO between your web application and ADFS using OpenID Connect and OAuth2:

**Prerequisites:**

* Your ADFS server should be configured and accessible.
* Your web application should be running in a Docker container on your client's web server VM.

**Steps:**

1. **Register your web application in ADFS:**
    * Open the ADFS Management console.
    * Navigate to **Relying Party Trusts** > **Add Relying Party Trust**.
    * Choose **Web application** as the type of relying party.
    * Enter a **Display name** for your application.
    * Select **OpenID Connect and OAuth 2.0 implicit grant** as the **Profile**.
    * Click **Next** and configure the following settings:
        * **Relying party identifier:** Enter the URL of your web application.
        * **Access Control Policies:** Choose the appropriate access control policy for your application.
        * **Client secrets:** Generate a client secret and add it to your application's configuration.
        * **Redirect URIs](https://www.google.com/search?q=%23%23%20Setting%20up%20SSO%20with%20ADFS%20and%20your%20web%20application%0A%0AHere%27s%20how%20to%20set%20up%20SSO%20between%20your%20web%20application%20and%20ADFS%20using%20OpenID%20Connect%20and%20OAuth2%3A%0A%0A%2A%2APrerequisites%3A%2A%2A%0A%0A%2A%20Your%20ADFS%20server%20should%20be%20configured%20and%20accessible.%0A%2A%20Your%20web%20application%20should%20be%20running%20in%20a%20Docker%20container%20on%20your%20client%27s%20web%20server%20VM.%0A%0A%2A%2ASteps%3A%2A%2A%0A%0A1.%20%2A%2ARegister%20your%20web%20application%20in%20ADFS%3A%2A%2A%0A%20%20%20%20%2A%20Open%20the%20ADFS%20Management%20console.%0A%20%20%20%20%2A%20Navigate%20to%20%2A%2ARelying%20Party%20Trusts%2A%2A%20%3E%20%2A%2AAdd%20Relying%20Party%20Trust%2A%2A.%0A%20%20%20%20%2A%20Choose%20%2A%2AWeb%20application%2A%2A%20as%20the%20type%20of%20relying%20party.%0A%20%20%20%20%2A%20Enter%20a%20%2A%2ADisplay%20name%2A%2A%20for%20your%20application.%0A%20%20%20%20%2A%20Select%20%2A%2AOpenID%20Connect%20and%20OAuth%202.0%20implicit%20grant%2A%2A%20as%20the%20%2A%2AProfile%2A%2A.%0A%20%20%20%20%2A%20Click%20%2A%2ANext%2A%2A%20and%20configure%20the%20following%20settings%3A%0A%20%20%20%20%20%20%20%20%2A%20%2A%2ARelying%20party%20identifier%3A%2A%2A%20Enter%20the%20URL%20of%20your%20web%20application.%0A%20%20%20%20%20%20%20%20%2A%20%2A%2AAccess%20Control%20Policies%3A%2A%2A%20Choose%20the%20appropriate%20access%20control%20policy%20for%20your%20application.%0A%20%20%20%20%20%20%20%20%2A%20%2A%2AClient%20secrets%3A%2A%2A%20Generate%20a%20client%20secret%20and%20add%20it%20to%20your%20application%27s%20configuration.%0A%20%20%20%20%20%20%20%20%2A%20%2A%2ARedirect%20URIs)
