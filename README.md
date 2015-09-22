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
