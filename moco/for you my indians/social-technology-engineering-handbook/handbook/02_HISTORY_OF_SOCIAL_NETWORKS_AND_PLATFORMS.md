# Part 02 — History of Social Networks and Social Platforms

**Research snapshot:** 13 November 2026  
**Purpose:** Samajhna ki online communities, profiles, friend graphs, feeds, photos, video, short-form video, recommendations aur creator ecosystems kaise evolve hue—and unse modern platform design ke kya lessons milte hain.

---

## 1. Social media ek single invention nahi tha

Aaj hum Instagram, YouTube, X, Facebook, Reddit, LinkedIn, Snapchat aur TikTok ko “social media” bol dete hain. Lekin social media ek single app, ek company ya ek inventor ki invention nahi hai. Ye decades mein develop hue features aur user behaviours ka combination hai.

Online social behaviour ke early forms:

- Electronic mail and mailing lists.
- Bulletin Board Systems (BBSs).
- Usenet newsgroups.
- Online chat rooms and instant messaging.
- Multi-user games and virtual communities.
- Blogs and personal home pages.
- Photo-sharing and video-sharing sites.
- Profile-based social network sites.
- Mobile-first social apps.
- Algorithmically ranked content platforms.

In products ne alag problems solve ki: conversation, identity, community, publishing, entertainment, professional relationships, discovery aur live interaction.

### Social network site ki useful academic definition

Danah boyd aur Nicole Ellison ke 2007 academic paper ke according, social network sites web-based services hain jahan users:

1. Ek public ya semi-public profile bana sakte hain.
2. Apne connections ki list articulate kar sakte hain.
3. Apni aur doosron ki connection lists ko view/traverse kar sakte hain.

Ye definition useful hai, lekin har social product ko isi narrow definition mein fit karna zaroori nahi. YouTube jaise content/community platforms ya Reddit jaise topic-led communities social interaction ke different patterns use karte hain.

**Important wording:** “First recognizable social network site” bolna “history ka first social media ever” bolne se zyada accurate hai. SixDegrees ko commonly first recognizable profile + visible-friends-list combination ke roop mein describe kiya jata hai, lekin usse pehle online communities, buddy lists, dating profiles and discussion networks already the.

## 2. 1970s–1990s: Social apps se pehle online communities

### Bulletin Board Systems (BBSs)

1970s ke end aur 1980s mein personal computer users dial-up modem se kisi host computer/BBS ko call kar sakte the. BBS operator apna computer service ke roop mein run karta tha. Users messages post karte, files exchange karte, forums/discussion areas use karte aur kabhi-kabhi online games khelte.

**Kaise kaam karta tha?**

1. User computer aur modem telephone line se connect karta.
2. Modem remote BBS system ko dial karta.
3. Host computer session accept karta.
4. User message boards, files ya chat use karta.
5. Session end hone par disconnect.

BBS aksar local/community scale par hota tha. Aaj ke cloud-hosted always-on global service jaisa model nahi.

### Usenet

Late 1970s se Usenet topic-based newsgroups ka distributed discussion system tha. Users different servers se messages read/post karte. Groups particular topics par focused hote. Ismein central single social-media company ka model zaroori nahi tha.

### Online services and chat

CompuServe, The Source, AOL aur doosre online services ne discussion, news, email, chat, shopping aur content ko consumer-friendly packages mein organize kiya. Instant messaging services ne presence/buddy-list communication ko mainstream banane mein role play kiya.

**Lesson:** Aaj ke “group”, “community”, “chat” aur “forum” features kaafi purane user needs ka modern implementation hain.

## 3. 1990s: Personal pages, blogs and profiles

Websites ne public identity/personal publishing ko easier banaya. Users apni home pages, interests, photos and links share karte the. Blogs ne regular publishing, chronological posts and comments ko popularise kiya. Online communities ne profiles aur membership directories add ki.

Is period mein social product ke individual parts develop ho rahe the:

- Profile page.
- Public posts.
- Friends/buddy lists.
- Comments and messages.
- Discussion communities.
- User directory/search.

Har website ke paas ye saare parts ek saath nahi the.

## 4. 1997 — SixDegrees.com: recognisable social-network pattern

SixDegrees.com 1997 mein launch hua. 2007 ke academic review ke according, isne profile creation, visible friends list aur friends ke friends ki lists browse karne jaise concepts ko ek site par combine kiya. 1998 ke around users friends lists browse kar sakte the. Site millions of users tak pahunchi, lekin 2000 mein band ho gayi.

### Ye idea important kyun tha?

Pehle online tools alag-alag user needs solve karte the—chat list, directory, personal webpage, dating profile. SixDegrees ne identity + explicit social graph ko ek place par joda.

### Social graph kya hota hai?

Users ko nodes aur relationships ko edges ke roop mein model kar sakte hain.

```text
User A ---- follows/friends ---- User B
   |                              |
   |                              |
User C ---- follows/friends ---- User D
```

Aaj ke systems mein relationship types alag ho sakte hain:

- Friend: often mutual connection.
- Follow: one-way relationship.
- Subscribe: content updates receive karna.
- Block: access/interaction restrictions.
- Mute: content visibility reduce/hide karna.

### SixDegrees ka business lesson

A good product idea alone enough nahi. Internet access, user habits, product-market fit, monetisation and infrastructure maturity bhi matter karte hain. Early product apne time se pehle ho sakta hai, lekin iska matlab automatically ye nahi ki product ko sirf technology ki wajah se failure hua.

## 5. 2002 — Friendster: friends-of-friends discovery

Friendster 2002 mein launch hua. Academic history ke according, product ne friends-of-friends ke through logon ko connect karne ka idea use kiya. Ye dating and social discovery ke context se start hua aur word-of-mouth se early users gain kiye.

Friendster ki growth ke saath technical problems report hui: servers aur databases rapid growth ke liye ready nahi the; users ko performance failures and interruptions face karne pade.

### Technical lesson

Growth ke pehle hi basic architecture ko scale ke liye overbuild karna zaroori nahi, lekin expected load, database design, caching, capacity planning, monitoring and reliability ko ignore karna dangerous hai.

Agar 50,000 users se 500,000 users tak growth aati hai, load sirf 10x nahi ho sakta. Users ke beech relationships aur feed interactions ki complexity extra load create kar sakti hai.

## 6. 2003 — MySpace: identity and self-expression

MySpace 2003 mein launch hua. Academic history ke mutabik, service ne Friendster aur other social sites se dissatisfied users ko attract kiya. MySpace profile customization aur music/band communities ke liye especially visible bana. Users apne profile pages ko HTML/CSS customisation se visually distinct bana sakte the.

### MySpace ka differentiator

- Personal profile identity.
- Friends list and comments.
- Music/band discovery.
- Creator and fan interaction.
- High personalisation of profile appearance.

MySpace ka rise ek important lesson deta hai: user ko self-expression aur community identity dena platform ka strong differentiator ho sakta hai.

### Trade-off

Highly customisable profile surfaces developer ke liye security, compatibility, performance and consistent UX challenges create kar sakte hain. User freedom aur safe/consistent rendering ke beech balance chahiye.

## 7. 2003 — LinkedIn: professional graph

LinkedIn ka origin 2002 mein Reid Hoffman ke living room se hua aur official launch 5 May 2003 ko hua, LinkedIn ke company history ke mutabik. Iska central network purpose professional identity, work relationships, hiring, jobs and business connections tha.

Ye example important hai kyunki har social network entertainment-centric nahi hota.

Professional platform ko different data and trust signals chahiye:

- Work history and skills.
- Employer and education information.
- Professional connections.
- Job listings and applications.
- Company pages.
- Recruitment and business tools.

**Lesson:** Target audience aur user job data model ko determine karte hain. Creator platform, dating platform, professional platform and gaming community ko same product blueprint se blindly build nahi karna chahiye.

## 8. 2004–2006 — Facebook: campus directory se broad social platform

Facebook 4 February 2004 ko Harvard students ke liye TheFacebook ke roop mein launch hua. Harvard Gazette ke historical article ke mutabik, initial idea online student directory/identity and connection experience tha. Site later other universities tak expand hui; 2005 mein “The” drop hua; 2006 mein registration broader users tak open hui.

Meta ki company timeline 5 September 2006 ko News Feed launch aur 26 September 2006 ko registration expansion record karti hai.

### News Feed ka product shift

Pehle users friends ke profiles manually visit karte. News Feed ne friends ki activities ko central stream mein bring kiya. Ye product navigation ko profile-by-profile browsing se aggregated feed experience mein shift karta hai.

### User backlash: feature launch ka lesson

News Feed launch par users ne privacy/visibility concerns raise kiye. Ye product history ka important point hai: technically useful aggregation users ko intrusive lag sakti hai jab visibility/consent expectations clear na hon. Feature ka UX, privacy controls, communication and defaults important hain.

### Feed architecture ka implication

News Feed jaisa feature simple “SELECT posts” query nahi hota jab scale grow hota hai. System ko decide karna padta hai:

- Kaunse sources se candidate posts aayenge?
- Kaunse users ke posts eligible hain?
- Privacy/block/mute restrictions kya hain?
- Chronological order ya ranking?
- Duplicate content and spam kaise remove hoga?
- Pagination and caching kaise hogi?

## 9. 2005 — YouTube: video publishing ka friction kam karna

YouTube February 2005 mein register hua, company ki 15-year retrospective ke according. Early concept duniya bhar ke logon ke liye video share karna easy banana tha. 23 April 2005 ko “Me at the zoo” video upload hua.

YouTube ne video production ko invent nahi kiya. Usne online video sharing/uploading ka consumer experience easier banaya.

### Video platform ka hidden technical challenge

Image upload se video platform substantially more complex hai:

1. Very large files receive karna.
2. Interrupted uploads handle karna.
3. Format/duration/file integrity validate karna.
4. Video ko multiple resolutions/bitrates mein transcode karna.
5. Thumbnails and metadata generate karna.
6. Streaming segments deliver karna.
7. Global bandwidth and CDN costs manage karna.
8. Copyright, safety and age-related review workflows support karna.

YouTube-style product ke liye object storage, media processing, queues, transcoding workers, streaming protocols and CDN architecture important hain. Iska detailed design Part 08 mein hoga.

## 10. 2005 — Reddit and topic-based community design

Reddit 2005 mein launch hua as a community-oriented discussion product. Iska core pattern personal friend graph se zyada topic-based communities, submissions, comments and voting par focused tha.

Ye ek important alternative model hai:

- Friend-graph product: “Mere friends/followed creators kya share kar rahe hain?”
- Interest/community product: “Mere interests ke topics par kya discussion ho raha hai?”

A social platform ko decide karna hota hai ki discovery identity graph, topic graph, creator graph ya combination par build hoga.

## 11. 2006 — Twitter (later X): short public messages and real-time conversation

Twitter ka original idea Odeo company ke brainstorming context mein develop hua. Computer History Museum and Twitter's own retrospective record Jack Dorsey's first “twttr” post on 21 March 2006. Public service July 2006 mein launch hua.

Initially 140-character limit SMS constraints se related thi. Product ka simple unit short status update tha. Users ne @mentions, hashtags and retweets jaise conventions/features use kiye, jisse product public conversation and real-time information network bana.

### Why short messages worked

- Low composition effort.
- Fast publishing.
- Easy mobile/SMS-era interaction.
- Public reply/conversation.
- Timely news, event and community updates.

### Technical implication

High-frequency short text is storage/bandwidth ke perspective se video se cheaper ho sakta hai, lekin real-time public distribution, abuse/spam, search, trending and moderation challenges create karta hai.

### Twitter to X naming history

2023 mein Twitter brand ko X ke roop mein rebrand kiya gaya. Product history ko samajhte waqt original Twitter-era features aur later product/company changes ko separate rakhna chahiye. Is handbook mein “X” current platform name aur “Twitter” historical service/brand reference ke liye use hoga.

## 12. 2007 onward — Smartphone and app-store shift

Touchscreen smartphones, app stores, built-in cameras, location, notifications and faster mobile data ne social experience ko change kiya.

Web-only social experience ke comparison mein mobile apps could:

- Camera se direct upload.
- Push notification receive.
- Location and device sensors use.
- Phone contacts permission (with consent and platform policy) integrate.
- Native media capture/edit experience provide.
- App icon se always-available entry point dena.

Lekin mobile app ka matlab automatic better privacy nahi. Permissions, background collection, device identifiers and analytics SDKs ke controls important hain.

## 13. 2009–2012 — Messaging and photo-first mobile social

Mobile-first apps ne social behaviour ko smaller, faster and camera-centric banaya.

### WhatsApp (2009)

Mobile messaging and groups ne phone number/contact network ke around communication model popularise kiya. Messaging-first product aur public-feed social network ke data/permissions/security needs different hain.

### Instagram (2010)

Instagram ek useful product-pivot case study hai. FTC case materials mein 2010 ke documents ka record hai ki Kevin Systrom aur Mike Krieger ne Burbn ko photo-sharing focus ke saath rework kiya. CBS reporting on the founders describes the transition from a location/check-in concept to a focused photo-sharing app. Instagram iOS app October 2010 mein launch hui.

**Why the pivot matters:** Burbn mein many activities/features the, lekin team ne dekha ki photo sharing user interest ka strongest part tha. Product ko narrow karne se main experience clearer ho sakta hai.

Instagram's early strengths included:

- Phone-camera-first workflow.
- Quick photo sharing.
- Filters/editing as a simple creative tool.
- Follow graph.
- Visual profile/feed.
- Hashtags/discovery (later expansion).

Instagram story sirf “filters ne success dilayi” nahi. Mobile camera habits, product simplicity, sharing network, creator behaviour, distribution and execution combined the.

### Snapchat (2011)

Snapchat's early idea was camera-based communication with disappearing Snaps. Snap's own early founder post describes the 2011 App Store launch and how high-school users used the product for spontaneous photo messaging.

Ephemeral content ne ek different user expectation propose ki: har shared moment permanent public profile post hona zaroori nahi.

Later Stories as a format changed how users shared temporary sequences. Temporary media ka matlab privacy guarantee nahi; recipients screenshots, screen recordings, external cameras or backups use kar sakte hain. UX copy ko users ko unrealistic privacy promise nahi dena chahiye.

## 14. 2010s — Multiple social product patterns

Is decade mein social platforms ke models diversify hue:

| Pattern | Example type | Main relationship/content model |
|---|---|---|
| Photo-first sharing | Instagram | Visual posts + follow graph |
| Ephemeral camera messaging | Snapchat | Direct sharing + temporary stories |
| Public microblogging | Twitter/X | Short text + public conversation |
| Video library and channels | YouTube | Video creators + subscriptions + recommendations |
| Professional identity | LinkedIn | Work graph + skills/jobs |
| Topic communities | Reddit | Subreddits/communities + voting/comments |
| Group messaging | WhatsApp/Telegram-like | Private groups and direct conversations |
| Livestreaming | Twitch-like | Live creator/audience interaction |
| Decentralised social networking | Mastodon-like | Federated servers and interoperable protocol model |

No single feed, profile or social graph model is best for every audience.

## 15. 2016–2018 — Douyin, TikTok and short-video recommendation

ByteDance ki company timeline Douyin launch in China in 2016 and TikTok launch outside mainland China in May 2017 record karti hai. TikTok newsroom ne 2018 mein musical.ly aur TikTok ko unify karne ki announcement ki.

Short-form video model ne mobile-native capture/editing, audio/sound reuse, creator tools, swipe-based consumption and personalised recommendation ko combine kiya.

### Important distinction

- **Douyin**: mainland China market product.
- **TikTok**: international product/brand for markets outside mainland China.
- **musical.ly**: separate short-form video app acquired by ByteDance and merged into TikTok in 2018.

These products have related ownership/history, but country versions, infrastructure, content moderation and regulatory environments should not be assumed identical.

### Recommendation shift

Traditional friend-graph feed mein followed accounts ka content dominant ho sakta tha. Recommendation-led short-video feeds mein system user ke interest signals se creators/content discover kara sakta hai, even when user has not followed the creator.

Possible signals:

- Video watch duration and completion.
- Rewatch behaviour.
- Likes, shares, comments, saves.
- “Not interested” and skips.
- Creator/content metadata.
- Language and region relevance.
- Safety and policy eligibility.

Exact production ranking formulas are platform-specific and not fully public. Kisi company ke precise algorithm ko guess karke fact ki tarah present nahi karna chahiye.

## 16. Social network ka core engine kaise evolve hua?

### Era A — Profile and friend-list model

User profile + friends list + directory. Main technical work: identity, profile storage, relationship management and basic search.

### Era B — Feed model

User ko doosron ke updates ek central timeline mein dikhana. Main technical work: candidate collection, permissions, ranking or chronological ordering, pagination and caching.

### Era C — Media platform model

Images, audio and video uploads. Main technical work: object storage, content validation, processing, thumbnails, transcoding, streaming, CDN and copyright/safety review.

### Era D — Mobile-first interaction model

Camera, GPS, push notifications and app-native UX. Main technical work: iOS/Android clients, device permissions, mobile networking, offline/retry handling and app releases.

### Era E — Recommendation-led discovery

System user interests estimate karke content suggest karta hai. Main technical work: event pipelines, candidate generation, ranking, experimentation, model evaluation, feedback and safety constraints.

### Era F — Creator and business ecosystems

Creators, brands, advertisers, subscriptions, payments, analytics and commerce. Main technical work: payouts, fraud controls, billing, identity verification, accounting, ad policy and regulatory compliance.

## 17. Platform success sirf features ki wajah se nahi hota

Social network ke growth mein multiple network effects and business factors ho sakte hain:

- **Direct network effect:** more people in the same network can make communication more useful.
- **Indirect network effect:** more creators attract viewers; more viewers attract creators.
- **Content supply:** enough useful and fresh content.
- **Discovery:** user ko relevant people/content milna.
- **Retention:** users ko wapas aane ka reason.
- **Distribution:** invitations, app stores, search, referrals and partnerships.
- **Trust:** spam, scams, harassment and unsafe content manageable ho.
- **Reliability:** login, feed, uploads and messages consistently work karein.
- **Economics:** revenue can support compute, bandwidth, staff, creators and safety operations.

A platform can have a clever algorithm and still fail if it has no unique content, no trust, no clear audience or no sustainable unit economics.

## 18. History se practical engineering lessons

| Historical case | What it teaches |
|---|---|
| SixDegrees | Profiles + visible social graph is a powerful product combination, but timing and sustainability matter |
| Friendster | Growth without enough technical capacity harms user trust and retention |
| MySpace | Customisation and subcultures can create identity, but flexibility has engineering and safety trade-offs |
| LinkedIn | Audience and purpose shape the data model and trust requirements |
| Facebook News Feed | Feed aggregation is useful, but privacy expectations and user controls must be designed together |
| YouTube | Video is an infrastructure-heavy product, not just a file-upload form |
| Twitter/X | Simple posting primitives can lead to complex public conversation, moderation and search needs |
| Instagram | Focused product scope and mobile-native UX can outperform a feature-heavy concept |
| Snapchat | Ephemeral UX is a product promise; it must not be confused with guaranteed secrecy |
| TikTok | Recommendation-led discovery can reduce dependence on following, but requires strong safety, feedback and evaluation systems |

## 19. How to use this history when designing your own platform

Before coding, answer:

1. Is your product mainly about people connecting, content publishing, professional identity, private messaging, community discussion or entertainment?
2. What is the main object: profile, post, video, message, event, project or community?
3. What is the main relationship: friend, follow, subscriber, group membership or creator-fan relationship?
4. How does a new user discover useful people/content before they have a large network?
5. What is the first “aha moment” that makes the user understand the product's value?
6. Does your first version need a ranked feed, or is chronological/curated feed enough?
7. Do you genuinely need video immediately, given its cost and operational complexity?
8. What user safety, privacy and moderation rules must exist before public access?

## 20. Glossary

- **Social graph:** users/entities and their relationships.
- **Friend graph:** usually mutual connection model.
- **Follow graph:** usually directed, one-way relationship model.
- **Feed:** stream of content shown to a user.
- **Timeline:** often chronological or activity-based stream.
- **Ranking:** ordering items according to a scoring/model system.
- **Recommendation:** predicting useful or interesting content for a user.
- **UGC (User-Generated Content):** content submitted by users.
- **Creator:** person/account publishing original or curated content.
- **Ephemeral content:** content designed to be available temporarily, subject to product implementation and limits.
- **Microblogging:** short-form frequent publishing and public conversation.
- **Network effect:** product value can increase as more users/participants join.
- **Retention:** user returning/continuing to use the product over time.
- **Moderation:** policy enforcement and content/account handling.
- **Content provenance:** information about origin/creation/transformations of content.

## 21. Self-check questions

1. Why is SixDegrees called an early recognizable social-network site, rather than the first form of online social interaction?
2. What technical problems did Friendster reportedly face as it grew?
3. How did MySpace encourage self-expression?
4. How is LinkedIn's professional graph different from an entertainment-focused social graph?
5. Why was News Feed a product and architecture shift?
6. Why is a video platform more infrastructure-heavy than a text-only platform?
7. How did Twitter's original SMS-era constraints influence its post format?
8. What was the product pivot from Burbn to Instagram?
9. What user behaviour did Snapchat's disappearing messages support, and what privacy caveat remains?
10. How does recommendation-led discovery differ from a pure following-based feed?

## 22. Practical exercise: build a historical product comparison

Choose three platforms from this chapter. For each, fill this table:

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

Do not just compare logos or features. Compare the product's core idea, user behaviour, architecture and business constraints.

---

## Sources and further reading

1. [boyd & Ellison (2007), Social Network Sites: Definition, History, and Scholarship](https://onlinelibrary.wiley.com/doi/10.1111/j.1083-6101.2007.00393.x) — academic definition; SixDegrees, Friendster and MySpace history.
2. [Computer History Museum — Networking & the Web timeline](https://www.computerhistory.org/timeline/networking-the-web/) — BBSs, online services, Usenet and earlier online communities.
3. [Harvard Gazette — Facebook, 10 years after](https://news.harvard.edu/gazette/story/2014/02/facebook-10-years-after/) — early Facebook context.
4. [Meta — Company information and milestones](https://www.meta.com/about/company-info/) — company timeline, including News Feed and platform milestones; company source.
5. [U.S. House hearing memorandum (GovInfo) — Facebook platform evolution](https://www.govinfo.gov/content/pkg/CHRG-115hhrg30956/pdf/CHRG-115hhrg30956.pdf) — independent government-published hearing material discussing News Feed and product history.
6. [YouTube Blog — YouTube at 15](https://blog.youtube/news-and-events/youtube-at-15-my-personal-journey/) — YouTube registration and early video-sharing origin; company source.
7. [YouTube Blog — Celebrating 10 Years of YouTube](https://blog.youtube/news-and-events/celebrating-10-years-of-youtube/) — first video and early growth retrospective; company source.
8. [Computer History Museum — March 21: first tweet](https://www.computerhistory.org/tdih/march/21/) — early Twitter concept and first post.
9. [X Blog — Nine years and counting](https://blog.x.com/en/company/nine-years-and-counting) — Twitter's retrospective on its early community-created features; company source.
10. [LinkedIn Careers — Why LinkedIn](https://careers.linkedin.com/WhyLinkedIn) — company origin and launch history; company source.
11. [Snap Newsroom — Let's Chat](https://newsroom.snap.com/lets-chat) — Snapchat's early product idea and 2011 launch; company source.
12. [ByteDance — Company milestones](https://www.bytedance.com/seed3d/) — Douyin, TikTok and musical.ly milestone timeline; company source.
13. [TikTok Newsroom — musical.ly and TikTok unite](https://newsroom.tiktok.com/musical-ly-and?lang=en) — 2018 merger/unification announcement; company source.
14. [U.S. House select committee document on social media](https://docs.house.gov/meetings/IF/IF00/20230323/115519/HHRG-118-IF00-20230323-SD030.pdf) — historical detail on TikTok/musical.ly development, presented in a government hearing context.
15. [CBS News — How Instagram found its focus](https://www.cbsnews.com/news/instagram-5-years-co-founders-kevin-systrom-mike-kreiger/) — founders' account of Burbn and photo-sharing focus.
16. [FTC court filing — Instagram/Burbn evidence](https://www.ftc.gov/system/files/ftc_gov/pdf/FTCReplytoMetaResponse-CounterstatementofMaterialFacts.pdf) — court-record material describing the 2010 Burbn-to-Instagram pivot; primary legal-record source.

*Research note:* Product timelines sometimes differ by prototype date, company incorporation date, beta date, public launch date or app-store availability. This chapter labels these milestones where the source supports the distinction. Company histories are identified as company sources; academic and government material is used where helpful for independent context.
