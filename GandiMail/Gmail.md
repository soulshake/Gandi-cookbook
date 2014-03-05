# Setting up a GandiMail mailbox in Gmail

## Configuring Gandi Mail for Gmail

This page contains instructions for setting up Gmail (aka Mail Fetcher) to send and receive from your Gandi mailboxes. 

*Note: This will allow you to import your GandiMail to your current ''@gmail.com'' inbox – not to be confused with [Google Apps a.k.a. Gmail for your domain](http://wiki.gandi.net/en:domains:management:googleapps).*

### Step 1: Receiving (POP/IMAP)

  - In your Gmail account, go to settings (click the gear icon to the upper right of your inbox, then click "settings")
  - Click the "Accounts" tab at the top.
  - Under "Check mail from other accounts (using POP3)" click "Add a POP3 mail account you own"
  - **Email address:** Enter the email address you want to be able to check from Gmail, i.e. `admin@example.com`, then click "next step" 
  - **Username:** Enter your **email address** again, i.e. `admin@example.com` (`admin` by itself won't work).
  - **Password:** Enter the password you chose when you created the `admin@` mailbox for `example.com`. (This must be a mailbox and not a forwarding address).
  - **POP Server:** Change it to `mail.gandi.net`
  - **Port:** `110` for POP or `995` for POP SSL

If successful, you'll be given the opportunity on the following screen to be able to send mail from the same address.

### Step 2: Sending (SMTP)

  - **Name:** Enter the name you want to appear in the "From:" field of your emails
  - **Email address:** Enter the same email address as in Step 1. Make your other selections and click Next.
  - **Send mail through your SMTP server?** You can send through Gandi SMTP, if you want:
    - **SMTP Server:** `mail.gandi.net` (this will probably pre-populate incorrectly)
    - **Port:** `25`, `465` (with SSL) or `587` (try one or the other)
    - **Username:** Same email address as before, ie `admin@example.com`

If successful, the following screen will request you either click the confirmation link in the email or enter a confirmation code to be able to send mail from the above address.

## Possible errors


### "Authentication failed"

  ```
  Server denied POP3 access for the given username and password.
  Server returned error: "Authentication failed."
  ```
  
  * You may have only entered your username, whereas you need to enter the whole email address.
  * You may be entering the wrong password.
  * You may be trying to add a forwarding address instead of a mailbox.

### "You already have the maximum number of accounts allowed."

You can only set up 5 external POP accounts in Gmail. Consider using a [forwarding address](http://wiki.gandi.net/en:mail:email-mailboxes-and-forwarding-addresses#how-can-i-set-up-e-mail-forwarding) instead.

### "We were unable to locate the other domain."

  ```
  There was a problem connecting to mail.yourdomain.tld
  Server returned error: "We were unable to locate the other domain.
  Please contact your other provider."
  ```

Replace `mail.yourdomain.tld` with `mail.gandi.net`.

### "SSL protocol error."

  ```
  There was a problem connecting to mail.gandi.net
  Server returned error: "SSL protocol error. Please try disabling SSL, 
  or contact your other provider to verify the correct port settings."
  ```

You may have selected "Always use a secure connection (SSL) when retrieving mail" but did not select the correct port for using SSL.

### "Unable to process the account info."

  ```
  Server denied POP3 access for the given username and password.
  Server returned error: "Unable to process the account info."
  ```
  
This error can occur when the wrong port is selected for a given configuration.

### "There was a problem connecting to mail.gandi.net"

  ```
  There was a problem connecting to mail.gandi.net
  Server returned error: "Missing +OK response upon connecting to the 
  server: * OK [CAPABILITY IMAP4rev1 LITERAL+ SASL-IR LOGIN-REFERRALS 
  ID ENABLE AUTH=PLAIN] Dovecot ready."
  ```

You may be trying to use an IMAP port. Gmail does not support IMAP import.

## See also
  * [Google/Gmail/Mail Fetcher support: Get mail from other accounts](http://support.google.com/mail/bin/answer.py?hl=en&answer=21288)
