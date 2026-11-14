# Part 01 — History of the Internet and the World Wide Web

**Research snapshot:** 13 November 2026  
**Purpose:** Samajhna ki modern social media ko possible banane wali network technology kahan se aayi, kis problem ko solve karne ke liye bani, aur aaj ek American application India ya kisi doosre country ke user tak kaise pahunch sakti hai.

---

## 1. Sabse pehle ek confusion clear karo: Internet aur Web same cheez nahi hain

Log daily conversation mein “Internet” aur “website” ko same samajh lete hain. Technical level par dono alag hain.

- **Internet**: interconnected networks ka global system. Ismein fibre cables, routers, mobile networks, internet service providers (ISPs), data centres, IP addressing aur routing protocols kaam karte hain.
- **World Wide Web (WWW / Web)**: Internet ke upar chalne wali services mein se ek. Websites aur web applications browser ke through mostly HTTP/HTTPS par data exchange karti hain.
- **Email**: Internet par chalne wali ek alag application/service family.
- **VoIP / video calling**: Internet connectivity ka use karke audio/video communication.
- **Online games**: Internet par chalne wale real-time applications.

Analogy: Internet ko roads, interchanges aur transport network samjho. Web ko us network par chalne wali ek transport/service category samjho. Email, video calling aur games bhi usi underlying network ka use kar sakte hain, lekin woh “Web page” nahi hain.

Iska social media se relation: Instagram ka web version browser se Web protocols use karta hai; Instagram ka mobile app bhi Internet use karta hai, lekin uska interface browser page hona zaroori nahi. Dono cases mein requests remote services tak pahunchti hain.

## 2. Internet se pehle: problem kya thi?

1960s se pehle computers bade, expensive aur aksar alag-alag institutions mein isolated systems the. Ek organisation ka computer doosri organisation ke computer se easily communicate nahi karta tha. Researchers ko remote computing resources share karne, research exchange karne aur reliable communication ka better method chahiye tha.

Traditional telephone networks ka model **circuit switching** tha. Call ke dauran network ek dedicated path/circuit reserve karta hai. Voice call ke liye ye useful hai, lekin computer data ke liye har waqt dedicated circuit reserve karna wasteful ho sakta hai—kyunki computer traffic bursty hota hai: kuch milliseconds data bheja, phir pause, phir aur data.

### Packet switching ka idea

Packet switching mein message ko chhote data units—**packets**—mein divide kiya jata hai. Har packet ke saath addressing/control information hoti hai. Network routers packets ko destination ki taraf forward karte hain. Destination par data ko order mein reconstruct kiya ja sakta hai; missing ya damaged data ko higher-level protocols handle kar sakte hain.

Simple comparison:

| Circuit switching | Packet switching |
|---|---|
| Session ke liye dedicated circuit/path reserve ho sakta hai | Network links par packets alag users ke traffic ke saath share ho sakte hain |
| Traditional voice-call model mein useful | Bursty computer communication ke liye useful |
| Path reservation central concept | Routing and packet forwarding central concept |
| Ek circuit mein capacity idle reh sakti hai | Link capacity statistical sharing se better use ho sakti hai |

Packet switching ka development ek single inventor ka kaam nahi tha. Paul Baran ne US mein resilient distributed communications ke ideas par kaam kiya; Donald Davies aur unki UK National Physical Laboratory team ne packet-switching concept aur “packet” terminology ko develop kiya; Leonard Kleinrock ne queueing/network performance theory mein contributions kiye; ARPA researchers ne in ideas ko practical network programme mein convert kiya. Ye parallel research streams thi, ek simple one-person invention story nahi.

**Kyun important tha?** Is approach ne alag-alag computers aur networks ko shared communication infrastructure par connect karna possible banaya.

## 3. ARPANET: Internet ki important early foundation

US Department of Defense ke Advanced Research Projects Agency (ARPA; later DARPA) ne research institutions ke computers connect karne ke liye ARPANET project support kiya. BBN (Bolt Beranek and Newman) ne Interface Message Processors (IMPs)—early packet-switching devices, jinhe modern routers ka ancestor samajh sakte ho—build karne ka kaam kiya.

### Early timeline

- **1968:** ARPA ne BBN ko early packet-switching network equipment build karne ka contract diya.
- **September 1969:** UCLA par first ARPANET node active hua.
- **October 1969:** UCLA aur Stanford Research Institute (SRI) ke beech first host-to-host connection/message attempt hua. Popular historical account ke mutabik intended word “LOGIN” tha; system “LO” ke baad crash hua. Is detail ko anecdotal milestone ke roop mein lo, Internet ka single “birth moment” samajhkar nahi.
- **December 1969:** Network ke four initial nodes the: UCLA, SRI, UC Santa Barbara (UCSB), aur University of Utah.

ARPANET ka original purpose Instagram ya public social networking banana nahi tha. Research computing resources share karna aur network communication test karna tha.

### ARPANET ne kya prove kiya?

1. Alag locations par computers network ke through communicate kar sakte hain.
2. Packet-switched infrastructure practical hai.
3. Network par useful applications develop ho sakti hain.
4. Protocol standardisation zaroori hai, warna different networks ek doosre ko samajh nahi paayenge.

## 4. Email: Internet ka early “killer application”

Network technology banane ke baad engineers ko ek useful application chahiye thi. Ray Tomlinson ne 1971 mein ARPANET par network email implement kiya. Unhone local machine messaging program aur file transfer capability ko combine karke doosre computer par user ko message bhejne ka method banaya.

Unka ek lasting design choice `@` sign tha: `user@host` mein user ko us machine/host se separate karna. Email ne network ko sirf computer scientists ke experiment se useful communication environment banane mein help ki.

Important nuance: electronic messages aur computer mail systems ke kuch forms ARPANET se pehle time-sharing machines par maujood the. Tomlinson ki major contribution networked email ko different computers ke beech workable banana aur familiar address notation establish karna thi.

**Product lesson:** Infrastructure ka value tab clear hota hai jab users ko us par ek practical task complete karne ka reason milta hai.

## 5. TCP/IP: alag networks ko ek Internet banana

ARPANET ke early stage mein NCP naam ka host protocol use hota tha. Problem ye thi ki future mein alag technology aur alag administrative control wale networks ko connect karna tha. Ek common protocol family ki zaroorat thi.

Vint Cerf aur Robert “Bob” Kahn ke work se Transmission Control Protocol (TCP) aur Internet Protocol (IP) ka design develop hua. TCP/IP ne network-of-networks architecture ke liye common foundation di.

- **IP (Internet Protocol):** addressing aur packet ko network-to-network route karne mein basic role.
- **TCP (Transmission Control Protocol):** connection-oriented reliable byte stream, sequencing, acknowledgements, retransmission aur flow control jaise mechanisms provide karta hai.
- **UDP (User Datagram Protocol):** connectionless datagrams; kuch real-time applications reliability ke kuch controls application layer par rakhna pasand karti hain.

**1 January 1983** ko ARPANET ka major NCP-to-TCP/IP transition hua—Internet history ka important “flag day”. Is transition ka lesson: jab protocol badalte hain, network ke connected systems ko compatibility planning chahiye hoti hai.

### TCP/IP social platform ke liye kyun relevant hai?

Jab user phone par post upload karta hai, request app se network ke through backend tak jaati hai. IP packets ko route karne ka base deta hai; TCP ya other transport protocols application communication ko carry karte hain. HTTPS ke andar HTTP request/response secure transport ke through exchange hota hai.

Ek social app developer ko IP routing protocol implement nahi karna hota, lekin latency, packet loss, timeouts, TLS, connection reuse aur retry behaviour samajhna chahiye.

## 6. DNS: human-friendly names ko network addresses tak resolve karna

Computers ko network addresses chahiye, lekin humans ko `example.com` jaisa naam yaad rakhna easier hai. **Domain Name System (DNS)** domain names ko records ke through IP addresses aur other service information se map karta hai.

Example flow:

1. User browser mein `example.com` type karta hai.
2. Device/browser DNS cache check karta hai.
3. Resolver DNS infrastructure se answer leta hai, agar cache mein na ho.
4. DNS record suitable IP address ya service target return karta hai.
5. Client us destination se network connection banata hai.

DNS sirf “website ka IP” nahi hai; different record types email routing, service discovery aur verification jaise kaam bhi support karte hain. DNS caching performance improve kar sakti hai, lekin stale records aur propagation timing deployment planning ko affect kar sakte hain.

## 7. Internet ka expansion: research network se global network

1980s–1990s mein academic, government, research aur commercial networks expand hue. NSFNET jaise backbone initiatives ne research networking ko expand kiya. Organisations, universities aur commercial providers ne network connections build kiye. Internet ek organisation ke single server se nahi chalta; multiple autonomous networks—ISPs, transit providers, content networks, research networks—interconnect karte hain.

### Teen terms samjho

- **ISP (Internet Service Provider):** user ya organisation ko Internet connectivity provide karta hai.
- **ASN (Autonomous System Number):** routing policy ke under operate karne wale network ko identify karne ka number.
- **BGP (Border Gateway Protocol):** autonomous systems ke beech reachability information exchange karne ka routing protocol.

Isliye Internet ka global nature sirf cloud companies ki wajah se nahi. Physical fibre, submarine cables, terrestrial networks, mobile networks, exchange points, peering agreements aur routing policy sab milkar connectivity banate hain.

## 8. World Wide Web: 1989–1993 ke breakthrough

1989 mein British computer scientist Tim Berners-Lee ne CERN (Switzerland) mein information-management proposal diya. CERN ke scientists aur institutions geographically distributed the; unhe documents aur research information ko linked form mein share karne ka practical system chahiye tha. Robert Cailliau ne Web ke early development aur promotion mein important collaboration ki.

1990 tak basic Web components develop ho chuke the:

- **HTML (HyperText Markup Language):** document structure and links.
- **HTTP (HyperText Transfer Protocol):** client aur server ke beech Web resources request/response exchange.
- **URL/URI:** resource ko identify/address karne ka format.
- **Web server:** resources serve karne wala software/system.
- **Browser:** Web resources ko retrieve aur render karne wala client.

First website CERN mein host hui. 30 April 1993 ko CERN ne World Wide Web software ko royalty-free basis par available karwaya, jisse adoption ko strong boost mila.

### WWW kya solve karta tha?

Internet computers ko connect kar raha tha, lekin connected information ko browse, link aur publish karne ka user-friendly universal method limited tha. Web ne hypertext documents ko network par link karna easy banaya. Ek document ke andar link par click karke doosre resource par jaana possible hua.

### Internet vs Web — real example

- YouTube website browser mein open karna: Web over Internet.
- YouTube mobile app mein video load karna: Internet-based app communication; UI native/webview ho sakta hai.
- App notification receive karna: Internet connectivity plus push-notification delivery infrastructure.
- Video stream: network ke through media segments/bytes delivery; ye sirf HTML page render karne tak limited nahi.

## 9. Browser aur search era

1990s mein browsers aur user-friendly interfaces ne Web ko academics se aage public users ke liye accessible banaya. NCSA Mosaic jaise browsers ne images and text ko unified view mein display karne ke experience ko popularise karne mein role play kiya. Netscape Navigator aur later Internet Explorer ne browser competition ko shape kiya.

Search engines aur web directories ne Web ke growing information space ko navigate karna easier banaya. Web portals, directories, search, bookmarks aur hyperlinks users ko information find karne mein help karte the.

**Platform lesson:** Discovery ka problem social media se pehle bhi tha. Jab content ka volume badhta hai, users ko search, categories, ranking, recommendations ya curated directories chahiye hoti hain.

## 10. Static pages se dynamic web applications tak

Early websites largely static documents the. Later server-side programming, databases, cookies, sessions, JavaScript and richer browser capabilities ne interactive products possible banaye.

Examples:

- User account create karna.
- Login ke baad personalised page dekhna.
- Form submit karke database change karna.
- Comments add karna.
- Search query ke hisaab se result generate karna.
- Shopping cart aur payments.
- Social feed ko per-user personalise karna.

Aaj ke web apps mein browser sirf page download nahi karta. Woh API requests bhejta hai, state manage karta hai, media streams load karta hai aur real-time connections maintain kar sakta hai.

### Aaj ke Web app request ka simplified flow

```text
User action
  -> Browser / mobile app
  -> DNS lookup
  -> Network connection
  -> TLS security handshake (for HTTPS)
  -> HTTP request
  -> CDN / load balancer / API gateway (architecture par depend)
  -> Application server
  -> Database / cache / other service
  -> HTTP response
  -> UI update
```

Har request exactly yehi path use nahi karti. Browser cache, service worker, CDN cache, direct object-storage uploads aur push channels alag paths bana sakte hain.

## 11. Web 2.0 aur user-generated content

“Web 2.0” popular term ban gaya jab websites read-only pages se interactive communities aur user-generated content platforms ki taraf shift hui.

Users ab sirf website padhte nahi the; woh:

- Profiles banate the.
- Blog publish karte the.
- Photos upload karte the.
- Videos share karte the.
- Comments likhte the.
- Ratings aur reviews dete the.
- Communities aur groups join karte the.

Is shift ka technical meaning: application ko user identity, permissions, content moderation, media storage, search, database writes, spam protection aur scalable delivery chahiye.

**Important:** “Web 2.0” koi single official protocol version nahi tha. Ye industry term tha jo interactive, participatory web trend describe karta tha.

## 12. Smartphone, apps aur mobile-first era

2007 ke baad modern touchscreen smartphones aur app ecosystems ne social products ko always-available camera, GPS, notifications, sensors aur mobile network access diya. 3G/4G, better cameras, app stores aur mobile operating systems ne behaviour badla.

Social products ke liye impact:

1. Photo capture and upload phone par natural ho gaya.
2. Location tagging and check-ins possible hue.
3. Push notifications return visits trigger kar sakti hain.
4. Vertical video mobile screen ke liye fit format ban gaya.
5. Creator content real time mein capture/publish karna easier hua.
6. Mobile network quality country aur region ke hisaab se vary karti hai—video quality adaptation important hua.

Aaj platform ko low-end phones, limited storage, metered data plans, intermittent connectivity, language diversity aur accessibility consider karni padti hai.

## 13. Cloud computing, object storage aur CDN

Aaj startup ko apna physical data centre build karna compulsory nahi. Cloud providers compute, database, networking, storage, managed queues aur many other services rent par dete hain.

### Main infrastructure layers

| Layer | Example role | Social app mein use |
|---|---|---|
| Compute | VM, container, serverless function | API and background workers |
| Relational database | Managed PostgreSQL | Users, posts, comments, follows |
| Cache | Redis | Hot data, sessions, rate limits, queues (specific design ke saath) |
| Object storage | S3-compatible bucket | Large photo/video/audio files |
| CDN | Edge cache/delivery network | Media and static assets ko users ke paas se serve karna |
| Queue | Managed or self-hosted message broker | Slow work ko asynchronous process karna |
| Observability | Logs, metrics, traces | Failure and latency diagnose karna |

### CDN kyun bana?

Agar user India mein hai aur origin server US mein, har 10 MB image/video ko US se direct bhejna latency aur transit cost badha sakta hai. CDN edge locations par cache copies rakh sakta hai. User ko nearest suitable edge se content mil sakta hai—lekin “nearest” ka matlab hamesha geographic nearest nahi, routing, capacity, cache availability aur provider policy matter karte hain.

CDN private content ko automatically safe nahi banata. Private media ke liye signed URLs/cookies, short expiry, correct cache policy, authorization aur cache purge/invalidation design chahiye.

### Video streaming ka shift

User-generated video ko multiple bitrate/resolution mein encode karke segmented delivery (for example HLS or MPEG-DASH, client support and stack par depend) ke through adaptive playback diya ja sakta hai. Player network condition ke according available quality select karta hai.

## 14. Global platform: ek country mein bani service doosre country mein kaise chalti hai?

Maan lo ek company US mein incorporate hui, backend cloud region Europe mein rakha, media object storage Asia region mein rakha, aur users India, Brazil, Japan aur Germany se connect kar rahe hain.

Isko samajhne ke liye five separate maps banao:

1. **Network map:** user ka ISP -> transit/peering -> CDN/edge -> application region.
2. **Compute map:** API servers kis cloud region/zone mein run karte hain?
3. **Data map:** account database, logs, backups, media and analytics kahan store/process hote hain?
4. **Vendor map:** email, OTP, analytics, payment, crash reports, moderation and support vendors kaunse countries mein operate karte hain?
5. **Legal map:** company establishment, user location, service category, data type, data transfer aur local rules ka effect.

### Important distinction: data residency vs data localisation vs data transfer

- **Data residency:** data physically kis geographic location par store hai.
- **Data localisation:** law ya regulation kuch data ko country ke andar store/process karne ki condition laga sakta hai.
- **Cross-border data transfer:** personal data ya other regulated information ek jurisdiction se doosri jurisdiction mein move hoti hai.
- **Data access:** support engineer ya vendor kisi doosre country se data access kare—ye bhi legal/privacy analysis ka part ho sakta hai, even when storage location unchanged ho.

Har country ka rule same nahi hota. Kuch laws transfer mechanisms/adequacy/safeguards allow karte hain; kuch sectors ya data categories par local storage/processing duties ho sakti hain; kuch governments specific services or data categories par separate requirements impose karte hain. Exact position future legal chapter mein current official sources se country-wise map ki jayegi.

### Example: user India mein, company America mein

A user India se a foreign social app par account banata hai. High-level technical sequence:

1. App DNS and network routing ke through suitable entry point tak pahunchti hai.
2. Login request TLS-protected connection par API tak jaati hai.
3. Backend identity/session check karta hai.
4. Database query user record read karti hai.
5. Feed service eligible posts collect/rank karti hai.
6. Image/video files CDN or object storage delivery path se aati hain.
7. Events analytics/monitoring pipeline mein ja sakte hain, according to privacy settings and product design.

Lekin **is example se ye prove nahi hota** ki data automatically America mein store hota hai ya India se bahar data transfer always permitted hai. Actual storage, vendors, legal obligations and transfer basis platform ke architecture aur applicable rules par depend karte hain.

## 15. Social platform engineering mein history se kya seekhna chahiye?

| Historical development | Engineering lesson |
|---|---|
| Packet switching | Shared infrastructure ko efficiently use karna |
| TCP/IP | Interoperability ke liye open standards and protocols |
| DNS | Human-friendly naming ke peeche distributed infrastructure |
| WWW/HTML/HTTP | Common interfaces and linking se adoption grow hota hai |
| Email | Technology tab valuable banti hai jab clear user problem solve kare |
| Dynamic web apps | Identity, state, database and permissions central ho jaate hain |
| Mobile apps | Device constraints and network quality UX ko shape karte hain |
| Cloud/CDN | Global products ko distributed compute and delivery chahiye |
| Video streaming | Large media ko upload, process, encode and deliver alag stages mein handle karo |

## 16. Basic glossary

- **ARPANET:** early packet-switched research network, Internet history ki major foundation.
- **Packet:** network par transmit hone wala formatted data unit.
- **Router:** packets ko next network destination ki taraf forward karta hai.
- **Protocol:** systems ke beech communication ke rules.
- **TCP:** reliable, ordered byte-stream transport protocol.
- **IP:** packet addressing/routing ka core protocol.
- **DNS:** domain names and service records resolve karne wala distributed naming system.
- **HTTP:** Web client/server request-response protocol.
- **HTTPS:** HTTP communication protected by TLS.
- **HTML:** web document structure markup.
- **URL:** resource locator.
- **ISP:** Internet connectivity provider.
- **BGP:** autonomous networks ke beech routing information exchange protocol.
- **CDN:** distributed content delivery/cache network.
- **Object storage:** large unstructured objects (photos/videos) store karne ka service/model.
- **Latency:** request/response mein lagne wala delay.
- **Throughput:** ek period mein transfer/process hone wala data.
- **Availability:** system kitne time usable/reachable hai.
- **Data residency:** data ki geographic storage location.

## 17. Self-check questions

1. Internet aur World Wide Web mein exact difference kya hai?
2. Packet switching bursty computer traffic ke liye useful kyun tha?
3. ARPANET ka original use-case kya tha?
4. TCP aur IP ke responsibilities ko simple words mein explain karo.
5. DNS ki zaroorat kyun hai jab IP addresses already exist karte hain?
6. Tim Berners-Lee ne Web ke liye kaunsi problem solve ki?
7. User-generated content ne server/database requirements ko kaise badla?
8. CDN private user media ko secure karne ke liye akela enough kyun nahi?
9. Ek US-based platform ko India mein serve karte waqt network, storage aur legal questions ko alag-alag kyun map karna chahiye?
10. Agar ek video US origin server par hai aur user Mumbai mein, toh delivery latency kaise reduce ki ja sakti hai?

## 18. Practical exercise

Paper par ya diagram tool mein ek simple global social app ka flow draw karo:

```text
India ka user
  -> mobile ISP / Wi-Fi ISP
  -> DNS resolver
  -> CDN edge
  -> application entry point / load balancer
  -> API service
  -> user database + cache
  -> media object storage (signed access)
```

Phir har arrow ke neeche likho:

- Kaunsa protocol/service involved ho sakta hai?
- Data kis direction mein ja raha hai?
- Kya personal data hai?
- Failure ho toh retry/fallback kya hoga?
- Is step ko secure kaise karoge?

---

## Sources and further reading

1. [DARPA — ARPANET history](https://www.darpa.mil/news/features/arpanet) — early ARPANET nodes and TCP/IP transition overview.
2. [Internet Society — A Brief History of the Internet](https://www.internetsociety.org/internet/history-internet/brief-history-internet/) — packet networking, early nodes and NCP-to-TCP/IP transition.
3. [Computer History Museum — Networking & the Web timeline](https://www.computerhistory.org/timeline/networking-the-web/) — packet switching, email, online services, BBSs, Usenet and Web milestones.
4. [Communications Museum Trust — Packet switching](https://www.comms.org.uk/emuseum/packetswitching/) — Donald Davies and packet-switching explanation.
5. [Lemelson-MIT — Ray Tomlinson](https://lemelson.mit.edu/resources/ray-tomlinson) — 1971 network email and the `@` notation.
6. [CERN — A short history of the Web](https://home.cern/science/computing/the-birth-of-the-web/short-history-web/) — Tim Berners-Lee, early Web and CERN's 1993 release.
7. [CERN — The birth of the Web](https://home.cern/science/computing/the-birth-of-the-web) — institutional history and restoration of the first website.
8. [W3C — History timeline description](https://www.w3.org/2005/01/timelines/description) — early Internet, TCP/IP, DNS and Web dates.
9. [ITU — Overview of ITU history](https://www.itu.int/en/history/pages/ITUsHistory-page-6.aspx) — global telecom and Internet context.

*Note: dates are simplified into a learning timeline; some technologies were developed over years by multiple teams, not invented in a single instant.*
