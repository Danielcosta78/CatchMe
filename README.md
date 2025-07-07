# CatchMe CAPTCHA & Bot Detection

A lightweight, customizable CAPTCHA and bot detection solution that protects your website without frustrating users.

## Features

✅ **Lightweight** - Just 71KB JavaScript delivered via CDN  
✅ **Effective Protection** - Blocks bots while remaining user-friendly  
✅ **Customizable** - Adjust appearance and behavior to match your site  
✅ **Bot Detection** - Advanced verification with configurable conditions  
✅ **Easy Integration** - Simple 3-step implementation  

## Installation

### CAPTCHA Implementation

1. Add the container div where you want the CAPTCHA to appear:
```html
<div id="captcha-container"></div>
```

2. Include the CDN script (preferably before `</body>`):
```html
<script src="https://catchmecaptcha.vercel.app/cdn/catchme.js"></script>
```

3. Configure with your settings:
```javascript
<script>
window.captchaConfig = {
    licenseKey: "YOUR_LICENSE_KEY", // Remove "Powered by" branding
    containerId: 'captcha-container',
    onSuccess: function() {
        // Handle successful verification
    }
    // See full configuration options in documentation
};
</script>
```

### Bot Detection Implementation

1. Add the container div:
```html
<div id="verification-button"></div>
```

2. Include the detection script:
```html
<script src="https://catchmecaptcha.vercel.app/cdn/botdetector.js"></script>
```

3. Configure detection:
```javascript
<script>
window.BotDetector.init({
    buttonContainer: {
        selector: "#verification-button"
    },
    callback: (results) => {
        console.log("Verification results:", results);
    }
    // See full configuration options
});
</script>
```

## Configuration Options

### CAPTCHA Options
- `licenseKey`: Remove "Powered by" branding ($10 one-time fee)
- `maxAttempts`: Failed attempts before lockout (default: 3)
- `captchaTitle`: Custom title text
- `customStyle`: CSS overrides for complete styling control
- Callbacks: `onSuccess`, `onFailure`, `onInit`

### Bot Detection Options
- `conditions`: Configure detection parameters (UA checks, mouse movement etc.)
- `button`: Customize verification button appearance
- `resultMessage`: Style success/failure messages
- `silent`: Run detection without UI elements

## Live Demo

See CatchMe in action on our [demo page](https://catchmecaptcha.vercel.app)

## License

Remove "Powered by CatchMe" branding with a one-time $10 license:
[![Buy Now](https://www.paypalobjects.com/en_US/i/btn/btn_buynowCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MV2RQ75CA8S82)

## Support

For issues or feature requests, please [open an issue](https://github.com/Danielcosta78/)

---

© 2025 CatchMe CAPTCHA | [Visit Website](https://catchmecaptcha.vercel.app)
