# mopub-skadnetwork-ids

Subscribe to notifications on this repository to be alerted of updates to SKAdNetwork IDs associated with MoPub Marketplace and ad networks serving via MoPub's mediation. 

# How to use
Do not pull SKAdNetwork IDs directly from this repository as they are unprocessed and might contain duplicates. To get a processed list, use the [MoPub SKAdNetwork IDs Manager](https://developers.mopub.com/publishers/skadnetwork-ids-manager/). The tool also allows custom input based on the IDs your app already has as well as third-party JSON URLs.

# How to extend
We provide an endpoint that you can ping from anywhere (wherever you can use `curl`). It's useful for when you cannot use the Manager above, or want to extend our logic in your own build scripts.

## Get supported partners
Ping the following endpoint:

```
curl -g -H "Content-Type:application/xml" \
https://us-central1-mopub-mediation.cloudfunctions.net/getSKAdNetworkIds/[\"getSupportedPartners\"]
```

to get an Array:

```
["AdColony","AppLovin","Chartboost","Facebook Audience Network","Fyber","Google","InMobi","ironSource","Mintegral","MoPub Marketplace","Pangle","Snap","Tapjoy","Unity Ads","Verizon Media","Vungle"]
```

## Get SKAdNetwork IDs for a supported network partner
Ping the following endpoint with the partner name:

```
curl -g -H "Content-Type:application/xml" \
https://us-central1-mopub-mediation.cloudfunctions.net/getSKAdNetworkIds/[\"Google\"]
```

to get a processed info.plist containing the IDs:

``` xml
<?xml version='1.0' encoding='UTF-8'?>
<!DOCTYPE plist PUBLIC '-//Apple//DTD PLIST 1.0//EN' 'http://www.apple.com/DTDs/PropertyList-1.0.dtd'>
<plist version='1.0'>
<dict>
    <key>SKAdNetworkItems</key>
    <array>
        <dict>
            <key>SKAdNetworkIdentifier</key>
            <string>2fnua5tdw4.skadnetwork</string>
        </dict>
        <dict>
            <key>SKAdNetworkIdentifier</key>
            <string>2u9pt9hc89.skadnetwork</string>
        </dict>
        ...
    </array>
</dict>
</plist>
```

You can string multiple partner names together in the call, as long as they are escaped and comma-separated. Note that, due to existing limitations on URL lengths (~2000 characters), we cannot accept requests that are too long.

## Get SKAdNetwork IDs for all supported network partners
Ping the following endpoint with the `all` param:

```
curl -g -H "Content-Type:application/xml" \
https://us-central1-mopub-mediation.cloudfunctions.net/getSKAdNetworkIds/[\"all\"]
```
