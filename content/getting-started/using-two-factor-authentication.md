<!--
title: 16 - Using two-factor authentication
featured: true
-->

# Using Two-Factor Authentication

To meet the increasing need for strong digital security, npm has introduced two-factor authentication (2FA).  Two-factor authentication prevents unauthorized access to your accounts and projects by confirming your identity using two methods. 

You have probably used 2FA before. For example, if you need to provide a code from your phone after you log in to your online bank account, your bank has enabled 2FA.  

Set two-factor authentication to restrict access to your account, and to limit or prevent the ability of others to publish or change your code.  

## New Security Options Related to Two-Factor Authentication

Here are actions you can take to increase security:

* Enable two-factor authentication on your user profile to prevent spoofing
* Limit access according to IP address ranges (CIDR)
* Generate one-time use Password Recovery codes in case you forget your password
* Create and delete (revoke) specialized tokens to allow targeted and controlled distribution, testing, and modifications

## Preparation

To get started using 2FA with your npm account, you will need an application that can provide a second authentication factor. If you don't have one, please download a product such as [Authy](https://authy.com/download/) or 
[Google Authenticator](https://support.google.com/accounts/answer/1066447). 

Some authenticators scan QR codes, others generate a one-time password, or OTP. 

(Note: npm will not use SMS (text-to-phone) as a method for authenticating users.)

## How to Enable Two-Factor Authentication on your Profile

Adding 2FA to your profile will prevent spoof attacks, which is when someone logs in as if they were you. To enable 2FA on your profile, use the command line interface. (The settings will also apply when you access npm from the website.) Here are the main commands: 

  `npm profile enable-2fa [auth-only|auth-and-writes]`
  `npm profile disable-2fa`
  
There are two levels of authentication, *auth only* and *auth-and-writes*:

* *auth only*  requires a one-time-password (OTP) when logging on or making changes to your account's authentification. 
* *auth-and-writes* This is the default setting. If you select this, npm will require an OTP in all instances that auth-only does. Additionally, npm will prompt you for an OTP when publishing a module, setting the latest version, changing access, and other actions. 

### How to Enable Auth-and-Writes Two-Factor Authentication

To require two-factor authentication when logging in, writing, publishing, and making other changes, type either command. (The auth-and-writes setting is the default.)
  
        npm profile enable-2fa
        npm profile enable-2fa auth-and-writes 
      
npm will return this message:
        
     
        > npm notice profile Enabling two factor authentication for auth-and-writes   
   
### How to Enable Auth-Only Two-Factor Authentification

If you want to enable 2FA, but you only want it to be activated when you first login, use the *auth-only* setting. 

        npm profile enable-2fa auth-only
        
 npm will return this message: 
 
        $ npm profile enable-2fa auth-only
        > npm notice profile Enabling two factor authentication for auth-only

#### How to Enter the Second Factor 

After you specify the setting you want to enable, npm will present a QR code:

![Masked QR Code And Prompt](/images/qr_code_and_prompt_masked.png)

If your authenticator can read QR codes, scan it. If not, use your authenticator to generate an OTP code, and enter it after this prompt:  

````
    Add an OTP code from your authenticator:
````

After you have successfully provided the second factor,  npm will display this message:

    2FA successfully enabled. 
    Below are your recovery codes, please print these out. 
    You will need these to recover access to your account 
    if you lose your authentication device.
 
#### Recovery Codes 

After setting up TFA, npm will generate recovery codes that will appear on your screen. Please print them and save them as described. Note: Some authenticators provide a method for you to store recovery codes.

    >**WARNING**: You must save these codes in a location that is not  
    not normally near the device you use to authenticate. If you lose
    this device, or forget your password, these codes will be your
    onlyw ay to get back online.

### How to Remove Two-Factor Authentication from your Profile

To remove 2FA from your profile, type this command:

```
    npm profile disable-2fa
```
   
npm will display:

````
    > npm password:   
````
Enter your npm password as prompted, then npm will display: 

```
   >Enter one-time password from your authenticator: 123456
``` 
 npm will confirm: 

```
   Two factor authentication disabled.
   
```

##Viewing & Setting Profile Values

To see the current status of your profile, type:

```
npm profile get
```
npm displays:

![npmgetprofile](/images/npm_get_profile.png)

To set a value, such as your twitter for example, type:

```
npm profile set twitter @node2joy

```

### Note

The commands `npm profile enable-tfa` and `npm profile enable-2fa`, with or without dash `'-'`, are aliases. Similarly, `npm profile disable-tfa` and `npm profile disable-2fa`, with or without dash `'-'` are aliases.

Please see the command line documentation for more details and other new profile settings now available from the command line. For example, the CLI doc explains more about setting profile values sfrom the command line. 

#Using Two-Factor Authentication with Tokens

Whenever you login to npm, a token is generated. 
This is part of npm's authentication process. Many coders use tokens to provide sufficient access to testing programs, for example. To enhance security npm now provides for you to:

* Restrict token access to read-only. 
* You can also delete (revoke) tokens that have been issued
* Create tokens that are auth-and-writes 
* Add two-factor authentication to tokens.
* Restrict tokens so that they only work in specific CIDR ranges. 

This section explains how to do these steps. 

Note: Right now you can only set 2FA from the command line interface (CLI) Even when you log in by website, you will need 2FA. In a future release, you will be able to set and manage 2FA settings from the website as well as the CLI.

##Getting Started: View your current tokens 

To see the tokens that have already been issued to your account, type:

```
$ npm token
```

Npm will display a table showing the current tokens, including a short id, the token, date created, and whether it is readonly.

When a token is read-only, it allows packages to run (for example, for a test) but the token cannot be used to make changes to the package. If a token is not set to read-only, it can 




![npmtoken](/images/npm_tokens.png)

 

CIDR

After validating tokens with CIDR, npm will display an additional column:

![npmtoken2](/images/npm_tokens_include_CIDR.png)

ADD HOW TO ADD CIDR. npm token create --cidr=list 
what is next?


