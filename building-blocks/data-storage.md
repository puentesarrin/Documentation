# Data Storage

The storage is an object in which we can put everything we want to save when a player saves the game.

We have to create a property where the player can store his data in it. So in `storage.js` we start with...

```javascript
monogatari.storage ({
  player: {   // add property
    name: ''  // add placeholder
  }
});

// Syntax
monogatari.storage ({   // object
  property1: {         // property of object
    placeholder1: 0,   // integer of property
    placeholder2: ''   // string of property
  }
});
```

If we now want to get the name after saving one in there, Monogatari features some custom string interpolation, which you can use by writing a storage key inside of two curly braces. This is how it would look in`script.js`.

```javascript
monogatari.storage ('player', { name: 'Monogatari'});              // example for saving a name
'{{player.name}} is a visual novel engine.'                       // example for display the name
```

To offer more possibilities in the game and to have a simpler overview in the storage file, you can create as many properties as you want, just make sure to use a comma before adding a property. Here is an example...

```javascript
monogatari.storage ({ 
  player_info: {
    name: '',
    age: '',
    city: ''
  },

  player_stats: {
    hp: 100,
    mp: 100,
    inventory: {
      gold: 1000,
      iron: 10
    }
  }
});
```

Which can be accessed as follows \(examples\)...

```javascript
{'Input': {                                                             // call input statement
  'Text': 'What is your name?',                                         // show text of the input box
  'Validation': function(input) {
      // Validation rule for the value
      return input.trim().length > 0;
  },
  'Save': function(input) {                                             // call save statement and start a function
      this.storage ('player_info', {                                    // store the value in the variable name
          name: input,
          age: 18                                                       // store 18 in the variable age
      });                                   
  },
}},

function (){
    this.storage ('player_info', {
        name: 'Georg'                                                    // save 'Georg' in variable name (overwrite old value)
    });

    this.storage ('player_stats', {
        hp: this.storage ('player_stats').hp - 50,                      // decrease hp minus 50
        inventory : {
            gold: this.storage ('player_stats').inventory.gold + 250    // add 250 gold
        }
    });                     
},

'{{player_info.name}} is {{player_info.age}} years old.',               // call name = 'Georg' and age = 18
'{{player_stats.mp}} costs the ability 'Fire Storm'.',                  // call mp = '100'
'{{player_stats.inventory.gold}}g is in his bag of gold.'               // call gold = 1250
```

If you want to see an example of the stat system \(created with storage.js\), [click me](https://hyuchia.com/Monogatari-Stat-System/).


