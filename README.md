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
<script src="https://cdn.jsdelivr.net/gh/Danielcosta78/CatchMe@main/cdn/captcha.js"></script>
```

3. Configure with your settings:
```javascript
<script>
    // CAPTCHA Configuration - Add this before loading the CAPTCHA script
    window.captchaConfig = {
        licenseKey: "SC-ACTIVATE-1234-5678-ABCD", // To remove the mark Powered by CatchMe
        redirectUrl: '#',  // Redirection URL (use '#' if handling via callback)
        
        /* Optional settings below */
        maxAttempts: 3,    // Maximum allowed attempts before lockout
        captchaTitle: 'Security Verification',
        captchaInstructions: 'Solve the simple math problem to continue',
        successMessage: 'Verification successful!',
        containerId: 'captcha-container',  // ID of your container element
        
        // Callback functions
        onSuccess: function() {
            // Handle successful verification
            alert('CAPTCHA validation passed!');
            // Enable your form submission here
        },
        onFailure: function(attempts) {
            // Handle failed attempts
            console.warn(`CAPTCHA failed after ${attempts} attempts`);
        },
        onInit: function() {
            // Runs when CAPTCHA loads
            console.log('CAPTCHA initialized successfully');
        },
        
        // Custom CSS overrides
        customStyle: `
            /* Main container */
            .captcha-container {
                background: #f8f9fa !important;
                border: 1px solid #dee2e6 !important;
            }
            
            /* Title text */
            .captcha-title {
                color: #2c3e50 !important;
            }
            
            /* Verify button */
            .verify-button {
                background: #3498db !important;
                transition: all 0.3s ease !important;
            }
            
            /* Hover state for button */
            .verify-button:hover {
                background: #2980b9 !important;
            }
            
            /* Input field */
            .answer-input {
                border: 2px solid #ddd !important;
            }
            /* ↓ more ↓
            .captcha-instructions
            .equation-container
            .equation-display
            .refresh-button
            .status-message
            .status-message.success
            .status-message.error */
        `
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
<script src="https://cdn.jsdelivr.net/gh/Danielcosta78/CatchMe@main/cdn/botdetector.js"></script>
```

3. Configure detection:
```javascript
<script>
    window.BotDetector.init({
      licenseKey: "",
      silent: false,
      callback: (results) => {
        // add your callback here
        // example
        if (results.isHuman) {
            console.log("Human detected - proceed");
            // Enable form submission, grant access, etc.
            document.getElementById('submit-btn').disabled = false;
        } else {
            console.warn("Bot detected - take action");
            // Disable features or show warning
            document.getElementById('secure-content').style.display = 'none';
        }
      },
      // Styles (optional)
      button: {
        text: "Verify Now",
        verifyingText: "Verifying...",
        successText: "Verified",
        failText: "Failed",
        styles: {
          background: "#4a6fa5",
          color: "#fff",
          borderRadius: "4px",
          fontSize: "16px",
          minWidth: "120px",
          minHeight: "40px",
          boxSizing: "border-box",
        },
        verifyingStyles: {
          background: "#6c757d",
          cursor: "not-allowed",
        },
        successStyles: {
          background: "#28a745",
        },
        failStyles: {
          background: "#d32f2f",
        },
      },
      resultMessage: {
        successText: "Human detected!",
        failText: "Bot detected!",
        styles: {
          marginTop: "5px",
          fontSize: "14px",
          fontWeight: "500",
          color: "#333",
          textAlign: "center",
          display: "block",
          position: "relative",
          background: "rgba(255, 255, 255, 0.9)",
          padding: "5px 10px",
          borderRadius: "4px",
          zIndex: "1000",
        },
        successStyles: {
          color: "#28a745",
        },
        failStyles: {
          color: "#d32f2f",
        },
      },
      buttonContainer: {
        selector: "#verification-button",
        inheritStyles: true,
      },
      // WARNING changing the parameters may cause malfunction
      conditions: {
        /* === Automation Detection === */
        hiddenWebDriver: { enabled: true, weight: 4 },       // Selenium/Puppeteer
        headlessBrowser: { enabled: true, weight: 3 },       // Chrome Headless
        automationTools: { enabled: true, weight: 3 },       // Tools like Cypress
  
        /* === Browser Analysis === */
        suspiciousUA: { enabled: true, weight: 3 },          // Invalid User-Agent
        browserPlugins: { enabled: true, weight: 2 },        // Missing plugins
        cookieSupport: { enabled: true, weight: 1 },         // Blocked cookies
        localStorage: { enabled: true, weight: 1 },          // Disabled localStorage
  
        /* === User Behavior === */
        linearMouseMovement: { enabled:   true, weight: 2 },   // Robotic movements
        keyboardPatterns: { enabled: true, weight: 2 },      // Artificial typing
        inactivityTimeout: { enabled: true, weight: 1 },     // No human interaction
  
        /* === Fingerprinting === */
        canvasFingerprint: { enabled: true, weight: 2 },     // Anomalous rendering
        webGLMetadata: { enabled: true, weight: 2 },         // Fake GPU
        audioContext: { enabled: true, weight: 1 },          // Inconsistent audio API
  
        /* === Geolocation === */
        timezoneDiscrepancy: { enabled: true, weight: 1 },    // Timezone vs IP
        languageDiscrepancy: { enabled: true, weight: 1 },    // Language vs location
        screenResolution: { enabled: true, weight: 1 },       // Suspicious resolution
  
        /* === Device Analysis === */
        touchSupport: { enabled: true, weight: 1 },          // Simulated touch
        deviceMemory: { enabled: true, weight: 1 },          // Anomalous memory
        hardwareConcurrency: { enabled: true, weight: 1 }    // CPU cores
      },
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
- `licenseKey`: Remove "Powered by" branding ($10 one-time fee)
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
