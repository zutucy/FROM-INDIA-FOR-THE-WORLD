# 05A — Networking Foundations and the History of Computer Networks

**Handbook:** Technology, Software Engineering and Global Digital Products  
**Part:** 05 — Networking and Internet Protocols  
**Language:** Detailed Hinglish (Roman Hindi + standard technical English)  
**Research snapshot:** 13 November 2026

---

## 1. Is chapter ka goal

Is chapter ke baad tum explain kar paoge:

- Do computers network par communicate kaise karte hain.
- Internet ek single company ka network nahi, balki interconnected networks ka system kyun hai.
- Packet switching, protocols, routers, switches, ISPs, autonomous systems aur Internet Exchange Points ka role.
- Networking ki history mein ARPANET, TCP/IP, Ethernet, NSFNET, DNS aur commercial Internet ka contribution.
- OSI model aur TCP/IP model ko practical debugging mein kaise use karna hai.
- Latency, bandwidth, throughput, packet loss, jitter aur availability mein difference.

Networking ko sirf social media ke liye mat padho. Banking, hospitals, games, video streaming, factories, cloud computing, AI services, online education, logistics, government systems aur almost har connected technology networking par depend karti hai.

## 2. Network kya hota hai?

**Computer network** do ya zyada computing devices ka system hai jo defined communication rules ke through data exchange kar sakta hai. Devices computers, phones, servers, printers, cameras, sensors, routers ya industrial machines ho sakte hain.

Example: ghar ke Wi-Fi par laptop, mobile aur smart TV connected hain. Ye devices local network par communicate kar sakte hain. Jab phone kisi public website ko request karta hai, traffic tumhare local network se ISP aur phir multiple networks ke through destination tak ja sakta hai.

### Network ke basic parts

| Part | Simple meaning | Kyu chahiye? |
|---|---|---|
| End device / host | Phone, laptop, server, camera | Data create ya consume karta hai |
| Network interface | Ethernet port ya Wi-Fi adapter | Device ko network medium se connect karta hai |
| Medium | Copper cable, fibre, radio waves | Signals carry karta hai |
| Switch | Same local network mein devices connect karta hai | Local frames ko correct port tak bhejta hai |
| Router | Different IP networks connect karta hai | Packets ko next network ki taraf forward karta hai |
| Access point | Wi-Fi devices ko wired network se connect karta hai | Wireless access deta hai |
| Firewall | Traffic rules enforce karta hai | Unwanted/unauthorized communication rokta hai |
| Server | Service provide karne wala system | Website, database, email, files, APIs serve karta hai |
| Client | Service request karne wala system | Browser, app ya device request bhejta hai |

**Client-server** ek common pattern hai, lekin Internet mein peer-to-peer communication, distributed systems aur device-to-device protocols bhi exist karte hain.

## 3. Data physically travel kaise karta hai?

Digital data bits (0 aur 1) hota hai, lekin network medium par bits ko signals ke form mein represent kiya jata hai:

- Copper cable mein electrical signals.
- Fibre-optic cable mein light pulses.
- Wi-Fi aur cellular mein radio-frequency electromagnetic signals.
- Satellite links mein radio signals, long-distance path aur ground stations ke through.

Har medium ki speed, capacity, distance, interference tolerance, cost aur deployment complexity different hoti hai.

### Copper, fibre aur wireless ka difference

| Medium | Strength | Limitation | Common use |
|---|---|---|---|
| Twisted-pair copper Ethernet | Affordable, office/home LAN ke liye practical | Distance and interference limits | PCs, switches, access points |
| Coaxial cable | Cable broadband systems mein useful | Provider architecture par depend | Cable Internet, TV networks |
| Fibre optic | Long distance, high capacity, electromagnetic interference se immune | Installation/splicing skills and equipment | Backbones, data centres, FTTH, submarine cables |
| Wi-Fi | Mobility and easy access | Shared radio medium, walls/interference, variable throughput | Homes, offices, public hotspots |
| Cellular | Wide-area mobile connectivity | Coverage, congestion, spectrum and plan dependency | Phones, IoT, mobile broadband |
| Satellite | Remote regions and ships/aircraft tak connectivity | Orbit ke hisaab se latency, capacity and weather/obstruction factors | Remote access, backup links |

**Important:** Advertised link speed aur app ka real download speed same nahi hote. Protocol overhead, congestion, server capacity, Wi-Fi interference, distance, packet loss and shared bandwidth actual throughput ko affect karte hain.

## 4. Packet switching: Internet ka fundamental idea

Purane communication systems mein kuch approaches dedicated path/circuit establish kar sakti thi. Packet-switched networking mein data ko smaller units—**packets**—mein divide karke shared network resources se bheja ja sakta hai.

Example: tum 5 MB ki image upload karte ho. Application data transport layer tak jata hai; network stack usse packets/segments mein organize karta hai. Routers har IP packet ko destination ki taraf forward karte hain. Different packets potentially different paths le sakte hain, aur destination par upper layers original data reconstruct kar sakti hain.

Packet switching ke advantages:

1. Network links multiple users ke beech statistically share ho sakte hain.
2. Different networks ko common protocol ke through interconnect kiya ja sakta hai.
3. Network path fail hone par routing alternatives available ho sakte hain, depending on topology and routing convergence.
4. Data communication bursty applications ke liye efficient ho sakti hai.

Trade-offs:

- Delay variable ho sakta hai.
- Packets drop, duplicate ya out-of-order arrive kar sakte hain.
- Congestion control aur retransmission ki need ho sakti hai.
- Real-time applications ko latency/jitter manage karna padta hai.

IP basic delivery service **best-effort** hai. IP by itself guarantee nahi karta ki packet deliver hi hoga, order same rahega ya duplicate nahi hoga. Reliability higher-level protocols ya applications implement karte hain. IPv4 ke original protocol design ke liye [RFC 791](https://www.rfc-editor.org/rfc/rfc791) dekho. [1]

## 5. Network protocol kya hota hai?

Protocol communication ka agreed rulebook hai. Protocol specify kar sakta hai:

- Message ka format.
- Fields ka meaning.
- Request aur response ka sequence.
- Errors ko kaise represent karna.
- Identity or authentication kaise verify karna.
- Data retransmit ya acknowledge kaise karna.
- Compatible implementations kaise behave karengi.

Human example: do log same language aur agreed conversation rules use karte hain. Computer protocols exact machine-readable rules define karte hain.

Examples:

| Protocol | Main role |
|---|---|
| Ethernet | Local wired network link technology |
| Wi-Fi (IEEE 802.11 family) | Wireless local networking |
| IP | Network addressing and packet forwarding |
| ICMP | IP network control/error messages |
| TCP | Reliable ordered byte stream between endpoints |
| UDP | Lightweight datagram transport without TCP-style delivery guarantees |
| DNS | Names ko network information, commonly IP addresses, se resolve karna |
| HTTP | Web/API request-response semantics |
| TLS | Secure communication channel |
| DHCP | Network configuration lease provide karna |
| BGP | Autonomous systems ke beech routing reachability exchange |

Ek important idea: protocols usually layers mein combine hote hain. Browser, DNS resolver, TCP/QUIC, IP aur Ethernet/Wi-Fi sab apne layer ka job karte hain.

## 6. Networking ki history — problem se Internet tak

History ko hero-story ki tarah mat dekho jisme ek person ne akela Internet invent kar diya. Modern Internet decades ke research, engineering, standards, institutions, universities, operators aur commercial infrastructure ka result hai.

### 1950s–1960s: Computers expensive aur isolated the

Early mainframe computers expensive the. Researchers chahte the ki remote terminals aur alag institutions ke computers computing resources share kar sakein. Traditional dedicated communication arrangements flexible nahi the. Packet-switching ideas independently develop hue. Paul Baran (RAND) ne distributed communications/packet switching par work kiya; Donald Davies aur team ne UK National Physical Laboratory mein packet network concepts develop kiye. Leonard Kleinrock ne queueing theory and packet-network analysis mein important research ki.

**Problem:** Ek central path ya dedicated link par dependency, expensive communication, aur geographically separated computers ko efficiently connect karna.

**Why packet switching mattered:** Messages ko packets mein divide karke network resources share kiye ja sakte the, aur network ko multiple nodes/links se design kiya ja sakta tha.

### 1969: ARPANET ke first nodes

U.S. ARPA-funded research program ke through ARPANET ka initial network 1969 ke end mein four nodes tak pahucha: UCLA, Stanford Research Institute (SRI), UC Santa Barbara aur University of Utah. First host-to-host connection attempt 29 October 1969 ko UCLA se SRI ke computer tak hua; system initial attempt par crash hua, aur short initial transmission ke baad connection complete hua. Is detail ko Internet ke famous early milestone ke roop mein yaad kiya jata hai.

ARPANET ka objective modern consumer social media banana nahi tha. It was a research network to interconnect computing resources and support communication. U.S. National Science Foundation ki history summary is four-node beginning ko describe karti hai. [2]

### 1970s: Internetworking ka bigger challenge

ARPANET ke alawa packet radio aur packet satellite jaise networks develop ho rahe the. Problem ye thi ki har network ki internal technology same nahi thi. Ek network ke computer ko doosre type ke network ke computer se communicate karwana tha.

1973 mein DARPA ne network interconnection research programme start kiya. Vinton Cerf aur Robert Kahn ne internetworking architecture ke development mein leading contributions diye. TCP/IP suite ke ideas ek hi din mein create nahi hue; proposals, experiments, multiple implementations aur community feedback ke through evolve hue. [3]

### 1974: Early TCP design paper

Cerf aur Kahn ka 1974 paper, *A Protocol for Packet Network Intercommunication*, heterogeneous packet networks ko common internetwork protocol se connect karne ka model explain karta hai. Initial design mein later separate TCP and IP responsibilities ke concepts ek broader protocol design mein the. Architecture evolve hokar layered TCP/IP suite bana.

### 1970s–1980s: Ethernet and LANs

Robert Metcalfe aur colleagues ne Xerox PARC mein Ethernet develop kiya. Ethernet local-area networking ko practical banane mein central raha. Offices aur labs ke computers ko same building/campus network mein connect karna easier hua. Aage chal kar Ethernet standards IEEE 802.3 family ke through evolve hue.

### 1 January 1983: ARPANET ka TCP/IP transition

ARPANET ne Network Control Protocol (NCP) se TCP/IP par transition kiya. Ye major coordinated migration tha. Iska importance: different networks ko common internetwork architecture par connect karna. Internet Society ki history transition date aur planning ko describe karti hai. [3]

### 1983–1987: DNS ka emergence

Hostnames ki manually maintained lists scale nahi kar rahi thi. Paul Mockapetris ne Domain Name System (DNS) design/specify kiya, jisse distributed hierarchical naming system develop hua. Core DNS concepts RFC 1034 aur implementation/specification RFC 1035 mein published hue (1987). [4]

### 1986 onwards: NSFNET

U.S. National Science Foundation ne NSFNET develop kiya, initially research/university community ke liye. Isne academic networks ko high-capacity backbone se connect karne aur Internet growth ko accelerate karne mein key role play kiya. 1995 mein NSFNET backbone funding phase out hui, jab commercial network providers aur interconnected private infrastructure grow kar chuke the. [5]

### 1990s: Web and commercial Internet growth

Tim Berners-Lee ne CERN mein World Wide Web ke core ideas—HTML, HTTP, URL/URI and browser/server model—develop kiye. Web Internet par chalne wali services mein se ek hai; Internet aur Web same cheez nahi. 1990s mein browsers, commercial ISPs, websites, search engines and e-commerce ne public adoption expand ki.

### 2000s–2020s: Broadband, mobile, cloud and edge

Broadband, fibre, Wi-Fi, smartphones, 4G/5G, hyperscale data centres, CDNs, video streaming, cloud infrastructure and IoT ne network traffic ka scale aur type badla. Ab networking sirf page load nahi: video calls, autonomous/industrial telemetry, multiplayer games, financial transactions, model inference, real-time collaboration aur distributed storage sab involve hain.

**History lesson:** Internet ek product launch se nahi bana. Open protocols, interoperability, independent network operators, standards processes, research, commercial investment aur incremental deployment ne ise grow kiya.

## 7. Internet vs Web vs Wi-Fi vs mobile network

Ye terms often mix ho jati hain:

- **Internet:** Globally interconnected networks aur IP-based communication infrastructure.
- **World Wide Web:** Internet par available hypertext/application system, jo URLs, HTTP and browsers jaise technologies use karta hai.
- **Wi-Fi:** Local wireless networking technology. Wi-Fi connected hona automatically public Internet access guarantee nahi karta.
- **Mobile/cellular network:** Operator-managed radio access and core network; ye Internet connectivity provide kar sakta hai.
- **Intranet:** Organization ka private internal network/services.
- **Extranet:** Controlled access wala private system jo selected external parties ko access de sakta hai.

## 8. OSI model aur TCP/IP model

Layering complex networking ko smaller responsibilities mein divide karti hai. OSI model ek conceptual seven-layer reference model hai. Practical Internet stack ko commonly 4/5 layer TCP/IP model se samjhaya jata hai. Dono exact same model nahi hain; mapping approximate hai.

| OSI layer | Example responsibility | Common examples |
|---|---|---|
| 7 Application | User-facing protocol semantics | HTTP, DNS, SMTP, SSH |
| 6 Presentation | Data representation, encoding, encryption concept | TLS often crosses traditional layer boundaries; JSON, UTF-8 |
| 5 Session | Conversation/session coordination concept | Session management in application protocols |
| 4 Transport | Process-to-process communication | TCP, UDP, QUIC (built over UDP) |
| 3 Network | Logical addressing and routing | IPv4, IPv6, ICMP |
| 2 Data Link | Local link delivery | Ethernet, Wi-Fi MAC |
| 1 Physical | Signal transmission | Copper, fibre, radio |

### TCP/IP simplified model

1. **Application:** HTTP, DNS, SMTP, SSH.
2. **Transport:** TCP, UDP; QUIC integrates transport and security design over UDP.
3. **Internet/Network:** IPv4, IPv6, ICMP.
4. **Link/Network Access:** Ethernet, Wi-Fi and physical media.

Encapsulation ka idea: application data transport-layer header ke saath segment/datagram ban sakta hai; network layer IP packet banati hai; link layer local frame banati hai. Receiving side reverse order mein decapsulation karti hai.

## 9. Network performance: sirf Mbps nahi

| Term | Meaning | Example impact |
|---|---|---|
| Bandwidth | Link capacity / theoretical maximum data rate | Link ki upper capacity |
| Throughput | Actual delivered data rate | Real download speed |
| Goodput | Useful application payload rate | Headers/retransmissions exclude karke useful data |
| Latency | Data ko travel/response karne mein delay | Button click ke baad server response |
| RTT | Round-trip time | Request jaakar reply aane ka time |
| Jitter | Delay ka variation | Voice/video call quality |
| Packet loss | Packets ka destination tak na pahunchna | Retransmission or choppy stream |
| Availability | Service reachable/working hone ka proportion | 99.9% monthly uptime target |

A 100 Mbps plan ka matlab ye nahi ki har app 100 Mbps goodput dega. Wi-Fi link, congestion, ISP route, server throughput and protocol overhead sab effect karte hain.

**Real-world examples:**

- Video conference: low latency and low jitter are important.
- Large backup: sustained throughput matters.
- Payment API: reliability, correctness and secure connectivity are important.
- Multiplayer game: latency and packet-loss patterns matter; small frequent updates may be more important than bulk throughput.
- Video streaming: adaptive bitrate, buffering and CDN placement matter.

## 10. Core vocabulary

| Term | Meaning |
|---|---|
| LAN | Local Area Network |
| WAN | Wide Area Network |
| WLAN | Wireless LAN |
| NIC | Network Interface Card/controller |
| MTU | Maximum Transmission Unit of a link/network path context |
| Packet | Network-layer data unit, commonly IP packet |
| Frame | Link-layer data unit |
| Port | Transport/application endpoint number, not a physical socket necessarily |
| Socket | OS programming abstraction for network communication endpoint |
| Gateway | Device/service forwarding traffic between networks or acting as protocol gateway |
| Subnet | A logically defined IP address range |
| ISP | Internet Service Provider |
| ASN | Autonomous System Number |
| IXP | Internet Exchange Point |

## 11. Short practical exercise

Apne own laptop par:

1. Network settings open karke Wi-Fi/Ethernet adapter details dekho.
2. IP address, subnet mask/prefix, default gateway and DNS server identify karo.
3. Wi-Fi disconnect karke observe karo ki local gateway unreachable ho jata hai ya nahi.
4. Same LAN par kisi device ko ping karne ki permission ho toh ping test karo.
5. Wi-Fi aur Ethernet (available ho toh) ke speed, latency and stability compare karo.

Public IP ko private address samajhkar expose mat karo. Screenshots share karne se pehle public IP, device name, SSID, MAC address aur location-sensitive information hide karna.

## 12. Self-check questions

1. Internet aur Web mein exact difference kya hai?
2. Packet switching ke bina large multi-network system ko grow karna kyun harder hota?
3. Router aur switch ki responsibility alag kaise hai?
4. IP delivery ko best-effort kyun kaha jata hai?
5. Bandwidth aur latency mein difference kya hai?
6. 1983 TCP/IP transition important kyun tha?
7. DNS ko manually maintained host file se replace karna global scale par kyun difficult hota?
8. Video call ke liye jitter kyun matter karta hai?

## References and further reading

1. [RFC 791 — Internet Protocol (IPv4), 1981](https://www.rfc-editor.org/rfc/rfc791)
2. [U.S. National Science Foundation — Birth of the Commercial Internet](https://www.nsf.gov/impacts/internet)
3. [Internet Society — A Brief History of the Internet](https://www.internetsociety.org/internet/history-internet/brief-history-internet/)
4. [RFC 1034 — Domain Names: Concepts and Facilities](https://www.rfc-editor.org/rfc/rfc1034)
5. [Internet Society — History of the Internet & Related Networks](https://www.internetsociety.org/internet/history-internet/brief-history-internet-related-networks/)
6. [Computer History Museum — Internet History](https://www.computerhistory.org/internethistory/)
7. [Cloudflare Learning Center — How the Internet Works](https://www.cloudflare.com/learning/network-layer/how-does-the-internet-work/)

---

**Next subchapter:** 05B — IP Addressing, Subnets, DNS, Routing and the Global Internet.
