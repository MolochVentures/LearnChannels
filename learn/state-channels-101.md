# State Channels 101

**How do state channels work?**

Three steps:

1. Two users lock the initial blockchain state \(e.g., each party's balance\) into a smart contract closely resembling a multisignature wallet. This ensures that the funds in the wallet can't be used elsewhere or removed until unlocked with an update that both parties have signed.
2. The two parties transact by passing state updates \(e.g., balance updates\) amongst themselves. If both parties agree on a state update, it _could_ be submitted to the smart contract at any time to unlock funds. 
3. When parties have finished transacting, they each submit state updates to the smart contract. If the state updates match, the blockchain state \(e.g., each party's balance\) is unlocked, typically in a different configuration than the initial state.

**Alright, that makes sense. But what if they disagree?**

Each state update that is signed by both parties is assigned a "nonce", or a number that uniquely identifies that update. More recent nonces trump older nonces.

As soon as Party A \(let's call her Alice\) submits a state update, a challenge period starts. During this period, Party B \(let's call him Bob\) has the opportunity to submit an update with a more recent nonce. When the challenge timer expires, the update with the most recent nonce is used to unlock the blockchain state and distribute funds appropriately.

**What happens if Bob isn't online or forgets to submit a state update?**

If the challenge period expires and Bob hasn't submitted a more recent state update than Alice, funds are disbursed according to the most recent double-signed state update \(in this case, the one submitted by Alice\). In this case, Bob isn't actually cheated out of any money--he misses out on the more recent state update \(which is likely beneficial to him\). Everyone gets paid the amount that they most recently agreed upon.

Obviously, that's a situation most people would like to avoid, especially since a party who intentionally submits an old state probably lost money in a later state update. There are a few potential solutions to this; one is the challenge timer itself, which at the very least allows Bob some time to submit his state update. Another is a third-party "watchtower" system, which would automatically monitor the channel and \(for a small fee\) submit the most recent update for Bob even if he's offline.

**This works great for simple payments, sure. But what about conditional payments or more complex state operations?**

Great question. See [the next section](payment-channels-vs.-state-channels.md)!

