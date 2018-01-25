Hello
-------

`DPL` Hi everybody ! Welcome to Hairy on Security. I'm Damien. I'm a security specialist who knows nothing about Java...

`RPE` ... and I'm Romain. People think I'm a Java expert, but security is not field of expertise. Together, we are going to talk about security, or rather how to integrate security consideration, during you development process.

`DPL` So you have Continuous Integration and we add Security... let's call it continuous security.

`RPE` Exaclty. That being said, where do we start? Because security is a rather broad topic to say the least ? For many java dev or architect it is a daunting task !

Threat Modeling 01:00
--------

`DPL` Indeed. Security is continuous process, touch any and all level, needs to have a global vision

`RPE` How to deal with such a large scope?

`DPL` There are solutions for that, one of them being Threat Modelling from M$ and OWASP.

`RPE` Ok, it sounds nice to have on a resume. And probably cool to brag during interview, or with people over a beer, but is it more than just some usual BS ? What does it do for you ?

`DPL` Well, it gaves you a framework or rather an inventory of things to concider about the security of your app.
It is a daunting task.
You need to isolate, pick a small sub-systems, within your application.
And then you'll be able to keep the threat model undercontrol and manageable.
It can even fit in your sprints, and to be readable, understood by all.

`RPE` OK, I'm on board now. Let's say how to use this Threat modeling.

Identify the threats: STRIDE
-------

`DPL` first step : identifying the threats. To do so, this model provides a mnemonic acronym to list the diffents categories of threats.

`RPE` Ok, so we have no time to cover all of that - it would complete separate talk. Let's be practical, let's look at one them. For instance, what this R stands for ?

`DPL` the threat behind that is *user* denial (example)

`RPE` And how to fix or mitigate the impact as they say ?

`DPL` *Audit trails* proving without doubt cred used

Assess the risks: DREAD 03:00
-------

`RPE` OK, now I got what STRIDE is, in the broad sense, but what about this other fancy acronym, DREAD ?

`DPL` DREAD is ment to describe risks in a language understanable by the company in order to assess them by understanding the possible damages.

`RPE` By damage, you mean how bad would an attack would be on our business?

`DPL` Exactly.

`RPE` Cool. Then, let's go through, briefly each of those letter.

`DPL` Reproducibility - how easy is it to reproduce the attack?

`RPE` Exploitability - how much work is it to launch the attack?

`DPL` Affected users - how many people will be impacted?

`RPE` Discoverability - how easy is it to discover the threat?

`DPL` Id treats + risks behind helps to do ...
YYYYYY

`RPE` OK, what I really like about all of this is that it's a brilliant *communication tool* between top management and low level expert - making each other language
understandeable by the other one. Sort of UML for security.

`DPL` Exactly.

USe Case
---

`RPE` Brilliant, now we know where to start. So let's talk application in a bit more concrete manner. Let's see describ a potential use case for an app.

`DPL` Yes, let's assume we have a regular, web-based Java app. A simple thing being deployed as WAR.
A simple WAR file

`RPE` Let's make it very simple. An internal app for employee, nothing sexy, nor fancy: it does make any ads placement, it's not doing marketing, nor high frequency trading. No big data, hadoop, machine learning, not even social app,...

`DPL` Cool.

`RPE` I agree :) . We are not going win followers on Twitter with this, neither pick up girls at FOSDEM we this thing

`DPL` No, we won't.

(pause)

`DPL` So now, let's discuss a bit how this app is going to be designed.
YYYYY Merge?
`RPE` Well, it's a Java app, so you have to throw in a shit load of frameworks right ? it's need to Hibernate the shit out of your Play framework, right ? It also needs to build by Gradle, because Maven is for has been.. And so on...

`DPL` (rolleyes)

`RPE` But the goods news it that security is like any other technical concerns - like logging. It has also Open Source framework. They are many out there, but let's take a look at a rather famous, complete one: Spring Security.

Spring Security 6mn
---

`DPL` OK,  I don't know anything about Java, so what this is doing for us ?

`RPE` Well, it's actually quite  appealing. It brings a all stack with many "security plumbering" being done for you. It gives you a very solid foundation to deal with authentification and access control within your app.

`DPL` OK, but does it handle man in the middle attack, for instance ?

`RPE` Yep, Spring Secu does support HSTS - which ensures to the clients that only HTTPS is being used.

`DPL` And what clickjacking ?

`RPE` Yep, it does it too. (frameOptions().sameOrigin())

`DPL` and the infamous XSS attacks ?

`RPE` that too - along Cross site scripting forgery, using CRSF Token.

`DPL` yep, and let's not forget a skeleton for audit trails and security logging. Like the one you need to address the previously mentione R of STRIDE - repudiation threat.
<<<<<<< Updated upstream

`RPE` Yep, it also provides supports for that...
=======
YYYYYY
`RPE` Yep, it also provides supports for that But the bottom line here is that there is a lot of security threats to a web app nowdays, and you probably needs something like Spring Security to help you deal with all of those.
>>>>>>> Stashed changes

(pause)

`RPE` But the bottom line here is that there is a lot of security threats to a web app nowdays, and you probably needs something like Spring Security to help you deal with all of those.

Intranet
----

`DPL` That being said, we don't have to be to worried for our app... After all, it's only internal, right ? It's thus well hidden within the confine of a compartimented VLAN, behind a bunch of firewalls. (ironic ton)

`RPE` Yeahhh :) Let's be serious. You know like me that this app is going to be used by most employee, using their laptop or desktop machine, that are most likely unmanaged. Meaning, they have root access and install whatever malware they came across.

`DPL` Yep, and also mobile+tablets, BYOD
YYYYYY
DESASTERS
`RPE` ... And all those devices also access the internet in the same time. So basically, any hacker is only one hop away from our so called secure internal app.

`DPL` But I don't have to worry - I got firewalls !!!! :D

Firewall 8mn
---------

`RPE` Yes, this is the most common misconception about FW. People thinks they provided security, while what they actually do is just QoS over the network.

`DPL` That, you have to explain to me. Because I'm a security expert and I have deployed FW as part of my design.

`RPE` As you should. But remember FW blocks access to some port right ?

`DPL` Yes.

`RPE` But generally those port are not used or not supposed to be used from an external point. But your app ports they need to be accessed, for your user to access the service, right ?

`DPL` Yes

`RPE` So, you have to let this traffic goes thru. Which means that any potential hacks will go thru this port - utterly ignoring all the closed port you have blocked. Basically going right around you FW.

`DPL` OK, I see your point. But my app has to be reachable to be used. The port can t be closed.

`RPE` Exactly. So the real trick is to *analyze* and *monitor* the content of the traffic. For instance, if you have a port open to send email, it should only be used for SMTP. Valid SMTP, and nothing else.

Sidenote about this. As a consultant I've been to many different IT, at many different companies. There, I generally graded how *ineffective* security was by the number of port being uselessly blocked.

`DPL` So if you couldn't get to your email using POP...

`RPE` .. Bad!

`DPL` If the IT were blocking your VPN ...

`RPE` ... Stupidly bad!

`DPL` If you couldn't SSH to the system from your local network?

`RPE` ... even more stupidfly bad and also pointless, with a SSH outbound, you can connect to a remote server, and then piggy back your way inside the IT (to the audience) - don't laugh, i've actually DONE that at some customers site.

`DPL` However, with all those ports being closed or blocked, you did provide a very strong complete illusion of security

`RPE` ... While making everyday tasks in the company, a living hell. (in the sake of security => bad usability).

`DPL` OK, so bottom line is the key to securing app is protocol and content filtering. It's actually quite nice, because you reduce the scale of the attack a java dev has to worry about misusing the *expected* input data. Anything going beyond the scope of what the app should get will already be dropped by the filtering.

(pause)

Our Data 11mn
=====

`RPE` Now, let talk about data...

`DPL` In our use case, we have no business, no backend uber, no wire transfer - basically no fund to get hacked to the dark web

`RPE` But we said it's a  typical "employee productivity tool", so it has data such as

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

`DPL` ok, so first let's start by the front - no other way around it, we need to encrypt everything and use SSL and HTTPS

`RPE` Right, SSL is secure , it's easy to configure - generally less than 10'. But keeping it safe and running smoothly requires a *lot of work* - it's an art in itself.
YYYYY -> rewrite this
`DPL` Yes, it requires constant monitoring and following updates thoroughly. even the biggest companines must deals with crisis, certificates being compromised or propagtation of unauthorized certificates.

(but still trusted by most browser). And BTW, who spotted it. SSL it out.dated. It's TLS now :)

`RPE` ok, on the front, we're good. Let's look at the backend.

(pause)

Because, the communication between the app and your DB (either it's NoSQL à la mongo or some regular SQL db) can be spy-ed on. You need to ensure that no one can access privilged information.

`DPL` some more encryption there, to set up and maintain. And not all of the DB have support for that - MongoDB used to be lacking in this regards for instance.

`RPE` But that's not all. The data lives in the DB. So on the system's storage. Hacker can potentially get access to the system running the DB.

`DPL` So you may also need to encrypt data there. But you have to be smart about it. Encrypting everything has a definitive cost in performance and resource, but encrypting the *wrong* thing is even worse!

YYYYYY: encrypted password! Hashed!
`RPE` And a perfect, somewhat recent, example, is the hack of Ashley Madison. Remember, it was a "adult dating website"... where one could try to find a mistress online. And they did everything right, they did encrypt the user's password. But not their email nor physical adress, and real name. All one needed to blackmail you! And the hack actually led to people comitting suicide because of that!

ref: http://money.cnn.com/2015/09/08/technology/ashley-madison-suicide/index.html

(pause)

2FA / SSO: 13mn
----

`RPE` OK, so now our app have its Java framework to secure itself, all its communications have been secure by encryption, but we do still need to let legitimate users access it.

`DPL` Yes, and they need to also to prove that they are legitimate users, so to ensure a *strong authentification*.

`RPE` And this is where you need to have 2FA in place, not just simple password

`DPL` or a lookup to the LDAP or Kerberos.

`RPE` But, btw what is 2FA ?

`DPL` (damien explains)

`RPE` 2FA is the only real way to have strong authentification, but one of the issue with it, it that can be quite uncomfortable for users. You need to always put out our token generator or your phone, and thus many users are fighting it, arguing it harms their productivity.

`DPL` And this is why you also need to have a proper SSO solution in place (to explain).

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

(pause)

cloud: 17mn
----

`RPE` OK, so our app have been built with security in mind, its internal behavior is secure by Spring security, we ensure strong authentification with 2FA and ensure a good user experience with SSO. Last, we secured the CI env and now our app is built, and ready to be deployed. So... let's go and deploy it ?

`DPL` where?

`RPE` I don't to manage this shit. Let's do what the cool kids are all doing - going "cloud native".

`DPL` Now you want to trust someone else conputer?

`RPE` Well, I see your point, but actually, I think cloud is more secure than "in house".

`DPL` How so ?

`RPE` Cloud deployment forces to update your system,and you are constantly building, fresh version of your system.

`DPL` which is better than 10y old sys with no patches

`RPE` my point exactly. True story: look at netflix and their chaos monkey (chaos monkey).

`DPL` But even with a fresh, up to date system, your are still not safe: look at Meltdown. It's still not fixed.

`RPE` ...Which bring us to our next, and most important point. Security is not only about patching and being up to date. It's also about being *ready* to be hacked.

(pause)

Firefigthers: 19mn
----

`RPE` A few years ago, now, Github had a massive DDOS attacked against them. They even kept their users informed through their twitter account. They were both very transparent about it but also actively fighting off the attack. Their team were both prepared to be hack and ready to react accordingly.

`DPL` status page sB

`RPE` This kind of transparency is actually crucial. Look at the mess Equifax did in the US by *not* communicating immediatly about their breach. They have endangered millions of people credit rating and the fact that the breach was hidden, did not end up helping it resolve it quickly.
YYYYYY
`DPL` The question is not if but when.

`RPE` Likel fire fighter, who are contiunously training to fight fire, your team needs to be ready to actively face an attack.

`DPL` Yes, but one can be ready ?

`RPE` Like a fire in a building you want to have smoking detector and fireproof door.

(ping pong)

<<<<<<< Updated upstream
`DPl` (Satan), an IDS which like a smoke detector , will allow to you know if you are being attacked
=======
`DPL` Which translate, in IT terms, in solution like IDS, SE Linux, and its Java counter part, the infamous Security Manager!

`RPE` (Satan), an IDS which like a smoke detector , will allow to you know if you are being attacked
>>>>>>> Stashed changes
      (SELinux), which is your best line of defense against a breach - it will ensure the hacked has very limited option from the point of penetration
      (Security Manager) exactly the same as a SELinux, but on the JVM level - who here is NOT using the security manager ?

`DPL` container security

`RPE` OK, so time to wrap up - what did we talk about during all this time.

Conclusion: 22mn
==========

`DPL` see the big picture, analyse risks, use threat modelling to see clearly where u stand

`RPE` don't ever think you are actually safe

`DPL` ...not even behind VLANs, and FWs

`RPE` your data is not safe either

`DPL` ...so encrypt what needs to...

`RPE` which means management secrets used strong auth 2FA

`DPL` ..with SSO because: useability is not excuse for lack of security -

`RPE` ... and security is not an excuse for a lack useability

`DPL` Also don't forget that the battefield has extended to new territories

`RPE` such as continuous integration, delivery and cloud

`DPL` finally, be *ready* to fight fire - because you are going to be haked

`RPE` ... or you are already?