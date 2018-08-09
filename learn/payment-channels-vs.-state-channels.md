# Payment Channels vs. State Channels

There are a variety of different [state channel-based projects](../projects.md) out there; you'll notice that some focus on payment channels and some focus on state channels. So what's the difference?

**Payment channels are a subset of state channels**

Payment channels are the simplest kind of state channel: they allow a user \(the sender\) to transfer money to another user \(the recipient\).

**Payment channels require radically simpler dispute resolution than state channels**

Recall that state channels use the blockchain as the ultimate arbiter. This means that there are a few types of disagreements \("dispute cases"\) that channels must account for. For example, if Bob and Alice are sending money back and forth and Bob tries to send a fake balance update, Alice can submit the last double-signed update to the channel contract. At that point, Bob will have the option to submit a more recent double-signed update; if he cannot, the contract will disburse funds in accordance with the update that Alice submitted.

Payment channels only need to account for a few simple dispute cases, and resolution comes down to who has the more recent double-signed state update. When you're dealing with a peer-to-peer transaction, there's really only one thing to disagree about: who should have how much money. To play a game of chess using a state channel, however, the participants need to agree on the rules of chess and the state channel needs to account for all the possible ways that two players can disagree. Just as participants in a payment channel behave as though their transactions are happening on-chain, participants in a state channel behave as though all their interactions are happening on-chain.

This happens through a process known as counterfactual instantiation, which we will discuss in the next section.

