# 👻 Ghost Input

**Ghost Input** is a lightweight, aggressive browser extension designed to restore system integrity to your browsing experience. It force-enables clipboard actions (Copy, Cut, Paste), Context Menus (Right-Click), and Text Selection on websites that attempt to disable them.

Unlike standard extensions that just remove event listeners, Ghost Input injects directly into the page's **Main World** context and monkey-patches the browser's native Event prototypes. This renders the website's blocking scripts ineffective before they even run.

## 🚀 Features

-   **God Mode Copy/Paste:** Bypasses restrictions on `Ctrl+C`, `Ctrl+V`, `Ctrl+X`, and `Ctrl+A`.
-   **Right-Click Restoration:** Re-enables the context menu on sites that block it.
-   **Prototype Override:** Hooks into `Event.prototype.preventDefault` and `stopPropagation` to ignore blocking attempts at the browser engine level.
-   **Dynamic Cleanup:** Periodically nukes inline handlers (e.g., `<input onpaste="return false">`) from the DOM.
-   **Manifest V3:** Built using the latest Chrome Extension standards.

## 🛠️ How It Works

Most "anti-copy" scripts work by listening for an event (like `keydown` or `copy`) and calling `event.preventDefault()`.

**Ghost Input** counters this by redefining `preventDefault` in the page's execution context:

1.  **Injection:** The script registers a content script with `world: "MAIN"`, allowing it to share variables and prototypes with the website's own JavaScript.
2.  **The Bypass:** It wraps `Event.prototype.preventDefault`. If the event is related to the clipboard or context menu, the call is silently ignored.
3.  **The Result:** The website *thinks* it blocked your action, but the browser executes it anyway.

## 📦 Installation (Developer Mode)

Since this is a custom tool, you can install it as an unpacked extension:

1.  Clone this repository or download the ZIP.
2.  Open Chrome and navigate to `chrome://extensions/`.
3.  Toggle **Developer mode** in the top right corner.
4.  Click **Load unpacked**.
5.  Select the folder containing the `manifest.json` file.

## 📂 File Structure

-   `manifest.json` - Extension configuration and permissions (Scripting, Host Permissions).
-   `background.js` - Service worker that registers the content script in the MAIN world.
-   `content.js` - The core logic that overrides prototypes and cleans up the DOM.

## ⚠️ Disclaimer

This tool is created for educational purposes and personal system integrity. Please respect the intellectual property rights of content creators even if you are able to copy text.

---
Developed by **Hanish**.
