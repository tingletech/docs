<!--
title: 18 - Modifying profile settings from the command line
featured: true
-->

# Modifying Profile Settings from the Command Line

You can now view and set profile features from the Command Line Interface (CLI). Use these are the commands:

```
npm profile get 
npm profile set <prop> <value>
```

##Viewing & Setting Profile Values

To see your current profile settings, type:

```
npm profile get
```
npm displays:

![npmgetprofile](/images/npm_get_profile.png)

You can set the following profile values from the command line:

* email
* password
* fullname
* homepage
* freenode
* twitter
* github

To set a value, such as your twitter name for example, add it at the end of the line as shown:

```
$npm profile set fullname nori pat marsupial
```
npm will prompt for credentials, then respond: 

```
Set fullname to nori pat marsupial
```
[Note to reviewers: Should I show each command as well as the response?]

##Enabling and Disabling Two-Factor Authenticaiton 


You can also enable and disable 2FA from the command line. This is explained here [Insert link to 2FA doc here]

### Notes

Please see the command line documentation for more details [insert reference here].
