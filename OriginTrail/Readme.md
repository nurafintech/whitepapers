# The OriginTrail Decentralized Network (ODN)
OriginTrail is a neutral, open-source protocol enabling data sharing between companies and organizations. It utilizes decentralized nodes and an off-chain technology stack to interface with legacy systems as well as other blockchains (permissioned and permissionless). OriginTrail allows businesses to improve interoperability among systems and facilitate trusted data exchange. <br/> <br/>
## The Idea's Origin
Over the years’ there have been a number of scandals involving food. There was the horse meat scandal (which was found in beef products), and then the baby milk scandal in China. There are many counterfeit wines and tobacco products on the market too. Medical supplies (one of GS1’s areas of expertise) can also potentially suffer.
#
ایده اولیه این پروژه برای هنگامی بود که سازندگان میخواستند روشی داشته باشند تا بتوانند محصولات با کیفیت کشاورزی یا لبنی را در شبکه ای قرار داده و خریدار با اطمینان از اصل بودن و با کیفیت بودن محصول، آن را خریداری کند. بنابراین به دنبال مکانیسمی هستیم که عده ای را تشویق کند داده ها را وارد کرده و عده ای دیگر در این شبکه، آن داده ها را طبق قول و قراری نگهداری کنند و در زمان نیاز، آن ها را تحویل دهند.
#

## How does blockchain come in to play?
Firstly, utilising a blockchain ledger to store the logistics data (and any other data necessary), there is the possibility to have an un-editable, and therefor more accountable system in place. <br>
**Tamper proof RFID tags are one such solution**, enabling a consumer brand to attach a coded RFID tag to each product, box or pallet of product they put through the supply chain. If that product is then tampered with during the supply process there then should be the opportunity to understand where that likely happened. From a consumer perspective, if there is no RFID tag present on a product they were expecting to have one (such as an expensive luxury good), it will automatically raise alarm bells, hopefully cutting out a large % of counterfeit goods as they will be shunned by the consumer, or more ideally removed from the chain earlier.
<br>
There are a number of blockchain companies working with these RFID tags already, including VeChain, Waltonchain, and Wabi (I may have unintentionally missed some out). All have various key partners in place already on a global scale, and some are currently being used in real-world uses. RFID can be specific to usage requirements, so for instance they can have temperature monitoring for chilled/frozen goods, be tamper proof for products that need to remain sealed, or just be more simple like a QR code.
<br/>
#
این پروژه ها اگر چه جذاب به نظر میرسند، اما هر کدام به دنبال پیاده سازی استاندارد های مخصوص خود بوده و در نتیجه اگر بخواهیم بخواهیم از تگ های مخصوص وی چین استفاده کنیم، دیگر به شبکه وی چین محدود خواهیم شد. خود شبکه وی چین به طور کامل غیرمتمرکز نیست. 
<br/>

**!شاید باید به جای اینکه از یک بلاکچینی که به بقیه برتری دارد، باید از چند بلاکچین استفاده کنیم**
<br> <br>
اینجاست که با در نظر گرفتن چهار ویژگی بنیادی، شبکه ای ایجاد کرده که در آن بتوان از بلاکچین های مختلف نیز یاری گرفت؛ در ادامه توضیح خواهیم داد.
#

## Network Features
The ODN Mainnet has been operating since December 2018 with actual enterprise “data jobs” being posted by data creator nodes and stored by data holding nodes (continue reading for examples). The OriginTrail protocol and the ODN has been built from the ground up with four core features:
1. **Interoperability and Data Integrity:**
  OriginTrail has been built to take advantage of globally recognized GS1 and W3C standards. This allows for efficient alignment of data from multiple sources, including both legacy systems and newer blockchain-powered systems. This data could be anything: tracking and tracing data, Internet-of-Things (IoT) data, descriptive attributes, etc. Once data is aligned, consensus checks to verify datasets from different stakeholders can take place; additionally, auditing via compliance organizations can be authorized automatically. Due to the sensitive nature of many supply chain and business use cases, the ODN is designed to provide a “zero-knowledge” method to prove data validity.<br>
This means that their protocol can be applied to any blockchain (including private ones) to enable **GS1** conformance. It can also integrate within a supply chain company’s current ERP solution. (ERP is basically a business’s internal process management software and it will deal with things like supply chain, but also other unrelated things — it depends on the company requirements). <br>
**The logistics data would be stored on their OriginTrail Decentralised Network**, which is in turn written to blockchain ledger for safety and assurance. The logistics company may not even need to have a block-chain themselves. It makes integrating new ideas with old working methods far more easy-to-do. Asking multi-billion-dollar companies to simply change everything over-night is almost impossible so you have to make it easy.
  
2. **Data Immutability:** A tamper-proof fingerprint (cryptographic hash) of the data is generated and placed on the a blockchain when first published to the ODN; this is then used to verify that data has not been modified in any way.
3. **Stability & Cost Efficiency:** As the “heavy lifting” of interoperability and data integrity takes place off-chain, the OriginTrail graph database operates cheaply and efficiently. Its open-sourced nature enables easy deployment and does not “rip and replace” legacy systems as other blockchain-based supply chain solutions do.
4. **Network Incentivization via Token Staking:** As detailed in the section below, the TRAC token is the means of compensation between data creators, data holders, and data consumers. It uses an innovative staking system to keep all parties honest; nodes are therefore incentivized for performing consensus checks and delivering data on demand.
#

برای ساخت این شبکه، چهار ویژگی بنیادی اصلی را در نظر میگیریم. <br/>
اول اینکه داده ها باید استاندارد و اصولی باشند به نحوی که هم بتوانیم داده های سیستم های قدیمی را وارد شبکه کنیم و هم داده های سیستم های جدیدتر مثل داده های بلاکچین های نوظهور. تیم سازنده برای اینکار با دو سازمان جهانی تعیین استاندارد های وب، یعنی GS1 و W3C شروع به همکاری کرده و به عضویت آن ها درآمده است. در داکیومنتی مجزا در مورد استاندارد های Uniform Asset Identifier  و Uniform Asset Loacators که مخصوص وب 3 طراحی شده اند و مانند URI , UAI های وب 1 میباشند. <br/>
دوم اینکه برای ایجاد اعتماد و اطمینان از صحت داده ها، باید روشی برای درستی آن ها اتخاذ کنیم و از بلاکچین برای ثبت hash مربوط به داده ها استفاده خواهیم کرد. <br/>
سوم اینکه روش های مدرن استفاده شده در بلاکچین های جدید، نیمتوانند به خوبی با سیستم های قدیمی ارتباط و تبادل داده برقرار کنند؛ بنابراین به جای جایگزین کردن آن ها به دنبال روشی برای تعامل با آن سیستم های قدیمی خواهیم بود. سیستم های مدرن موجود بر پایه بلاکجین، حتی اگر بتوانند از داده های سیستم های قدیمی وب 1 و 2، استفاده کنند، برای تبادل و تعامل با آن ها هزینه های نسبتا زیادی را خواهد گرفت. بنابراین سعی میکنیم این هزینه ها را کاهش دهیم. <br/>
چهارم اینکه اگر میخواهیم شبکه ای decentralized داشته باشیم، باید افراد مختلف را تشویق کنیم تا به شبکه ما اضافه شوند.<br/> <br/>
این چهار ویژگی بنیادی در کنار هم هستند که اوریجین تریل را از بلاکچین های private ای مثل بلاکچین IBM و راه حل زنجیره تامین بر پایه آن یعنی TradeLens مجزا میکند.
تریدلنز پلتفرمی است که با استفاده از بلاکچین غیرمتمرکز ساخته شده توسط IBM، روش هایی برای بهینه کردن ورد و خروج و ردیابی کانتینرها در گمرک ها و خلیج ها و کشتی ها ارائه دهد که البته شاید برای افرادی خاص یا دولت چین که میخواهند اجناسی خاص را سوار بر کشتی کنند، خیلی جذاب باشد اما به آن صورت نتوانست مورد استقبال عموم قرار گیرد.
<br/><br/>
#
## OringinTrail Decentralized Network
At the core is a decentralized network of data providers, data creators, data holders, and data viewers:

![](https://miro.medium.com/max/1400/1*F_izA26JNTEcxJGzVVdo1w.jpeg) <br><br>
در حال حاضر از بلاکچین های Etherum و Gnosis و Polygon استفاده شده و از NEO و IOTA استفاده نمیشود.

  Data enters the OriginTrail Decentralized Network through a Data Creator node. This data source could be from any number of business functions, including existing ERPs, blockchains (permissioned and permissionless), etc. A cryptographic data hash of the data is first fingerprinted to a blockchain to ensure data immutability. This data is then passed (via a bidding process) to 3+ Data Holder nodes that agree to hold the data for the terms of a contract. Data holder nodes are essentially decentralized, interconnected servers and provide that data upon demand to relevant parties.<br>

The data can be treated exactly how the data creator wants. Data creators can set the data to be public or private, have the data expire after a certain number of weeks/years, or have that data (or parts of data) shared only with appropriate parties. Sensitive data is protected using zero-knowledge methods in a privacy-by-design approach. These data holding nodes also function as a vast, decentralized knowledge graph to connect data sets across companies and/or supply chain partners quickly and efficiently. This core feature of the ODN is one of the major selling points for protocol adoption, as searching for inter-related data between partners has not been possible before. This writeup on the decentralized knowledge graph is highly recommended to learn more.<br>

Data holding nodes were designed to be very decentralized. They are open to anyone with 3000+ TRAC, and if the data job meets your criteria (job length, data size, etc.) then your node could be randomly assigned the job. All data holding nodes are equal; having more TRAC per node only means you can accept additional jobs compared to others.<br>
 
 ![](https://miro.medium.com/max/1400/0*6vELJQpYp6K56ALx)

 <br>

 1. Data Provider (DP)
The Data Provider (DP) is an entity that publishes supply chain data to the network. A typical scenario would be a company that would like to publish and share its data from their ERP system about products that are part of their supply chain. Data Providers can also be consumers interacting with the network through applications, or devices, such as sensors that provide information about significant events in the supply chain. <br>
The interest of the Data Provider is to be able to safely store data on the network, as well as to be able to connect it and cross-check with the data of other DPs within the network. Depending on the use case, providing data to the network can be incentivised with the Trace token.

2. Data Creator Node (DC)
The Data Creator node (DC) is an entity representing a node that will be responsible for importing the data provided by the DP, making sure that all the criteria of DP are met (e.g. the availability of the data on the network for a desired time or a factor of replication). While we typically expect that Data Providers will run their own Data Creator nodes, it is not a requirement. Third party DC nodes may provide the service for one or several Data Providers. The DC node is an entry point for information to the network and the relationship between the DPs and the DCs is not regulated by the protocol.<br>
The responsibility of the DC node is to negotiate, establish and maintain the service requested by the DP in relationship with its associated Data Holder (DH) nodes. Furthermore, DC nodes are responsible to check if data is available on the network during the time of service and initiate the litigation process in case of any disputes.

3. 3 Data Holder Node (DH)
The Data Holder (DH) is a node that has committed itself to storing the data provided by a DC node for a requested period of time and making it available for the interested parties (which could also be the DC node itself). For this service, the Data Holder will be compensated in TRAC tokens. The DH node has the responsibility to preserve the data intact in its unaltered, original form, as well as to provide high availability of the data in terms of bandwidth and uptime.
<br>It is important to note that the DH node can be a DC node at the same time, in the context of the data that it has introduced to the network. As noted, the same software runs on all the nodes in the network, providing for symmetrical relations and thus not limiting scalability.
<br>The Data Holder may also wish to find data that is not directly delivered by DCs but is popular, and offer it to interested parties. Therefore, it is probable that Data Holders will listen to the network, search for data that is frequently requested, and replicate it from other Data Holders to also store, process and offer it to the Data Viewers. However, since such Data Holders are not bound by the smart contract to provide the service, there is a certain risk that these Data Holders may offer false data or tamper with the data, or even pretend to have data that they don’t have.<br>
To mitigate this risk, a node will be required to deposit a stake for executing an agreement. This stake will be stored in case it is proven that the Data Holder tried to sell altered data while Data Viewers will have a mechanism to check if all the chunks of data are valid and initiate a litigation procedure in case of any inconsistencies.<br>
The amount of stake is set per agreement within each node. The DC node may require a minimum amount of stake to form an agreement with DH nodes, informing them of these amounts by publishing this information when they create an “Offer” on the blockchain. The stake settings can be setup either directly in the node configuration files or through a UI application (Houston).
<br>

#
پس به طور خلاصه، با استفاده از قرارداد های هوشمند و توکن هایی که به عنوان وثیقه قفل میشن، مکانیسم نگهداری از داده ها رو ایجاد میکنیم.
نکته مهم اینجاست که اگرچه یک نود نگهدارنده داده، میتواند مبلغ خیلی زیادی توکن رو به عنوان وثیقه گرو بگذارد تا به نوعی پرستیژ خود را بالا برده و با این کار برای کیفیت کاری که انجام میدهد تبلیغ کند، اما لزوما این معیار، تنها معیار بررسی میزان اعتبار یک نود برای نگهداری داده ها نمیباشد.
#

4. Data Viewer
The Data Viewer (DV) is an entity that requests data from any network node able to provide that data. The Data Viewer will be able to send two types of queries to the network. The first type is a request for listing data on the network for a specific set of batch identifiers of the product supply chain they are interested in, where they will be able to retrieve the all connected data of the product trail. The second type is a retrieval query for the specific data set from the listed one in the first request. In both cases, the Data Viewer will receive the offers from all the nodes that have the data, together with their compensation requests for retrieving of the data that will be sent. The Data Viewer can decide which offers it will accept and deposit the requested compensation funds on the escrow smart contract. The providing node then sends the encrypted data in order for the Data Viewer to test the validity of the data. Once the validity of the data is confirmed, the Data Viewer will get the key to decrypt the data while the smart contract will unlock the funds for the party that provided the data. <br>
The interest of the Data Viewer is to get the data for as affordable as possible, but also to be sure that the provided data is genuine. Therefore, the Data Viewer also has an opportunity to initiate the litigation procedure in case the data received is not valid. If that happens, and it is proven that Data Viewer received false data, the stake of the corresponding DH node is lost.<br>

#
در واقع همان مکانیسم اسلشینگ، نیز در اینجا صادق میباشد و اگر نودهای نگهداری داده، وظیفه خود را در حفظ داده به خوبی انجام ندهند، مبلغ وثیقه گذاشته خود را از دست خواهند داد.
#

## Service Initiation Process: The Bidding Mechanism
To get data onto the OriginTrail network, **the Data Provider sends tokens and data to a chosen DC node. The Data Creator sends tokens to the smart contract with tailored escrow functionalities and broadcasts a data holding request (Offer) with the required terms of cooperation.** All interested DH node candidates then automatically respond with their bids to the smart contract, which will include the price for the service per data unit, the stake amount and minimum time for providing the service.

The minimum factor of replication is 2N+1, where the minimum value for N is is the amount of stakeholders involved in the supply chain observation, while the actual factor may be larger. To mitigate the possibility for fixing the results of the public offering, the smart contract will close the application procedure only after a certain number of Data Holders — greater than the replication factor — answer the call. Once the application procedure is finished, the smart contract selects the required number of Data Holders based on the parameters in the DH bids. **The selection process operates on the principle of the closest data hash address, preferring DH nodes which have IDs that are ‘closer’ to the replicated data hash address, so a potential malicious Data Creator, who may own several DH nodes, can’t influence the process and pick its own nodes.**

The Data Creator will deposit the compensations in tokens for the Data Holders on an escrow smart contract that Data Holders will be able to progressively withdraw from as time passes, and up to the full amount once the period of service is successfully finished. The smart contract will take care that funds are unlocked incrementally. It is up to the Data Holder to decide how often it will withdraw the funds for the part of the service that is already delivered, as each withdrawal is a transaction on the blockchain. Ideally, the DH node will withdraw their funds at the end of successfully providing the service to minimize transaction costs.

In order **to participate in the service, the Data Holder will also have to deposit a stake in the amount proportional to the amount of the job value.** This stake is necessary as a measure of security, ensuring that data will not be deleted or tampered in any way, and that it will be provided to third parties according to the requirements. The stake is set via a “stake factor” which presents a multiplier of the bid value (i.e. a stake factor of 1 means that the staked amount is equal to the amount of tokens agreed for the service).

![](https://miro.medium.com/max/1400/0*6ws7e8gyQLH68qoS)

<br>

## Token Utility
1. Engaging in the OriginTrail Ecosystem. Data creators and data holders must have TRAC staked in their nodes to take part in the ODN. More TRAC staked in nodes means more data jobs can be published or held.

2. Publishing data to the ODN. Data creators publish data jobs on the ODN using TRAC to compensate 3+ data holding nodes for their time and resources. The exact value of TRAC for each data job is dependent on market forces, but parameters like job length and data size affect it. This TRAC is locked in a smart contract until the job’s completion.

3. Collateralization by Data Holders. To prevent data tampering and as a promise to hold data for a set period of time, TRAC from a data holder’s stake is also locked via smart contract for the length of the data job. Failure to provide data on-demand leads to loss of this staked TRAC to the data creator. Upon completion of the terms of the job, the data holder earns back their original stake and the TRAC staked by the data creator. <br>
Note that data holding node is not like a typical crypto “masternode.” They actively accept and provide data and are more akin to servers; most (all?) people run them on VPS providers due to the potential to lose TRAC staked (by failing to provide data if there is downtime). Some knowledge of a Linux environment is essential.

4. Staking TRAC. Individuals will soon be able to stake their TRAC on Version 6.0 of the ODN. Stakers will be able to get a share in the profits of the data job. This locks TRAC into the network for months and years, constricting supply. More information is coming soon.

5. Knowledge Incentivization. The final usecase for TRAC is through a data ecosystem that allows data creators to sell their data on the open market. For example, the recently announced EU-sponsored Food Safety Market aims to develop an industrial data platform for food certification in Europe by 2023. There are also Data Markets being built for both pharmaceuticals and satellite imagery; this has the potential to unlock valuable proprietary siloed data previously thought unsellable.

The OriginTrail Parachain super-charges these data marketplaces with the addition of knowledge tokens, knowledge wallets, the knowledge marketplace, and knowledge tenders. They allow individuals to buy and sell data in a trusted, private way; the developers say this will increase TRAC’s utility by orders of magnitude. Because this is tied into to the Polkadot ecosystem, all Polkadot/Kusama projects will be able to utilize this feature.

![](https://miro.medium.com/max/560/0*KKudihKKLiamQUdg) <br>
![](https://miro.medium.com/max/560/0*yqj_ThJCfFELvCSy) <br>
#
شاید جذاب ترین بخش شبکه اوریجین تریل گراف دانش غیرمتمرکز آن باشد که تا کنون حدودا هشتصد هزار دارایی مختلف در آن ثبت شده و معنادهی شده است.

گراف دانش، همان سیستمی است که گوگل و ناسا و آمازون و دیگر شرکت های بزرگ دیگر، برای طبقه بندی مفهومی داد ها از آن استفاده میکنند.

پس یعنی در وهله اول شبکه غیرمتمرکز اورجین تریل محفلی برای شرکت ها و افراد به منظور بستری من باب زنجیره تامین بوده که در با چندین بلاکچین مختلف میتواند، کار کند.
در وهله دوم، این شبکه یک گراف دانش غیرمتمرکز بوده که دارایی ها را به یکدیگر متصل کرده و معنا میدهد.

در وهله سوم، بحث پاراچین اورجین تریل و همکاری آن با پولکدات پیش میاید که سعی میکنند، با داشتن شبکه ای بلاکچین محور، تبدیل کردن دارایی ها به توکن و قرار دادن آن در شبکه و گراف اوریجین تریل را تسهیل و تسریع کند. در این باره در داکیومنتی جداگانه توضیح خواهیم داد.
#

TRAC tokenomics
The Trace token (TRAC) is used for DKG operation and incentivising protocol behavior. It is needed to perform the operations such as publishing on the network, and is a utility token that drives the entire DKG. TRAC was launched in 2018 as an ERC-20 token on the Ethereum network with a fixed supply of 500,000,000 tokens. The core utility of TRAC is:

<li> Publishing and updating assets - Asset publishers are using TRAC to compensate OriginTrail DKG node runners which ensure data replication required for discoverability of assets and verifiability of published data. The exact value of TRAC required for each data upload is dependent on market forces, but parameters like data longevity and size affect it. </li>
<li> Collateral on DKG nodes - locking TRAC by network participants running DKG network nodes acts as a collateral that increases their stake in the network, increasing the node’s chances of receiving fees for hosting a particular segment of the DKG. </li>
<li>Delegating to DKG nodes - token holders can delegate their TRAC tokens to those nodes that allow their stake to be increased by third parties. In return they are able to earn part of the rewards that the node is receiving. </li>
<li> Staking on keywords - Assets owners can lock-up their TRAC to have their assets show up higher in search results of a particular keyword (similar to how Google AdSense impacts discoverability of webpages in Google search). </li>
<li>TRAC as a fungible token - since TRAC is a fungible token created under ERC-20 standard it is transferable and usable in any way ERC-20 assets are. This includes TRAC being included in smart contracts mechanisms created on any of the networks TRAC is operating in and is bridged to (at the time of writing Ethereum, Gnosis and Polygon). One such example are data marketplace smart contracts which allow TRAC to be used as a compensation token for selling and purchasing Assets.

#

تا اینجا میبینیم که چقدر مورد کاربری برای این توکن درنظر گرفته شده که اگر تعداد دیتاجاب ها به مرور زمان زیاد شود، برای هر کاری به این توکن نیاز خواهیم داشت، در نتیجه هر کسی که به نحوی در این اکوسیستم درگیر شود، باید توکن را خریداری کند؛ همه این ها در کنار هم فشار های خریدی را روی توکن اعمال کرده ک چون تعداد توکن ها از قبل مشخص بوده و به آن ها زیاد نخواهد شد، قیمت این توکن نیز به مرور بالا خواهد رفت.
<br>
![رشد نمایی دیتاجاب های شبکه اوریجین تریل](https://miro.medium.com/max/1400/0*m3Y2lZ-3fDhLUi35)

![](https://github.com/nurafintech/whitepapers/blob/main/OriginTrail/OriginTrail%20Data%20Jobs.png)

<br>
نحوه توضیح توکن های از قبل ماین شده و آماده در سال 2019 و 2020:

![](https://miro.medium.com/max/1400/0*fAFMmAX3vKKIxxnl)

All of the TRAC available in the “soft lock” column will be used in the protocol development fund for future improvements (132.5 million total)

https://miro.medium.com/max/1400/0*gtmGSHbJxYnW5e0x

همانطور که ملاحظه میکنید به خوبی درباره توجیه اقتصادی توکن مربوطه فکر شده است و در دو سال سه سال گذشته، تعداد دیتاجاب  ها نیز به صورت نمایی رشد داشته است.

![](https://miro.medium.com/max/1400/1*U8RZPCFjuvfY2iVkhM0Yxg.jpeg)

![](https://miro.medium.com/max/1400/1*AGrwu12GUrB2wY2H_ipmXA.jpeg)

 حتی در گزارش مفصل بانک آمریکا درباره حوزه کریپتو در آگوست 2021 منتشر شد و وبسایت سی بی اینسایتس نیز این گزارش را مورد تحلیل قرار داده، اکوسیستم اوریجین تریل را جز پلتفرم هایی که در رادار این بانک بزرگ آمریکایی قرار دارد:

![](https://pbs.twimg.com/media/FA-uZ_UUYAQiK1S?format=png)

<br>

