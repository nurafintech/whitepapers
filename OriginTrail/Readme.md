# The OriginTrail Decentralized Network (ODN)
OriginTrail is a neutral, open-source protocol enabling data sharing between companies and organizations. It utilizes decentralized nodes and an off-chain technology stack to interface with legacy systems as well as other blockchains (permissioned and permissionless). OriginTrail allows businesses to improve interoperability among systems and facilitate trusted data exchange. <br/> <br/>
## The Idea's Origin
Over the years’ there have been a number of scandals involving food. There was the horse meat scandal (which was found in beef products), and then the baby milk scandal in China. There are many counterfeit wines and tobacco products on the market too. Medical supplies (one of GS1’s areas of expertise) can also potentially suffer.

ایده اولیه این پروژه برای هنگامی بود که سازندگان میخواستند روشی داشته باشند تا بتوانند محصولات با کیفیت کشاورزی یا لبنی را در شبکه ای قرار داده و خریدار با اطمینان از اصل بودن و با کیفیت بودن محصول، آن را خریداری کند. بنابراین به دنبال مکانیسمی هستیم که عده ای را تشویق کند داده ها را وارد کرده و عده ای دیگر در این شبکه، آن داده ها را طبق قول و قراری نگهداری کنند و در زمان نیاز، آن ها را تحویل دهند.
<br/> <br/>
## How does blockchain come in to play?
Firstly, utilising a blockchain ledger to store the logistics data (and any other data necessary), there is the possibility to have an un-editable, and therefor more accountable system in place. <br>
**Tamper proof RFID tags are one such solution**, enabling a consumer brand to attach a coded RFID tag to each product, box or pallet of product they put through the supply chain. If that product is then tampered with during the supply process there then should be the opportunity to understand where that likely happened. From a consumer perspective, if there is no RFID tag present on a product they were expecting to have one (such as an expensive luxury good), it will automatically raise alarm bells, hopefully cutting out a large % of counterfeit goods as they will be shunned by the consumer, or more ideally removed from the chain earlier.
<br>
There are a number of blockchain companies working with these RFID tags already, including VeChain, Waltonchain, and Wabi (I may have unintentionally missed some out). All have various key partners in place already on a global scale, and some are currently being used in real-world uses. RFID can be specific to usage requirements, so for instance they can have temperature monitoring for chilled/frozen goods, be tamper proof for products that need to remain sealed, or just be more simple like a QR code.
<br>
این پروژه ها اگر چه جذاب به نظر میرسند، اما هر کدام به دنبال پیاده سازی استاندارد های مخصوص خود بوده و در نتیجه اگر بخواهیم بخواهیم از تگ های مخصوص وی چین استفاده کنیم، دیگر به شبکه وی چین محدود خواهیم شد. خود شبکه وی چین به طور کامل غیرمتمرکز نیست.  <br>  
**!شاید باید به جای اینکه از یک بلاکچینی که به بقیه برتری دارد، باید از چند بلاکچین استفاده کنیم**
<br> <br>
اینجاست که با در نظر گرفتن چهار ویژگی بنیادی، شبکه ای ایجاد کرده که در آن بتوان از بلاکچین های مختلف نیز یاری گرفت؛ در ادامه توضیح خواهیم داد.

## Network Features
The ODN Mainnet has been operating since December 2018 with actual enterprise “data jobs” being posted by data creator nodes and stored by data holding nodes (continue reading for examples). The OriginTrail protocol and the ODN has been built from the ground up with four core features:
1. **Interoperability and Data Integrity:**
  OriginTrail has been built to take advantage of globally recognized GS1 and W3C standards. This allows for efficient alignment of data from multiple sources, including both legacy systems and newer blockchain-powered systems. This data could be anything: tracking and tracing data, Internet-of-Things (IoT) data, descriptive attributes, etc. Once data is aligned, consensus checks to verify datasets from different stakeholders can take place; additionally, auditing via compliance organizations can be authorized automatically. Due to the sensitive nature of many supply chain and business use cases, the ODN is designed to provide a “zero-knowledge” method to prove data validity.<br>
This means that their protocol can be applied to any blockchain (including private ones) to enable **GS1** conformance. It can also integrate within a supply chain company’s current ERP solution. (ERP is basically a business’s internal process management software and it will deal with things like supply chain, but also other unrelated things — it depends on the company requirements). <br>
**The logistics data would be stored on their OriginTrail Decentralised Network**, which is in turn written to blockchain ledger for safety and assurance. The logistics company may not even need to have a block-chain themselves. It makes integrating new ideas with old working methods far more easy-to-do. Asking multi-billion-dollar companies to simply change everything over-night is almost impossible so you have to make it easy.
  
2. **Data Immutability:** A tamper-proof fingerprint (cryptographic hash) of the data is generated and placed on the a blockchain when first published to the ODN; this is then used to verify that data has not been modified in any way.
3. **Stability & Cost Efficiency:** As the “heavy lifting” of interoperability and data integrity takes place off-chain, the OriginTrail graph database operates cheaply and efficiently. Its open-sourced nature enables easy deployment and does not “rip and replace” legacy systems as other blockchain-based supply chain solutions do.
4. **Network Incentivization via Token Staking:** As detailed in the section below, the TRAC token is the means of compensation between data creators, data holders, and data consumers. It uses an innovative staking system to keep all parties honest; nodes are therefore incentivized for performing consensus checks and delivering data on demand.

برای ساخت این شبکه، چهار ویژگی بنیادی اصلی را در نظر میگیریم. <br/>
اول اینکه داده ها باید استاندارد و اصولی باشند به نحوی که هم بتوانیم داده های سیستم های قدیمی را وارد شبکه کنیم و هم داده های سیستم های جدیدتر مثل داده های بلاکچین های نوظهور. تیم سازنده برای اینکار با دو سازمان جهانی تعیین استاندارد های وب، یعنی GS1 و W3C شروع به همکاری کرده و به عضویت آن ها درآمده است. در داکیومنتی مجزا در مورد استاندارد های Uniform Asset Identifier  و Uniform Asset Loacators که مخصوص وب 3 طراحی شده اند و مانند URI , UAI های وب 1 میباشند. <br/>
دوم اینکه برای ایجاد اعتماد و اطمینان از صحت داده ها، باید روشی برای درستی آن ها اتخاذ کنیم و از بلاکچین برای ثبت hash مربوط به داده ها استفاده خواهیم کرد. <br/>
سوم اینکه روش های مدرن استفاده شده در بلاکچین های جدید، نیمتوانند به خوبی با سیستم های قدیمی ارتباط و تبادل داده برقرار کنند؛ بنابراین به جای جایگزین کردن آن ها به دنبال روشی برای تعامل با آن سیستم های قدیمی خواهیم بود. سیستم های مدرن موجود بر پایه بلاکجین، حتی اگر بتوانند از داده های سیستم های قدیمی وب 1 و 2، استفاده کنند، برای تبادل و تعامل با آن ها هزینه های نسبتا زیادی را خواهد گرفت. بنابراین سعی میکنیم این هزینه ها را کاهش دهیم. <br/>
چهارم اینکه اگر میخواهیم شبکه ای decentralized داشته باشیم، باید افراد مختلف را تشویق کنیم تا به شبکه ما اضافه شوند.<br/> <br/>
این چهار ویژگی بنیادی در کنار هم هستند که اوریجین تریل را از بلاکچین های private ای مثل بلاکچین IBM و راه حل زنجیره تامین بر پایه آن یعنی TradeLens مجزا میکند.
تریدلنز پلتفرمی است که با استفاده از بلاکچین غیرمتمرکز ساخته شده توسط IBM، روش هایی برای بهینه کردن ورد و خروج و ردیابی کانتینرها در گمرک ها و خلیج ها و کشتی ها ارائه دهد که البته شاید برای افرادی خاص یا دولت چین که میخواهند اجناسی خاص را سوار بر کشتی کنند، خیلی جذاب باشد اما به آن صورت نتوانست مورد استقبال عموم قرار گیرد.
<br/><br/>

## OringinTrail Decentralized Network
At the core is a decentralized network of data providers, data creators, data holders, and data viewers:

![](https://miro.medium.com/max/1400/1*F_izA26JNTEcxJGzVVdo1w.jpeg) <br><br/>
در حال حاضر از بلاکچین های Etherum و Gnosis و Polygon استفاده شده و از NEO و IOTA استفاده نمیشود.

  Data enters the OriginTrail Decentralized Network through a Data Creator node. This data source could be from any number of business functions, including existing ERPs, blockchains (permissioned and permissionless), etc. A cryptographic data hash of the data is first fingerprinted to a blockchain to ensure data immutability. This data is then passed (via a bidding process) to 3+ Data Holder nodes that agree to hold the data for the terms of a contract. Data holder nodes are essentially decentralized, interconnected servers and provide that data upon demand to relevant parties.<br>

The data can be treated exactly how the data creator wants. Data creators can set the data to be public or private, have the data expire after a certain number of weeks/years, or have that data (or parts of data) shared only with appropriate parties. Sensitive data is protected using zero-knowledge methods in a privacy-by-design approach. These data holding nodes also function as a vast, decentralized knowledge graph to connect data sets across companies and/or supply chain partners quickly and efficiently. This core feature of the ODN is one of the major selling points for protocol adoption, as searching for inter-related data between partners has not been possible before. This writeup on the decentralized knowledge graph is highly recommended to learn more.<br>

Data holding nodes were designed to be very decentralized. They are open to anyone with 3000+ TRAC, and if the data job meets your criteria (job length, data size, etc.) then your node could be randomly assigned the job. All data holding nodes are equal; having more TRAC per node only means you can accept additional jobs compared to others.<br>
