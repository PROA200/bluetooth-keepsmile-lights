
## Install packages
```
npm install
```
## Generate ssl cert to enable https

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ./selfsigned.key -out selfsigned.crt
```
## Run with
```
node app.js
```

Mobile devices can go to localhost:3000 or \<machine ip\>:3000 to view the webpage with buttons to control device.

## Browser Permissions
navigate to:
```
chrome://flags
```

The two required experimental features are:
```
Experimental Web Platform features
Use the new permissions backend for Web Bluetooth
```

Post commands can be sent in the form:
```json
{"command":"lightsON"}
```
or
```json
{"command":"lightsOFF"}
```

At the top of the app.js file there is a chromeUserDataDir variable that needs to be set to the directory of your chrome permission cache. Basically there are authorization concerns when accessing a devices bluetooth through a the web browser and the browser will cache a prior authorization but the chromedriver doesn't use the same browser cache so you'll have to authorize it every time if you don't point to the same location. For a backend service to work without providing the users feedback it needs access to the original browser cache so if you want to use the post commands above it's neccessary.


Originally I wanted this to only run on android/Mobile devices in the background and was working on a native app but the package management is trash. The backend bit of this project is probably better served by a service native to the device hosting the service. In my case my computer didn't have bluetooth so it originally wasn't an option. (recently got a bluetooth dongle which made the backend stuff possible, but I don't know if connectivity will reach from my server downstairs)

It's possibly interesting to point out that if the server is out of range or doesn't have bluetooth capabilities you can still use this on a mobile device since it's using your mobile bluetooth.

The explicit goal is to get to a point of using whisper.ai to translate voice commands into controlling the device. The backend service bit is going to be important in the long run, but for now being able to hit a button on a web page to turn the lights on and off is pretty cool.