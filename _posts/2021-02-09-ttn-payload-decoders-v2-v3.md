---
title: "Using TTN v2 payload decoders with the TTN v3 Stack"
date: "2021-02-09"
layout: post
---

The community driven LoRaWAN network [The Things Network](https://www.thethingsnetwork.org/) is in the midst of migrating from the existing v2 version of its LoRaWAN stack to the newer v3 version. It's a mostly [manual process](https://www.bjoerns-techblog.de/2021/01/ttn-v3-stack-applikation-und-device-migration/), and one of the things that people have to adapt are the payload decoders for LoRaWAN applications.

The v2 stack used 3 separate functions, a decoder, a converter and a validator function.

![The payload decoder functions in TTN v2](/images/ttn_decoders_v2.png)

In the v3 stack, there is only a single function. For more details on the inputs etc, check out the [TTI v3 documentation](https://www.thethingsindustries.com/docs/integrations/payload-formatters/javascript/).

![The payload decoder functions in TTN v3](/images/ttn_decoders_v3.png)

I wanted to come up with a very simple way to convert one to the other, and here it is.

You can copy all the TTN v2 converter functions into the editor field in the TTN v3 payload decoder configuration. Make sure to keep the original function names. If you didn't use one or more of the functions, you can just skip copy&pasting them. Then, add the following additional function at the bottom:

```javascript
function decodeUplink(input) {
  var data = input.bytes;
  var valid = true;

  if (typeof Decoder === "function") {
    data = Decoder(data, input.fPort);
  }

  if (typeof Converter === "function") {
    data = Converter(data, input.fPort);
  }

  if (typeof Validator === "function") {
    valid = Validator(data, input.fPort);
  }

  if (valid) {
    return {
      data: data
    };
  } else {
    return {
      data: {},
      errors: ["Invalid data received"]
    };
  }
}
```

With that, you don't need to do any further adaptations to your existing payload decoders, and can keep them split up into separate functions, which might be nice as well. I tested this with the Paxcounter, which only provides a Decoder function, and it works perfectly fine this way.

This is up as a GitHub gist as well: [decoder.js](https://gist.github.com/tiefpunkt/9407f4049365c065fdd6905adf949993)
