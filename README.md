# govolcanic-banners

HTML5 display banners for [govolcanic.hu](https://www.govolcanic.hu/), a webshop selling Hungarian volcanic-soil wines.

## What it is

GoVolcanic (Empire Wines Kft., Somlóvásárhely) sells wines from volcanic terroirs: Somló, Badacsony, Eger, Tokaj. I built a display-ad set for their 2023 retargeting campaign in four IAB sizes:

| Size | File |
|------|------|
| 300×250 | `300x250/300x250.html` |
| 300×600 | `300x600/300x600.html` |
| 640×360 | `640x360/640x360.html` |
| 970×250 | `970x250/970x250.html` |

## How the product rotation works

Each banner is a self-contained HTML file with inline CSS, split into a white product half and a red brand half (`#BE1E2D`). On load it fetches `wines.json` from Linode Object Storage and renders one wine at random:

```js
fetch('https://govolcanic-banners.eu-central-1.linodeobjects.com/wines.json')
```

Every entry carries a name, a tasting note, a price, a bottle shot and a deep link to the product page. Adding a wine to the campaign means editing one JSON file on the bucket, with no re-export and no ad-network re-upload. That was the whole point: the client could swap the promoted bottles themselves.

Fonts come from Google Fonts (Inter). Nothing else is loaded.

## Run it

```bash
python3 -m http.server 8000
# then open http://localhost:8000/300x250/300x250.html
```

The banners need a live `wines.json` at the bucket URL. Point the `fetch` at the local `wines.json` to preview offline.

## Files

```
300x250/ 300x600/ 640x360/ 970x250/   one HTML file + logo per size
wines.json                            the product feed (mirror of the bucket copy)
images/                               bottle shots
govolcanic-banners-2023-10-16.zip     the delivery archive handed to the ad ops team
```

## Status

Delivered October 2023, one commit, not maintained. The prices in `wines.json` are from 2023.

## License

MIT for the code. Bottle photography and the GoVolcanic mark belong to Empire Wines Kft.
