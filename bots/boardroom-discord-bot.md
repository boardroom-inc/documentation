# Boardroom Discord Bot

[See the Bot Repo here](https://github.com/Zerquix18/boardroom-discord-bot)

A bot to interact with Boardroom's API and subscribe to new events.

There are two sets of commands: Commands to get general information and commands for subscriptions.

Subscriptions are run through every 30 seconds, but the checks are only done based on the `frequency` argument. By default this is every 15 minutes.

## Set up

This bot uses AWS DynamoDB to store the subscriptions, so the `aws-cli` must be set up in the machine running it, with a table called `subscriptions` and a primary key called `id`. You can see a CDK example [here](https://github.com/Zerquix18/boardroom-bot-cdk/blob/master/lib/boardroom-stack-stack.ts#L28).

The name of the table can be changed from the Dynamo service on this project.

The `.env.example` can be used to create an `.env` file which the token which is created on the [Discord Developer Portal](https://discord.com/developers/applications).

Once there's an `.env` file, run the commands:
- `npm install`
- `npm run tsc`
- `node bot.js`

## Commands

#### ./protocol_list
Lists all protocols supported by Boardroom.

#### ./protocol_proposals
Lists all proposals in a protocol

Options:
* `cname` (required) - Code name for the protocol must be [a-z0-9] (e.g "uniswap")

#### ./protocol_voters
Lists all voters in a protocol

Options:
* `cname` (required) - Code name for the protocol must be [a-z0-9] (e.g "uniswap")

#### ./proposal_votes
Lists all voters in a protocol

Options:
* `refid` (required) - Unique code representing proposal (ends with =)

#### ./protocol_get
Retrieves information about a specific protocol.

Options:
* `cname` (required) - Code name for the protocol must be [a-z0-9] (e.g "uniswap")

#### ./proposal_get
Retrieves information about a specific proposal.

Options:
* `refid` (required) - Unique code representing proposal (ends with =)

#### ./voters_votes
Retrieves the votes of a specific address.

Options:
* `address` (required) - Address of the voter

#### ./voters_get
Retrieves information about a voter.

Options:
* `address` (required) - Address of the voter

#### ./stats
Prints Boardroom's global statistics.

#### ./subscribe_to_protocols
Be notified any time a new protocol is added.

Options:
* `frequency` - How often to check (in hours). Default is 15 minutes (0.25)

#### ./subscribe_to_protocol_proposals
Be notified any time a new proposal is added.

Options:
* `cname` (required) - Code name for the protocol must be [a-z0-9] (e.g "uniswap")
* `frequency` - How often to check (in hours). Default is 15 minutes (0.25)

#### ./subscribe_to_proposal_state
Be notified any time the state of a proposal changes.

Options:
* `refid` (required) - Unique code representing proposal (ends with =)
* `frequency` - How often to check (in hours). Default is 15 minutes (0.25)

#### ./subscribe_to_proposal_votes
Be notified any time a proposal has a new vote.

Options:
* `refid` (required) - Unique code representing proposal (ends with =)
* `frequency` - How often to check (in hours). Default is 15 minutes (0.25)

#### ./subscribe_to_voter_votes
Be notified any time an address votes.

Options:
* `address` (required) - Address of the voter
* `frequency` - How often to check (in hours). Default is 15 minutes (0.25)

#### ./subscribe_to_stats
Display global statistics from time to time.

Options:
* `frequency` - How often to check (in hours). Default is 15 minutes (0.25)

#### ./show_all_subscriptions
Lists all active subscriptions, including their number which allows to delete them.

#### ./delete_subscription
Delete a subscription

* `id` - Subscription unique identifir (uuid) which you can get from `/show_all_subscriptions`.

#### ./delete_all_subscriptions
Delete all subscriptions.
