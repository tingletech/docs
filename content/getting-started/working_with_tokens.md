<!--
title: 17 - Working with tokens
featured: true
-->

# Working with Tokens

Every time you login to npm, a security token (a hexidecimal string) is generated. The token authenticates your account, and can be provided to applications or other users to give them access to perform continuous integration testing, or perform other functions that require permission.  For example, Travis-CI allows you set an environment variable to be a token. This gives Travis-CI the access to *automatically download updates to packages as they become available* so that tests can be continually updated. 

[**Reviewer Question:** Is italicized sentence accurate?]

Any person or application that has your full-permission token has the same account rights that you do. Because this is level of access is higher than the access level normally needed to install packages or conduct automated testing,  npm's release 5.5.1 includes new commands that you can use to control tokens.

[**Reviewer Question:** Prior to 2fa (and now, if you don't enable it) could someone with your full permission token login as you and change all your settings, thus hijacking your account? )

But what if you needed to revoke access to an application, or to another user? What if you wanted to create new tokens for specific purposes? This new release provides these enhanced security features.  You can now create and revoke specialized tokens to allow targeted and controlled distribution, testing, and modifications.

New commands empower you to:

* View tokens for easier tracking and management
* Create new tokens, specifiying type
* Delete/revoke tokens 
* Set tokens to be read-only (install-only)
* Set tokens to have full publishing permissions 
* Limit access according to IP address ranges (CIDR)


##How to View the Tokens On Your Account: 

Until now, to see your tokens, you had to copy tokens from a resource file, or provide the token via the resource file. Now, you can easily view the tokens associated with your account by typing:

 `npm token list`. 

![npmtokenlist](/images/npm-token-list-shorter-list.png)

The following table explains the token list. 

List Result	 	| Purpose
------------- 	| -------------
id				 	| Use the id to refer to the token in commands
token			  	| This is the first part of the actual token 
created			| Date the token was created
readonly		  	| If no, the token provides full permissions
CIDR whitelist  	| Restricts token use by IP address

The CIDR whitelist column only appears if one or more of the tokens has a CIDR whitelist restriction.

**Note**: If you have enabled two-factor authentication on your profile, you have an additional layer of security augmenting the new token security features. No one will be able to modify or create your tokens unless they provide the second authentication factor. 

##How to Create New Tokens

`npm token create [--read-only] [--cidr=list]`

Before you create a new token, decide which type of token you want:

* read-only (installation/distribution rights)
* full permission (publishing rights)
* CIDR whitelist (restricted by ip address)

The default setting for new tokens is full-permission.

* *Read-only* tokens allow installation and distribution.
* *Full-permission* tokens allow installation, distribution, publishing, and all rights that you have on your account
* *CIDR whitelist* tokens can only be used from specified ip address ranges. Use this to restrict tokens to a single company, or a specified developer team, for example. 

When a token is read-only, it allows packages to run (for example, for a test) but the token cannot be used to make changes to the package. If a token is not explicitly set to read-only, it has full permissions, including publish and modification rights. 

###How to Create a New Full-Permission token:

To create a new full permission token, type:

'npm token create'

If you have set up two-factor authentication, you will be prompted for your npm password, followed by an OTP. npm will display this table: 

![npmtokencreatelong](/images/npm-token-create-long-version.png)

Note that readonly is set to *false*.

###How to Create a New Read-Only Token

To create a new read-only token, type:

`npm token create --read-only`

If you have set up two-factor authentication, you will be prompted for an npm password, followed by an OTP. npm will display this table: 

![npmtokencreatereadonly](/images/npm-token-create-readonly.png)

Note that read-only is set to *true*.

###How to Create a New CIDR-Restricted Token

To limit the token so that it can only be used from specified ip addresses, you can create a CIDR-restricted token. CIDR is an acronym for Classless Inter-Domain Routing. The [CIDR Wiki page](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) will get you started. 

This makes it possibe for you to force anyone working with the token to either physically be at a specified ip address, or accessing the package through a Virtual Private Network (VPN),

[**Reviewer Question:** Is the previous sentence accurate?]

```
npm token create --[--cidr=list]
''''

example.: 
npm token create --cidr=192.0.2.0/24
```

If you have set up two-factor authentication, you will be prompted for an npm password, followed by an OTP. npm will display this table: 

![npmtokencreatecidr](/images/CIDR-create-token.png)

If you get the following message:

```
npm ERR! CIDR whitelist contains invalid CIDR entry: X.X.X.X./YY,Z.Z.. . .

```

(where the string returned is the one you entered) please ensure that the CIDR string is valid and in the appropriate format. 

**Reviewer Question**: Any guidelines about the format not covered here?


###How to Create a CIDR-Restricted Read-Only Token

To create a CIDR-restricted token that is also read-only, type:

```
npm token create --read-only ----cidr=list
```

##How to Revoke Tokens

You can revoke a token, whether it was created since this new release, or whether it was created several years ago. This allows you to gain control of access you may wish to take back. 

The command to revoke a token is:

```npm token revoke'```

An alias is:

```npm token delete'```

To revoke a token:

1. Type `npm token list` to find the token ID affiliated with the token you want to delete. 
2. Type 'npm token revoke 123456', where 123456 is the token id. Note: you cannot use the short version of the token in this step. npm will report 'Removed 1 token'
3. Type 'npm token list' to confirm that the token has been removed. 

The following screen shot demonstrates these steps:

![npmtokenrevokeshort](/images/npm-token-revoke-shorter.png)