# Transactions

To understand the types of Interactions it is important to know how transactions are structured. A transaction is one part of the entire interaction and is made up of a sequence of actions.

## Types

There are five types of transactions:

- **Read** - Get attributes and/or events from a server
- **Write** - Modify attribute values
- **Invoke** - Invoke cluster commands
- **Subscribe** - Create subscription for clients to receive periodic updates from servers automatically
- **Report** - Maintain the subscription for the Subscribe Interaction

## Initiators and Targets

Interactions happen between an initiator node and target node(s). The initiator starts the transaction, and the target responds to the initiator's action. More specifically, the transaction is usually between a client cluster on the initiator node and a server cluster on the target node.

## Transaction ID

The transaction ID field must be present in all actions to indicate the logical grouping of the actions as part of one transaction. All actions that are part of the same transaction must have the same transaction ID.

## Groups

Groups of devices allow an initiator to send an action to multiple targets. This group-level communication is known as groupcast, which leverages Ipv6 multicast messages.

## Paths

Paths are the location of the attribute, event, or command an interaction seeks to access.

Examples of path assembly:

- \<path\> = \<node\> \<endpoint\> \<cluster\> \<attribute / event / command\>
- \<path\> = \<group ID\> \<attribute / event / command\>

When group casting, a path may include the group or a wildcard operator to address several nodes simultaneously, decreasing the number of actions required and thus decreasing the response time of an interaction. Without group casting, humans may perceive latency between multiple devices reacting to an interaction. For example, when turning off a strip of lights, a path would include the group containing all the lights instead of turning off each light individually.

## Untimed and Timed Transactions

Transactions can either be untimed or timed. An untimed transaction remains open to the receiver for an indefinite period, whereas a timed transaction establishes a maximum period (usually a few seconds) to receive a return action.

Timed transactions are mainly used for devices such as doors or locks because they protect assets and thus are a greater target for intercept attacks. To understand why timed transactions are effective it is important to understand the nature of intercept attacks:

1. The initiator node sends an initial message directed to the target node.
2. An attacker intercepts the message and holds it, preventing the message from reaching the target.
3. Since the initiator did not receive a message back from the target, the initiator sends another message.
4. The attacker intercepts this second message and sends the first message to the target, keeping the second message for later use.
5. The target receives the first message as if it were arriving from the initiator node, sending a confirmation response to the initiator node and, unknowingly, the attacker.

The problem lies in the second message; since the target never received the second message, the attacker now has a valid message to use at its convenience. The message may elicit a response from the target node such as “unlock” or “open door,” which means that the network now has a breach in security. By establishing a maximum period to receive a message back, a timed transaction effectively guards against intercept attacks. The attacker can no longer hold a message to use at its convenience, as the message will expire after a set time.

Although timed transactions are important in guarding against attacks, they increase the complexity of a network since they need more actions. Therefore, they are only recommended for use on transactions that give access to valuable information.

