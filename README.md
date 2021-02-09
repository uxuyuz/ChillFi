
![alt text](https://github.com/ssemino/ChillFi/blob/main/Assets/Resources/README/readme00.png)
 
 ## Introduction
 
 The project completed using **Unity 2020.2.1f1**. Please, make sure to open it in a proper Unity version, because reimport for later versions break the project's workability.
 To retrieve the data from DeFi aggregators we use **Shrimpy** and **CoinMarketCap** APIs.
 
 Target project platform is **Standalone** (Windows and OSX), however that's possible to compile it for mobile platforms if needed.
 
 Project purpose is a procedural generation of a hypotetical trader room for YouTube stream with DeFi aggregator live data displaying at two monitors and predefined Spotify music playlist that should play during the stream.
 **ChillFi** app generates visual part of the stream, **Spotify** plays the music (so we don't need any sounds comes from the app itself) and **OBS Studio** (or it's analog) launched in background to record and stream the gathered video/audio procedural simulation to YouTube.
 
 **WARNING!**
 To get the proper Unity version you can get it from an archive page here: https://unity3d.com/ru/get-unity/download/archive
 
 ## Quick Start Guide
 
 Once you have the project opened you can test it by press **Play** button at the top.
 
 At start Unity will forward you to your browser, where it will ask you to login into your Spotify account.
 
 That happens because of **Spotify4Unity** plugin that had been integrated to display current track that have been playing through **Spotify** during the streaming session.

### Disable Spotify AutoConnect
For development and debug purposes you can disable this **AutoConnect** feature to not spend time to close **Spotify** Login page each time you enter Unity **PlayMode**.
You can disable it in **SpotifyService** MonoBehaviour class at **SpotifyService** gameObject.

![alt text](https://github.com/ssemino/ChillFi/blob/main/Assets/Resources/README/readme01.png)

### DeFi symbols setup

If you need to change a list of DeFi symbols that comes from **CoinMarketCap** service, you just need to change a symbol to proper one in **ShrimpyService** MonoBehaviour class at **ShrimpyService** gameObject. You can also change the order of the symbols by changing it in this list.

![alt text](https://github.com/ssemino/ChillFi/blob/main/Assets/Resources/README/readme02.png)

**WARNING!** Make sure you set a proper symbol definition in this list, because if you will set incorrect value that **CoinMarketCap** doesn't have - the app will get an error.

## DeFi APIs' workflow

To get a live DeFi symbols data for our app we use **Shrimpy API** (https://developers.shrimpy.io/docs/) and **CoinMarketCap API** (https://coinmarketcap.com/api/documentation/v1/).
The first one used to get the data for a small monitor and have some limitations during **Shrimpy** service policy. We have only 60 request per minute for one authenticated IP (that sends API-KEY request header) or just 10 requests per minute without API-KEY.
Even though we have anough space to get a live trades data to show.
**Shrimpy** gets OrderBook for us with all the current bids and asks. **SHrimpyService** class choose randomly bid or ask for us with a symbol from our list.
