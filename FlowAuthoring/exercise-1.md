---
description: Security Users
---

# Exercise 1

Your organization has been extremely impressed by the work you’ve done over the past few months with FME. They now have a better understanding of the possibilities that FME offers and they decided to install an FME Flow for further automations. They asked you to be the FME Flow administrator. It is now your job to ensure that the FME Flow runs smooth, secure and efficient.

You know how important security is and you’ve therefore decided to create individual users and give them the proper permissions based on the work they will be doing.

**Assignment**:

You will have to login on the FME Flow and create the following users and assign the right role/permissions based on the purpose they have on the FME Flow:

<table data-header-hidden><thead><tr><th valign="top">Username</th><th valign="top">Purpose</th></tr></thead><tbody><tr><td valign="top">*Your name*</td><td valign="top">This will be the user you will use in the course. It should be a powerful user that can change settings on its own and is responsible for maintaining the server.</td></tr><tr><td valign="top">Ryan</td><td valign="top">Ryan is an experienced FME <em>developer</em> who will be developing and uploading workspaces to the FME Flow.</td></tr><tr><td valign="top">Chris</td><td valign="top">Chris doesn’t use FME at all. He works at the HR department but needs to be able to run workspaces and FME Flow apps to automate his tasks.</td></tr><tr><td valign="top">Emma</td><td valign="top">Emma is an experienced FME <em>developer</em> who will be developing and uploading workspaces to the FME Flow</td></tr><tr><td valign="top">Amy</td><td valign="top">Amy is a new FME developer. At this point she will only need permissions to upload and run workspaces and access the “Data” and “Temp” resources. She should <em>not</em> be allowed to remove data from these resources.</td></tr></tbody></table>

<details>

<summary>Tips:</summary>

* There are several ways to open FME Flow.
  * From the windows start menu.
  * From the browser
    * [http://localhost/fmeserver](http://localhost/fmeserver)
    * [http://fmetraining/fmeserver](http://fmetraining/fmeserver)

- The login to FME Flow by default is:
  * **Username**: admin
  * **Password**: \*Same as you used to login on this machine\*

* Login as each user to see if they are setup correct.

</details>

<details>

<summary>Bonus:</summary>

Amy has permissions to run workspaces, however she cannot see any workspace to run. This because she is missing certain permissions. Can you figure out which permissions she is missing to run a workspace?

Create a repository where she has full access to create, update and remove workspaces and run them.

</details>

{% hint style="info" %}
In today's world, security is extremely important. Bad actors try to get access to data and personal information all the time. It is therefore important to implement proper security rules. FME Flow has some build in options. Here are a few tips:

* If you install FME Flow (or for instance our IT department) try and see to it that you use HTTPS.
  * Https ensures that all traffic you send over the web is encrypted. This means that if a person would listen in on your web-traffic, they wont be able to see what you are sending or receiving. _If you "don't" use https, they can for instance see your username and password, tokens, data sources etc._
* Adopt Least Privilege for users.
  * Least privilege means that you only give users access to the resources and functions that they actually need to perform there job. This will cost you more time to set up but it increases your security by a lot. You don't simply want to give every user "admin" access because it makes it easy.
  * You can create "Roles" in FME to simplify this process.
* Enforce strong password policies
  * Strong password policies ensure that users cannot use simple passwords that are easy to guess/crack as a bad actor. So no "12345, password, qwerty123" kind of passwords.
    * These passwords can be cracked in less than a second!
  * FME has several build in functions to help you ensure that users comply with this:
    * Minimum Length.
    * Must not contain Username.
    * Must contain uppercase letters.
    * Must contain lowercase letters.
    * Must contain a digit or special character.
    * Password reuse (you can specify how many unique passwords they need to use before they can go back to the first one).
* Enable "Require Password Change on Next Login" when you create a new user.
  * The first time this user will login on the FME Flow they will be prompted to change their password.
* Enable "Password Expiration"
  * This will ensure that the user has to change their password after X amount of days.
* Don't share credentials or accounts.
  * Every user should have their own account. This so that you can set the previous explained "least privilege" and to be able to audit their actions etc.
* Monitor account audit logs.
  * FME Flow has a build in "System Events" function for the admins. Here they can see if Users create or delete resources. However, you can also see failed login attempts. Repeated login events can be a bad actor trying to guess a users passwords. It can be good to trigger an alarm for this.
* Regularly audit access.
  * You want to regularly go through your user list and see if the user is still active or still needs permissions. Even more important, are all the users still working for your company? Clean up users that should no longer have access to FME FLow!
{% endhint %}
