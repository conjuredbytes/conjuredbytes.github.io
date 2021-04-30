---
layout: post
title: Extra Considerations for Domain and Registrar Security
---

Registering a domain name is probably the easiest step in the pipeline
from cool idea to cool project. We've all got a few "cool idea" domains registered and sitting around, right? Assuming you actually do something with that cool domain you'll probably pick a registrar, set up your nameservers, and
forget it. You'll rarely log back into your registrar.

However, your domain name is one of the most important
links in the availability and security of your projects. Below are some
extra considerations I believe you should explore while deciding
where and how you want to register your domains.

## Choosing a registrar

Choose a well-known and established registrar with transparent ownership
information. Their legal and registration policies should be easy to
find and read. They should be easy to contact and quick to respond to
inquiries. You'll rarely contact your registrar but when you do it's
likely to be for a significant or time-sensitive issue.

Supporting two-factor authentication in their control panel is a no
brainer. There should be immutable logging and alerting of all
significant activity on the account such as user logins or changes to
domain configuration. You should be able to set a contact email address
for the registrar separate from the address listed in your domain's
WHOIS contact information. Preferably one that isn't hosted on a domain
in the same account in case there's ever an issue with your name servers causing email deliverability issues. 

## Consider ccTLDs carefully

Country code top-level domains, e.g. .us, .ca, .uk are intermingled in
politics. Choosing to use a ccTLD, especially a foreign-to-you ccTLD can
cause your domain to be affected by the politics of the ccTLD's nation.
For example, [*a country could leave a
union*](https://www.zdnet.com/article/81000-uk-owned-eu-domains-suspended-as-brexit-transition-ends/),
[*a government could
collapse*](https://www.inverse.com/article/8672-the-bizarre-afterlife-of-su-the-domain-name-and-last-bastion-of-the-ussr),
or [*a people could reclaim their home from colonial
powers*](https://www.theregister.com/2019/05/27/io_domains_uk_un/ ".io was just too cool to pass up, ok?").

## Registrar and registry locks

First as a reminder, your registrar is the company you paid and who
registered the domain name for you e.g. GoDaddy, Namecheap, etc... The
registry is the entity that operates the top-level domain you registered
within. For example, .com and .net's registry is [*Verisign*](https://www.verisign.com/). Every top-level
domain has a registry that operates it.

Domains can be affected by various status codes called EPP codes. There
are two kinds, client codes and server codes. Client codes can be added
and removed by the registrar and server codes can only be added and
removed by the registry. There are quite a few of these codes that mean
a plethora of different things but we're just going to pay attention to
the ones that prevent the transfer, change, or deletion of your domain.

These are the codes we care about for the purposes of this post:

[*https://www.icann.org/epp\#clientTransferProhibited*](https://www.icann.org/epp#clientTransferProhibited)

[*https://www.icann.org/epp\#clientUpdateProhibited*](https://www.icann.org/epp#clientUpdateProhibited)

[*https://www.icann.org/epp\#clientDeleteProhibited*](https://www.icann.org/epp#clientDeleteProhibited)

[*https://www.icann.org/epp\#serverTransferProhibited*](https://www.icann.org/epp#serverTransferProhibited)

[*https://www.icann.org/epp\#serverUpdateProhibited*](https://www.icann.org/epp#serverUpdateProhibited)

[*https://www.icann.org/epp\#serverDeleteProhibited*](https://www.icann.org/epp#serverDeleteProhibited)

You can see what codes are enacted by looking up your domain's WHOIS
information.

### Registrar locks

Your registrar at minimum should have already registrar locked your
domain by applying the clientTransferProhibited status code. Thus
causing registrars to reject transfer requests for your domain name.
You'd need to log into your control panel or contact the registrar to
remove this status code before your domain could be transferred out of
your control. This is probably enough for most people.

### Registry locks

If your domain is high value and likely to be the recipient of frequent
targeted social engineering attacks you should registry lock it. Doing
this makes changes to your domain much more difficult both for you and
would be attackers. Your registrar will have to manually contact the
registry on your behalf and ask for the specific status codes to be
added or removed. 

For example, if an attacker was able to log into your registrar
control panel and serverUpdateProhibited and serverTransferProhibited were applied to your domain they still wouldn't be able to make changes to authoritative name servers or transfer the domain until an
actual person reviewed it and asked the registry to remove the status
codes. This out-of-band step adds a significant layer of difficulty. 

Registry locks are difficult to get applied on most registrars as they
add significant overhead to managing your domains. They are usually only
applied by enterprise focused registrars like [*CSC*](https://www.cscglobal.com/global/web/csc//domains-and-trademarks.html) or [*MarkMonitor*](https://markmonitor.com/). If you're using a retail registrar
you'll probably have to call and specifically ask for registry locks be applied. Even then they may not enact them for you.

Enterprise registrars are enterprise expensive so if you're not an
enterprise and you really want to registry lock your domain a workaround
is registering yourself as a reseller on [*OpenSRS*](https://opensrs.com/), transferring your
domains to yourself, and paying them \$300 per domain to have them
[*manage the registry lock*](https://opensrs.com/domain-add-ons/).


## WHOIS phishing and email bombs

To prevent targeted phishing attacks WHOIS information should not
identify a specific individual. Use a generic name like
'DNS Admin', a generic email address like 'domains@example.com', and a
specifically purposed phone number for domain management.

Adversaries will sometimes use an [*email
bomb*](https://en.wikipedia.org/wiki/Email_bomb) on your WHOIS contact
addresses to hide important alerts from your registrar in an avalanche
of spam in your inbox. This was part of the attempt to [*hijack
Fastmail's domains in
2014*](https://fastmail.blog/2014/04/10/when-two-factor-authentication-is-not-enough/).
Make sure you're filtering and labeling your email in such a way that
important emails from your registrar are always visible to you.

## Understand *who is* proxying your WHOIS and why it matters

When using a WHOIS proxy service take care to note who is running the
proxy service. It's usually your registrar or a subsidiary of the
registrar who runs these but not always. Proxies replace your
information in the WHOIS database with their own. This keeps your
information private but can potentially open you up to exploitation as
the information in WHOIS is frequently used for management of your
domain. For example, the 'Administrator Contact' email address in WHOIS
is the email address used to verify ownership of a domain. This address
is frequently used in transfer requests as well as domain validated TLS
certificates.
