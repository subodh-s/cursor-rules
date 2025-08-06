# CursorRule: Chrome Extension for Cursor AI IDE

## Overview
This CursorRule provides a step-by-step guide to create a Chrome extension that integrates with the Cursor AI IDE, enabling enhanced productivity and custom features for users.

## Steps

1. **Set Up Project Structure**
   - Create a new directory for your Chrome extension.
   - Add the following files:
     - `manifest.json`
     - `background.js`
     - `content.js`
     - `popup.html`
     - `popup.js`

2. **Create `manifest.json`**
   - Define the extension metadata, permissions, and scripts.
   - Example:
     ```json
     {
       "manifest_version": 3,
       "name": "Cursor AI IDE Extension",
       "version": "1.0",
       "description": "Enhance Cursor AI IDE with custom features.",
       "permissions": ["activeTab", "storage"],
       "background": {"service_worker": "background.js"},
       "action": {"default_popup": "popup.html"},
       "content_scripts": [{
         "matches": ["<all_urls>"],
         "js": ["content.js"]
       }]
     }
     ```

3. **Implement Background Script (`background.js`)**
   - Handle extension events and messaging.
   - Example:
     ```js
     chrome.runtime.onInstalled.addListener(() => {
       console.log('Cursor AI IDE Extension installed.');
     });
     ```

4. **Create Content Script (`content.js`)**
   - Interact with web pages and inject features into Cursor AI IDE.
   - Example:
     ```js
     if (window.location.hostname.includes('cursor.so')) {
       // Inject custom UI or features
       console.log('Cursor AI IDE detected.');
     }
     ```

5. **Build Popup UI (`popup.html` & `popup.js`)**
   - Provide a user interface for extension actions.
   - Example `popup.html`:
     ```html
     <html>
     <body>
       <h1>Cursor AI IDE Extension</h1>
       <button id="run">Run Feature</button>
       <script src="popup.js"></script>
     </body>
     </html>
     ```
   - Example `popup.js`:
     ```js
     document.getElementById('run').addEventListener('click', () => {
       chrome.tabs.query({active: true, currentWindow: true}, (tabs) => {
         chrome.scripting.executeScript({
           target: {tabId: tabs[0].id},
           func: () => alert('Feature executed!')
         });
       });
     });
     ```

6. **Test and Package**
   - Load the extension in Chrome via `chrome://extensions` (Enable Developer Mode).
   - Test all features in the Cursor AI IDE.
   - Package and publish as needed.

---

This CursorRule provides a template for building Chrome extensions tailored for Cursor AI IDE. Customize scripts and UI as required for your use case.
