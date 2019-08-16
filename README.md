# Web Accessibility Beacons

## Abstract

Web Accessibility Beacons draft specification proposes a standardized mechanism that allows websites to request and receive accessibility information that should be considered when content is presented to a visitor.

## Goal

Allow for website designers and developers to receive essential accessibility information to make web content more accessible for everyone.

This main goal of this standard specification is to allow for dynamic content adaption to the specific needs of the user - adjustment of font spacing, font size, font type, colors and color combinations, and similar.

This standard aims to make web accessibility commonplace and frictionless to both web users and web developers.

## Current TODO

1. Define user workflow for enabling the Accessibility Beacons API 
2. Develop a simple, common standard API
3. Standardize the API (WHATWG)

## Conformance

The key words "MUST", "MUST NOT", "REQUIRED", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in the normative parts of this specification are to be interpreted as described in [RFC2119](https://www.ietf.org/rfc/rfc2119.txt).

## Technical implementation

Valid Accessibility beacons are listed here.

This list might expand or change while the specification is not finalized.

|Value|Description|
|-------|-------------|
|`dyslexia`|Adapt content for [dyslexia](https://en.wikipedia.org/wiki/Dyslexia)|
|`protanopia`<sup>1</sup>|Adapt content for [protanopia](https://en.wikipedia.org/wiki/Color_blindness#Protanopia)|
|`deuteranopia`<sup>1</sup>|Adapt content for [deuteranopia](https://en.wikipedia.org/wiki/Color_blindness#Deuteranopia)|
|`tritanopia`<sup>1</sup>|Adapt content for [tritanopia](https://en.wikipedia.org/wiki/Color_blindness#Tritanopia)|
|`achromatopsia`<sup>1</sup>|Adapt content for [achromatopsia](https://en.wikipedia.org/wiki/Achromatopsia)|
|`high-contrast`|Adapt content for [reduced contrast sensitivity](https://en.wikipedia.org/wiki/Contrast_(vision)#Contrast_sensitivity_and_visual_acuity)|
|`pse`|Adapt content for [photosensitive epilepsy](https://en.wikipedia.org/wiki/Photosensitive_epilepsy)|
|`screen-reader`|Adapt content to [screen-readers](https://en.wikipedia.org/wiki/Screen_reader)|

**Notes**

<sup>1</sup> - Only one value of MUST be sent at any given time (TODO: verify).

### High level API proposal

This standard proposes a new JavaScript API that allows website developers access to aforementioned beacon values.

```js
if (!('Accessibility' in window)) {
    // No support for Accessibility api
}

else if (Accessibility.permission === 'granted') {
    // Access already granted
    var options = Accessibility.options; // array: ['dyslexia', ...]
    // Adjust the content etc.
}

else if (Accessibility.permission !== 'denied') {
    // Request access
    Accessibility.requestPermission().then(function (permission) {
        if (permission === 'granted') {
            var options = Accessibility.options; // array: ['dyslexia', ...]
            // Adjust the content etc.
        }
    });
}
```

## Contributing

You are free to contribute suggestions and pull requests to this specification. All content contributions
must be submitted using the same license(s) used for the specification itself, and you must explicitly say so
in the pull request.

## License

All non-software content published here is dedicated to public domain under the terms and conditions of 
[CC0 1.0 Universal Public Domain Dedication](./LICENSE_CONTENT.txt).

All source code, software designs, examples of and any other software content is dedicated to public domain under the terms 
and conditions of [Unlicense](./LICENSE_SOFTWARE.txt)
