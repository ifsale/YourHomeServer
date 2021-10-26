# YourHomeServer

A powerfull nodejs server based on express module to control tuya and miio devices locally or over the cloud

## Installation and start server

```
git clone https://github.com/ifsale/YourHomeServer.git

cd YourHomeServer

git rm --cached config/cloud.json &&
git rm --cached config/conditions.json &&
git rm --cached config/config.json &&
git rm --cached config/scenes.json &&
git rm --cached config/local/devices.json &&
git rm --cached package.json

git reset

git update-index --assume-unchanged config/local/devices.json &&
git update-index --assume-unchanged config/cloud.json &&
git update-index --assume-unchanged config/scenes.json &&
git update-index --assume-unchanged config/conditions.json &&
git update-index --assume-unchanged config/config.json &&
git update-index --assume-unchanged package.json

npm install

node app.js

```

## Tuya local module
Use this module to control  control Tuya/Smart Life devices locally

```
npm install codetheweb/tuyapi
```

## Miio local module
Use this module to control Mi Home devices locally
```
npm install miio-api
```

## Tuya cloud module
Use this module to control  control Tuya/Smart Life devices over the cloud

```
npm install tuyacloudnodejs
```

## SmartThings cloud module
Use this module to control  control Smart Things devices over the cloud

```
npm install smartthingsnodejs
```
## Configuration files

### Server configuration
Configure the parameters for the server in the file ./config/config.json
	
### Device configuration
Configure your devices in the file ./config/local/devices.json

Configure device example:
```
"lr-light1":
{
	"id": "eba9bce17c59213edf47g1",
	"key": "af7edc409a4a6cc6" ,
	"ip": "192.168.2.8" ,
	"type": "tuya" ,	// tuya|miio|smartthings
	"category":"dj" 	// categories found in ./config/local/schemas.json
}
```
Configure scene to be triggered example (acts as a device):
````
"sc-tv-mute-toggle":
{
	"id": "InQoaFbmBrqyPRTm" ,
	"type": "tuya" ,
	"category":"scene"
}
```
## Basic usage
To control a device locally use the following endpoint
http://address:port/local/device/{label}/?actions={actions}&values={values}

## Main endpoints

Actions are found in the schema file.\
Cloud types are "scenes|devices|home|token" for tuya and "devices|apps|subscriptions" for SmartThings\
Use get-methods for each type as a method to see all the cloud methods available

Run an action on a device\
http://address:port/local/device/{label}/?actions={actions}&values={values}

Run a scene\
http://address:port/local/scene/{name}/

Query a scene\
http://address:port/local/query/{name}/

Evaluate a condition\
http://address:port/local/eval/{name}/

Direct tuya cloud requests\
http://address:port/cloud/tuya/{type}/{configLabel}/{deviceID|label}/{method}/

Direct SmartThings cloud requests\
http://address:port/cloud/smartthings/{type}/{configLabel}/{deviceID|label}/{method}/{component?}/{capability?}/



*** Cloud support is available for tuya and SmartThings devices at the moment (no cloud Xiaomi support).
