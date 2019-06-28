# Thermostat

### Specification:

- [x] Thermostat starts at 20 degrees
- [x] You can increase the temperature with an up function
- [x] You can decrease the temperature with a down function
- [x] The minimum temperature is 10 degrees
- [x] If power saving mode is on, the maximum temperature is 25 degrees
- [x] If power saving mode is off, the maximum temperature is 32 degrees
- [x] Power saving mode is on by default
- [x] You can reset the temperature to 20 with a reset function
- [x] You can ask about the thermostat's current energy usage: < 18 is low-usage, < 25 is medium-usage, anything else is high-usage.
- [x] (In the challenges where we add an interface, low-usage will be indicated with green, medium-usage indicated with black, high-usage indicated with red.)

### JQuery:

1. download the script or grab one off a CDN. Load it in index.html.

Download:

```
<script src="js/jquery.min.js"></script>
```

CDN:

```
<script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
```

2. only execute functions when the DOM is loaded:

```
$(document).ready(function() { })
```

this wraps the JQuery document.

3. JQuery selector with an event listener:

```
$('element').on('event', function() {

})

// Or:

$('element').click(function() { })

// also callbacks:

$('#some-heading').click(function() {
  // this function is the callback!
})
```

events can be clicks, scrolls, typing and other forms of interaction within the browser.

4. Set a new object:

```
var thermostat = new Thermostat();
```

5. to DRY out the code:

```
function updateTemperature() {
  $('#h1').text(`Current temperature: ${term._temperature}`);
}

// to call it:

$(document).ready(function() {
  var thermostat = new Thermostat();
  updateTemperature();

  $('#temp-up').click(function() {
    thermostat.increaseTemperature();
    updateTemperature();
  });
  
  function updateTemperature() {
    $('#temperature').text(thermostat.temperature);
  };
});
```