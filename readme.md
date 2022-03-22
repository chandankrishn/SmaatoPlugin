# Smaato Cordova Plugin

Present Smaato Ads in Mobile App/Games natively from JavaScript. 

Highlights:
- [x] Easy-to-use APIs. Display Ad with single line of Js code.
- [x] Support Banner, Interstitial, Native, and Video Ads.
- [x] One plugin supports all plataforms.
- [x] Multiple banner size, also support custom size.
- [x] Fixed and overlapped mode.
- [x] Auto fit on orientation change.
- [x] Actively maintained, prompt support.

Compatible with:

* Cordova CLI, v3.5+
* Intel XDK and Crosswalk, r1095+
* IBM Worklight, v6.2+

## Instalation ##

To install this plugin, follow the Command-line Interface Guide. You can use one of the following command lines:
```

cordova plugin add https://github.com/chandankrishn/SmaatoPlugin.git
```
If use with Intel XDK:
Project -> CORDOVA 3.X HYBRID MOBILE APP SETTINGS -> PLUGINS AND PERMISSIONS -> Third-Party Plugins ->
Add a Third-Party Plugin -> Get Plugin from the Web, input:
```
Name: Smaato Ads
Plugin ID: com.pherasoft.cordova-plugin-smaato
[x] Plugin is located in the Apache Cordova Plugins Registry
```

## Quick Start Example Code ##

Step 1: Create a cordova project and make buttons to init , load , show or call them on successcallback 

```javascript
//Adding eventListner from the main UI
document.addEventListener('deviceready', onDeviceReady, false);

//Set Ad Id for banner and rewarded
var smaato = {

    interstitialAdId: '130626426', // Phones 120 x 20
    bannerAdId: '130635706', // Phones 168 x 28
    rewardedAdId: '133149969' // Phones 216 x 36
};

//Custom video details to play after reward video
var CustomVideo =
{
    baseUrl : 'https://gateway.pinata.cloud/ipfs/QmUCEtnEssT8xonBBWZeoGbev3NmPKPJo7SbrHJxAA9jSW/',
    count : '3'
}
//For switch to handle callbacks
const rewardAdEvent = {
    onAdLoaded : 0,
    onAdFailedToLoad : 1,
    onAdError : 2,
    onAdClosed : 3,
    onAdClicked : 4,
    onAdStarted : 5,
    onAdReward : 6,
    onAdTTLExpired : 7
};

const interstitialAdEvent = {
    onAdLoaded : 0,
    onAdFailedToLoad : 1,
    onAdError : 2,
    onAdClosed : 3,
    onAdClicked : 4,
    onAdStarted : 5,
    onAdReward : 6,
    onAdTTLExpired : 7
};

const bannerAdEvent = {
    onAdLoaded : 0,
    onAdFailedToLoad : 1,
    onAdClicked : 2,
    onAdImpression : 3,
    onAdTTLExpired : 4
}
//When the app has been started and ready to play ads
function onDeviceReady() {
    // Cordova is now initialized. Have fun!
    setOptions();
    console.log('Running cordova-' + cordova.platformId + '@' + cordova.version);
    document.getElementById('deviceready').classList.add('ready');
    document.getElementById("showVideo").addEventListener("click", showVideo);
    document.getElementById("banner").addEventListener("click", showBannerAd);
    // document.getElementById("interstitial").addEventListener("click", showInterstitalAd);
    document.getElementById("rewarded").addEventListener("click", showRewardedAd);
    document.getElementById("loadRewarded").addEventListener("click", loadRewardedAd);
    document.getElementById("initSmaato").addEventListener("click", initSmaato);
    document.getElementById("closeBannerAd").addEventListener("click", closeBannerAd);
}
//it will be automatically called when device is ready
function setOptions() {

    console.log("Set Options: ",smaato.bannerAdId);
    window.plugins.Smaato.setOptions({
        interstitialAdId: smaato.interstitialAdId,
        bannerAdId: smaato.bannerAdId,
        rewardedAdId: smaato.rewardedAdId
    });
}

//To show any ad first we need to init make a call on this function from UI
function initSmaato() {
    console.log("initSmaato called");
    document.getElementById("div1").innerHTML = "initSmaato";
    window.plugins.Smaato.initSmaato();
}

//To be called to show banner ads
function showBannerAd() {
    console.log("showBannerAd called");
    document.getElementById("div1").innerHTML = "testBanner";
    window.plugins.Smaato.showBannerAd({},successCallbackBA,failureCallbackBA);
}
//To be called to show Interesterial ads
function showInterstitalAd() {
    console.log("showInterstitalAd called");
    document.getElementById("div1").innerHTML = "testInter";    
    window.plugins.Smaato.showInterstitialAd({},successCallbackRA,failureCallbackRA);
}

//To show rewarded Ad should be called after loadRewardedAd()
function showRewardedAd() {
    console.log("showRewarded called");
    document.getElementById("div1").innerHTML = "testRewarded";
    window.plugins.Smaato.showRewardedAd({},successCallbackRA,failureCallbackRA);
}

//To be called untill success callback
function loadRewardedAd()
{
    console.log("loadRewarded called");
    document.getElementById("div1").innerHTML = "testLoadRewarded";
    window.plugins.Smaato.loadRewardedAd({
      baseUrl : CustomVideo.baseUrl,
      count : CustomVideo.count
    },successCallbackRA,failureCallbackRA);
}

//To close banne ads
function closeBannerAd() {
    console.log("closeBannerAd called");
    document.getElementById("div1").innerHTML = "closeBannerAd";
    window.plugins.Smaato.closeBannerAd({},successCallbackBA,failureCallbackBA);
}

//to handle successcallbacks and do whatever you want

function successCallbackRA(result) {
    console.log("successCallbackLRA: "+ result);

    switch (result) {
        case rewardAdEvent.onAdLoaded:
            
            break;
        case rewardAdEvent.onAdClosed:
            
            break;
        case rewardAdEvent.onAdClicked:
            
            break;
        case rewardAdEvent.onAdStarted:
            
            break;
        case rewardAdEvent.onAdReward:
            
            break;
        default:
            break;
    }
}
//to be called on failure
function failureCallbackRA(error) {
    console.log("failureCallbackLRA: "+ error);

    switch (error) {
        case rewardAdEvent.onAdFailedToLoad:
            
            break;
        case rewardAdEvent.onAdError:
            
            break;
        case rewardAdEvent.onAdTTLExpired:
            
            break;
        default:
            break;
    }
}

function successCallbackBA(result) {
    console.log("successCallbackBA: "+ result);

    switch (result) {
        case bannerAdEvent.onAdLoaded:
            
            break;
        case bannerAdEvent.onAdClicked:
            
            break;
        default:
            break;
    }
}
function failureCallbackBA(error) {
    console.log("failureCallbackBA: "+ error);

    switch (error) {
        case bannerAdEvent.onAdFailedToLoad:
            
            break;
        case bannerAdEvent.onAdImpression:
            
            break;
        case bannerAdEvent.onAdTTLExpired:
            
            break;
        default:
            break;
    }
}

function successCallback(result) {
    consconsole.log("successCallback: "+ result);
}

function failureCallback(error) {
    console.log("failureCallback: "+ error);
}

