Hello
-------

`DPL` Hi everybody ! Welcome to Hairy on Security. I'm Damien...

`RPE` ... and I'm Romain. We are going to talk about security, or rather how to integrate security consideration, during you development process.

`DPL` Sort of doing something akin to "Continous Security" - pretty much like we already do Continuous Integration.

`RPE` Exaclty. That being said, where do we start? Because security is a rather broad topic to say the least ? For many java dev or architect it is a daunting task !

Threat Modeling
--------

`DPL` Indeed. Security is continuous process, touch any and all level, needs to have a global vision
but I wondered should we deal with such a large scope ?
I seeked for help.
I've been told to look into an interesting.
methodology pushed from M$ and OWASP.

It's called "Threat Modeling".

it's supposed to be really helpful.

`RPE` Ok, it sounds nice on a resume, and probably cool to brag during interview people or chat over a beer, but is it more than just BS ? What does it actually do for you ?

`DPL` Well, it gaves you a framework or rather an inventory of a sort to think about the security of your app. As you said, it is daunting task, so you need to isolate, pick a small a small enoug sub-systems, within your overall solution. For the threat model to remain manageable, that is feasible within a projcet iteration sprint, and to be readable, understood by all.

`RPE` OK, I'm on board now. Let's say how to use this Threat modeling.

Identify the threats: STRIDE
-------

`DPL` first step : identifying the threats. To do so, this model provides a mnemonic acronym to list the diffents categories of threats.

`RPE` Ok, so we have no time to cover all of that - it would complete separate talk. Let's be practical, let's look at one them. For instance, what this R stands for ?

`DPL` the threat behind that is *user* denial (example)

`RPE` And how to fix or mitigate the impact as they say ?

`DPL` *Audit trails* proving without doubt cred used

Assess the risks: DREAD
-------

`RPE` OK, now I got what STRIDE is, but what about this other fancy acronym, DREAD ?

`DPL` key aspect => assess the risk business wise. thus DREAD providing a classification scheme

`RPE` By damage, you mean how bad would an attack would be on our business? Let's go through, briefly each of those letter.

`DPL` Reproducibility - how easy is it to reproduce the attack?

`RPE` Exploitability - how much work is it to launch the attack?

`DPL` Affected users - how many people will be impacted?

`RPE` Discoverability - how easy is it to discover the threat?

`DPL` Id treats + risks behind helps to do ...

`RPE` OK, what I really like about all of this is that it's a brilliant *communication tool* between top management and low level expert - making each other language
understandeable by the other one. Sort of UML for security.

`DPL` Exactly.

USe Case
---

`RPE` Brilliant, we know where to start. But now, to be more concrete, let's take an application as use case.

`DPL` Yes, let's assume we have a regular, web-based Java app. A simple thing being deployed as WAR.

`RPE` Yes, let's make it very simple. It does make any ads placement, it's not doing marketing, nor high frequency trading. No big data, hadoop, machine learning, not even social app,...

`DPL` Cool.

`RPE` A simple, internal, back end app, doing a mash up of internal data for your company employe. Nothing fancy.

`RPE` We are not going win followers on Twitter with this, neither pick up girls at FOSDEM we this thing

`DPL` No, we won't.

(pause)

`DPL` So now, let's discuss a bit how this app is going to be designed.

`RPE` Well, it's a Java app, so you have to throw in a shit load of frameworks right ? it's need to Hibernate the shit out of your play framework, while being build by Gradle, because Maven is as been... or the other way around ?

`DPL` (rolleyes)

`RPE` And like any other concern, security also have framework. They are many out there, but let's take a look at a rather famous, complete one: Spring Security.

Spring Security 6mn
---

`DPL` OK,  I don't know anything about Java, so what this is doing for us ?

`RPE` Well, it's actually quite  appealing. It brings a all stack with many sec plumbering being done for you. It gives you a very solid foundation to deal with authentification and access control.

`DPL` OK, but does is handles man in the middle attack, for instance ?

`RPE` Yep, Spring Secu does support HSTS - which ensures to the clients that only HTTPS is being used.

`DPL` And what clickjacking ?

`RPE` Yep, it does it too. (frameOptions().sameOrigin())

`DPL` and the infamous XSS attacks ?

`RPE` that too - along Cross site scripting forgery, using CRSF Token.

`DPL` yep, and let's not forget a skeleton for audit trails and security logging. Like the one you need to address the previously mentione R of STRIDE - repudiation threat.

`RPE` Yep, it also provides supports for that.

pause

Intranet
----

`DPL` That being said, we don't have to be to worried for our app... After all, it's only internal, well hidden within the confine of a compartimented VLAN, behind a bunch of firewalls. (ironic ton)

`RPE` Yeahhh :) Let's be serious. You know like me that this app is going to be used by most employee, using their laptop or desktop machine, that are most likely unmanaged. Meaning, they have root access and install whatever malware they came across.

`DPL` Yep, and also mobile+tablets, BYOD

`RPE` Not even talking about those indeed. And all those devices also access the internet in the same time. So basically, any hacker is only one jump away from our app.

`DPL` But I don't have to worry - I got firewalls !!!! :D

Firewall 8mn
---------

`DPL` Well, fw are securing stuff, aren't they ? :)

`RPE` No, they are not. This is the most common misconception about FW. People thinks they provided security, while what they actually do is just QoS over the network.

`DPL` That, you have to explain to me. Because I'm a security expert and I have deployed FW as part of my design.

`RPE` As you should. But remember FW blocks access to some port right ?

`DPL` Yes.

`RPE` But generally those port are not used or not supposed to be used from an external point. But your app ports they need to be accessed, for your user to access the service, right ?

`DPL` Yes

`RPE` So, you have to let this traffic goes throuhg. Which means that any potential hacks will go through this.

`DPL` OK, I see your point. But my app has to be reachable to be used. The port can t be closed.

`RPE` Exactly. So the real trick is to *analyze* and *monitoring* the content of this allowed traffic.For instance, if you have a port open to send email, it should only be used for SMTP.
Sidenote about this. As a consultant I've been to many different IT, at many different companies. There, I generally graded how *ineffective* security was by the number of port being uselessly blocked.

`DPL` So if you couldn't get to your email using POP...

`RPE` .. Bad!

`DPL` If the IT were blocking your VPN ...

`RPE` ... Extra bad!

`DPL` If you couldn't SSH to the system from your local network?

`RPE` ... even more of a bad mark.  And pointless, with a SSH outbound, you can connect to a remote server, and then piggy back your way inside the IT (to the audience - don't laugh, i've DONE that).

`DPL` However, with all those ports being closed or blocked, you did provide a very strong complete illusion of security

`RPE` While making everyday tasks in the company, a living hell. (in the sake of security => bad usability).

`RPE` OK, so bottom line is the key to securing app is protocol and content filtering. It's actually quite nice, because you reduce the scale of the attack a java dev has to worry about misusing the *expected* input data. Anything going beyond the scope of what the app should get will already be dropped by the filtering.

Our Data 11mn
=====

`DPL` ok so filter content, clean but also need to returns data, right ? And what about the confidentiality of those ?

`RPE` No business, no backend uber, no wire transfer - basically no fund to get hacked to the dark web

`DPL` But a nice data mash up, typical "employee productivity tool", such as

* employee address, phonee number
* salaries, financial package
* current deals and opportunities

ping pong

* PII - bound by law to keep private - especially here in Germany
* restricted - on top of being confidential of course
* confidential

`DPL` OK, so we need to keep this secure

`RPE` Which means *encrypting* all data that go through the system, from one end to an other.

Encrypt the front-end 12mn
-------

`DPL` ok, so first let's start by the front - no other way around it, I need to encrypt everything
and use SSL and HTTPS

`RPE` Right, SSL is secure , it's easy to config - generally less than 10', but keeping it safe and running smoothly requires a *lot of work* - it's an art in itself.

`DPL` Yes, it requires constant monitoring and following updates thoroughly. even the biggest companines must deals with crisis, certificates being compromised or propagtation of unauthorized certificates
(but still trusted by most browser). And BTW, who spotted it. SSL it out.dated. It's TLS now :)

`RPE` ok, on the front, we're set and good. Let's look at the backend.

(pause)

Because, the communication between the app and your DB (either it's NoSQL à la mongo or some regular SQL db) can be spy-ed on. You need to ensure that no one can access privilged information nonetheless.

`DPL` some more encryption there, to set up and maintain.

`RPE` But that's not all. The data lives in the DB. So on the system's storage. Hacker can potentially get access to the system running the DB.

`DPL`So you may also need to encrypt data there. But you have to be smart about it. Encrypting everything has a definitive cost in performance and resource, but encrypting the *wrong* thing is even worse!

`RPE` And a perfect, somewhat recent, example, is the hack of Ashley Madison. Remember, it was a "adult dating website"... where one could try to find a mistress online. And they did everything right, they did encrypt the user's password. But not their email nor physical adress, and real name. All one needed to blackmail you! And the hack actually led to people comitting suicide because of that!

ref: http://money.cnn.com/2015/09/08/technology/ashley-madison-suicide/index.html

(pause)

2FA / SSO: 13mn
----

`RPE` OK, so now our app have it Java framework to secure it's internal plumbering, all the communication have been secure by encryption, but legitimate users do need to connect to it, right ,

`DPL` and yes, and they need to also to prove that they are legitimate users, so to ensure a strong authentification.

`RPE` And this is where you need to have 2FA in place, not just simple password

`DPL` or a lookup to the LDAP or Kerberos.

`RPE` The issue is that 2FA can be quite uncomfortable for users. You need to always put out our token generator or your phone

`DPL` And this is why having a proper  SSO solution in place is crucial.

`RPE` Yes! Too often, security constraint are used to justify poor UX.

(pause)

`RPE` OK, now our app have been more/less secure. But nowdays, the battefield of security has extended quite a lot. People often don't realise it, but one can be attacked or hacked by other means than just exploiting a defect in the app.

CI: 14mn
=========

`DPL` Nowadays CI holds secrets than can be used to hack app
=> needs to be secure too => battlefield has extended to encompass
all chains
New SPoF of our infra

So secret can not be put in: code, configuration,

Where do we put our secrets?

`RPE` Yes, this is core of the issue. Secret management is *not* easy. And in these day and age, you need automation and thus a dedicated tool to manage those (like Ansible Vault)

`DPL` But the secrets are not the only weakness.

`RPE` Indeed! CI is all about building your app and 99% of your app is *not* your code. Dependencies are fetch from all over the place... and this from the Internet - that you then trust implicitly!

`DPL` mirror all you get, and check the checksum.

`RPE` which, btw, has been the model pushed by Red Hat with Satelite for years, but also in the Java world with repository such as Nexus, Artifactory and so on.

`DPL` Well manage your artifacts!

pause

cloud: 17mn
----

`RPE` OK, so our app have been built with security in mind, its internal behavior is secure by Spring security, we ensure strong authentification with 2FA and ensure a good user experience with SSO. Last, we secured the CI env and now our app is built, and ready to be deployed. So... let's go and deploy it ?

`DPL` where?

`RPE` I don't to manage this shit. Let's do what the cool kids are all doing - going "cloud native".

`DPL` Now you want to trust someone else conputer?

`RPE` Well, actually, using the cloud might be more secure that your own computer. Cloud deployment forces to update your system,and you are constantly building, fresh version of your system.

`DPL` which is better than 10y old sys with no patches

`RPE` true story, look at netflix story about this (chaos monkey)

`DPL` And your are still not safe: look at Meltdown. It's still not fixed.

`RPE` Which bring us to our next, and most important point. You need to not only prepare your security but also be ready to be hacked.

Firefigthers: 19mn
----

`RPE` A few years ago, now, Github had a massive DDOS attacked against them. They even kept their users informed through their twitter account. They were both very transparent about it but also actively fighting off the attack. Their team were both prepared to be hack and ready to react accordingly.

`DPL` status page sB

`RPE` This kind of transparency is actually crucial. Look at the mess Equifax did in the US by *not* communicating immediatly about their breach. They have endangered millions of people credit rating and the fact that the breach was hidden, did not end up helping it resolve it quickly.

`DPL` The question is not if but when.

`RPE` Likel fire fighter, who are contiunously training to fight fire, your team needs to be ready to actively face an attack.

`DPL` Yes, but one can be ready ?

`RPE` Like a fire in a building you want to have fireproof door, smoke detector and emergency stairs case.

(ping pong)

`DPL` Which translate, in IT terms, in solution like Satan, SE Linux, and its Java counter part, the infamous Security Manager!

`RPE` (Satan), an IDS which like a smoke detector , will allow to you know if you are being attacked
      (SELinux), which is your best line of defense against a breach - it will ensure the hacked has very limited option from the point of penetration
      (Security Manager) exactly the same as a SELinux, but on the JVM level - who here is NOT using the security manager ?

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
