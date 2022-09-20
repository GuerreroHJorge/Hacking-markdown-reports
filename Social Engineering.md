
## Sumary
Social Engineering

Use social engineering tools to get personal information.

## Descritpion

Using a Ubuntu Server virtual machine in [DigitalOcean](https://www.digitalocean.com/)  create a fake Facebook login to get credentials with [Social Engineering Toolkit](https://fr.wikipedia.org/wiki/Social_Engineering_Toolkit). The goal is to create credible Phishing campaigns for the targets: ITESO students and Facebook users.

## Steps to reproduce:

1. **Requirements**
- Have a [DigitalOcean](https://www.digitalocean.com/)  account.
- Have a [noip](https://www.noip.com/) account.

2. **Create a fake Facebook login**

- Open your DigitalOcean account and create a droplet with Ubuntu.
- Use the password `123.Password` to create your droplet.
- Open a terminal from the ubuntu server. Login with root user.
- Install Setoolkit, using the following steps.
- Install git `apt-get install git`
- `sudo -sH`
- `git clone https://github.com/trustedsec/social-engineer-toolkit/ set/`
- `cd /opt/set`
- `python3 setup.py install`
- `
apt-get install python3-ptyprocess`
- Create a fake Facebook login using the following steps in the ubuntu terminal.
- `setoolkit`
- `1`
- `2`
- `3`
- `2`
- `[Server IP]`
- `facebook.com`
- Now the page is created and you are capturing the credentials.
- Use your noip account to create a hostname for your ip Ubuntu server.
- Use [Emkei.cz](https://emkei.cz/) to send an email from a fake email.
- In this Email send your noip hostname.
- Example: Suspicious activity has been detected on your account. Click on the following link to continue with the security settings.
http://facebok.hopto.org


## References

- [DigitalOcean](https://www.digitalocean.com/)
- [noip](https://www.noip.com/)
- [Install python3-ptyprocess deb package](https://ubuntu.pkgs.org/16.04/ubuntu-main-i386/python3-ptyprocess_0.5-1_all.deb.html)
- [Setoolkit Error](https://waglerocks.com/issues-and-fixes/something-went-wrong-printing-the-error-no-module-named-pexpect/)
- [Setoolkit Tutorial](https://pablokribo.wordpress.com/2016/06/20/install-setoolkit-on-ubuntu-14-04/)
