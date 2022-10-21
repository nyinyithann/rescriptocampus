# Constrain Arguments
#### JavaScript
```JavaScript
/* play.js */
function openWith(browserName) {
  if (browserName === 'chrome') {
    return 'opening with chrome ...';
  }
  if (browserName === 'safari') {
    return 'opening with safari ...';
  }
  if (browserName === 'firefox') {
    return 'opening with firefox ...';
  }
  if (browserName === 'edge') {
    return 'opening with edge ...';
  }
}

function queueWith(state) {
  if (state === 0) {
    return 'task is in the queue with low priority.';
  }
  if (state === 6) {
    return 'task is in the queue with high priority.';
  }
  if (state === 7) {
    return 'task is in the queue with top proirity.';
  }
  throw new Error('Unexpected state');
}

export { openWith, queueWith }
```

#### Rescript Binding
```reasonml
@module("./play") external openWith: (
    @string[
        | #chrome
        | #safari
        | #firefox
        | @as("edge") #IE
    ]
) => string = "openWith"

@module("./play") external queueWith:(
    @int[
        |#low
        |@as(6) #high
        |#top
    ]
) => string = "queueWith"

/* usage */
openWith(#chrome) -> Js.log
openWith(#safari) -> Js.log
openWith(#firefox) -> Js.log
openWith(#IE) -> Js.log

queueWith(#low)->Js.log
queueWith(#high)->Js.log
queueWith(#top)->Js.log
```
