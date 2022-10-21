# Fixed Arguments

# Special-case: Event Listeners
#### JavaScript
```JavaScript
/* play.js */
class Game {
  #eventMap;
  #timeOutId;

  constructor() {
    this.#eventMap = new Map();
  }

  on(eventName, event) {
    this.#eventMap.set(eventName, event);
    return this;
  }

  play() {
    console.log('play...');
    clearTimeout(this.#timeOutId);
    this.#eventMap.get('play')?.();
    this.#timeOutId = setTimeout(
      () => this.#eventMap.get('completed')?.('You won!'),
      2000
    );
  }

  exit() {
    clearTimeout(this.#timeOutId);
    this.#eventMap.get('exit')?.('Bye');
  }
}

export { Game };
```

#### Rescript Binding
```reasonml
type game
@new @module("./play") external createGame: unit => game = "Game"
@send external gameOnPlay: (game, @as("play") _, unit => unit) => unit = "on"
@send external gameOnCompleted: (game, @as("completed") _, string => unit) => unit = "on"
@send external gameOnExit: (game, @as("exit") _, string => unit) => unit = "on"

/* usage */
let myGame = createGame()
myGame->gameOnPlay(()=>Js.log("lets start the game ..."))
myGame->gameOnCompleted(x=>Js.log(x))
myGame->gameOnExit(x=>Js.log(x))
myGame->play
myGame->exit
```
