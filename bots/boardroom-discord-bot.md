# Boardroom Discord Bot

\*\*\*\*[**See the Bot Repo here**](https://github.com/boardroom-inc/boardroom-discord-bot)\*\*\*\*

A bot to interact with Boardroom's API and subscribe to new events.

There are two sets of commands: Commands to get general information and commands for subscriptions.

Subscriptions are run through every 30 seconds, but the checks are only done based on the `frequency` argument. By default, this is every 15 minutes.

## Set up

This bot uses AWS DynamoDB to store the subscriptions, so the `aws-cli` must be set up in the machine running it, with a table called `subscriptions` and a primary key called `id`. You can see a CDK example [here](https://github.com/Zerquix18/boardroom-bot-cdk/blob/master/lib/boardroom-stack-stack.ts#L28).

The name of the table can be changed from the Dynamo service on this project.

The `.env.example` can be used to create an `.env` file which the token which is created on the [Discord Developer Portal](https://discord.com/developers/applications).

Once there's an `.env` file, run the commands:

* `npm install`
* `npm run tsc`
* `node bot.js`

## Commands

### ./protocol\_list

Lists all protocols supported by Boardroom.

### ./protocol\_proposals

Lists all proposals in a protocol

Options:

* `cname` \(required\) - Code name for the protocol must be \[a-z0-9\] \(e.g "uniswap"\)

### ./protocol\_voters

Lists all voters in a protocol

Options:

* `cname` \(required\) - Code name for the protocol must be \[a-z0-9\] \(e.g "uniswap"\)

### ./proposal\_votes

Lists all voters in a protocol

Options:

* `refid` \(required\) - Unique code representing proposal \(ends with =\)

### ./protocol\_get

Retrieves information about a specific protocol.

Options:

* `cname` \(required\) - Code name for the protocol must be \[a-z0-9\] \(e.g "uniswap"\)

### ./proposal\_get

Retrieves information about a specific proposal.

Options:

* `refid` \(required\) - Unique code representing proposal \(ends with =\)

### ./voters\_votes

Retrieves the votes of a specific address.

Options:

* `address` \(required\) - Address of the voter

### ./voters\_get

Retrieves information about a voter.

Options:

* `address` \(required\) - Address of the voter

### ./stats

Prints Boardroom's global statistics.

### ./subscribe\_to\_protocols

Be notified any time a new protocol is added.

Options:

* `frequency` - How often to check \(in hours\). Default is 15 minutes \(0.25\)

### ./subscribe\_to\_protocol\_proposals

Be notified any time a new proposal is added.

Options:

* `cname` \(required\) - Code name for the protocol must be \[a-z0-9\] \(e.g "uniswap"\)
* `frequency` - How often to check \(in hours\). Default is 15 minutes \(0.25\)

### ./subscribe\_to\_proposal\_state

Be notified any time the state of a proposal changes.

Options:

* `refid` \(required\) - Unique code representing proposal \(ends with =\)
* `frequency` - How often to check \(in hours\). Default is 15 minutes \(0.25\)

### ./subscribe\_to\_proposal\_votes

Be notified any time a proposal has a new vote.

Options:

* `refid` \(required\) - Unique code representing proposal \(ends with =\)
* `frequency` - How often to check \(in hours\). Default is 15 minutes \(0.25\)

### ./subscribe\_to\_voter\_votes

Be notified any time an address votes.

Options:

* `address` \(required\) - Address of the voter
* `frequency` - How often to check \(in hours\). Default is 15 minutes \(0.25\)

### ./subscribe\_to\_stats

Display global statistics from time to time.

Options:

* `frequency` - How often to check \(in hours\). Default is 15 minutes \(0.25\)

### ./show\_all\_subscriptions

Lists all active subscriptions, including their number which allows to delete them.

### ./delete\_subscription

Delete a subscription

* `id` - Subscription unique identifir \(uuid\) which you can get from `/show_all_subscriptions`.

### ./delete\_all\_subscriptions

Delete all subscriptions.

