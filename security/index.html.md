---
layout: markdown_page
title: Security Best Practices
---

## Other Security Topics

- [Security Team handbook](/handbook/engineering/security/)
- [Security questions from customers, and their answers](/security)

## On this page
{:.no_toc}

- TOC
{:toc}

## Best Practices

1. **Never reuse** a password you use on a company account, not for another
   GitLab service nor for a personal account.
1. Set up [1Password] as your password manager and set a **strong and unique**
   master password.
1. Use 1Password to [generate strong passwords] for any new accounts.
1. When signing up for a new service ask yourself which team members you need to
   **share access** with. There are three types of account access for these services, Individual, OAuth, and Single. All Individual and OAuth account services have a secure note in the 'Shared' vault. This note lists the administrators you can contact to gain access to the service for Individual services or lists the account you can use to get access for OAuth services. During onboarding you should be added to all relevant Individual services by default.
   1. **Individual services** (created manually per person, such as our Google accounts): keep your credentials to yourself by storing them in your 'Personal' vault in the GitLab 1password account.
   1. **OAuth services** (authentication through GitLab or Google accounts, such as for grafana).
   1. **Single services** (services that don't allow individual accounts or where it is too expensive): store the credentials in an appropriate company 1Password vault ('Shared' or otherwise) so that your colleagues can sign in using the same credentials.
1. If 2FA should be on for the new user account, make sure to store recovery codes in the login, and use [1Password TOTP].
1. If you need to give more people access to credentials [move them](https://discussions.agilebits.com/discussion/comment/133692/#Comment_133692) to a vault that they can access. Never duplicate credentials! If needed put them in the 'Shared' vault that the whole company can access or make a suggestion to create a new vault in the "1Password Shared Folders" Google Sheet. Do not share passwords on a per person basis by sharing them via 1Password, this makes it hard to reason about the sharing and doesn't change when the responsibilities change.
1. Do not copy passwords from inside a 1Password vault to a personal password vault or other password store. 1Password should be the only password
vault used for teams. Team passwords should not be duplicated and potentially exposed to compromise in personal password vaults.
1. When asked security questions (what is your favorite pet, etc.) do not answer truthfully since that is easy to research. Make up an answer and write both the question and answer in 1Password.
1. Do not share credentials via email, issue comments, chat etc. This includes
   email addresses to login and API keys. Use 1Password vaults for this. You
   will be invited to applicable vaults after joining the company.
1. If you want to see your vaults or ask to be added to a new one please leave
   a comment in the "1Password Shared Folders" Google Doc.
1. If you're missing an appropriate vault [make a suggestion to mark the relevant cell](https://support.google.com/docs/answer/6033474?hl=en) in the
   "1Password Shared Folders" Google Sheet.
1. Refer to the items with NAME_OF_SITE credentials in VAULT_NAME. For example:
   "for access please see the AOL credentials in the Luddite vault".
1. Do not
   store credentials in a vault if everyone has their own user account for the
   service.
1. Do not let your password manager store the **master password**. It is okay to
   store the login.
1. Do not allow your web browser (e.g. Chrome, Safari) to store passwords when prompted. This presents an unnecessary risk and is redundant as 1Password should serve as the sole password management application.
1. Enable two-factor authentication (2FA) with [1Password TOTP] for your Google, Slack, GitLab.com, and dev.gitlab.org accounts.
1. You can also consider using a [Yubikey](https://about.gitlab.com/2016/06/22/gitlab-adds-support-for-u2f/) with GitLab.
1. Use **Full-Disk Encryption** on your work computer and phone. Mac users may<a name="encrypt-home-folder"></a>
   use [FileVault] (for details, refer to [Apple Support](https://support.apple.com/en-in/HT204837))
   and GNU/Linux users may use LUKS (for the basic idea, refer to the
   [Arch Linux Wiki](https://wiki.archlinux.org/index.php/Dm-crypt)).
   Closing the lid of your laptop, and thus suspending it to RAM, does NOT
   protect you, even if your hard drive is encrypted. Power off your computer
   completely (don’t just suspend it) when you think it’s at risk of falling
   into someone else’s hands, like right before going through customs when
   entering a new country. This defends against memory-based attacks. Read more
   on the matter in [this article](https://theintercept.com/2015/04/27/encrypting-laptop-like-mean/).
1. Set up a screen saver with **password lock** on your laptop. The timeout
   can depend on how you use your laptop.
1. Never leave your unlocked computer **unattended**. Activate the screensaver,
   lock the desktop, or close the lid.
1. If you like to backup your computer make sure the backup drive is encrypted and use a strong password.
1. For backups on macOS (OSX) follow this tutorial: [How to use Time Machine](https://support.apple.com/en-us/HT201250)
1. **Report** suspect situations to an officer of the company.
1. If you have security **suggestions** put them on the [team call agenda].
1. Never **dismiss** a security report as invalid. Keep asking questions until
   the researcher comes to the same conclusion or stops responding.
1. Do not **forward** company emails (@gitlab.com) to a non-company email address.
1. Do not click on links in emails you did not request yourself (requested
   password reset is OK, anything else is suspect).
   **Exception:** During the onboarding process you may receive account
   registration emails for various services GitLab uses. Before clicking these
   links confirm with People Operations that they initialized the process.
   Clicking itself is a problem even when you don't enter a password, because a
   visit can already be used to execute a [0-day attack]. We simulate phishing
   attacks by having an external service send emails to our company email
   addresses to ensure everyone is aware of the threat.
1. If you get strange emails personally or other things related to security feel free to ask our security people for help, [they might be aiming for the company](https://medium.com/starting-up-security/learning-from-a-year-of-security-breaches-ed036ea05d9b).
1. The CEO will not send you an [email to wire cash]. Feel free to verify any
   unusual requests with a video call.
1. During offboarding, your 1Password account is deleted, which includes the **Personal** vault in the GitLab team account. If you want to
   keep your personal passwords, please copy/move them to [your personal local vault or your separate individual account](#1password-private-use).
1. We will configure applications of which we store the passwords in 1Password to [not periodically reset passwords](https://www.cesg.gov.uk/articles/problems-forcing-regular-password-expiry).
1. Do not install software with many known security vulnerabilities (as [listed in the handbook](/handbook/tools-and-tips/#do-not-use)). When in doubt, do not install until after checking with the team by discussing in an issue, and then document the verdict in the handbook.

[1Password]: https://1password.com
[generate strong passwords]: https://support.1password.com/guides/mac/generate-a-strong-password.html
[1Password TOTP]: #1password-totp
[Google Authenticator]: https://support.google.com/accounts/answer/1066447?hl=en
[FileVault]: https://support.apple.com/en-us/HT204837
[team call agenda]: https://docs.google.com/document/d/1JiLWsTOm0yprPVIW9W-hM4iUsRxkBt_1bpm3VXV4Muc/edit
[0-day attack]: https://en.wikipedia.org/wiki/Zero-day_(computing)
[email to wire cash]: http://blog.centrify.com/ceo-fraud-business-email-compromise/

## 1Password Guide

1Password is a password manager. Ideally you memorize one strong password -
hence the name - and let 1Password generate and manage strong, unique passwords
for every site for which you have a login.

### Terminology

Following this guide, it will be helpful to understand a few terms we'll be
using throughout.

- **App:** A native 1Password application (OSX, iOS, Windows, Android).
- **Extension:** A web browser extension/plugin that communicates with the
  **App** to provide access to your passwords securely without leaving the
  browser.
- **Vault:** What 1Password calls any grouping of secure data, such as logins or
  secure notes. Sometimes called a "keychain".

### 1Password

1Password can be used in two different ways - as a standalone application
(by purchasing a standalone license) or as a hosted service (by subscribing).
GitLab uses 1Passwords for Teams which is a hosted service.

If you want to use 1Password for your private passwords not related to your work at GitLab, [there are a few of options](#1password-private-use).

### 1Password for Teams

1Password for Teams stores all **Vaults** on the 1Password servers and allows
for sharing between multiple people on the same team.

Everyone at GitLab should already be signed up for our [Teams account]. This
gives you access to the web interface, allowing you to view the Vaults we've
configured and given you access to.

In addition to the shared vaults such as **Shared**, **Support**,
**Marketing**, each member of the team has a vault called **Personal** which
*only you can see*, and allows you to store personal credentials within our
team's account.

To really get the full benefit of 1Password, you'll need to hook our Teams
account up to one of the native apps.

### Adding the GitLab Team to a 1Password app

This guide will cover setting up the [OSX app]. It's their lead platform and is
the most up-to-date. These instructions may or may not work for the Windows
version.

1. Download and install the 1Password [OSX app].
1. Launch the app.
1. Click "Sign in to your 1Password account" button. If there is no such button
please follow the instructions for [updating 1Password](#1password-update).

Now you'll need the **Emergency Kit** PDF that 1Password told you to save when
you registered your **Teams** account.

If you saved it as a digital PDF file:

1. Open the PDF file
1. Click **Scan QR Code**
1. Drag the scanner window over the QR code on the PDF sheet

If you printed the PDF:

1. Click **Sign In Manually**
1. For **Team URL** enter **gitlab.1password.com**
1. For **Account Key** enter the Account Key from your Emergency Kit
1. For **Email Address** enter your `@gitlab.com` email
1. For **Master Password** enter the password to your **Teams** account (*not*
   the password you created above when you chose "I'm a new user")

After the Team is added, you should see some notifications about vaults being
added to 1Password. By default you'll have **Shared** and **Personal**, and
may have access to others.

### Updating 1Password to support the Teams feature<a name="1password-update"></a>

*Read this section only if you could not follow the instructions in "Adding
the GitLab Team to a 1Password app" section.*

1. At the prompt, choose "I'm a new user". *Note:* This is one source of
   confusion. "I created my Teams account, I'm not new!" Just go with it.
1. Enter a master password, confirmation, and hint. This can (and should) be
   different from the password you used for our **Teams** account. This password
   gates access to your **local, private** Vault on your computer and/or phone.
1. Skip over the remaining dialogs (syncing, newsletter, etc.)
1. You should now have an empty vault called **Primary**.

Because the Teams feature is not available in your current version of 1Password,
we need to update the app to the latest version:

1. Go to **Preferences**
1. Go to **Updates**
1. Click **Check Now**
1. Install the update and relaunch
1. After relaunch, go to **Preferences** again
1. Go to **Teams**
1. Click the **+** icon

### Vaults

Click the **Vault Selector** in the upper-left corner of the window:

![Vault Selector](/handbook/security/1password-vault-selector.png)

**Personal** is your *remote, private* vault that *is* synced to the GitLab
1Password for Teams account, and *can not* be viewed by anyone else on the team,
including admins.

**Shared** is a vault that everyone on the GitLab Teams account has access to
both read and write.

### Browser Extension

Go to [Browser extensions](https://agilebits.com/onepassword/extensions) and
install the extension for whatever browser you're using. You *should not* need a
beta version here.

With the extension installed, you should be able to go to a site that has
credentials stored in our Team vault and log in:

![Mailchimp Login](/handbook/security/1password-login.gif)

---

If you don't see the site listed in the results window, make sure you're using
the correct vault:

![Vault switching](/handbook/security/1password-vault-change.gif)

### Saving Logins

When 1Password detects a login form submission, it may ask if you want to save
the login with a dialog like this:

![Save login](/handbook/security/1password-save-login.png)

If you do want to save it, make sure the appropriate **Vault** is selected
first.

### Several accounts and unlocking the app

Please refer to [1Password FAQ](https://support.1password.com/faq/#i-have-several-accounts-and-vaults-which-password-do-i-use-to-unlock-1password).

This means that if you are planning to use both GitLab team account and a
separate individual account you should first sign in to the individual
account. By doing this you will be able to unlock 1Password app using
Master Password of the individual account.

If you have been using 1Password before joining GitLab, and you receive a prompt
titled **Migrate To Account**, choose **I'll move later**. There is no harm in
doing this, and it is easy to move items between vaults.

### 1Password for your private passwords<a name="1password-private-use"></a>

You are encouraged to use 1Password for your private passwords, not related to your work at GitLab.
This makes it less likely for a security breach to occur. You can purchase a standalone license or
start an individual subscription. While under the GitLab team subscription, it is also possible to create
and use a personal local vault (same features of a standalone license, without the cost).

Please bear in mind that if you decide to purchase a standalone license or create a personal local vault, your data is
stored only in a local folder on your computer. You can optionally sync this
folder to Dropbox or iCloud (if you are using a Mac/iOS) to make it available
on your phone's 1Password app, or on another computer.

Signing up for a subscription seems to be the solution now recommended by the
company behind 1Password.

To create a personal local vault:

1. Go to **Preferences**
1. Go to **Advanced**
1. Under **Local Vaults**, check **Allow creation of vaults outside of 1Password accounts**
1. Enter your Master Password
1. A new local vault (**Primary**) is created outside the GitLab team account
1. If you want to setup sync for your new local vault, go to **Preferences > Sync**

### Two Factor Authentication and Time-based One Time Passwords<a name="1password-totp"></a>

There are several ways to get your Two Factor Authentication (2FA) codes.
You can get them sent via SMS or use an app like Google Authenticator to
generate them. 1Password provides an alternative solution that does not
require using your smartphone: 1Password Time-based One Time Passwords
(TOTP). 2FA codes are displayed directly in the 1Password app running on your
laptop.

To enable TOTP for a saved account:

1. Open 1Password app
1. Go to the item for which you want to set up TOTP
1. Click **Edit** in the bottom right corner
1. Click 3 dots icon
   ![3 little dots](/handbook/security/1password-totp.png)
1. Select **One-Time Password**
1. Click QR code icon that appeared
1. Scan QR code using the transparent window
1. Click **Save**
1. 2FA code should be displayed now

Please refer to the [1Password blog] for more information on how TOTP works.

[1Password blog]: https://blog.agilebits.com/2015/01/26/totp-for-1password-users/

If scanning of QR code using the tranparent window with 1Password Mac app fails on a recent Mac OS, please consider to use 1Password iOS app which could do the same and support Touch ID to login.

### Example Usage<a name="1password-example-usage"></a>

This is an example of how <a href="https://gitlab.com/u/rspeicher">Robert</a>,
one of our developers, uses 1Password:

> Once you fully commit to using 1Password to manage all of your security
> information, it really does make life easier.

> I memorize one strong password and let the app generate
> everything else. Every site I use has a unique password that I can't
> compromise because I don't even know it, and a hacked site can't compromise
> it because the password is never re-used on another site.

> I store my shipping and credit card info in 1Password and use the browser
> extension to quickly fill out shipping and billing information on shopping
> sites.

> I store my passport data, along with a digital scan, in 1Password; drivers
> license info and scan; insurance info; software license keys; any important
> information that needs to be secure but still easily accessible when I need it,
> from anywhere. I sync my personal vault to my personal Dropbox so it's
> available on my phone, tablet, laptop, and desktop.

> Even my 1Password for Teams account information is stored in my personal
> **Primary** vault, with the Emergency Kit PDF as a secure attachment:

> ![Teams Login](/handbook/security/1password-teams-login.png)

> I have no idea what the password is. I've never actually typed it. And that's
> the idea.

### Traveling with 1Password

When traveling with a device that has access to the GitLab 1Password vaults, be
sure to [enable Travel Mode](https://support.1password.com/travel-mode/) in 1Password. Travel Mode removes copies of any
1Password vaults that are not tagged as "safe for travel" from your mobile devices.
None of the GitLab team vaults are marked as safe for travel so you will need
to either create a dedicated travel vault or mark your personal vault as safe for
travel.

Once you have enabled Travel Mode open 1Password on each device you will be taking
with you so that it can sync with 1Password.com and remove any vaults that cannot
be used while traveling.

For more information on Travel Mode and how it works, see the [agilebits blog].

[agilebits blog]: https://blog.agilebits.com/2017/05/18/introducing-travel-mode-protect-your-data-when-crossing-borders/
[1Password for Teams]: https://blog.agilebits.com/2015/11/03/introducing-1password-for-teams/
[Teams account]: https://gitlab.1password.com/
[OSX app]: https://agilebits.com/downloads

## Security Awareness Training

During their first two weeks at GitLab new team members should receive an email
with links to Security Awareness Training. This training covers how to recognize
phishing attacks, how to safely use public wireless networks, and some general
security tips and principles.

### Phishing Tests

GitLab conducts routine phishing tests using a third-party testing platform. All
team members will occasionally receive emails that are designed to look like
legitimate business-related communications but will in actuality be simulated
phishing attacks. Real phishing attacks are designed to steal credentials or
trick the recipient into downloading or executing dangerous attachments. No
actual attempts will be made by GitLab or the third-party testing site to steal
credentials or execute malicious code.

The goal of these campaigns is not to catch people clicking on dangerous links
or punish those who do, but rather to get people thinking about security and the
techniques used by attackers via email to trick you into running malicious
software or disclosing web passwords. If you fall victim to one of these
simulated attacks feel free to take the training courses again or to ask the
security team for more information on what could've been done to recognize the
attack. What you shouldn't do is feel any shame for having clicked on the link
or entered any data, nor should you feel like you need to _cop_ to the security
team and let them know you made a mistake. Making a mistake online is
practically the reason the Internet was invented.

### How to identify a basic phishing attack

When you receive an email with a link, hover your mouse over the link or view
the source of the email to determine the link's true destination.

If you hover your mouse cursor over a link in Google Chrome it will show you
the link destination in the status bar at the bottom left corner of your browser
window.

![Hover Example](/images/phishing/hover-status-bar-example-chrome.png)

In Safari the status bar must be enabled to view the true link destination
(View -> Show Status Bar).

Some examples or methods used to trick users into entering sensitive data into
phishing forms include:

* Using HTTP(S) with a hostname that begins with the name of a trusted
site but ends with a malicious site.

![Malicious Domain](/images/phishing/malicious-domain.png)

* Using a username or password inside the request that corresponds to the name
of a trusted domain and assuming the viewer won't view the whole URL.

![Trick Username](/images/phishing/username-password.png)

* Using a data URI scheme instead of HTTP(S) is a particularly devious means of
tricking users. Data schemes allow the embedding of an entire web page inside
the URI itself. Data schemes will not show the typical green lock in the address
bar of a browser that is customarily associated with a verified SSL connection.

![Data Scheme](/images/phishing/data-scheme.png)

When viewing the source of an HTML email it is important to remember that the
text inside the "HREF" field is the actual link destination/target and the text
before the `</A>` tag is the text that will be displayed to the user.

`<a href="http://evilsite.example.org">Google Login!</a>`

In this case, "Google Login!" will be displayed to the user but the
actual target of the link is "evilsite.example.org".

After clicking on a link always look for the green lock icon and "secure" label
that signify a validated SSL service. This icon alone is not enough to verify the
authenticity of a website, however the lack of the green icon does mean you
should never enter sensitive data into that website.

![Green Lock Example](/images/phishing/green-lock-example.png)

### What to do if you suspect an email is a phishing attack

Whether you believe that you have received an email from our testing platform or
you believe you have received a real phishing attempt, the best thing to do is
to delete the email. GMail also offers the option to report the email directly
to Google as a phishing attempt which will result in its deletion. If you
suspect that the email is targeted specifically at you or GitLab, please
notify the security team so it can be investigated. You can also notify other
team members via Slack. If you forward the phishing email to the security team
please do so as an attachment and not inline. To forward the email as an
attachment from inside GMail:

  1. In the reply options choose "show original"
  1. Choose "download original"
  1. Save to your local drive or Google Drive
  1. Create a new email with the saved email as an attachment

If you receive an email that appears to come from a service that you utilize,
but other details of the email are suspicious -- a private message from a
sender you don't recognize, for example -- do not click on any links in the
email. Instead use your own bookmark for the site or manually type the address
of the website into your browser.

## Using the panic email address

GitLab provides a `panic@gitlab.com` email address for team members to use in
situations that require an immediate security response. Should a team member lose
a device such as a thumb drive, Yubikey, mobile phone, tablet, laptop, etc. that
contains their credentials or other GitLab-sensitive data they should send an
email to `panic@gitlab.com` right away. When the production and security teams
receive an email sent to this address it will be handled immediately. Using this
address provides an excellent way to limit the damage caused by a loss of one of
these devices.
