---
layout: post
title: Domain and Registrar Security
---

If you’re like me, and you get a rush of dopamine anytime you register a domain for, “a totally real and awesome webapp I’m definitely going to make someday” you might have a bunch of domains sitting around doing nothing. In reality, If you’re not like me, and you actually get things done, you might have an actually important domain name registered for you’re totally awesome web app. If this is the case, you probably want to make sure it’s secure. 

I did some thinking one day and realized that for all the ways you can secure your website there is often a single point of failure, your domain name. Domain hijacking seems relatively rare, but it happens. Sure, properly configured certificates can potentially alert your site’s visitors to the fact that something’s phishy, but availability is an important aspect of security and getting your domain hijacked will lead to some likely significant downtime. There’s also a whole slew of other issues someone can get up to if they have control of your domain. Someone could assume important email addresses and gain access to more systems or do any number of nefarious things that usually require domain validation. 

Defending against these attacks really boils down to the competence of your domain registrar, and, if hosted elsewhere your DNS servers. For simplicity, I’m just going to assume you’re hosting your DNS servers with your registrar. If your DNS is hosted elsewhere most things discussed here can apply to that service as well. 

## Choosing a registrar

The first layer of defense would be your choice of registrar. I won’t suggest any particular one, but Google yours and see if they have a good track record. Maybe submit a ticket and see how their support experience is. You’ll rarely contact your registrar but when you do it could be for a critical issue, so the speed and competence of their support staff is of paramount importance. 

Your registrar should support some basic security features in their account system. Must have features would include two-factor authentication and an alert system when certain events happen, like someone logging into your account or changing domain settings. These alerts should be delivered to an email address not published in WHOIS records, and, if possible, hosted on a domain not managed in that account. If these features aren’t supported, look elsewhere for a better registrar. 

## Consider ccTLDs carefully

Country code top-level domains, e.g. .us, .ca, .uk, .jp, etc. are intermingled in the laws of their sponsor nation. If choosing a ccTLD that is not native to you make sure you can abide by their laws and know that they might change, and you have no say in the matter. For example, [a country could leave a union](https://www.zdnet.com/article/81000-uk-owned-eu-domains-suspended-as-brexit-transition-ends/), [a government could collapse](https://www.inverse.com/article/8672-the-bizarre-afterlife-of-su-the-domain-name-and-last-bastion-of-the-ussr), [or a people could reclaim their home from colonial powers](https://www.theregister.com/2019/05/27/io_domains_uk_un/). 

## Secured at the registry level

If you’re unfamiliar, the registry and registrar are different entities. The registrar is the company that registered the domain at the registry on your behalf. Domains will have different registries, and some registries support more thorough security options. Verisign, the registry for .com and .net domains supports something called registry locking. When your domain is registry locked the registrar loses some control of your domain and will have to manually contact the registry to remove the lock. When a domain is fully registry locked it will be unable to transfer, delete, change WHOIS information, or change nameservers until the lock is removed. This out-of-band step means that if someone were to gain access to your registrar account, they still wouldn’t be able to do any damage to your domain. 

Registry locks aren’t always easy to get applied to your domains. They add overhead that most retail registrars don’t want to deal with on top of the thousands of “I forgot my password” emails they already get. If you want to registry lock, you have two options. Your first option is to use an enterprise registrar like [MarkMonitor](https://markmonitor.com/) or [CSC](https://www.cscglobal.com/global/web/csc//domains-and-trademarks.html). However, if you go to their websites, you’ll realize there aren’t straight forward prices listed, and it very much is a “If you have to ask, you can’t afford it” situation. If you don’t have enterprise money, you have another option: [OpenSRS](https://opensrs.com/). You can register yourself as a domain reseller on OpenSRS, transfer your domains to yourself, and pay them the 300 some USD per domain to [manage a registry lock for you](https://opensrs.com/domain-add-ons/). 

## WHOIS phishing and email bombs

To prevent targeted phishing attacks, you shouldn’t identify the specific individual who manages your domain via WHOIS information. Use a generic name like “DNS Admin” and a generic email address like domains@example.com. 

You’ll also want to make sure you always get important emails regarding your domain that are sent to the WHOIS contact address. A super l33t hacker-man may use an [email bomb](https://en.wikipedia.org/wiki/Email_bomb) to spam your inbox in an avalanche of spam to hide important notifications regarding your domain. This was part of the attempt to [hijack Fastmail’s domains in 2014](https://fastmail.blog/historical/when-two-factor-authentication-is-not-enough/). Make sure you’re filtering your email in such a way that you’ll never miss an important email.

## Understand *who is* proxying your WHOIS

WHOIS proxy services are usually operated by your registrar, or a subsidiary shell company set up by them, but not always. If you use a proxy service, make note of who’s running it. It might keep your information from being public, but it could open you up to (admittedly niche) methods of exploitation. The data in WHOIS records is often used for functions related to the management of your domain. For example, the Administrator email address can be used to prove ownership and verify domain validated certificates. 

Consider forgoing WHOIS proxy services and follow the advice I mentioned above regarding WHOIS contact data. If you’re an individual and you don’t want your address or phone number published, use a PO box and a Google Voice number. 

Alternatively, if you trust your WHOIS proxy service, just use them. I’m not aware of any significant incidents involving domain hijacking via WHOIS proxy services but it’s theoretically possible. 

There you have it, now you can register your dopamine domains and secure them too. 
