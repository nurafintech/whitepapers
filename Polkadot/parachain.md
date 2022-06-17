## Introduction

فرض کنیم برای ایده ای ناب و جدید به یک بلاکچین مجزا نیاز داشته باشیم. برای توسعه و پیاده سازی، باید قبل از پر و بال دادن به ایده اولیه، باید به فکر پیاده سازی بلاکچین مربوطه باشیم که در آن صورت ناچارا زمان و هزینه بسیاری را صرف پیاده سازی بلاکچین کرده و سپس به سراغ ایده اصلی میرویم.

این مشکل اصلی بسیاری از نوآوران صنعت بلاکچین میباشد. پلتفرم پلکادات دقیقا به حل این مشکل پرداخته است، به این صورت که با بلاکچین اصلی خود یعنی relay chain اجازه ساخت بلاکچین های جانبی را حول محور خود میدهد که این بلاکچین های مربوطه امنیت مورد نیاز خود را برای بلاک های جدید ساخته شده، از relay chain تامین کرده و افرادی که اجازه استفاده از این بلاکچین های جانبی را دارند، دیگر بدون نیاز به فکر کردن درباره پیاده سازی بلاکچین مربوطه، به بسط دادن ایده و پیاده سازی لاجیک و منطق خود بر روی بلاکچین های جانبی خواهند پرداخت.
<br>

#

## Sharding: scaling by subset selection

**The goal of sharding is to improve throughput by splitting work, in the form of transactions, across many chains known as shards.** The shards are referenced by and secured by a top-level blockchain. **In Polkadot the top-level blockchain is called the relay chain and the shards are parachains.** Most of the data that appears on the relay chain are transactions that include references to new parachain blocks, which makes processing any fork of the relay chain itself cheap.

This diagram or similar ones are distributed widely over the internet. They show how validators are split into groups and assigned to parachains and get parachain block proposals from collators.

![](https://polkadot.network/content/images/size/w1000/2022/01/Relay-Chain.png) <br>

Sharding is only an improvement to scalability if each validator only needs to check some of the submitted parachain blocks, as opposed to all of them. If there were 10 parachains, and each validator had to check all blocks from all 10 chains, we might as well just put all of the transactions onto one blockchain and call it a day. **The trick is to find a way for each validator to do as little verification work as possible while still maintaining economic security:** that validators who advocate for bad parachain blocks are economically disincentivized from doing so. More concretely, it should be impossible for an adversarial group of validators to collude to get a bad parachain block included in the finalized relay chain before losing all of their stake to slashing. Validators, and indeed small subsets of validators, can collude to get bad parachain blocks referenced by unfinalized forks of the relay chain, but we guarantee that these forks are ignored before finality and the offenders are slashed.

![Parachain blocks are finalized when a relay-chain block that references them is finalized](https://polkadot.network/content/images/size/w1000/2022/01/Finality.png) <br>

Let’s set down some concrete assumptions about the adversary that we defend against:
* The adversary can control up to 1/3 of all validators, and can control all of these validators to behave exactly as desired.
* The adversary can view all network messages between honest validators and the validators it controls
* The adversary can DoS up to X% of the validators at any time, preventing them from sending or receiving messages.
* It takes a fixed delay before the adversary can begin to DoS any validator

#

## Parachain consensus

The base unit of parachain consensus isn't actually a parachain, but something that we call an **availability core** or **core** for short. **These are something like CPU cores: they operate in parallel, and have work scheduled onto them in discrete time-slots.** Each parachain has its own dedicated core, which means that it's always scheduled onto a particular core. However, we can also multiplex multiple chains onto a single core. The only difference is the scheduling algorithm.

Cores serve as an effective description of the throughput of the relay chain. Cores directly correspond to the amount of work validators need to do. Each core can handle up to one parachain block per each relay-chain block, at peak.

In any sharded blockchain system, where only some validators check each parachain block, data availability is a crucial component to make sure that the data necessary to check a parachain block can be recovered for the purposes of fraud detection. <br>
Availability cores are managed by the relay chain and track which parachain blocks are pending data availability. **The main purpose of availability cores is as a scheduling primitive and to provide backpressure when data availability is slower than usual.**

The logic of an availability core looks like this. Cores are empty when they're ready to accept a new parachain block, at which point they become occupied. Then, the data either becomes available or the availability process times out. At that point, the core becomes empty again.

![](https://polkadot.network/content/images/size/w1000/2022/01/Availability-Core-Logic.png)

It's helpful to divide parachain consensus up into 5 distinct protocols that are intertwined in relay-chain consensus:
1. Collation is the process by which parachain blocks are created. Collators build a parachain block and send it to validators.