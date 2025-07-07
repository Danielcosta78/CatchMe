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
        hiddenWebDriver: { enabled: true, weight: 3 }, // WebDriver is present but hidden (common in bot evasion)
        untrustedEvents: { enabled: true, weight: 3 }, // Input events not triggered by a real user (e.g. via JS)
        webdriver: { enabled: true, weight: 2 }, // Standard WebDriver detection (navigator.webdriver = true)
        headless: { enabled: true, weight: 2 }, // Headless browser detected (e.g., headless Chrome)
        linearMouseMovement: { enabled: true, weight: 2 }, // Mouse moves in straight lines (not natural)
        tooPerfectDelays: { enabled: true, weight: 2 }, // Interaction delays are too precise or repetitive
        suspiciousUA: { enabled: true, weight: 1 }, // Suspicious or uncommon User-Agent string
        fakeLanguages: { enabled: true, weight: 1 }, // navigator.languages is empty or spoofed
        fakePermissions: { enabled: true, weight: 1 }, // navigator.permissions returns unrealistic or static values
        windowDimensionsMatch: { enabled: true, weight: 1 }, // Outer and inner window sizes match perfectly (common in bots)
        fontRenderingFailed: { enabled: true, weight: 1 }, // Failure in rendering fonts (headless/browserless environments)
        canvasFingerprintMismatch: { enabled: true, weight: 1 }, // Canvas fingerprint doesn't match expected values (spoofed)
        noPlugins: { enabled: true, weight: 0.5 }, // navigator.plugins is empty (unusual for normal browsers)
        performanceTooFast: { enabled: true, weight: 0.5 }, // Page loads or responses are unnaturally fast
        rapidClicks: { enabled: true, weight: 0.5 }, // Too many clicks in a short time (bot-like behavior)
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
