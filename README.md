# Gomi
Gomi is a game designed to help developers get started with HTTP
server/client development with Go. The game Gomi is a simplified
version of the famous “Omi” game played by Sri Lankans. Players
will implement the client in Go which will play the game using a
simple HTTP api.

## Game Rules
The game requires 2 teams with 2 players each. The server decides
who chooses the trump card. The player to dealer's right, who announced
the trump suit, leads any  card to the first trick. The other players
play in turn, anticlockwise  around the table, and  must follow suit
if able to; a player who holds  no card of the suit led may play any
card. If no trumps are played, the trick is won by the highest card
of  the suit that was led. If any trumps were played the highest trump
wins the trick. The winner of the trick gathers the four cards, stacks
them face down in the team's trick pile, and leads any card to the next
trick. (http://www.pagat.com/whist/omi.html)

## Contributing
This is a community project by members of the **Colombo Gophers** meetup
group. The game server is built by group members and will be relaeased
under an open source license when it's ready.

### Why should I contribute?
Although this is a game server, it covers many aspects of a modern web based
application. This includes, handling http, json and databases and many more.
This is also a good chance to get your go code reviewed by more experienced Go
developers. You can learn your errors and discover much better ways to code.

### How to contribute?
There are 2 primary ways to contribute, first is to identify missing and incorrect
parts of the system and add Github issues about them. The second method is to
contribute code and fix existing issues and add missing features. When contributing
code, please fork this repository and create a pull request with changes.
