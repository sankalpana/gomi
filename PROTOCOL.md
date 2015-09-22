# Protocol

Gomi is a game designed to help developers get started with HTTP
server/client development with Go. The game Gomi is a simplified
version of the famous “Omi” game played by Sri Lankans. Players
will implement the client in Go which will play the game using a
simple HTTP api.

## Gomi Game Rules
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

## Game Server API

### Registration
Before doing anything, users must register on the game server with a
username and a password. As security is not a primary concern and we
want to make it easy for clients, we can send the username and the
password with requests to authenticate.

```
// POST /register
{
  username: "",
  password: ""
}
```

```
// Response
{
        error: "",
}
```

### Starting a Game
After registration, users can join a game. The game will be created if
it doesn’t exist. A player is not allowed to play in more than one game
at at time. If the player joins a new game they will be removed from
their current game and automatically lose that game. Players can create
game rooms with unique names. The room remains active until the game ends
(when one of the payers leave the game). When joining the game, players
can enter a team name which will be used to pair users when starting the
game. If 2 users join with the same team name, they will belong to the
same team.

```
// POST /game/join
{
  auth: {username: "", password; ""},
  game: "",
  team: "",
}
```

```
// Response
{
  error: "",
}
```

### Getting game status
At any time after joining the game players can request the game room status.
This includes all details the player should know about the game. Players can
poll this url to get updates.

```
// POST /game/status
{
  auth: {username: "", password; ""},
  game: "",
}
```

```
// Response
{
  ready: true,
  trump: {username: "", suite: null},
  players: [
    {username: "", team: ""},
    {username: "", team: ""},
    {username: "", team: ""},
    {username: "", team: ""},
  ],
  cards: [
    {suite: "", value: ""},
    {suite: "", value: ""},
    {suite: "", value: ""},
    {suite: "", value: ""},
  ]
}
```

The server picks which player should announce the trump card. No other
actions will be accepted from players until a suite is selected by the player.

```
// POST /game/trump
{
  auth: {username: "", password; ""},
  game: "",
  suite: "",
}
```

```
// Response
{
  error: "",
}
```

After selecting the trump suite, game status returns more information
which includes all the cards the user has, current table and the previous
table (if it exists).

```
// POST /game/status
{
  auth: {username: "", password; ""},
  name: "",
}
```

```
// Response
{
  ready: true,
  trump: {username: "", suite: ""},
  players: [
    {username: "", team: ""},
    {username: "", team: ""},
    {username: "", team: ""},
    {username: "", team: ""},
  ],
  cards: [
    {suite: "", value: ""},
    {suite: "", value: ""},
    {suite: "", value: ""},
    {suite: "", value: ""},
    {suite: "", value: ""},
    {suite: "", value: ""},
    {suite: "", value: ""},
    {suite: "", value: ""},
  ],
  table: [
    null,
    {suite: "", value: ""},
    {suite: "", value: ""}
    null,
  ],
  previous: [
    {suite: "", value: ""}
    {suite: "", value: ""}
    {suite: "", value: ""}
    {suite: "", value: ""}
  ],
}
```

In above response, we can get that player 2 played first and the server
is waiting for player 4 to play. We can also see the previous set of cards
on the table if it’s available. If it's current players turn, he can play a card.

```
// POST /game/play
{
  auth: {username: "", password; ""},
  game: "",
  card: {suite: "", value: ""},
}
```

```
// Response
{
  error: "",
}
```

The player must have the card and the play must follow Gomi game rules.
