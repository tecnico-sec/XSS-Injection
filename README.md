Instituto Superior Técnico, Universidade de Lisboa

**Network and Computer Security**

# Lab guide: Cross-Site Scripting (XSS)

## Goals

- Learn how to detect the presence of a XSS vulnerability.
- Learn how to exploit a XSS vulnerability.
- Learn the existing techniques to protect systems against XSS.

## Introduction

For this lab we propose the XSS Attack Lab that is part of the [SEED Labs Project](https://seedsecuritylabs.org/).

Refer to the [lab webpage (XSS)](https://seedsecuritylabs.org/Labs_16.04/Web/Web_XSS_Elgg/) for full details.
In the end of this lab session you are supposed to be able to complete Tasks 1 to 4 of XSS.

Needed Files (1):

- [Description of SEED Labs XSS lab](https://seedsecuritylabs.org/Labs_16.04/PDF/Web_XSS_Elgg.pdf) Tasks 1-4

Follow the document above but try to solve the challenges by yourself. Be inquisitive. Ask yourself why is it working and if there are other methods/solutions to achieve the same results. When you are stuck, check below if we have any tip to help you out.

## Setup

- The address of the vulnerable site is `http://www.xsslabelgg.com` (local to the VM).
- Instructions on how to setup the lab environment are [here](https://github.com/tecnico-sec/Setup).

## Tips

### Task 1: Posting a Malicious Message to Display an Alert Window

- Log in as one of the users `U1` (eg, `alice`) and edit that user's `brief description`

        <script>alert("XSS");</script>
- Log in as another user `U2` (eg, `boby`) and see if you get the alert once you check `U1`'s profile.
- Not working? Check the console (Ctrl + Shift + k). If you copied the string from the pdf file, what appears to be a single quote is actually a special character. Try writing the payload yourself, or rewriting the quote.
- For the second part of this task, add the longer script to `U2`'s `brief description`, and login as a different user to see if you are attacked when checking `U2`'s profile.
- If you want to use `www.example.com` to run your exploits from the `localhost` you might want to add it in `/etc/hosts` as well as in `/etc/apache2/sites-available/000-default.conf`. See Section 2 (Configuring DNS and Configuring Apache Server).  
Also, do not forget to restart `apache`

      sudo service apache2 restart

## Task 3: Stealing Cookies from the Victim’s Machine

- Redirect the attack to a site you control. You can use it's ip address or you might as well use `www.example.com` that is pointing to your localhost (set in Task1).
- A simple way to listen for connections is to use `nc -lv <port>`.
- How to listen to multiple connections? Unfortunately `nc` can only listen to a single connection. If you want to listen to multiple connections you might want to use a site such as `https://postb.in`.

## Task 4: Becoming the Victim’s Friend

- Login as user `U1` and become friend with `Samy`. Take note of what that `GET` request was. That is what you need to replicate.
- Edit Samy's profile accordingly. Then login as `U2` and look at Samy's profile. Is `U2` now friend's with Samy?
- Have you thought about Question 1? and Question 2?

## Task 5: Modifying the Victim’s Profile (Optional)

- Login as user `U1` and see what happens when you change `U1`'s profile. Take note of what that `POST` request was. That is what you need to replicate.
- Edit Samy's profile accordingly. Then login as `U2` and look at Samy's profile. Did `U2`'s profile changed?
- Have you thought about Question 3?

## Task 7: Countermeasures

- Observe what happens when you turn on each of the referred protection methods.
- Were you able to succeed as before?

**Acknowledgments**

Original version: Pedro Adão

Revisions: Nuno Sabino

----

[SIRS Faculty](mailto:meic-sirs@disciplinas.tecnico.ulisboa.pt)
