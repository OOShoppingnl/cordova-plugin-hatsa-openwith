# cordova-plugin-hatsa-openwith
Cordova plugin voor open-met-functionaliteit op Android, en enkel op Android en dus NIET op iOS

**Opmerking:** Ik heb alle bestanden die volgens mij bij iOS horen eruit gehaald, en eveneens uit `plugin.xml`. 

**LET OP:** Het bestand `AbstractOpenwithActivity.java` moet aangepast worden zodat er in dit bestand verwezen wordt naar de 
`MainActivity` van onze app. Er staat nu nog `com.example.hello.MainActivity.class` maar `com.example.hello` is de 
naam van het hello-world-project.

**BRON:** [https://github.com/nyholmsolutions/cordova-plugin-openwith](https://github.com/nyholmsolutions/cordova-plugin-openwith)

# Usage
In de `www/js` map van je project, voeg deze funtie toe aan `index.js`.

```
function setupOpenwith() {

    // Increase verbosity if you need more logs
    //cordova.openwith.setVerbosity(cordova.openwith.DEBUG);

    // Initialize the plugin
    cordova.openwith.init(initSuccess, initError);

    function initSuccess()  { console.log('init success!'); }
    function initError(err) { console.log('init failed: ' + err); }

    // Define your file handler
    cordova.openwith.addHandler(myHandler);

    function myHandler(intent) {
        console.log('intent received');

        console.log('  action: ' + intent.action); // type of action requested by the user
        console.log('  exit: ' + intent.exit); // if true, you should exit the app after processing

        console.log(intent);

        if (intent.exit) { cordova.openwith.exit(); }
    }
}
```

Voer de functie uit op het event `deviceready`.

```
var app = {
    
    ...
    
    onDeviceReady: function() {
        
        ...
        
        setupOpenwith();
    },

    ...
    
};
```