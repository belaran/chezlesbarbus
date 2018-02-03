* RPE is :large_blue_circle: - does it work ?
* DPL is :red_circle: - does it work ?

Hello
-------

:red_circle: `DPL` Hi everybody ! Welcome to Hairy Security. I'm Damien. I'm a security specialist who knows nothing about Java...

:large_blue_circle: `RPE` ... and I'm Romain, a so-called Java expert, who knows even less about security...

:red_circle: `DPL` Together, we are going to talk about security, or rather how to integrate security consideration, during you development process.

(pause)

:large_blue_circle: `RPE` Where do we start? Because security is a rather broad topic to say the least ?

(((click))))

Threat Modeling 01:00
--------

:red_circle: `DPL` There are solutions for that, one of them being Threat Modelling from M$ and OWASP.

:large_blue_circle: `RPE` Ok, it sounds nice to have on a resume. And probably cool to brag during interview, or with people over a beer, but is it more than just some usual BS ? What does it do for you ?

:red_circle: `DPL` Well, it gaves you a framework or rather an inventory of things to consider about the security of your app.
It is a daunting task.
You need to isolate, pick a small sub-systems, within your application.

:large_blue_circle: `RPE` Oh, OK, so it helps you to keep the threat model undercontrol and manageable.

:red_circle: `DPL` Yes and it can even fit in your sprints, and to be readable, understood by all.

:large_blue_circle: `RPE` OK, I'm on board now! Let's say how to use this Threat modeling of yours.

:red_circle: `DPL` Basically it has two parts - identify by acronyms: STRIDE and DREAD.

(((click)))

Identify the threats: STRIDE
-------

:red_circle: `DPL` first step : identifying the threats by *categories*.

:large_blue_circle: `RPE` Ok, so we have no time to cover all of that - it would complete separate talk. Let's be practical, let's look at one them. For instance, what this R stands for ?

:red_circle: `DPL` the threat behind that is *user* denial (example)

:large_blue_circle: `RPE` And how to fix or mitigate the impact as they say ?

:red_circle: `DPL` *Audit to trails*, ex: employee lies about a t-rex. You prove his login was used.

Assess the risks: DREAD 03:00
-------

:large_blue_circle: `RPE` OK, now I got what STRIDE is, in the broad sense, but what about this other fancy acronym, DREAD ?

:red_circle: `DPL` DREAD is meant to describe *risks* in a language understanable by the company in order to assess them by understanding the possible damages.

:large_blue_circle: `RPE` By damage, you mean how bad would an attack would be on our business?

:red_circle: `DPL` Exactly.

(ping pong)
:large_blue_circle: `RPE` Cool. Then, let's go through, briefly each of those letter.

:large_blue_circle: `RPE` Reproducibility ? :red_circle: `DPL` - how easy is it to reproduce the attack?

:large_blue_circle: `RPE` Exploitability ? :red_circle: `DPL` - how much work is it to launch the attack?

:large_blue_circle: `RPE` Affected users ? :red_circle: `DPL`-  how many people will be impacted?

:large_blue_circle: `RPE` Discoverability ? :red_circle: `DPL` - how easy is it to discover the threat?

:red_circle: `DPL` So the goal is to *identify* and *measure* the risk behing the threat.

:large_blue_circle: `RPE` OK, what I really like about all of this is that it's a brilliant *communication tool* between top management and low level expert - making each other language
understandeable by the other one. Sort of UML for security.

:red_circle: `DPL` Exactly.

:large_blue_circle: `RPE` If do like UML

(pause)

(((click)))

Use Case
---

:large_blue_circle: `RPE` Brilliant, now we know where to start. So let's talk application in a bit more concrete manner. Let's see describ a potential use case for an app.

:red_circle: `DPL` Yes, let's assume we have a regular, web-based Java app. A simple thing being deployed as WAR.
A simple WAR file

:large_blue_circle: `RPE` Let's make it very simple. An internal app for employee, nothing sexy, nor fancy: it doing high frequency trading,  no big data, hadoop, no machine learning, not even social app,...

:red_circle: `DPL` #coolapp

:large_blue_circle: `RPE` Exactly!

(pause)

:red_circle: `DPL` So now, let's discuss a bit how this app is going to be designed.

:large_blue_circle: `RPE` Well, it's a Java app, so you have to throw in a shit load of frameworks right ? it's need to Hibernate the shit out of your Play framework, right ? It also needs to build by Gradle, because Maven is for has been.. And so on...

:red_circle: `DPL` (rolleyes)

:large_blue_circle: `RPE` But the goods news it that security is like any other technical concerns - like logging. It has also Open Source framework. They are many out there, but let's take a look at a rather famous, complete one: Spring Security.

(((click)))

Spring Security 6mn
---

:red_circle: `DPL` OK,  I don't know anything about Java, so what this is doing for us ?

:large_blue_circle: `RPE` Well, it's actually quite  appealing. It brings a all stack with many "security plumbering" being done for you. It gives you a very solid foundation to deal with authentification and access control within your app.

:red_circle: `DPL` OK, but does it handle man in the middle attack, for instance ?

:large_blue_circle: `RPE` Yep, Spring Secu does support HSTS - which ensures to the clients that only HTTPS is being used.

:red_circle: `DPL` And what clickjacking ?

:large_blue_circle: `RPE` Yep, it does it too. (frameOptions().sameOrigin())

:red_circle: `DPL` and the infamous XSS attacks ?

:large_blue_circle: `RPE` that too - along Cross site scripting forgery, using CRSF Token.

:red_circle: `DPL` yep, and don't forget a skeleton for audit trails and security logging.

:large_blue_circle: `RPE` Like the one you need to address the previously mentione R of STRIDE - repudiation threat. Yes! it also provides supports for that...

(pause)

:large_blue_circle: `RPE` Bottom line is that there is a lot of security *threats* to a web app nowdays, and you'll need something like Spring Security to help you ensure your webapp is able to cope with those.

(pause)

(((click)))

Intranet 06:00
----

:large_blue_circle: `RPE` That being said, we don't have to be to worried for our app... After all, it's only internal, right ? It's thus well hidden within the confine of a compartimented VLAN, behind a bunch of firewalls.

:red_circle: `DPL` Yeahhh :) Let's be serious. You know like me that this app is going to be used by most employee, using their laptop or desktop machine, that are most likely unmanaged. Meaning, they have root access and install whatever malware they came across.

:large_blue_circle: `RPE` Not even,  mobile+tablets,

:red_circle: `DPL` BYOD / BYOD. So we have a bunch of users using unsafe device to access our app.

:large_blue_circle: `RPE` ... And all those devices also access the internet in the same time. So basically, any hacker is only one hop away from our so called secure internal app.

:red_circle: `DPL` But I don't have to worry - I got firewalls !!!! :D

Firewall 8mn
---------

:large_blue_circle: `RPE` Yes, this is the most common misconception about FW. People thinks they provided security, while what they actually do is just QoS over the network.

:red_circle: `DPL` That, you have to explain to me. Because I'm a security expert and I have deployed FW as part of my design.

:large_blue_circle: `RPE` As you should. But remember FW blocks access to some port right ?

:red_circle: `DPL` Yes.

:large_blue_circle: `RPE` But generally those port are not used or not supposed to be used from an external point. But your app ports they need to be accessed, for your user to access the service, right ?

:red_circle: `DPL` Yes

:large_blue_circle: `RPE` So, you have to let this traffic goes thru. Which means that any potential hacks will go thru this port - utterly ignoring all the closed port you have blocked. Basically going right around you FW.

:red_circle: `DPL` OK, I see your point. But my app has to be reachable to be used. The port can't be closed.

(((click)))

:large_blue_circle: `RPE` Exactly. So the real trick is to *analyze* and *monitor* the content of the traffic. For instance, if you have a port open to send email, it should only be used for SMTP. Valid SMTP, and nothing else.

Sidenote about this. As a consultant I've been to many different IT, at many different companies. There, I generally graded how *ineffective* security was by the number of port being uselessly blocked.

:red_circle: `DPL` So if you couldn't get to your email using POP...

:large_blue_circle: `RPE` .. Bad!

:red_circle: `DPL` If the IT were blocking your VPN ...

:large_blue_circle: `RPE` ... Stupidly bad! I need my VPN for Red Hat to help you!

:red_circle: `DPL` And no SSH access for you, just for an other user they trust,

:large_blue_circle: `RPE` ... even more stupidfly bad and also pointless, with a SSH outbound, you can connect to a remote server, and then piggy back your way inside the IT (to the audience) - don't laugh, i've actually DONE that at some customers site.

:red_circle: `DPL` With all those ports being closed or blocked, you did provide a perfect illusion of security

:large_blue_circle: `RPE` ... While making everyday tasks in the company, a living hell. (in the sake of security => bad usability).

(pause)

:red_circle: `DPL` OK, so bottom line is the key to securing app is protocol and content filtering.

:large_blue_circle: `RPE` It's actually quite nice, because you reduce the scale of the attack a java dev has to worry. Anything going beyond the scope of what the app should get will already be dropped by the filtering.

(((click)))

(pause)

Our Data 11mn
=====

:red_circle: `DPL` Now, let talk about data... In our use case, we have no business, no backend uber, no wire transfer - basically no fund to get hacked to the dark web

:large_blue_circle: `RPE` But we said it's a  typical "employee productivity tool", so it has data such as

* employee address, phonee number
* salaries, financial package
* current deals and opportunities

ping pong

* PII - Personally identifiable information - bound by law to keep private - especially here in Germany
* restricted - on top of being confidential of course
* confidential

:red_circle: `DPL` OK, so we need to keep this secure

:large_blue_circle: `RPE` Which means *encrypting* all data that go through the system, from one end to an other.

Encrypt the front-end 12mn
-------

:red_circle: `DPL` ok, so first let's start by the front - no other way around it, we need to encrypt everything and use SSL and HTTPS

:large_blue_circle: `RPE` Right, SSL is secure , it's easy to configure - generally less than 10'. But keeping it safe and running smoothly requires a *lot of work*...

:red_circle: `DPL` Yes, it's heavy. It's something you will do only once a year and if you fail you take all your clients down but you don't even know it. I'm not even talking about a compromised or leaked certificate.

:large_blue_circle: `RPE` Ok, but let's say we did that... We're good now, right? SSL is safe?

:red_circle: `DPL` Well, no, SSL it outdated. It's TLS now :)

:large_blue_circle: `RPE` ok, on the front, we're good. Let's look at the backend.

(pause)

(((click)))

Because, the communication between the app and your DB (either it's NoSQL à la mongo or some regular SQL db) can be spy-ed on. You need to ensure that no one can access priviliged communication..

:red_circle: `DPL` some more encryption there, to set up and maintain. And not all of the DB have support for that - MongoDB used to be lacking in this regards for instance.

:large_blue_circle: `RPE` But that's not all. The data lives in the DB. So on the system's storage. Hacker can potentially get access to the system running the DB.

(((click)))

:red_circle: `DPL` So you may also need to encrypt data there. But you have to be smart about it. Encrypting everything has a definitive cost in performance and resource, but encrypting the *wrong* thing is even worse!

:large_blue_circle: `RPE` And a perfect, somewhat recent, example, is the hack of Ashley Madison. Remember, it was a "adult dating website"... where one could try to find a mistress online. And they did everything right, they did hash the user's password. But not their email nor physical adress, and real name. All one needed to blackmail you! And the hack actually *led to people comitting suicide* because of that!

ref: http://money.cnn.com/2015/09/08/technology/ashley-madison-suicide/index.html

:red_circle: `DPL` Ohh... This can escalate quite quickly :)

(pause)

(((click)))

2FA / SSO: 13mn
----

:large_blue_circle: `RPE` OK, so now our app have its Java framework to secure itself, all its communications have been secure by encryption, but we do still need to let legitimate users access it.

:red_circle: `DPL` Yes, and they need to also to prove that they are legitimate users, so to ensure a *strong authentification*.

:large_blue_circle: `RPE` And this is where you need to have 2FA in place, not just simple password

:red_circle: `DPL` neither a lookup to the LDAP or Kerberos.

:large_blue_circle: `RPE` But, btw what is 2FA ?

:red_circle: `DPL` (damien explains)

:large_blue_circle: `RPE` 2FA is the only real way to have strong authentification, but one of the issue with it, it that can be quite uncomfortable for users. You need to always put out our token generator or your phone, and thus many users are fighting it, arguing it harms their productivity.

:red_circle: `DPL` And this is why you also need to have a proper SSO solution in place (to explain).

:large_blue_circle: `RPE` example

:red_circle: `DPL` Yes, this is why security constraint can NOT be used to justify poor UX - look at Slack, for instance. You don't even a password, and it's still secured!

(pause)

:large_blue_circle: `RPE` OK, now our app have been more/less secure. But nowdays, the battefield of security has extended quite a lot. People often don't realise it, but one can be attacked or hacked by other means than just exploiting a defect in the app.

CI: 14mn
=========

:red_circle: `DPL` Nowadays CI holds secrets than can be used to hack app
=> needs to be secure too => battlefield has extended to encompass
all chains
New SPoF of our infra

So secret can not be put in: code, configuration,

Where do we put our secrets?

(((click)))

:large_blue_circle: `RPE` Yes, this is core of the issue. Secret management is *not* easy. And in these day and age, you need automation and thus a dedicated tool to manage those (like Ansible Vault)

:red_circle: `DPL` But the secrets are not the only weakness.

:large_blue_circle: `RPE` Indeed! CI is all about building your app and 99% of your app is *not* your code. Dependencies are fetch from all over the place... and this from the Internet - that you then trust implicitly!

:red_circle: `DPL` mirror all you get, and check the checksum.

:large_blue_circle: `RPE` which, btw, has been the model pushed by Red Hat with Satelite for years, but also in the Java world with repository such as Nexus, Artifactory and so on.

:red_circle: `DPL` Well manage your artifacts!

(pause)

cloud: 17mn
----

:large_blue_circle: `RPE` OK, so our app have been built with security in mind, its internal behavior is secure by Spring security, we ensure strong authentification with 2FA and ensure a good user experience with SSO. Last, we secured the CI env and now our app is built, and ready to be deployed. So... let's go and deploy it ?

:red_circle: `DPL` where?

:large_blue_circle: `RPE` I don't to manage this shit. Let's do what the cool kids are all doing - going "cloud native".

:red_circle: `DPL` Now you want to trust someone else conputer?

:large_blue_circle: `RPE` Well, I see your point, but actually, I think cloud is more secure than "in house".

:red_circle: `DPL` How so ?

:large_blue_circle: `RPE` Cloud deployment forces to update your system,and you are constantly building, fresh version of your system.

:red_circle: `DPL` which is better than 10y old sys with no patches

:large_blue_circle: `RPE` my point exactly. True story: look at netflix are running with 2 days old vm.

:red_circle: `DPL` But even with a fresh, up to date system, your are still not safe: look at Meltdown. It's still not fixed.

:large_blue_circle: `RPE` ...Which bring us to our next, and most important point. Security is not only about patching and being up to date. It's also about being *ready* to be hacked.

(pause)

Firefigthers: 19mn
----

:large_blue_circle: `RPE` A few years ago, now, Github had a massive DDOS attacked against them. They even kept their users informed through their twitter account. They were both very transparent about it but also actively fighting off the attack. Their team were both prepared to be hack and ready to react accordingly.

:red_circle: `DPL` status page sB

:large_blue_circle: `RPE` This kind of transparency is actually crucial. Look at the mess Equifax did in the US by *not* communicating immediatly about their breach.

:red_circle: `DPL` They have endangered millions of people credit rating and the fact that the breach was hidden, did not end up helping it resolve it quickly.

:large_blue_circle: `RPE` In short, The question is not if you are hacked but when you are hacked.

:red_circle: `DPL` Like fire fighter, who are contiunously training to fight fire, your team needs to be ready to actively face an attack.

:large_blue_circle: `RPE` Like a fire in a building you want to have smoking detector and fireproof door.

(ping pong)

:red_circle: `DPL` Which translate, in IT terms, in solution like IDS / SE Linux ...

:large_blue_circle: `RPE` ... and its Java counter part, the infamous Security Manager! That everbody here is using right ?

:red_circle: `DPL` container security

(pause)

:large_blue_circle: `RPE` OK, so time to wrap up - what did we ramble about for the last twenty minutes.....

Conclusion: 22mn
==========

:red_circle: `DPL` see the big picture, analyse risks, use threat modelling to see clearly where u stand

:large_blue_circle: `RPE` don't ever think you are actually safe

:red_circle: `DPL` ...not even behind VLANs, and FWs

:large_blue_circle: `RPE` your data is not safe either

:red_circle: `DPL` ...so encrypt what needs to...

:large_blue_circle: `RPE` which means management secrets and using strong authentification

:red_circle: `DPL` ... which does NOT means forgetting useability for the sake security....

:large_blue_circle: `RPE` Also don't forget that the battefield has extended to new territories

:red_circle: `DPL` such as continuous integration, delivery and cloud

:large_blue_circle: `RPE` finally, be *ready* to fight fire - because you are going to be hacked

(pause)

:red_circle: `DPL` Are you sure you are NOT being hacked right now ? :)
