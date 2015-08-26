# Purpose of this file

Before we start writing a formal protocol specification, I thought it would be a good idea to put some general notes into a document.

# Core RPG Elements

Here we can define a list of elements that we agree are important parts of an RPG.  They must be very important elements, things that without which would result in a system that is not an RPG.  An example of something that would NOT go in this list would be assets such as sound or graphics, as RPGs can be text based.

* Actors
* Items
* Quests
* World Movement
* Data Queries

## A few notes on Actors

I think Actors can be an umbrella term to represent both player-controlled characters and NPCs, and that distinguishing the two can be left to specific implementations.  However, I think this should be discussed further.

## Notes on world movement

I'm thinking for the sake of simplicity, initially, the client should simply (as controlled by the player) sends a simple message to the server asking whether the given direction of movement is valid, and the server will return a boolean value of some sort stating whether or not its valid (very basic networked collision detection) and then another message is sent declaring that the player is making a move.  It will be up to the client software to make sure that the move declaration message is one of the valid moves that would have already been checked earlier, though some error checking will be needed at the very least for purposes of debugging.  This is bordering on implementation specific functionality, but should be considered when designing error codes.

My reasoning for separating the check for a valid move and the actual declaration of a move is that hypothetically, a client could use an algorithm to check all possible moves for the entirety of the current observable world to make it easy to render a map of where there are "walls" and where there aren't.  This would be specifically helpful for an RPG with a roguelike interface, where you don't need extra asset data to render the world, but just a view of where you can and can't walk.  Again, this is open for further discussion.

## Data Queries

I believe this is necessary for the protocol to allow a variety of implementation specific values to be sent back and forth.  It could be as simple as a client sending some sort of key to request a value in the server's "database".  The type of database (whether it be flat file, relational, NoSQL, etc.) is unimportant, as that is another implementation specific decision.  Another thought is for clients to be able to write new values back in, which is important in a lot of cases.  Again, implementation specific, but a server could maintain control by setting permissions on some values, making a variety of them read-only for most clients.

## Notes on items and quests

I need to flesh this out more, but I think they are both important enough that they should be built in to the protocol.

## Combat

Combat may also be a consideration as a core element, but it is not currently a high priority.

# Technical Details

We are thinking of starting out with this being a text-based protocol but also adding a binary mode later on.

## User Authentication

Some servers may want to allow anonymous access, so this is implementation specific.  Implementations will want to use the data querying functionality for the purpose of any authentication scheme that they feel is necessary.  Open for discussion though.
