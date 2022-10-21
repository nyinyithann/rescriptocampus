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
@send external play: game => unit = "play" 
@send external exit: game => unit = "exit" 
@send external on: (game, @string [
    |#play (unit => unit)
    |#completed (string => unit)
    |#exit (string => unit)
]  ) => game = "on"

/* usage */
let myGame = createGame()
myGame
    ->on(#play (() => Js.log("let's start...")))
    ->on(#completed (x => Js.log(x)))
    ->on(#exit (x => Js.log(x)))
    ->ignore
myGame->play
myGame->exit
```
