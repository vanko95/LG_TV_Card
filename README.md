# Remote Control card #

LG TV Remote Control card based on https://github.com/dimagoltsman/content-card-remote-control to work with tasmota-ir.


Put js and the folder files in your www dir and add the js files to your resources in ui-lovelace.yaml
```
resources:
  - url: /local/content-card-remote-control.js
    type: module
```
Put in scripts.yaml 
```
ir_code:
  sequence:
  - data_template:
      payload: '{"Protocol":"NEC","Bits": 32,"Data": 0x{{ data }}}'
      topic: 'cmnd/{{host}}/irsend'
    service: mqtt.publish
```
Put in configuration.yaml
```
script: !include scripts.yaml
```

Configuration is very easy. first, find your tasmota MQTT_CLIENT_ID for sending packets (can be found under tasmota web configuration page),
and then just configure the tasmota ir codes for each button.

All buttuns are configured according to the id of the button in the html section of `remote-html.js`


LG remote example:
```
      - type: "custom:content-card-remote-control"
        remote_host: 'tasmota-ir'
        name: LG Tv
        remote_template: lg_new
        buttons:
          power: "20DF10EF"
          source: 
          button1:  
          button2:  
          button3:  
          button4:  
          button5:  
          button6:  
          button7:  
          button8:  
          button9:  
          buttonClear:
          button0:
          buttonEnter:
          exit:
          info:
          menu:
          channeldown:
          channelup:
          netflix:
          left: 
          right: 
          top: 
          bottom: 
          ok: 
          back:
          volplus: 
          volmin: 
          mute: 
      
```

# Contribution
If you want to add your own remote template, you can do it in a new folder near the 'simple' and 'lg' remotes and
set remote_template to the name of your new folder. 
Just make sure you are changing the html and css methods suffixes

#you are also welcome to contribute new templates. you can add new buttons and remove buttons, just make sure their id matches the id you put in the yaml#

Please update JS file, add remote_host with your tasmota MQTT_CLIENT_ID
