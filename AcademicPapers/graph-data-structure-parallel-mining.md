### Improve Blockchain Performance
using Graph Data Structure and Parallel Mining

#

## I. Introduction
Blockchain is the backend of decentralized digital currencies. The field has gradually broadened, several limitations and
disadvantages of the original design are showing up, one
of the problems concerning the scalability of capacity and
performance.
 For a high performance blockchain
protocol which can increase the fundamental performance,
data structure change is required. The chain data structure
and Proof of Work algorithm are designed like a singleuser operation system, only one user is allowed to touch the blockchain data. <br>

This paper details the new protocol of a blockchain system.
The key contribution of this work is the solution which
provides a method to build a blockchain with practical performance. The new data structure plays the flexible role of
framework and the new mining mechanism increases the
overall performance. The outcome could be use scenario, such
as a micro transactions system, blockchain with big data or a
new generation banking system.<br>
در واقع هدف پیاده سازی نوعی ساختمان داده ای است به شکل یک گراف تا بتوان با استفاده از آن به صورت پارالل، بلاک های جدید را ایجاد کرد.

#

## II. Model and Goal
It is well established that a blockchain system is consisted
with N full nodes. Full node comes with the whole history
transactions information, and the nodes are connected with
reliable peer-to-peer network. Meanwhile there are M miners
waiting for transaction requests and being ready to pack the
transaction data into blockchain. <br>
In the classic blockchain, the whole Miners are competing to
solve a mathematics puzzle by iterating a number called nonce.
The puzzle has a target with certain difficulty. When the puzzle
is solved, a new block will be created. The recent transactions
are packed into the new block. As will be described below,
several problems has been discovered on this model:
1. Most of the power energy for calculation is wasted, as
too much competition results in only one winner. Allowing
one winner only means this miner acts like a central lock to
limit the blockchains performance.<br>
کلی قدرت محاسباتی صرف شده تا فقط یک ماینر که پازل محسباتی را حل کرده، تراکنش ها را در بلاک خود بسازد که همین باعث کند شدن پروسه تولید بلاک های جدید و سرعت پردازش تراکنش ها میشود.
2. The transactions need to wait for the next new block
generation to be confirmed. It means transactions can not be
finished in real time.
تراکنش ها باید تا ساخته شدن بلاک بعدی، منتظر مانده و پردازش شوند.

برای بهتر شدن عملکرد بلاکچین، میتوان زمان ساخته شدن بلاک ها را کاهش یا اندازه هر بلاک را افزایش داد اما با بالا رفتن کاربران سیستم، این روش ها کارساز نخواند بود.
<br>
برای بهتر شدن عملکرد، ابتدا ساختمان داده زیجیره بلاک ها را به یک زنجیره گراف تغییر میدهیم که در ادامه آن را توضیح میدهیم.
<br>
دوم به جای یک ماینر از چند ماینر به صورت، پارالل استفاده میکنیم.
<br>
سوم اینکه از بحث data sharding استفاده میکنیم تا تا بتوانیم بجای اینکه همه تراکنش ها را تنها در یک بلاک قرار دهیم و کپی آن در تمامی نود ها قرار گیرد، سعی میکنیم تمامی تراکنش ها را به چندین قسم تقسیم کرده و آن قسم ها را در نود های مختلف قرار دهیم.
<br>

#

### III. CHAIN AND GRAPH
As is well-known the chain data structure has been widely
used in Bitcoin and other products. Directed acyclic
graph(DAG) was used in IoTA.
The GraphChain data structure idea was inspired from DAG.
The main reason to change the data structure is to find a way
to replace sequential operations with parallel operations. The
data structure GraphChain is showed in Fig 1. GraphChain
is a customized data structure, it’s not a typicial DAG. The
block usually has two inputs and two outputs, and the block
represents the accounts’ status after transaction. Another important point is that the inputs have the direction. If it’s a sending account, it should connect to the input point above.
Hence, the receiving account should be connected with the input point below.
Unlike chains, GraphChain don’t need to pack the transactions into a single thread. With GraphChain transactions can be added in parallel by different miners. <br>
#
اگر چه این روش از ایده DAG استفاده میکند، اما خود ساختمان داده مربوطه یک DAG نیست.
<br>

![Fig 1](https://raw.githubusercontent.com/nurafintech/whitepapers/main/AcademicPapers/the-graph-chain-data-structure.png)
<br>

#

### IV. PARALLEL MINING

In parallel mining by solving the puzzle, miners
have become the leader. The leader is on duty for the next
period of time.
Unlike the traditional blockchain for example Bitcoin,
the new mechanism requires the miner, who won the election,
to stay online for its duty time.
<br>
استفاده همزمان از چندین ماینر منتخب که همان لیدر ها هستند، باعث میشود تا اگر برای هر کدام از آن ها اتفاقاتی نظیر قطعی اینترنت و برق رخ داد، ساخت بلاک های جدید با مشکل مواجه نشود:

A. Miner to Leader
On the basis of parallel mining, when a miner is elected as a leader, the leader serves his duty for a certain time. In a sliding time window, m (number of) miners are elected to leaders. According to Bitcoin [1] system, the researchers set the election interval time to 10 minutes and the service time to 1 hour. It results that 6 leaders are online in a sliding time window. The leaders listen to the peer-to-peer network and wait for new transaction requests while they are on duty. Once the new transaction is broadcasting, leaders pack it into GraphChain. As the delay of communication between leaders, there are chances that same transaction is packed into the GraphChain multiple times by different leaders. Only m (number of) leaders are working in parallel, resulting in maximum of m (number of) forks of the GraphChain.
#
فرض میکنیم که یک شبکه peer-to-peer شبیه به شبکه بیت کوین داریم. تمامی ماینر ها شروع به حل پازل محاسباتی بر پایه PoW کرده و هر 10 دقیقه، 6 تا از آن هایی که سریع تر از بقیه پازل را حل کرده باشند، به عنوان لیدر انتخاب میشوند.
این شش لیدر باید در یک ساعت بعدی، به سرویس دهی و پردازش تراکنش ها و ساخت بلاک های جدید بپردازند.
#
B. Accounts
An account usually starts with zero balance. Account balance changes because of transactions. At least two accounts are involved within a transaction. The account block is a nontransaction block, usually only having one output(Fig 1). The transaction block represents two account’s balance status.
#

پس ما دو نوع بلاک در شبکه در نظر میگیریم، یکی همان اکانت ها که در واقع hash های مربوط به ولت افراد میباشد.
یکی هم برای حساب کتاب موجودی آن ها.
#
C. Issue and Revoke Assets
The block issuing or revoking assets requires special signature from certain private key, or more than one keys. Any non-transaction block with assets above zero should be verified
carefully in the mechanism design.

D. Transactions
Any transaction should happen between at least two accounts. The senders balance must be above zero. As shown in Fig 1, each transaction block usually has two inputs and two outputs. A transaction block stands for two accounts current balances, one of them being a sender account and the other a receiver account.
#

در واقع شبیه به همان مدل UTXO استفاده شده در بیت کوین میباشد.
#

E. Scalability
The scalability of Bitcoin [1] and related system is limited. The reasons include block size, the overall data amount, the block propagation speed and miner’s capacity. In Bitcoin [1]’s design, one miner is selected to pack the transactions from the past 10 minutes. The rule acts like a central lock, preventing other miners from contribution.
#
بجای اینکه از یک ماینر استفاده بکنیم، از چندین ماینر ( لیدر ) به صورت پارالل استفاده خواهیم کرد.
#
F. Election for the Leaders
In Bitcoin, miner who finds the new block has the privilege to pack the transactions from the past 10 minutes into that new block. In GraphChain system, leaders are elected to pack the transactions for the certain time.
#
در بیت کوین، وقتی یک ماینر وقتی که کار خود را به پایان رساند، پاداش خود را دریافت کرده و میتواند از شبکه خارج شود.
در گراف چین، بر روی لیدر ها و کار پردازش تراکنش ها آن به میزان مدت زمان خاصی، حساب باز میکنیم، بنابراین باید تعداد آن ها به میزانی باشد، که اگر اتفاق بدی برای یکی یا چندی از آن ها رخ داد، کار ساخت بلاک های جدید با مشکل نشود. لذا حداقل دو لیدر برای یا بیشتر را برای ساخت بلاک ها انتخاب خواهیم کرد.
لیدر ها با یکدیگر به رقابت پرداخته و تعداد آن ها بر حسب نیاز سیستم انتخاب خواهد شد.
#
The leader is elected in the similar way that Bitcoin miner finds the new block. The method is PoW based. A miner who wants to be an leader, the world wide competition is required. The difference is that Bitcoin rewards the new block to the winner miner, GraphChain grants the qualify to the winner miner. The miner became a leader will work with other leaders for a while to pack the user transactions into GraphChain.
#
پس تا اینجا با روش PoW  ماینر ها رقابت کرده و تعدادی از حل کنندگان اولیه پازل محاسباتی، به عنوان لیدر انتخاب خواهند شد.
#
In parallel mining scenario, limited number of leaders try to solve much simpler puzzle. If a leader retries certain times and still can not find the result meeting the target, this leader will give up. Because the puzzle is simple enough, it’s assumed that at least one leader should be able to get the puzzle answer and create the next transaction block. The result is that several blocks may be created by different leaders for one transaction. The block whose creator spends less retries will be the lucky new block. The simple modification of PoW algorithm is called Proof of Luck(PoL).
#
یک نسخه سبک و قابل حل تر PoW را برای رقابت میان لیدرها در نظر میگیریم.
لیدر در طی بازه زمانی که در اختیار دارند، با حل پازل های محاسباتی آسان این Lite PoW، به ساخت و بلاک های جدید و پردازش تراکنش هایی که هنوز unpacked میباشند، میپردازند.
در چنین مدلی، ممکن است یک تراکنش، توسط چندین لیدر پردازش شده و در بلاک ساخته شده توسط هر لیدر قرار گیرد. در اینصورت تنها بلاکی توسط سیستم انتخاب میشود که لیدر آن با تعداد تلاش کمتری، پازل محاسباتی را حل کرده و بلاک مربوطه را ساخته باشد.
به این بلاک، lucky new blcok گفته و به کل این پروسه، Proof of Luck میگوییم.
در این مدل، انخاب تراکنش های unpacked، توسط ماینر ها کاملا تصادفی بوده که برای بالارفتن عملکرد شبکه، میتوانیم برای تراکنش های قدیمی تر، اولویت دهیم تا زودتر توسط لیدرها پردازش شوند.
#

### V. DATA SHARDING

The chain data structure is hard to be ’sharded’ because the blockchain can not be split by account.
The existing solution suggests keeping the certain period of times blockchain by snapshot. The accounts balance list also need to keep stand-alone. Dropping part of the blockchain data will cause the difficulty in data verification.
#
در سیستم حسابداری یو تی اکس او ی بیت کوین این کار خیلی سخت و در سیستم بر پایه اکانت اتریوم این امر نشدنی میباشد.
#
Also, the term ’sharding’ here is different from Ethereum's sharding’. thereum’s sharding is to increase the capacity with a twolayer design. In GraphChain, the sharding can be done by
splitting data by user.
#
یعنی شاردینگ داده ای که برای گراف چین در نظر میگیریم با شاردینگ لایه ای اتریوم متفاوت میباشد.
در گراف چین، میخواهیم با تقسیم کردن و شکاندن تمامی تراکنش ها که در هر بلاک باید ثبت شوند، به چندین قسم و ذخیره آن قسم ها در نود هایی که کارشان نگهداری از این داده هاست، حجم بلاک ها را کاهش داده و به بتوانیم تراکنش هایی که مستقل از یکدیگرند و هیچ ربطی به هم ندارند، به طور مجزا در گراف مد نظر ذخیره و پردازش کنیم.
#

As the high TPS’s requirement for the production environment, the overall size of data will be increased very fast.
Assume there are 2000 TPS, about 24G data will be generated
per day. Less PC will meet the condition to act as the full clone node.
Data shard on GraphChain divides the data by accounts. In general a user account internally is represented as hash. A node can be simply designed to keep all the transaction information related the accounts whose hash starts with ’a’ or ’b’. By this configuration, the huge data can be kept separately by many nodes with redundancy.
#
هش های کاربران را دسته بندی کرده ( مثلا بر اولین حروفی که با آن ها شروع میشوند) و در هنگام پردازش تراکنش ها، در این نود درستی و صحت میزان موجودی و تراکنش های قبلی هر هش را بررسی میکنیم.
با استفاده cache کردن نیز میتوانی به این امر سرعت بخشیم.
#
If network delay, a leader may try to pack a transaction which is already done by other leaders. According to the longest chain rule, in the case of two chains with same length, PoL algorithm is used to decide which fork to go.

It’s also found that the overall performance would be goingdown while more transactions are appended into GraphChain. The reason is when the chain length increases, the databaseneed to lookup the chain to verify if the transaction exists already in the blocks. This issue is solved by adding cache. After applying this technique we can observe quite average performance in Fig 2.

![Fig 2](https://raw.githubusercontent.com/nurafintech/whitepapers/main/AcademicPapers/the-graph-chain-data-structure-performance.png)

#

### Use Cases:
There are several directions that GraphChain and parallel
mining could be applied for:
1. Micro transactions. Now Bitcoin and Ethereum are valued
at high price, even a small transaction fee will be expensive
if converted to a legal currency. GraphChain allowing multi
miners could be useful in the decentralized currency system
which supports the micro transactions, as in GraphChain’s
design each block contain only one transaction. No block
waiting time is required to confirm the transaction if enough
miners are available.
2. Blockchain for data. Now privacy problems are a big
issue, personal data have already become giant companies’
private assets. In future there will be blockchain for certain
field, for example the health data. If huge amount of data
is insert into blockchain, it will be expensive to store it.
GraphChain split the data unit into the smallest transaction
level and the data are linked across different nodes. As a result,
shard data are possible through this data structure.
3. Blockchain for banking. The banking is looking for
digital currency solution. Existing blockchain can not meet
the demand due to the performance and scalability issues.
In this situation, new technologies will change the industry
completely. The traditional banking system accepts deposits
and loans to enterprises. To get deposit safely, huge costs
were invested in IT systems as the election version of pen
and paper. Regulation policies have been made, but they still
need humans to follow it. Blockchain is a gorgeous invention,
because that regulation part is no longer required for humans.
The costs in regulation can be unbelievably low. A scalable
and high performance blockchain will play an important role
in the banking industry.


#

### نقد و بررسی

اول اینکه، در این سیستم در مورد نود هایی که باید داده های Shard شده را در خود نگهداری کنند، بحثی نشده است. پیاده سازی این نودها به صورتی که توجیه اقتصادی داشته باشد، خود نیازمند روش هایی از قبیل توکنایز کرده پروسه مربوط به این کار میباشد و این کار یک چالش بسیار بزرگ میباشد. <br>
دوم اینکه در این روش در مورد نحوه پیاده سازی قرارداد های هوشمند و بحث state handling  اکانت ها در هر بلاک صحبتی نشده بود. برای بیت کوین راه حل های لایه دومی میتوان در نظر گرفت. برای شبکه گراف مانند، چالش پیش رو احتمالا بسیار پیچیده تر خواهد بود. <br>
سوم اینکه اگر تنها یک کوین را در نظر بگیریم این روش بسیار کارا باشد، با توجه به اینکه امکان مقیاس پذیری غیرخطی را در نمودار مربوطه مشاهده کردیم. <br>

**چهارم اینکه در مورد نسخه آسان تر PoW که همان زیر بنای Proof of Luck میباشد، صحبت شد. اگر به صورت سیستماتیک تعداد زیادی ماینر با قدرت پردازشی بالا به شبکه اضافه شده و تعدادی از آن ها به صورت همزمان به عنوان لیدر انتخاب شوند، میتوانند بلاک ها به طور دلخواه دستکاری کنند، و شبه حمله ای شبیه به حمله 51 درصد امکان پذیر خواهد بود.
 پروژه IOTA نیز با مشکل حمله 40 درصد مواجه است. بنابراین در مورد امنیت این ساختار داده صحبت نشده است!**


در مورد اول، پروژه هلیوم و اوریجین تریل، روش هایی برای نود هایی که قرار است داده ها در خود ذخیره کنند، ارائه شده است.

#

## References

https://arxiv.org/pdf/1808.10810.pdf
