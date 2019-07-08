# Bowling challenge - 29-30.06.2019

## Setup:

1. Set up an npm project before installing npm packages. In your project directory run:

```
npm init
```

2. npm will install a package.json file - this is somewhat similar to Gemfile
3. add ESLint to your project:

```
npm install --save-dev eslint
```

4. Configure ESLint:

```
eslint --init
```

This will create a '.eslintrc.js' file in the root directory, which needs to be configured. It can be configured with a plugin like:

- [this Airbnb base style guide](https://www.npmjs.com/package/eslint-config-airbnb-base)

Once you've installed the plugin, add this inside your .eslintrc.js:

```
"extends": "airbnb-base",
"extends": "airbnb-base/legacy", // not sure if necessary
```

remove the default 'extends: eslint recommended'  

5. run tests with

```
npm test
```

lint this module with itself by running:

```
npm run lint
```

run linting with:

```
eslint

//or

eslint file.js
```

6. you can add .eslintignore file or this bit inside package.json:

```
{
  "name": "mypackage",
  "version": "0.0.1",
  "eslintConfig": {
      "env": {
          "browser": true,
          "node": true
      }
  },
  "eslintIgnore": ["hello.js", "world.js"]
}
```

7. Add JQuery to project (current: jquery-3.4.1.min.js)

## Game logic:

Two classes: Scoreboard/game and Frame, or
Three classes: Scoreboard, Game and Frame

Game - runs game, calculates points, polices frames so there's no more than 10, keeps track of bonuses
Scoreboard - updates points and back points with each closed frame, communicates with interface
Frame - holds frame info: number, roll one, roll two, strike, spare, and possibly points

Ed's hint: start with a perfect gutter game - set that up, add unit and feature tests, escalate

---

# Attempt 2:

in Count app:

**in CountModel.js**

function addSum() takes an argument and adds it to this._count;

added a setter and accessor for local variable _score;

CountModel needs to be used as it holds all the functions!!

**in app.rb**

score variable to store score the way the count variable holds the count ???
stored in session as score:

**ScoreController.js**

a copy of CountController with the setup for this button, hopefully functional;
_setupOneButtonToUpdateScore();
_setupTwoButtonToUpdateScore();
_setupThreeButtonToUpdateScore();

**ScoreView.js**

a copy of CountView that creates the ScoreView object for display;

pass to app.rb ??

js files used for Score:
- CountModel
- ScoreController
- ScoreView
- index.js
- ScorePersister (has get and set functions, not to be confused with the setScore and set functions of the CountModel)

[good solution to study](https://github.com/saypop/bowling-challenge)






