Hello
-------

`DPL` Hi everybody ! Welcome to Hairy on Security. I'm Damien...

`RPE` I'm Romain

Continuous Security
----

`RPE` ... and this is s basically our message of today :)

`RPE` so if you are manager, now it means you can already leave the room or fall asleep.

`pause`

`RPE` That being said, where do we start? Because security is a rather broad topic to say the least

Threat Modeling
--------

`DPL` Indeed. Security is continuous process, touch any and all level, needs to have a global vision
but I wondered should we deal with such a large scope ?
I seeked for help.
I've been told to look into an interesting.
methodology pushed from M$ and OWASP.

It's called "Threat Modeling".

it's supposed to be really helpful.

`RPE` Ok, nice on a resume, cool to brag during interview people or chat over a beer, but
what does it actually do ?

`DPL` Well, you need to isolate, pick a small a small enoug sub-systems, within your overall solution. For the threat model to remain manageable, that is feasible within a projcet iteration sprint, and to be readable, understood by all.

Identify the threats: STRIDE
-------

`DPL` first step : identifying the threats
and this model provides a mnemonic acronym to list the
diffents categories of threats.

`RPE` Ok, so we have not time to cover that - it would complete separate talk. Let's be practical,
look at one them. For instance, what R stands for ?

`DPL` the threat behind that is user denial (example)

`RPE` How to fix or mitigate the impact as they say ?

`DPL` Audit trails prooving without doubt cred used

Assess the risks: DREAD
-------

`DPL` key aspect => assess the risk business wise. thus DREAD providing a classification scheme

`RPE` Damage meaning how bad would an attack be?

`DPL` Reproducibility - how easy is it to reproduce the attack?

`RPE` Exploitability - how much work is it to launch the attack?

`DPL` Affected users - how many people will be impacted?

`RPE` Discoverability - how easy is it to discover the threat?

`DPL` Id treats + risks behind helps to do ...

`RPE` communication tool between top management and low level expert - making each other language
understandeable by the other one

DeepDive
---

`RPE` Brilliant, we know where to start. let's take a look at our app, now.
Let me guess, it does look fancy, is that a desktop app for creatives ?

`RPE` let's Deep dive => it's a add placement, it's not marketing, high frequency trading
not big data, hadoop, machine learning, not even social,...

`RPE` Not going to help win followers on Twitter, or pick up girls at a local geeky bar or the local hackerspace. (don't laugh I've a girlfiends like that)

Our Use Case
---
#Cool
`DPL` True, it's a good old fashion enterprise app. Quite boring to chat about over a beer.

`RPE` unless we throw some docker in 

`DPL` we could, but I have better and trendier , heard about :


`RPE` Java framwork

Spring Security 6mn
---

`RPE` what was appealing to me in this stack was the spring sec plumbering coming with it.
It brings solid foundation for ACL

`DPL` man in the middle attack

`RPE` Spring Secu supports HSTS - qui indique au client que seul https sera utilisé.

`DPL` and what clickjacking ?

`RPE` frameOptions().sameOrigin()

`DPL` and the infamous XSS attacks ?

`RPE` that too - along Cross site scripting forgery, il me fournit une solution  à base crsf Token, in short - a shit load of fancy acronyms to brag at parties

`DPL` yep, and let's not forget a skeleton for audit trails and security logging

`DPL` like the one you need to address the previously mentione R of STRIDE - repudiation threat.

pause

Intranet
----

`DPL` That being said, I'm not that worried in the end, because my app is only internal, well hidden
within the confine of a compartimented VLAN, behind a bunch of firewalls.

`RPE` Yeeaaahhh, about that. Don't you think it's a bit naive of you ? I mean you do have user
connectiong to your app from their laptop?

`DPL` Yep, and also mobile+tablets

`RPE` of course they are... And from those, I'm guessing they also to the internet

`DPL` I know where ur getting at - and to make it worse, some has even root privliges, plus not managed. BYOD example

`RPE` Bring your own desaster! Bottom line is, internet is just a short
hop away...

`DPL` But I don't have to worry - I got firewalls !!!! :D

Firewall 8mn
---------

`DPL` Well, fw are securing stuff, aren't they ? :)

`RPE` No, they are not. FW blocks access to unused ports - but your app needs to be accessed, therefore
the port to it needs to be open, isn't it ?

`DPL` Yes

`RPE` FW mostly aims are helping networking traffic, reducing unneeded load on the system. Its usual usage
does not provide security to *your* app. It reduces DoS attacks, but does not protect apps itself.

`DPL` Ok. But my app has to be reachable to be used. The port can t be closed. 

`RPE` You look at how they are used. If you open a port send mails, it should only have SMTP, for
instance.

Sidenote about this, I generally grade how ineffective a security is by the number of port
being uselessly blocked.

`DPL` So if you can't get email using POP...

`RPE` .. Bad

`DPL` If IT blocks VPN ...

`RPE` ... same.

`DPL` If I can't SSH to the system from my network?

`RPE` Worse and pointless, with a SSH outbound, you can connect to a remote server, and then piggy back
your way inside the IT. However, with all those ports being closed or blocked, you did provide a
very strong complete illusion of security.

`DPL` While making everyday tasks in the company, a living hell. (in the sake of security => bad
usability).

`RPE` OK, so bottom line is the key to securing app is protocol and content filtering,

in java apps we all have a Rpx in from of our systems so why not asking them to clean our the ...


Our Data 11mn
=====

`DPL` ok so filter content, clean but also need to returns data

Our Data Encrypt
---

`DPL` no business, no backend uber, no wire transfer - basically no fund to get hacked to the dark web

`RPE` Always nice to have

`DPL` But a nice data mash up, typical "employee productivity tool", such as

* employee address, phonee number
* salaries, financial package
* current deals and opportunities

ping pong

* PII - bound by law to keep private - especially here in Germany
* restricted - on top of being confidential of course
* confidential

`DPL` OK, so we need to keep this secure

`RPE` Which means encrypting all data that go through the system, from one end to an other.

Encrypt the front-end 12mn
-------

`DPL` ok, so first let's start by the front - no other way around it, I need to encrypt everything
and use SSLde bout en bout, commencons alors par le front, on prévoit évidemment de tout servir en https

`RPE` Right, SSL is secure , but doing it correctly requires a lot of work - it's an art in itself.

`DPL` And requires constant monitoring and following updates thoroughly. even the biggest companines
must deals with crisis, certificates being compromised or propagtation of unauthorized certificates
(but still trusted by most browser). And BTW, who spotted it. SSL it out.dated. It's TLS now :)

`DPL` can your https server to detect new weakness and obsolete packages

`RPE` ok, on the front, we're set and good. Let's look at the backend.

Encryp the backend
-------

`RPE` Recap => encrypt: App to DB

`DPL` And also the *data* in the DB

ref: hack ashley madison

2FA / SSO: 13mn
----

`RPE` So for the users 
2FAfor strong auth and SSO for confort

CI: 14mn
=========

`DPL` Nowadays CI holds secrets than can be used to hack app 
=> needs to be secure too => battlefield has extended to encompass
all chains
New SPoF of our infra

So secret can not be put in: code, configuration, 

Where do we put our secrets?

`RPE` You need a dedicated tool for putting our secret in a Vault

secret management is not easy

`DPL` But the secrets are not the only weakness. 

`RPE` CI is about building you app and 99% of your app is not your code. Dependencies... from the Internet that you trust obviously... :)

`DPL` mirror all you get, and check the checksum.

`RPE` model pushed by RH with Satelite, Java/Nexus

`DPL` Well manage your artifacts!

pause

cloud: 17mn
----

`RPE` wrap up: App built! Let's deploy?

`DPL` where?

`RPE` I don't to manage this shit. We go to the cloud.

`DPL` Now you want to trust someone else conputer?

`RPE` don't be, cloud forces u to be more secure, system always rebuild

`DPL` which is better than 10y old sys with no patches

`RPE` netflix story

`DPL` And your are still not safe: look at Meltdown. It's still not fixed.

`RPE` Shortly: be ready to be hacked.

Firefigthers: 19mn
----

`RPE` github story

`DPL` status page sB

`RPE` Equifax

`DPL` The question is not if but when.

`RPE` And real fire fighter and contiunously training.

So define what you are suppose to do and check for it. This is the model of SELinux,

`RPE` OK, so time to wrap up - what did we talk about during all this time:

Conclusion: 22mn
==========

`DPL` see the big picture, analyse risks, use threat modelling to see clearly where u stand

`RPE` don't ever think you are actually safe

`DPL` ...not even behind VLANs, and FWs

`RPE` your data is not safe either

`DPL` ...so encrypt

`RPE` which means management secrets used 2FA

`DPL` ..with SSO because: useability is not excuse for lack of security - and security is not an excuse for a lack useability

`RPE` Also don't forget that the battefield has extended to new territories

`DPL` such as continuous integration, delivery and cloud

`RPE` finally, be *ready* to fight fire - because you are going to be haked

`DPL` ... or you are already.
