# Weeks 11-12 to dos:

## Goals:

- [x] final project  

## Misc to do:

- [ ] build a Chrome extension 
- [ ] go through the Bowling scoreboard kata walkthrough 
- [ ] CodeCademy & Udemy - watch JS/DOM manipulation/backend JS tutorials
- [ ] sign up for Egghead trial
- [ ] finish the Git Branching tutorial
- [ ] finish Wes Bos' JS course and move on to React
- [ ] add an XP values dev pill
- [x] look into [Firestore db](https://firebase.google.com/docs/firestore) and other non-relational dbs
- [x] install Rust and Cargo
- [ ] [Rustlings](https://github.com/rust-lang/rustlings/)



## JS things to look up:

- [x] query selectors - syntax?
- [ ] document vs documentElement
- [ ] document.documentElement.style.setProperty(args??)
- [ ] targeting elements by event property (gaining visibility of event properties with console.log(e))
- [x] CSS - transitions with cubic-bezier


### Wes Bos notes

JS - passing a function to event listener - pass as arg without parentheses because with parentheses it would execute on window open, not on event listened for:

```
// the function:
function toggleActive(e) { // event passed into the function is the transition end event
  if(e.propertyName.includes('flex')) { // covers flex and flex-grow
    this.classList.toggle('open-active'); // toggles class in panel
    }
  }
  
// the event listener:
panels.forEach(panel => panel.addEventListener('transitionend', toggleActive)); // only on this event run toggleActive()

```


---

# Lifetime total hours of coding:

```
786
```
