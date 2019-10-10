# Web Accessibility Beacons

## Current status

Withdrawn in favor of competing [Media Queries Level 5](https://drafts.csswg.org/mediaqueries-5/) - it covers nearly all the features proposed by WAB, and despite lacking any privacy controls to speak of, seems to be the preferred choice by the community at large.

## Abstract

Web Accessibility Beacons draft specification proposes a standardized mechanism that allows website developers to request accessibility information from web clients. This allows developers to adapt web content for improved accessibility.

## Goal

Allow for website designers and developers to receive essential accessibility information to make web content more accessible for everyone.

This main goal of this standard specification is to allow for dynamic content adaption to the specific needs of the user - adjustment of font spacing, font size, font type, colors and color combinations, and similar.

This standard aims to make web accessibility commonplace and frictionless to both web users and web developers.

## Current TODO

1. Define user workflow for enabling the Accessibility Beacons API;
2. Develop a simple, common standard API;
3. Propose and standardize the specification (WHATWG).
4. Current client API is vulnerable to timing attacks allowing actors to fingerprint the device based on WAB enabled/disabled state. This needs to be addressed.

## Conformance

The key words "MUST", "MUST NOT", "REQUIRED", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in the normative parts of this specification are to be interpreted as described in [RFC2119](https://www.ietf.org/rfc/rfc2119.txt).

## Implementation

Accessibility Beacons consists of browser workflow and client API. The browser workflow allows for the end-user to configure predefined accessibility options for browser installation. 

The client API allows for websites to request accessibility hints from web browsers which implement Accessibility Beacons API.

### Client API

This standard proposes a new JavaScript API that allows website developers access to aforementioned beacon values.

```js
if (!('Accessibility' in window)) {
    // No support for Accessibility api
}

else if (Accessibility.permission === 'granted') {
    // Access already granted
    var options = Accessibility.options; // array of beacons: ['dyslexia', ...]
    // Adjust the content etc.
}

else if (Accessibility.permission !== 'denied') {
    // Request access
    Accessibility.requestPermission().then(function (permission) {
        if (permission === 'granted') {
            var options = Accessibility.options; // array of beacons: ['dyslexia', ...]
            // Adjust the content etc.
        }
    });
}
```

### Accessibility Beacons
Valid Accessibility Beacons are listed here.

*Note*: This list is subject to change while more research is done to determine what conditions to communicate and how.

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

### Browser implementation

Web browsers MAY request or suggest the user select accessibility beacons to expose during the initial installation of the browser software.

Web browsers MUST request the user to select accessibility beacons the first time Accessibility API permission is requested by a website IF the user has not already explicitly dismissed the Accessibility API feature before.

Web browsers MUST allow the user to dismiss the Accessibility API feature for current software installation or given end-user when user preferences are synchronized between several installations.

When end-user has dismissed the Accessibility API feature, the client API should always return "denied" permission status whenever Accessibility API permission is requested by a website, without prompting end-user input.

Web browsers MAY preselect Accessibility API beacons for the end-user depending on the end-users environment.

Web browser MUST request explicit permission from the end-user to expose Accessibility Beacons to websites. 

Web browser MUST NOT re-request previously denied Accessibility Beacons permission to end-user within a scope of a single domain name.

Web browser MUST request explicit permission from the end-user to expose Accessibility Beacon for each specific domain visited when Accessibility API permission is requested. Permission granted or declined MUST NOT extend to subdomains. 

Web browser MUST allow the user to manage access grants to domains in the configuration options of the web browser.

### Example browser feature workflows

#### Workflow A

New installation, new user, browser prompt enabled by the vendor, user declines.

1.User installs web browser with Accessibility Beacons feature;
2. User is prompted to enable accessibility beacons;
3. User declines the feature;
4. All permission requests from websites return "denied" without user prompt;

The browser MUST allow the user to enable and configure Accessibility Beacons feature in the browser configuration options.

#### Workflow B

Browser upgrade, Accessibility Beacons feature introduced, browser prompt enabled by the vendor, user declines.

1. User installs an update with Accessibility Beacons feature;
2. User is prompted to enable accessibility beacons;
3. User declines the feature;
4. All permission requests from websites return "denied" without user prompt;

The browser MUST allow the user to enable and configure Accessibility Beacons feature in the browser configuration options.

#### Workflow C

Accessibility Beacons feature enabled and configured by the user, the user visits a website. The website has not been previously granted or declined access to Accessibility Beacons feature.

1. Website requests access to Accessibility Beacons feature;
2. User is prompted to grant or decline access accessibility beacons for this website;
3. User grants access to the Accessibility Beacons feature
4. All further permission requests from website domain return "granted" without user prompt;

The browser SHOULD allow the user to easily withdraw the access grant for the domain that is currently being viewed.

## Contributing

You are free to contribute suggestions and pull requests to this specification. All content contributions
must be submitted using the same license(s) used for the specification itself, and you must explicitly say so
in the pull request.

## License

All non-software content published here is dedicated to public domain under the terms and conditions of 
[CC0 1.0 Universal Public Domain Dedication](./LICENSE_CONTENT.txt).

All source code, software designs, examples of and any other software content is dedicated to public domain under the terms 
and conditions of [Unlicense](./LICENSE_SOFTWARE.txt)
