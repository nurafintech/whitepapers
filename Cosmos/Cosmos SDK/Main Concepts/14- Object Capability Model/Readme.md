# Object Capability Model

## Access control is mostly widely achieved via access control lists (ACLs)
 **Metadata** or **database tables** that **specify** which **user is allowed to perform which actions**. This requires that the application boundary enclose all of the data and users.
 
  In **fully centralized systems**, this works reasonably well since all requests go through **the same controlling source**. However, as real world use cases inevitably expand, ACLs need to cover increasing **complexity**, **exceptions**, and **roles**. It often becomes error prone to write and maintain, and makes the ACL subsystem itself a target for attackers.

The object capability (OCAP) model works in the opposite mode. While ACLs are **reactive & centralized,** OCAP is **proactive & decentralized** — **an agent is allowed to perform some action if they have poof of those rights**.

 This makes access control very granular, work offline, and in certain variants (like ours) empowers users to delegate rights to others to act on their behalf.
This greatly simplifies access control by presenting a document that includes what the user is permitted to do.

The complexity arises from managing which credentials exist, and revoking them. The standard approch is to maintain a public revocation list, which is checked on each request. We will go into that in more depth later.

# Comparison to Access Control Lists (ACLs) In Designing Athorization Mechanisms

* ACLs / Reactive Auth

    The access control mechanism that is most widespread today is ACL. This works by keeping a list of users and what they're allowed to who (which resources and what they're able to do with them). This requires maintaining a complex mapping in a central location, plus a process that mediates the interaction.

    This is a bit like having a guard outside of a building. You ask them to perform actions on your behalf. The stop you, check your ID, look up if you're allowed to do that, and pass the message along if so. If you break into the back of the building (sneak past the guard), you have full access.

    **The advantage of this reactive model is that it's very easy to remove capabilties from the central list. The disadvantage is that the list tends towards having very complex rules over time, and it doesn't scale well or work offline.**

    ![](https://2299956098-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-LofgqakffpAtg_wUAUS%2F-MiOhYm7-e4Jni_PEutI%2F-MiOi3yNv2wdQm9ARuwD%2FScreen%20Shot%202021-08-30%20at%2017.59.34.png?alt=media&token=c1cc9f08-8230-4b9c-9a4a-ec8df1e2ff2f)


* OCAP / Proactive Auth

    OCAP is less known today, but has good real-world analogies.
    
    For instance, a movie ticket asserts that you are allowed to watch a film at a certain location at a certain time. It doesn't depend on your passport or a list somewhere. If you're holding that ticket you're allowed in.

    This scales very well and works offline, because it requires no central list. Having ticket is the complete proof. This model doesn't require writing complex rules or maintaining state. It is said to be "proactive".

    The downside is that revocation is more challenging. OCAP tends to use the principle of least authority to scope what the grantee's capabilities to what is safe at the time it's issued. This can commonly include access to a narrow set of resources, an expiration time, and so on.

    ![](https://2299956098-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-LofgqakffpAtg_wUAUS%2F-MiOhYm7-e4Jni_PEutI%2F-MiOi6wDvbSAf-gbjwJ0%2FScreen%20Shot%202021-08-30%20at%2017.59.38.png?alt=media&token=5297cf14-474e-49c6-8803-74305323e450)

* Balance

    Since they both have tradeoffs, it's rare to see a pure ACL or pure OCAP system. Typically they borrow some techniques from each other. For instance, an ACL-driven backend may issue stateless JWTs, or OCAP systems may maintain a (central or replicated) revocation list.

# Object-capability model in Data Flow

Before we start to explain Ocaps, we need to be familiar with these terms:
## Glossary of related terms
* **object-capability system**:

    A computational system that implements principles described in this article.
* **object**:

    **An object has local state and behavior.** An object in this sense is both a subject and an object in the sense used in the access control literature.
* **reference**:

   **An unforgeable communications channel (protected pointer, opaque address)** that unambiguously designates a single object, and provides permission to **send messages** to that object.
* **message**:

   **What is sent on a reference.** Depending on the system, messages may or may not themselves be first-class objects.
* **request**:

    An operation in which a message is sent on a reference. When the message is received, the receiver will have access to any references included in the message.
* **attenuation**:

    A common design pattern in object-capability systems: given one reference of an object, create another reference for a **proxy object** with certain security restrictions, such as only permitting read-only access or allowing revocation. T**he proxy object performs security checks on messages that it receives and passes on any that are allowed.**
    
    **Deep attenuation** refers to the case where the same attenuation is applied transitively to any objects obtained via the original attenuated object, typically by use of a **"membrane".**

<br>
The object-capability model is a computer security model. A capability describes a transferable right to perform one (or more) operations on a given object. It can be obtained by the following combination:

* **An unforgeable reference (in the sense of object references or protected pointers) that can be sent in messages.**
* **A message that specifies the operation to be performed.**

The security model relies on not being able to forge references.

* Objects can interact only by sending messages on references.
* A reference can be obtained by:
    1. **Initial conditions: In the initial state of the computational world being described, object A may already have a reference to object B.**
    2. **Parenthood: If A creates B, at that moment A obtains the only reference to the newly created B.**
    3. **Endowment: If A creates B, B is born with that subset of A's references with which A chose to endow it.**
    4. **Introduction: If A has references to both B and C, A can send to B a message containing a reference to C. B can retain that reference for subsequent use.**

Languages such Java, C#, JavaScript violate these conditions of the conditions of the object-capability model.

Note, however, that some uses of the term "capability" are not consistent with the model, such as POSIX "capabilities".


# Advantages of object capabilities in Data Flow

Computer scientist E. Dean Tribble stated that **in smart contracts, identity-based access control did not support well dynamically changing permissions, compared to the object-capability model.** He analogized the ocap model with giving a valet the key to one's car, without handing over the right to car ownership.

**The structural properties of object capability systems favor modularity in code design and ensure reliable encapsulation in code implementation.**

These structural properties **facilitate** the analysis of **some security properties** of an object-capability **program** or operating system. Some of these – in particular, **information flow properties** – can be analyzed at the **level of object references and connectivity**, **independent of any knowledge** or analysis of the code that **determines the behavior of the objects**. As a consequence, these security properties can be established and maintained in the presence of new objects that contain unknown and possibly malicious code.

These structural properties stem from the two rules governing access to existing objects:

1) **An object A can send a message to B only if object A holds a reference to B.**
2) **An object A can obtain a reference to C only if object A receives a message containing a reference to C.**

As a consequence of these two rules, **an object can obtain a reference to another object only through a preexisting chain of references.** In short, "Only connectivity begets connectivity."


# Object-Capability Model in Cosmos SDK

When thinking about security, it is good to start with a specific threat model. Our threat model is the following:

We assume that a thriving ecosystem of Cosmos SDK modules that are easy to compose into a blockchain application will contain faulty or malicious modules.

For example, the following code snippet violates the object capabilities principle:

<code>
type AppAccount struct {...}

account := &AppAccount{

    Address: pub.Address(),

    Coins: sdk.Coins{sdk.NewInt64Coin("ATM", 100)},

}

sumValue := externalModule.ComputeSumValue(account)</code>

The method ComputeSumValue implies a pure function, yet the implied capability of accepting a pointer value is the capability to modify that value. The preferred method signature should take a copy instead.

`sumValue := externalModule.ComputeSumValue(*account)`


Or another example:

<code>
app.AccountKeeper = authkeeper.NewAccountKeeper(

	appCodec, keys[authtypes.StoreKey], app.GetSubspace(authtypes.ModuleName), authtypes.ProtoBaseAccount, maccPerms, sdk.Bech32MainPrefix,
)

app.BankKeeper = bankkeeper.NewBaseKeeper(

	appCodec, keys[banktypes.StoreKey], app.AccountKeeper, app.GetSubspace(banktypes.ModuleName), app.ModuleAccountAddrs(),
)

stakingKeeper := stakingkeeper.NewKeeper(

	appCodec, keys[stakingtypes.StoreKey], app.AccountKeeper, app.BankKeeper, app.GetSubspace(stakingtypes.ModuleName),
)

app.MintKeeper = mintkeeper.NewKeeper(

	appCodec, keys[minttypes.StoreKey], app.GetSubspace(minttypes.ModuleName), &stakingKeeper,
	app.AccountKeeper, app.BankKeeper, authtypes.FeeCollectorName,
)

app.DistrKeeper = distrkeeper.NewKeeper(

	appCodec, keys[distrtypes.StoreKey], app.GetSubspace(distrtypes.ModuleName), app.AccountKeeper, app.BankKeeper,
	&stakingKeeper, authtypes.FeeCollectorName,
)

app.SlashingKeeper = slashingkeeper.NewKeeper(

	appCodec, keys[slashingtypes.StoreKey], &stakingKeeper, app.GetSubspace(slashingtypes.ModuleName),
)

app.CrisisKeeper = crisiskeeper.NewKeeper(
	app.GetSubspace(crisistypes.ModuleName), invCheckPeriod, app.BankKeeper, authtypes.FeeCollectorName,
)

app.FeeGrantKeeper = feegrantkeeper.NewKeeper(appCodec, keys[feegrant.StoreKey], app.AccountKeeper)

</code>

![](https://raw.githubusercontent.com/cosmos/cosmos-sdk/release/v0.46.x/docs/uml/svg/keeper_dependencies.svg)

## References
* https://whitepaper.fission.codes/access-control/cap-authz
* https://en.wikipedia.org/wiki/Object-capability_model#Advantages_of_object_capabilities
* https://github.com/cosmos/cosmos-sdk/blob/v0.46.0/simapp/app.go#L258-L283