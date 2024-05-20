## Overview

Overview
This repository contains examples of how to use the Chrome Extensions API, including the Scripting API and User Scripts API. These examples demonstrate how to execute scripts in the context of web pages, modify web page content, and send messages between different parts of an extension.

##
## Features

Features
- **Script Injection**: Inject scripts into web pages at different stages of document loading (document_end, document_idle).
- **Content Modification**: Modify the web page content by changing the background color.
- **Messaging**: Send and receive messages between different parts of the extension (e.g., background scripts, popup scripts, and content scripts).

##
## Installation Instructions

Installation Instructions

1. **Clone the repository**:
   ```bash
   git clone https://github.com/EmiliaPaz/ChromeExtensions_Examples.git
   ```

2. **Open Chrome and navigate to the Extensions page**:
   - Type `chrome://extensions/` in the address bar.

3. **Enable Developer Mode**:
   - Toggle the switch in the top-right corner to enable Developer Mode.

4. **Load the extension**:
   - Click on the "Load unpacked" button.
   - Select the directory where you cloned the repository.

5. **Test the examples**:
   - Open a new tab and visit any website to see the scripts in action.
   - Open the extension's popup to interact with the manually triggered scripts.

##
## Usage Examples

Usage Examples

### Injecting Scripts 

Example of how scripts are injected from `background.js`:

```javascript
chrome.scripting.registerContentScripts(
  [{
    id: 'inject-script-purple',
    js: ['content_script_purple.js'],
    matches: ['<all_urls>'],
    runAt: 'document_end',
    world: 'MAIN'
  }]
);

chrome.scripting.registerContentScripts(
  [{
    id: 'inject-script-orange',
    js: ['content_script_orange.js'],
    matches: ['<all_urls>'],
    runAt: 'document_idle',
    world: 'MAIN'
  }]
);
```

### Modifying Web Page Content 

Example content script `content_script_purple.js` changes the background color to purple:

```javascript
console.log('content script register at document end (purple)');
document.body.style.background = 'purple';
```

### Messaging Between Scripts

Example of sending messages from `user_script.js`:

```javascript
// User script can send messages when 'messaging' is enabled.
async function sendMessage() {
  // Create button
  let button = document.createElement('button');
  button.textContent = 'Send Message';
  button.onclick = () => {
    chrome.runtime.sendMessage({ text: 'Hello from user script' }, (response) => {
      console.log(response);
    });
  };
  document.body.appendChild(button);
}
```

##
## Code Summary

Code Summary

### Scripting API

- **`background.js`**: Registers content scripts to be injected at different stages (e.g., `document_end`, `document_idle`).
- **`content_script_blue.js`**: Changes the background color to blue.
- **`content_script_green.js`**: Changes the background color to green.
- **`content_script_orange.js`**: Changes the background color to orange.
- **`content_script_purple.js`**: Changes the background color to purple.
- **`content_script_yellow.js`**: Changes the background color to yellow.
- **`popup.js`**: Handles interactions from the popup window, allows for dynamic script injections.

### User Scripts API

- **`background.js`**: Configures user scripting and registers a script for specific sites.
- **`user_script.js`**: Modifies the webpage by inserting div elements and handles messaging.
- **`popup/popup.js`**: Listens for and sends messages to the user script.

##
## License

License
This project is licensed under the MIT License. For more information, see the [LICENSE](LICENSE) file.

---

Feel free to explore and modify the examples provided to better understand how Chrome Extensions can enhance web pages and user interaction. Happy coding!