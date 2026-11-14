# Part 02 — History of Social Networks and Social Platforms

**Research snapshot:** 13 November 2026  
**Purpose:** Understand how online communities, profiles, friend graphs, feeds, photo sharing, video, short-form video, recommendations and creator ecosystems developed—and what those histories teach us about modern product design.

---

## 1. Social media was not a single invention

Today, we group Instagram, YouTube, X, Facebook, Reddit, LinkedIn, Snapchat and TikTok under the label *social media*. Social media is not one application, one company or one inventor's creation. It is a combination of features and user behaviours that evolved over several decades.

Early forms of online social interaction included:

- Electronic mail and mailing lists.
- Bulletin Board Systems (BBSs).
- Usenet newsgroups.
- Online chat rooms and instant messaging.
- Multi-user games and virtual communities.
- Blogs and personal home pages.
- Photo- and video-sharing services.
- Profile-based social network sites.
- Mobile-first social applications.
- Algorithmically ranked content platforms.

These products addressed different needs: conversation, identity, community, publishing, entertainment, professional relationships, discovery and live interaction.

### A useful academic definition of a social network site

A 2007 academic paper by danah boyd and Nicole Ellison describes social network sites as web-based services where users can:

1. Create a public or semi-public profile.
2. Articulate a list of connections.
3. View and navigate their own and other users' connection lists.

This definition is useful, but not every social product must fit this narrow pattern. Content and community platforms such as YouTube or Reddit may organise interaction differently.

**Use careful wording:** Calling SixDegrees an early recognisable social network site is more accurate than calling it the first form of online social interaction. Online communities, buddy lists, dating profiles and discussion networks existed before it.

## 2. The 1970s–1990s: online communities before modern social apps

### Bulletin Board Systems (BBSs)

From the late 1970s and through the 1980s, personal-computer users could connect to a host computer or BBS through a dial-up modem. A BBS operator ran a computer as a community service. Users posted messages, exchanged files, visited discussion areas and sometimes played online games.

A simplified connection worked like this:

1. A user connected a computer and modem to a telephone line.
2. The modem dialled the remote BBS system.
3. The host computer accepted the session.
4. The user browsed message boards, files or chat features.
5. The user ended the session and disconnected.

Many BBSs served local communities. They were not equivalent to today's always-on, globally hosted cloud services.

### Usenet

Usenet emerged in the late 1970s as a distributed discussion system organised into topic-based newsgroups. Users read and posted messages through different servers. Groups focused on particular interests. The system did not require one central social-media company.

### Online services and chat

Services such as CompuServe, The Source and AOL packaged discussion, news, email, chat, shopping and other content for consumers. Instant-messaging services helped make presence indicators and buddy-list communication familiar to mainstream users.

**Lesson:** Modern group, community, chat and forum features are newer implementations of long-standing user needs.

## 3. The 1990s: personal pages, blogs and profiles

The Web made it easier to publish personal identities and information. Users created home pages, listed interests, shared photos and linked to other people. Blogs popularised regular publishing, chronological posts and comments. Online communities added profiles and member directories.

Individual pieces of today's social products were developing separately:

- Profile pages.
- Public posts.
- Friend and buddy lists.
- Comments and messages.
- Discussion communities.
- User directories and search.

Not every website offered all of these features at the same time.

## 4. 1997 — SixDegrees.com: a recognisable social-network pattern

SixDegrees.com launched in 1997. The 2007 academic review describes it as combining profile creation, visible friends lists and browsing of friends-of-friends in one website. Around 1998, users could browse friends lists. The site reached millions of users but closed in 2000.

### Why was the idea important?

Earlier online tools often addressed separate needs: chat lists, directories, personal web pages or dating profiles. SixDegrees brought identity and an explicit social graph together in one place.

### What is a social graph?

A social graph models users or entities as **nodes** and relationships between them as **edges**.

```text
User A ---- follows/friends ---- User B
   |                              |
   |                              |
User C ---- follows/friends ---- User D
```

Modern platforms may support different relationship types:

- **Friend:** often a mutual connection.
- **Follow:** usually a one-way relationship.
- **Subscribe:** receive updates from a person or channel.
- **Block:** restrict access or interaction.
- **Mute:** reduce or hide content without necessarily blocking the account.

### Business lesson from SixDegrees

A good product idea is not enough. Internet access, user habits, product-market fit, monetisation and infrastructure maturity also matter. An early product may arrive before its market is ready, but it is not safe to assume that technology alone caused its failure.

## 5. 2002 — Friendster: discovery through friends of friends

Friendster launched in 2002. Academic histories describe its use of friends-of-friends relationships to help people discover one another. The product began in a dating and social-discovery context and gained early users through word of mouth.

As Friendster grew, technical problems were reported. Its servers and databases were not ready for rapid growth, and users experienced performance problems and interruptions.

### Technical lesson

It is not necessary to overbuild an architecture for massive scale before a product has users. However, ignoring expected load, data modelling, caching, capacity planning, monitoring and reliability is dangerous.

Growth from 50,000 to 500,000 users may create more than ten times the work. Relationships and feed interactions can add complexity beyond the raw account count.

## 6. 2003 — MySpace: identity and self-expression

MySpace launched in 2003. According to historical accounts, it attracted users who were dissatisfied with Friendster and other social sites. It became especially visible for profile customisation and music/band communities. Users could make their profile pages visually distinctive through HTML and CSS customisation.

### MySpace's differentiators

- Personal profile identity.
- Friends lists and comments.
- Music and band discovery.
- Creator and fan interaction.
- Extensive customisation of profile appearance.

MySpace shows that self-expression and community identity can be strong product differentiators.

### The trade-off

Highly customisable profile surfaces can create security, compatibility, performance and consistent-user-experience challenges. A platform must balance user freedom with safe and predictable rendering.

## 7. 2003 — LinkedIn: the professional graph

LinkedIn originated in 2002, when Reid Hoffman and colleagues began working on the idea, and officially launched on 5 May 2003 according to LinkedIn's company history. Its central purpose was professional identity, work relationships, hiring, jobs and business connections.

This matters because not every social network is entertainment-focused.

A professional platform needs different data and trust signals:

- Work history and skills.
- Employer and education information.
- Professional connections.
- Job listings and applications.
- Company pages.
- Recruitment and business tools.

**Lesson:** The target audience and the user's task shape the data model. A creator platform, dating service, professional network and gaming community should not blindly use the same product blueprint.

## 8. 2004–2006 — Facebook: from a campus directory to a broad social platform

Facebook launched on 4 February 2004 as TheFacebook for Harvard students. A Harvard Gazette historical article describes the early idea as an online student directory and identity/connection experience. The service later expanded to other universities; in 2005, “The” was dropped from the name; in 2006, registration opened to a wider audience.

Meta's company timeline records the News Feed launch on 5 September 2006 and the registration expansion on 26 September 2006.

### The product shift introduced by News Feed

Previously, users often visited friends' profiles individually. News Feed brought friends' activities into one central stream. This shifted navigation from profile-by-profile browsing to an aggregated feed experience.

### User backlash: a lesson from a feature launch

When News Feed launched, users raised privacy and visibility concerns. This is an important product lesson: aggregation may be technically useful but can feel intrusive when visibility and consent expectations are unclear. User experience, privacy controls, communication and defaults must be designed together.

### What News Feed implies for architecture

At scale, a feed is more than a simple `SELECT posts` database query. A system must decide:

- Which sources provide candidate posts?
- Which posts are eligible for a particular user?
- Which privacy, block and mute restrictions apply?
- Should ordering be chronological or ranked?
- How should duplicate content and spam be handled?
- How should pagination and caching work?

## 9. 2005 — YouTube: reducing friction in video publishing

YouTube was registered in February 2005, according to the company's 15-year retrospective. Its early purpose was to make it easy for people around the world to share video. On 23 April 2005, the “Me at the zoo” video was uploaded.

YouTube did not invent video production. It made the consumer experience of uploading and sharing online video easier.

### The hidden technical challenge of a video platform

A video platform is substantially more complex than an image-upload form:

1. Receive very large files.
2. Handle interrupted uploads.
3. Validate formats, duration and file integrity.
4. Transcode videos into multiple resolutions and bitrates.
5. Generate thumbnails and metadata.
6. Deliver streaming segments.
7. Manage global bandwidth and CDN costs.
8. Support copyright, safety and age-related review workflows.

A YouTube-style product needs object storage, media processing, queues, transcoding workers, streaming protocols and CDN architecture. The detailed design appears in later parts of this handbook.

## 10. 2005 — Reddit and topic-based community design

Reddit launched in 2005 as a community-oriented discussion product. Its core pattern focused more on topic-based communities, submissions, comments and voting than on a personal friend graph.

This illustrates two different product models:

- **Friend-graph product:** “What are my friends or followed creators sharing?”
- **Interest/community product:** “What is being discussed in the topics I care about?”

A social platform must decide whether discovery is based on an identity graph, topic graph, creator graph or a combination.

## 11. 2006 — Twitter (later X): short public messages and real-time conversation

Twitter's original idea developed during brainstorming at the Odeo company. The Computer History Museum and Twitter's own retrospective record Jack Dorsey's first “twttr” post on 21 March 2006. The public service launched in July 2006.

The original 140-character limit was related to SMS constraints. The basic product unit was a short status update. Users adopted conventions and features such as `@` mentions, hashtags and retweets, helping the service become a network for public conversation and real-time information.

### Why did short messages work?

- Low effort to compose.
- Fast publishing.
- Simple interaction in the mobile/SMS era.
- Public replies and conversations.
- Timely news, event and community updates.

### Technical implication

High-frequency short text may be cheaper than video in terms of storage and bandwidth, but it still creates real-time public distribution, spam, abuse, search, trending and moderation challenges.

### From Twitter to X

In 2023, the Twitter brand was rebranded as X. When studying the product's history, separate features from the Twitter era from later company and product changes. This handbook uses **X** for the current platform name and **Twitter** when referring to the historical service or brand.

## 12. From 2007 onward — smartphones and app stores

Touchscreen smartphones, app stores, built-in cameras, location features, notifications and faster mobile data changed social experiences.

Compared with a Web-only experience, mobile applications could:

- Upload directly from the camera.
- Receive push notifications.
- Use location and device sensors.
- Integrate with phone contacts when permission and platform policies allow it.
- Provide native media capture and editing.
- Offer an always-available entry point through an app icon.

However, a mobile application is not automatically more private. Permissions, background collection, device identifiers and analytics SDKs need controls.

## 13. 2009–2012 — messaging and photo-first mobile social products

Mobile-first applications made social behaviour more immediate, camera-centred and convenient.

### WhatsApp (2009)

Mobile messaging and groups made phone-number and contact-network communication familiar to many users. A messaging-first product has different data, permission and security requirements from a public-feed social network.

### Instagram (2010)

Instagram is a useful case study in product focus. FTC case materials include 2010 records describing Kevin Systrom and Mike Krieger reworking Burbn around photo sharing. Reporting by CBS on the founders describes the transition from a location/check-in concept to a focused photo-sharing application. Instagram's iOS app launched in October 2010.

**Why the pivot matters:** Burbn included many activities and features, but the team observed that photo sharing was the strongest area of user interest. Narrowing the product can make its main experience clearer.

Instagram's early strengths included:

- A phone-camera-first workflow.
- Quick photo sharing.
- Filters and editing as simple creative tools.
- A follow graph.
- Visual profiles and feeds.
- Hashtags and discovery as the product expanded.

The story is not simply “filters created success”. Mobile camera habits, product simplicity, the sharing network, creator behaviour, distribution and execution all contributed.

### Snapchat (2011)

Snapchat's early idea was camera-based communication using disappearing Snaps. Snap's own early founder post describes the 2011 App Store launch and how high-school users used the product for spontaneous photo messaging.

Ephemeral content proposed a different expectation: not every shared moment had to become a permanent public profile post.

Later, Stories changed how users shared temporary sequences. Temporary media does not guarantee privacy. Recipients may take screenshots, record the screen, use an external camera or retain backups. Product wording should not promise unrealistic secrecy.

## 14. The 2010s: multiple social product patterns

During this decade, social platforms diversified:

| Pattern | Example type | Main relationship or content model |
|---|---|---|
| Photo-first sharing | Instagram | Visual posts and follow graph |
| Ephemeral camera messaging | Snapchat | Direct sharing and temporary Stories |
| Public microblogging | Twitter/X | Short text and public conversation |
| Video library and channels | YouTube | Video creators, subscriptions and recommendations |
| Professional identity | LinkedIn | Work graph, skills and jobs |
| Topic communities | Reddit | Communities, voting and comments |
| Group messaging | WhatsApp/Telegram-style services | Private groups and direct conversations |
| Livestreaming | Twitch-style services | Live creator/audience interaction |
| Decentralised social networking | Mastodon-style services | Federated servers and interoperable protocols |

No single feed, profile or social-graph model is best for every audience.

## 15. 2016–2018 — Douyin, TikTok and short-video recommendations

ByteDance's company timeline records the launch of Douyin in China in 2016 and TikTok outside mainland China in May 2017. TikTok's newsroom announced the unification of musical.ly and TikTok in 2018.

The short-form video model combined mobile-native capture and editing, reusable audio, creator tools, swipe-based viewing and personalised recommendations.

### Important distinctions

- **Douyin:** Product for the mainland China market.
- **TikTok:** International product/brand for markets outside mainland China.
- **musical.ly:** A separate short-form video application acquired by ByteDance and merged into TikTok in 2018.

These products have related ownership and history, but their country versions, infrastructure, moderation and regulatory environments should not be assumed to be identical.

### The recommendation shift

In a traditional friend-graph feed, content from followed accounts may dominate. In a recommendation-led short-video feed, the system can discover creators and content from user-interest signals even when the user has not followed the creator.

Possible signals include:

- Video watch duration and completion.
- Rewatch behaviour.
- Likes, shares, comments and saves.
- “Not interested” feedback and skips.
- Creator and content metadata.
- Language and regional relevance.
- Safety and policy eligibility.

Production ranking formulas are platform-specific and are not fully public. Do not guess a company's exact algorithm and present the guess as fact.

## 16. How the core engine of social networks evolved

### Era A — Profile and friend-list model

The user profile, friends list and directory were central. Main technical work included identity, profile storage, relationship management and basic search.

### Era B — Feed model

Content from different sources appeared in one central timeline. Main technical work included candidate collection, permission checks, ranking or chronological ordering, pagination and caching.

### Era C — Media-platform model

Images, audio and video became central. Main technical work included object storage, file validation, processing, thumbnails, transcoding, streaming, CDN delivery and copyright/safety review.

### Era D — Mobile-first interaction model

Camera, GPS, push notifications and native application experiences became important. Main technical work included iOS/Android clients, device permissions, mobile networking, offline/retry handling and app releases.

### Era E — Recommendation-led discovery

Systems began estimating user interests to recommend content. Main technical work included event pipelines, candidate generation, ranking, experimentation, model evaluation, feedback and safety constraints.

### Era F — Creator and business ecosystems

Creators, brands, advertisers, subscriptions, payments and analytics became part of the product. Main technical work included payouts, fraud controls, billing, identity verification, accounting, advertising policy and regulatory compliance.

## 17. Platform success is not caused by features alone

Social-network growth may involve several network effects and business factors:

- **Direct network effect:** More people in the same network can make communication more useful.
- **Indirect network effect:** More creators can attract viewers, and more viewers can attract creators.
- **Content supply:** Enough useful and fresh content must exist.
- **Discovery:** Users need to find relevant people and content.
- **Retention:** Users need a reason to return.
- **Distribution:** Invitations, app stores, search, referrals and partnerships can bring users.
- **Trust:** Spam, scams, harassment and unsafe content must be manageable.
- **Reliability:** Login, feed, uploads and messages must work consistently.
- **Economics:** Revenue must support compute, bandwidth, staff, creators and safety operations.

A platform can have a clever algorithm and still fail if it lacks unique content, trust, a clear audience or sustainable unit economics.

## 18. Practical engineering lessons from platform history

| Historical case | What it teaches |
|---|---|
| SixDegrees | Profiles and a visible social graph are a powerful combination, but timing and sustainability matter. |
| Friendster | Growth without adequate technical capacity can damage trust and retention. |
| MySpace | Customisation and subcultures can create identity, but flexibility brings engineering and safety trade-offs. |
| LinkedIn | Audience and purpose shape the data model and trust requirements. |
| Facebook News Feed | Feed aggregation is useful, but privacy expectations and controls must be designed together. |
| YouTube | Video is an infrastructure-heavy product, not just a file-upload form. |
| Twitter/X | Simple posting primitives can lead to complex public conversation, moderation and search requirements. |
| Instagram | Focused scope and mobile-native UX can outperform a feature-heavy concept. |
| Snapchat | Ephemeral UX is a product promise; it should not be confused with guaranteed secrecy. |
| TikTok | Recommendation-led discovery can reduce dependence on following, but requires safety, feedback and evaluation. |

## 19. How to use this history when designing your own platform

Before writing code, answer:

1. Is your product mainly about connecting people, publishing content, professional identity, private messaging, community discussion or entertainment?
2. What is the main object: profile, post, video, message, event, project or community?
3. What is the main relationship: friend, follow, subscriber, group membership or creator-fan relationship?
4. How will a new user discover useful people or content before having a large network?
5. What is the first “aha moment” that makes the product's value clear?
6. Does the first version need a ranked feed, or is a chronological or curated feed enough?
7. Is video genuinely necessary at launch, given its cost and operational complexity?
8. Which safety, privacy and moderation rules must exist before public access?

## 20. Glossary

- **Social graph:** Users or entities and the relationships between them.
- **Friend graph:** Usually a mutual-connection model.
- **Follow graph:** Usually a directed, one-way relationship model.
- **Feed:** A stream of content shown to a user.
- **Timeline:** Often a chronological or activity-based stream.
- **Ranking:** Ordering items according to a scoring or model system.
- **Recommendation:** Predicting which content may be useful or interesting to a user.
- **UGC (User-Generated Content):** Content submitted by users.
- **Creator:** A person or account that publishes original or curated content.
- **Ephemeral content:** Content designed to be available temporarily, subject to the product's implementation and limitations.
- **Microblogging:** Frequent publishing of short-form updates and public conversation.
- **Network effect:** A product's value may increase as more relevant users or participants join.
- **Retention:** Users returning to or continuing to use a product over time.
- **Moderation:** Applying policies to content and account activity.
- **Content provenance:** Information about the origin, creation or transformation of content.

## 21. Self-check questions

1. Why is SixDegrees called an early recognisable social-network site rather than the first form of online social interaction?
2. What technical problems did Friendster reportedly face as it grew?
3. How did MySpace encourage self-expression?
4. How is LinkedIn's professional graph different from an entertainment-focused social graph?
5. Why was News Feed a product and architecture shift?
6. Why does a video platform require more infrastructure than a text-only platform?
7. How did Twitter's original SMS-era constraints influence its post format?
8. What was the product pivot from Burbn to Instagram?
9. Which user behaviour did Snapchat's disappearing messages support, and what privacy caveat remains?
10. How does recommendation-led discovery differ from a feed based only on followed accounts?

## 22. Practical exercise: build a historical product comparison

Choose three platforms from this chapter and complete the table:

| Question | Platform A | Platform B | Platform C |
|---|---|---|---|
| First target user | | | |
| User problem | | | |
| Main content type | | | |
| Relationship model | | | |
| Discovery method | | | |
| Main technical challenge | | | |
| Monetisation direction | | | |
| Safety/privacy concern | | | |
| What would you learn from it? | | | |

Do not compare only logos or features. Compare the product's core idea, user behaviour, architecture and business constraints.

---

## Sources and further reading

1. [boyd & Ellison (2007), *Social Network Sites: Definition, History, and Scholarship*](https://onlinelibrary.wiley.com/doi/10.1111/j.1083-6101.2007.00393.x) — academic definition and history of SixDegrees, Friendster and MySpace.
2. [Computer History Museum — Networking & the Web timeline](https://www.computerhistory.org/timeline/networking-the-web/) — BBSs, online services, Usenet and earlier online communities.
3. [Harvard Gazette — Facebook, 10 years after](https://news.harvard.edu/gazette/story/2014/02/facebook-10-years-after/) — early Facebook context.
4. [Meta — Company information and milestones](https://www.meta.com/about/company-info/) — company timeline, including News Feed and platform milestones; company source.
5. [U.S. House hearing memorandum (GovInfo) — Facebook platform evolution](https://www.govinfo.gov/content/pkg/CHRG-115hhrg30956/pdf/CHRG-115hhrg30956.pdf) — government-published hearing material discussing News Feed and product history.
6. [YouTube Blog — YouTube at 15](https://blog.youtube/news-and-events/youtube-at-15-my-personal-journey/) — YouTube registration and early video-sharing origin; company source.
7. [YouTube Blog — Celebrating 10 Years of YouTube](https://blog.youtube/news-and-events/celebrating-10-years-of-youtube/) — first video and early growth retrospective; company source.
8. [Computer History Museum — March 21: first tweet](https://www.computerhistory.org/tdih/march/21/) — early Twitter concept and first post.
9. [X Blog — Nine years and counting](https://blog.x.com/en/company/nine-years-and-counting) — Twitter's retrospective on community-created features; company source.
10. [LinkedIn Careers — Why LinkedIn](https://careers.linkedin.com/WhyLinkedIn) — company origin and launch history; company source.
11. [Snap Newsroom — Let's Chat](https://newsroom.snap.com/lets-chat) — Snapchat's early product idea and 2011 launch; company source.
12. [ByteDance — Company milestones](https://www.bytedance.com/seed3d/) — Douyin, TikTok and musical.ly milestone timeline; company source.
13. [TikTok Newsroom — musical.ly and TikTok unite](https://newsroom.tiktok.com/musical-ly-and?lang=en) — 2018 merger/unification announcement; company source.
14. [U.S. House select committee document on social media](https://docs.house.gov/meetings/IF/IF00/20230323/115519/HHRG-118-IF00-20230323-SD030.pdf) — historical detail on TikTok/musical.ly in a government-hearing context.
15. [CBS News — How Instagram found its focus](https://www.cbsnews.com/news/instagram-5-years-co-founders-kevin-systrom-mike-kreiger/) — founders' account of Burbn and photo-sharing focus.
16. [FTC court filing — Instagram/Burbn evidence](https://www.ftc.gov/system/files/ftc_gov/pdf/FTCReplytoMetaResponse-CounterstatementofMaterialFacts.pdf) — court-record material describing the 2010 Burbn-to-Instagram pivot.

*Research note:* Product timelines may differ by prototype date, company incorporation, beta date, public launch or app-store availability. The chapter distinguishes these milestones when sources support that distinction. Company histories are identified as company sources; academic and government material provides additional context.
