---
title: 'Bitcoin Optech Newsletter #224'
permalink: /hi/newsletters/2022/11/02/
name: 2022-11-02-newsletter-hi
slug: 2022-11-02-newsletter-hi
type: newsletter
layout: newsletter
lang: hi
---
इस सप्ताह का समाचार पत्र वैकल्पिक रूप से नोड्स को पूर्ण RBF को सक्षम करने की अनुमति देने के बारे में
निरंतर चर्चा का वर्णन करता है, BIP324 संस्करण 2 एन्क्रिप्टेड ट्रांसपोर्ट प्रोटोकॉल के एक डिजाइन तत्व पर
प्रतिक्रिया के लिए अनुरोध करता है, LN विफलताओं और विशेष नोड्स के लिए देरी को विश्वसनीय रूप से
जिम्मेदार ठहराने के लिए एक प्रस्ताव का सारांश देता है, और लिंक करता है आधुनिक LN HTLCs के लिए एंकर
आउटपुट का उपयोग करने के विकल्प के बारे में चर्चा। नए सॉफ़्टवेयर रिलीज़ और रिलीज़
उम्मीदवारों की घोषणाओं के साथ हमारे नियमित अनुभाग भी शामिल हैं --- LNडी के लिए एक सुरक्षा महत्वपूर्ण
अद्यतन --- और लोकप्रिय Bitcoin Infrastructure सॉफ़्टवेयर में उल्लेखनीय परिवर्तनों के विवरण शामिल हैं।

## समाचार

- **mempool स्थिरता:** Anthony Towns ने Bitcoin-Dev मेलिंग सूची पर एक [चर्चा] शुरू की
  [कस्बों की स्थिरता] लेनदेन रिले और mempool स्वीकृति के लिए Bitcoin Core की नीतियों को
  कॉन्फ़िगर करना आसान बनाने के परिणामों के बारे में, जैसे कि `mempoolfullrbf` विकल्प के योग द्वारा
  किया गया था Bitcoin Core की विकास शाखा (see न्यूज़लेटर्स [#205][news205 rbf],
  [#208][news208 rbf], [#222][news222 rbf], और [#223][news223 rbf])।
  उनका दावा है कि "यह अतीत में Core द्वारा किए गए कार्यों से अलग है, इसमें पहले
  हमने यह सुनिश्चित करने की कोशिश की है कि एक नई नीति सभी के लिए अच्छी हो (या जितनी जल्दी हो सके), और
  फिर इसे लागू होते ही इसे सक्षम कर दिया। . जो भी विकल्प जोड़े गए हैं, वे या तो संसाधनों के उपयोग को इस
  तरह से नियंत्रित करने के लिए हैं जो tx प्रसार को महत्वपूर्ण रूप से [प्रभावित] नहीं करते हैं, नए व्यवहार के
  विवादास्पद होने पर लोगों को पुराने व्यवहार पर वापस जाने की अनुमति देने के लिए (उदाहरण के लिए
  -mempoolreplacement = 0 विकल्प 0.12 से 0.18 तक), और कार्यान्वयन का परीक्षण/debug करना
  आसान बनाने के लिए। लोगों को एक नया रिले व्यवहार देते हुए वे ऑप्ट-इन कर सकते हैं जब हम डिफ़ॉल्ट
  रूप से चालू करने के लिए पर्याप्त आश्वस्त नहीं होते हैं जो दृष्टिकोण मैंने अतीत में Core को लेते देखा है उससे मेल नहीं खाता है।"

    Towns तब विचार करते हैं कि क्या यह विकास के लिए एक नई दिशा है: "पूर्ण [RBF][topic RBF] युगों से विवादास्पद रहा है,
    लेकिन Devs द्वारा व्यापक रूप से पसंद किया जाता है [...] और जब लोग अन्य डिफ़ॉल्ट झूठे विकल्पों का प्रस्ताव
    करते हैं, तो उनके Merging के लिए काफी अधिक प्रतिरोध होगा, उपयोगकर्ताओं के पास विकल्प होने के बारे में
    सभी बातों के बावजूद जो अभी चल रहे हैं।" लेकिन, यह मानते हुए कि यह एक नई दिशा है, वह
    उस निर्णय के कुछ संभावित परिणामों का मूल्यांकन करता है:

    - *<!--it-should-be-easier-to-get-default-disabled-alternative-relay-options-merged-->
      डिफ़ॉल्ट-अक्षम वैकल्पिक रिले विकल्पों को मर्ज करना आसान होना चाहिए:* यदि उपयोगकर्ताओं को
      अधिक विकल्प देना बेहतर माना जाता है, तो रिले नीति के कई पहलू हैं जिन्हें कॉन्फ़िगर करने
      योग्य बनाया जा सकता है। उदाहरण के लिए, Bitcoin नोड्स किसी भी लेनदेन को रिले करने से इनकार
      करने के लिए नोड को कॉन्फ़िगर करने के लिए एक स्क्रिप्ट pubkey पुन: उपयोग (`spkreuse`) विकल्प प्रदान
      करता है जो [एक पते का पुन: उपयोग][topic output linking]।

    - *<!--more-permissive-policies-require-widespread-acceptance-or-better-peering-->
      अधिक अनुमेय नीतियों के लिए व्यापक स्वीकृति या बेहतर पीयरिंग की आवश्यकता होती है:* डिफ़ॉल्ट
      रूप से एक Bitcoin Core नोड आउटबाउंड कनेक्शन के माध्यम से आठ साथियों के साथ लेन-देन करता है,
      इसलिए कम से कम 30% नेटवर्क को नोड के 95% होने से पहले अधिक अनुमेय नीति का समर्थन करने
      की आवश्यकता होती है। कम से कम एक यादृच्छिक रूप से चुने गए सहकर्मी को खोजने का मौका जो
      समान नीति का समर्थन करता हो। नीति का समर्थन करने वाले जितने कम नोड हैं, उतनी ही कम
      संभावना है कि एक नोड उस नीति का समर्थन करने वाला एक सहकर्मी ढूंढेगा।

    - *<!--better-peering-involves-tradeoffs-->
      बेहतर पीयरिंग में ट्रेडऑफ़ शामिल हैं:* Bitcoin नोड्स P2P `addr`, [`addrv2`][topic addr v2],
      और `संस्करण` संदेशों के सेवा क्षेत्र का उपयोग करके अपनी क्षमताओं की घोषणा कर सकते हैं, जिससे समान रुचि
      वाले नोड्स को प्रत्येक को खोजने की अनुमति मिलती है। अन्य और उप-नेटवर्क बनाते हैं (जिन्हें *तरजीही पीयरिंग*
      कहा जाता है)। वैकल्पिक रूप से, सामान्य हितों वाले पूर्ण नोड ऑपरेटर स्वतंत्र रिले नेटवर्क (जैसे LN नोड्स के बीच
      एक नेटवर्क) बनाने के लिए अन्य सॉफ़्टवेयर का उपयोग कर सकते हैं। यह तब भी रिले को
      प्रभावी बना सकता है जब केवल कुछ नोड एक नीति को लागू करते हैं, लेकिन एक दुर्लभ नीति को
      लागू करने वाले नोड्स को पहचानना और सेंसर करना आसान होता है। इसके लिए खनिकों को इन
      उप-नेटवर्कों और वैकल्पिक नेटवर्कों में शामिल होना पड़ता है, जिससे खनन की जटिलता और
      लागत बढ़ जाती है। इससे लेन-देन के चयन को केंद्रीकृत करने का दबाव बढ़ जाता है, जिससे
      सेंसरशिप भी आसान हो जाती है।

        इसके अतिरिक्त, अपने कुछ साथियों की विभिन्न नीतियों को लागू करने वाले नोड दो
        साथियों के साथ विलंबता और बैंडविड्थ को कम करने के लिए [कॉम्पैक्ट ब्लॉक रिले][topic compact block relay]
        और [erlay][topic erlay] जैसी तकनीकों का पूरा लाभ नहीं उठा पाएंगे जब दोनों peers के पास सामान जानकारी हो।

    इस लेखन के रूप में जारी चर्चा के साथ, Towns की पोस्ट को कई व्यावहारिक प्रतिक्रियाएं मिलीं। हम अगले
    सप्ताह के न्यूजलेटर में एक अपडेट प्रदान करेंगे।

- **BIP324 संदेश पहचानकर्ता:** Bitcoin-Dev मेलिंग सूची में Peter Wullie [पोस्ट किया गया][wuille bip324]
  [bip324][bips #1378] draft specification for [version 2 P2P encrypted transport protocol]
  [topic v2 p2p transport] के अद्यतन की प्रतिक्रिया है। प्रोटोकॉल  (v2 परिवहन)। बैंडविड्थ को बचाने के लिए,
  v2 ट्रांसपोर्ट मौजूदा प्रोटोकॉल के 12-Byte संदेश नामों को पहचानकर्ताओं के साथ 1 Byte के रूप में छोटा करने की
  अनुमति देता है। उदाहरण के लिए, `संस्करण` संदेश का नाम, जो 12 Byte तक गद्देदार है, को 0x00 से बदला जा सकता है।
  हालांकि, छोटे संदेश नाम नेटवर्क में संदेशों को जोड़ने के लिए भविष्य के विभिन्न प्रस्तावों के बीच संघर्ष के जोखिम को बढ़ाते हैं।
  Wullie इस समस्या के चार अलग-अलग दृष्टिकोणों के बीच ट्रेडऑफ़ का वर्णन करता है और समुदाय से इस topic के बारे
  में राय मांगता है।

- **LN रूटिंग विफलता एट्रिब्यूशन:** LN भुगतान प्रयास कई कारणों से विफलता में समाप्त हो सकते हैं, अंतिम
  रिसीवर से अस्थायी रूप से ऑफ़लाइन होने वाले रूटिंग नोड्स में से एक को भुगतान preimage जारी करने से इंकार
  कर दिया। किन नोड्स के कारण भुगतान विफल हुआ, इसकी जानकारी खर्च करने वालों के लिए निकट-भविष्य
  के भुगतानों के लिए उन नोड्स से बचने के लिए बेहद उपयोगी होगी, लेकिन LN प्रोटोकॉल आज उस जानकारी को
  किसी खर्च करने वाले को संप्रेषित करने के लिए रूटिंग नोड्स के लिए कोई प्रमाणित विधि प्रदान नहीं करता है।

    कई साल पहले, Joost Jager ने एक समाधान प्रस्तावित किया (देखें [न्यूज़लेटर #51][news51 attrib]),
    जिसे अब उन्होंने [अपडेट किया हुआ][jager attrib] सुधार और अतिरिक्त विवरण के साथ किया है। तंत्र उन
    नोड्स की जोड़ी की पहचान सुनिश्चित करेगा जिनके बीच भुगतान विफल हुआ (या उनमें से एक के बीच पहले विफलता संदेश सेंसर
    किया गया था या विकृत हो गया था)। Jager के प्रस्ताव का मुख्य पहलू यह है कि यह विफलताओं के लिए LN onion संदेशों
    के आकार में उल्लेखनीय रूप से वृद्धि करेगा यदि अन्य LN गुण समान रहे, हालांकि विफलताओं के
    लिए onion संदेशों का आकार उतना बड़ा नहीं होना चाहिए यदि LN हॉप्स की अधिकतम संख्या हो कम हो जाये।

    वैकल्पिक रूप से, Rusty Russell [सुझाव दिया][russell attrib] कि एक व्ययकर्ता [सहज भुगतान][topic spontaneous payments]
    के समान एक तंत्र का उपयोग कर सकता है जहां प्रत्येक रूटिंग नोड का भुगतान किया जाता है, भले ही अंतिम भुगतान विफल हो जाए।
    खर्च करने वाला यह पता लगा सकता है कि उसने कितने satoshi भेजे और कितने सतोषियों को वापस प्राप्त किया।

- **<!--anchor-outputs-workaround-->एंकर आउटपुट वर्कअराउंड:** Lightning-Dev मेलिंग सूची में Bastien Teinturier [पोस्ट किया गया][teinturier fees]
  [anchor output][topic anchor outputs] कई निर्धारित आउटपुट के साथ प्रत्येक [HTLC][topic htlc] का उपयोग करने के
  लिए अलग-अलग शुल्क पर का एक [प्रस्ताव][bolts #1036] जारी किया। [CPFP][topic cpfp] तंत्र के माध्यम से लेनदेन में
  शुल्क जोड़ने की अनुमति देने के लिए [CPFP कार्व-आउट][topic cpfp carve out]
  नियम के विकास के साथ एंकर आउटपुट पेश किए गए थे [CPFP][topic CPFP] तंत्र [पिननेबल][topic transaction pinning]
  LN के दो-पक्षीय अनुबंध प्रोटोकॉल के लिए। हालांकि, Teinturier [नोट्स][bolts #845] कि CPFP का उपयोग
  करने के लिए प्रत्येक LN नोड को गैर-LN UTXO का एक पूल किसी भी समय खर्च करने के लिए तैयार रखने की
  आवश्यकता होती है। तुलना करके, HTLC के कई संस्करणों को अलग-अलग शुल्क के साथ निर्धारित करने
  से उन शुल्कों का भुगतान सीधे HTLC के मूल्य से किया जा सकता है --- कोई अतिरिक्त UTXO प्रबंधन
  की आवश्यकता नहीं है, उन मामलों को छोड़कर जहां कोई भी निर्धारित शुल्क पर्याप्त नहीं था।

    वह कई शुल्क वाले HTLCs प्रदान करने के विचार के लिए अन्य LN डेवलपर्स से समर्थन मांग रहा है। इस
    लेखन के रूप में सभी चर्चा Teinturier [PR][bolts #1036] पर हुई है।

## रिलीज और रिलीज उम्मीदवार

*लोकप्रिय Bitcoin इन्फ्रास्ट्रक्चर परियोजनाओं के लिए नए रिलीज और रिलीज उम्मीदवार। कृपया नई रिलीज़ में
अपग्रेड करने या रिलीज़ उम्मीदवारों का परीक्षण करने में मदद करने पर विचार करें।*

- [LND 0.15.4-beta][] और [0.14.4-beta][lnd 0.14.4-beta] **सुरक्षा महत्वपूर्ण** रिलीज़ हैं जिनमें हाल के ब्लॉक
  को संसाधित करने में समस्या के लिए एक बग फिक्स शामिल है। सभी यूजर्स को अपग्रेड करना चाहिए।

- [Bitcoin Core 24.0 RC2][] नेटवर्क के सबसे व्यापक रूप से उपयोग किए जाने वाले पूर्ण नोड कार्यान्वयन के अगले संस्करण के
  लिए एक रिलीज उम्मीदवार है। एक [गाइड टू टेस्टिंग][bcc testing] उपलब्ध है।

  **चेतावनी:** इस रिलीज के उम्मीदवार में `mempoolfullrbf` कॉन्फ़िगरेशन विकल्प शामिल है, जो कई प्रोटोकॉल और
  एप्लिकेशन डेवलपर्स का मानना ​​​​है कि न्यूजलेटर [#222][news222 rbf] और [#223][news223 rbf] में वर्णित
  व्यापारी सेवाओं के लिए समस्याएँ पैदा कर सकता है।. Optech RC का मूल्यांकन करने और सार्वजनिक चर्चा में भाग
  लेने के लिए प्रभावित होने वाली किसी भी सेवा को प्रोत्साहित करता है।

## उल्लेखनीय कोड और दस्तावेज़ीकरण परिवर्तन

*इस सप्ताह [Bitcoin Core][bitcoin core repo], [Core Lightning][core lightning repo],
[Eclair][eclair repo], [LDK][ldk repo], [LND][LND Repo] में उल्लेखनीय परिवर्तन।
[libsecp256k1][libsecp256k1 repo], [Hardware Wallet Interface (HWI)][hwi repo],
[Rust Bitcoin][Rust bitcoin repo], [BTCPay Server][btcpay server repo],
[BDK][bdk repo], [Bitcoin Improvement Proposals (BIP)][BIPs repo], और
[Lightning BOLTs][bolts repo]।*

- [Bitcoin Core #23927][] pruned हुए नोड्स पर `getblockfrompeer` को नोड की वर्तमान Synchronization
  प्रगति के नीचे की ऊंचाई तक प्रतिबंधित करता है। यह भविष्य के ब्लॉकों को पुनः प्राप्त करने से उत्पन्न होने वाले एक फ़ुटगन को
  रोकता है जिससे नोड की ब्लॉक-फ़ाइलें छंटाई के लिए अयोग्य हो जाती हैं।

  Bitcoin Core लगभग 130 MB की फाइलों में ब्लॉक को स्टोर करता है, जिस क्रम में वह उन्हें प्राप्त करता है। Pruning
  संपूर्ण ब्लॉक फ़ाइलों को त्याग देगा, लेकिन सिंक्रनाइज़ेशन द्वारा संसाधित नहीं किए गए ब्लॉक वाली किसी भी फ़ाइल को नहीं छोड़ेगा।
  एक छोटे से डेटा भत्ते का संयोजन और `getblockfrompeer` RPC के बार-बार उपयोग से कई ब्लॉक-फाइलें छंटाई के लिए
  अयोग्य हो सकती हैं, और एक छंटे हुए नोड को इसके डेटा भत्ते से अधिक होने का कारण बन
  सकता है।

- [Bitcoin Core #25957][] [block filter index][topic compact block filters]
  (यदि सक्षम हो) का उपयोग करके डिस्क्रिप्टर वॉलेट के लिए रेस्कैन के प्रदर्शन में सुधार करता है, जो उन ब्लॉकों को
  छोड़ देता है जो खर्च नहीं करते हैं या वॉलेट के लिए प्रासंगिक UTXO बनाते हैं। .

- [Bitcoin Core #23578][] [hwi][topic hwi] का उपयोग करता है और [BIP371] के लिए हाल ही में मर्ज
  किए गए समर्थन (देखें [न्यूज़लेटर #207][news207 bc22558]) [Taproot][topic taproot] ​​के लिए बाहरी
  हस्ताक्षर समर्थन की अनुमति देता है Taproot कीपथ खर्च करने के लिए।

- [Core Lightning #5646][] [x-only public key][news72 xonly] को हटाने के लिए
  [ऑफ़र्स][topic offers] के प्रयोगात्मक कार्यान्वयन को अपडेट करता है (इसके बजाय
  [संपीड़ित pubkey][compressed pubkeys] का उपयोग करते हुए, जिसमें एक अतिरिक्त Byte होता है)।
  यह एक अन्य प्रायोगिक प्रोटोकॉल [ब्लाइंड Payment][blinded payments] के
  अग्रेषण को भी लागू करता है। PR विवरण चेतावनी देता है कि "इसमें ब्लाइंड भुगतान के साथ चालान
  बनाना और वास्तव में भुगतान करना शामिल नहीं है।"

- [LND #6517][] एक नया RPC और घटना जोड़ता है जो एक उपयोगकर्ता को निगरानी करने की अनुमति देता है जब एक
  आने वाले भुगतान ([HTLCs][topic htlc]) को पूरी तरह से बंद कर दिया जाता है ताकि नए चैनल संतुलन वितरण को
  प्रतिबिंबित करने के लिए प्रतिबद्धता लेनदेन को अपडेट किया जा सके।

- [LND #7001][] अग्रेषण इतिहास RPC (`fwdinghistory`) में नए फ़ील्ड जोड़ता है, यह दर्शाता है कि किस चैनल पार्टनर
  ने हमें और उस पार्टनर को भुगतान भेजा है जिसे हमने भुगतान भेजा है।

- [LND #6831][] HTLCs इंटरसेप्टर कार्यान्वयन को अपडेट करता है (देखें [न्यूज़लेटर #104][news104 intercept])
  आने वाले भुगतान (HTLCs) को स्वचालित रूप से अस्वीकार करने के लिए यदि इंटरसेप्टर से जुड़े क्लाइंट ने इसे उचित रूप
  से संसाधित नहीं किया है समय की राशि। यदि किसी HTLC की समाप्ति के निकट आने से पहले उसे स्वीकार या अस्वीकार नहीं
  किया जाता है, तो चैनल पार्टनर को अपने फंड की सुरक्षा के लिए चैनल को बंद करने के लिए बाध्य करना होगा। यह मर्ज
  किए गए PR की उस समाप्ति से पहले स्वत: अस्वीकृति सुनिश्चित करता है कि चैनल खुला रहता है। खर्च करने
  वाला कभी भी फिर से भुगतान भेजने का प्रयास कर सकता है।

<!-- नीचे दी गई प्रतिबद्धता LND की मास्टर शाखा के लिए एक सीधा push प्रतीत होता है -->
- [LND 609cc8b][] एक [सुरक्षा नीति][lnd secpol] जोड़ता है, जिसमें कमजोरियों की रिपोर्ट करने के निर्देश शामिल हैं।

- [Rust Bitcoin #957][] हस्ताक्षर करने के लिए एक API जोड़ता है [PSBTs][topic psbt]। यह हस्ताक्षर करने का
  समर्थन नहीं करता है [Taproot][topic taproot] अभी तक खर्च करता है।

- [BDK #779][] ECDSA हस्ताक्षरों के [low-r grinding][topic low-r grinding] के लिए समर्थन जोड़ता है,
  जो सभी हस्ताक्षरों के आकार को एक Byte से कम करने की अनुमति देता है।

{% include references.md %}
{% include linkers/issues.md v=2 issues="23927,25957,5646,6517,7001,6831,957,779,1036,845,1378,23578,22558" %}
[bitcoin core 24.0 rc2]: https://bitcoincore.org/bin/bitcoin-core-24.0/
[bcc testing]: https://github.com/bitcoin-core/bitcoin-devwiki/wiki/24.0-Release-Candidate-Testing-Guide
[lnd 609cc8b]: https://github.com/LightningNetwork/lnd/commit/609cc8b883c7e6186e447e8d7e6349688d78d4fd
[lnd secpol]: https://github.com/lightningnetwork/lnd/security/policy
[towns consistency]: https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2022-October/021116.html
[news205 rbf]: /hi/newsletters/2022/06/22/#full-replace-by-fee
[news208 rbf]: /hi/newsletters/2022/07/13/#bitcoin-core-25353
[news222 rbf]: /hi/newsletters/2022/10/19/#transaction-replacement-option
[news223 rbf]: /hi/newsletters/2022/10/26/#rbf
[wuille bip324]: https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2022-October/021115.html
[news72 xonly]: /en/newsletters/2019/11/13/#x-only-pubkeys
[compressed pubkeys]: https://developer.bitcoin.org/devguide/wallets.html#public-key-formats
[blinded payments]: /en/topics/rendez-vous-routing/
[news104 intercept]: /en/newsletters/2020/07/01/#lnd-4018
[news51 attrib]: /en/newsletters/2019/06/19/#authenticating-messages-about-ln-delays
[jager attrib]: https://lists.linuxfoundation.org/pipermail/lightning-dev/2022-October/003723.html
[russell attrib]: https://lists.linuxfoundation.org/pipermail/lightning-dev/2022-October/003727.html
[teinturier fees]: https://lists.linuxfoundation.org/pipermail/lightning-dev/2022-October/003729.html
[lnd 0.15.4-beta]: https://github.com/lightningnetwork/lnd/releases/tag/v0.15.4-beta
[lnd 0.14.4-beta]: https://github.com/lightningnetwork/lnd/releases/tag/v0.14.5-beta
[news207 bc22558]: /hi/newsletters/2022/07/06/#bitcoin-core-22558