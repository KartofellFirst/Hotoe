# Fluent-X Native Capabilities API
Official shorthand is fxAPI. In JS it is named `fx`. <br>
`fxAPI` is fully supported by Hotoe engine and shipped within every EWA built with it<br>

Fluent-X API v1.0.0 toolkit contains 5 categories of methods:<br>
*absolute necessary* -> [visit](#surface-management) <br>
<sup>input regions management, closing an application and etc</sup><br>
*IPC related* -> [visit](#ipc-related-methods) <br>
<sup>communicate your JS backend to whatever other backend you want through local IPC</sup><br>
*Filesystem related* -> [visit](#file-system-api) <br>
<sup>write, open and remove files from disk right from your JS backend</sup><br>
*Local database* -> [visit](#json-atabase) <br>
<sup>store and read values from cache without managing files</sup><br>
*other* -> [visit](#other) <br>
<sup>global shortcuts and terminal commands execution</sup><br>

# not finished

### Surface Management 
Setting up the input region:
> ```html
> <body SIR>...whatever...</body> <!--SIR - Set as Input Region-->
> ```
> Now `<body>` prevents clicks through the transparent webview overlay. Alternatively, add the `.hotoe-input-region-regulator-box` class manually.

Recalculating input regions after DOM updates (resizing/moving elements):
> ```javascript
> SIRs(); // Recalculates bounding boxes
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.recalculateInputRegions()</nobr></pre></details>

Managing focus events globally: <br>
<sup>when any of your input regions is receives or looses the pointer focus, this triggers</sup>

> ```javascript
> focus {
>     if (!focus) {
>         console.log("Cursor left the input region");
>     }
> }
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>window.addEventListener('focusEvent', function(event) {
>     const focus = event.detail;
>     if (!focus) {
>         console.log("Cursor left the input region");
>     }
> });</nobr></pre></details>

### IPC Related Methods

Publishing string into IPC:
> ```html
> <button onclick="push('button clicked')"></button>
> ```
> *IPC server:*
> ```bash
> button clicked
> ```
> 
> <details><summary>parses into (click):</summary>
> <pre><nobr>button onclick="fx.pushString('button clicked')"</nobr></pre></details>

Adding IPC message listener:
> ```javascript
> receive {
>     console.log(message);
>     push("Got your message, dear backend!");
> }
> ```
> 
> <details><summary>parses into (click):</summary>
> <pre><nobr>window.addEventListener('busMessage', function(event) {
>     const message = event.detail;
>     console.log(message);
>     push("Got your message, dear backend!");
> });</nobr></pre></details>

---

### File System API

All file operations support path shortcuts like `~/` (home directory) or `$CONFIG/`.
<details><summary>Full list of supported shortcuts (click)</summary>
  
  - `$DOWNLOADS`  
  - `$DOCUMENTS`  
  - `$DESKTOP`  
  - `$VIDEOS`  
  - `$PICTURES`  
  - `$MUSIC`   
  - `$CONFIG`  
  - `$DATA`  
  - `$CACHE`  
  - `$HOME`  
</details>

Reading text files & checking existence:
> ```javascript
> read("~/Hotoe/main.py")
>     .then(file => console.log(file.content))
>     .catch(err => console.log("File missing or unreadable:", err));
> ```
> 
> In this usecase `file` contains:
> 1. `type` *(string)* — text
> 2. `mime` *(string)* — mimetype of the file
> 4. `content` *(string)* — formed data URI for fast loading into src attributes
>
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.requestFileContent("~/Hotoe/main.py")</nobr></pre></details>

Reading binary files / Opening images:
> To load local images or binary assets into the DOM, set them directly as a data URL source:
> ```javascript
> // 
> read("~/Hotoe/assets/icon.png", true).then(file => { document.querySelector('#avatar').src = file.content });
> ```
>
> In this usecase `file` contains:
> 1. `type` *(string)* — binary
> 2. `mime` *(string)* — mimetype of the file
> 3. `encoded` *(string)* — raw encoded base64 content
> 4. `content` *(string)* — formed data URI for fast loading into src attributes
>
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.requestFileContent("~/Hotoe/assets/icon.png")</nobr></pre></details>

Creating or writing files (String or Base64):
> ```javascript
> // Write plain text
> write("~/Hotoe/main.txt", "Hello World!");
>
> // Write raw binary/image data from a Base64 string (3rd argument = true)
> write("~/Hotoe/saved_image.png", base64String, true)
>     .then(() => console.log("Image binary saved!"))
>     .catch(err => console.error(err));
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.writeFile("~/Hotoe/saved_image.png", base64String, true)</nobr></pre></details>

Deleting a file:
> ```javascript
> remove("~/Hotoe/temp.txt");
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.removeFile("~/Hotoe/temp.txt")</nobr></pre></details>

Scanning directories:
> ```javascript
> scan("~/Hotoe").then(dir => {
>         dir.items.forEach(item => {
>             const [name, path, isDir, size] = item;
>             console.log(`${isDir ? "📁" : "📄"} ${name} (${size} bytes)`);
>         });
>     });
> ```
> Each item in `dir.items` returns a fixed 4-element array:
> 1. `name` *(string)* — File name (`"main.py"`)
> 2. `path` *(string)* — Full resolved path (`"/home/user/Hotoe/main.py"`)
> 3. `isDir` *(boolean)* — `true` if directory, `false` if file
> 4. `size` *(number)* — File size in bytes
>
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.scanDirectory("~/Hotoe")</nobr></pre></details>

---

### Input Regions & Focus



---

### Hotkeys
Setting up a global hotkey combination, that works even when your app loses focus:
> ```javascript
> hotkey("SUPER+D", "myevent")
> 
> /* you can setup events listener immediately
> or only after user allows registration (hotkey(...).then(e => / user allowed registration logic / ))
> or warn him after he refused to do that (hotkey(...).catch(e => / user declined the request logic /))
> */
> window.addEventsListener("myevent", function (e) {
>     push("user just pressed SUPER+D!")
> })
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.registerHotkey()</nobr></pre></details>
>
> <details><summary>Wayland problems (click)</summary>
> Unfortunately, on Wayland reading global keyboard events is impossible.  
> 
> We've solved this problem by shipping small CLI utility inside our Wayland backend, but even this do not guarantee that after user allows the registration, he will not forget to bind combination to his config or will not bind it to another key combination.  
>  
> If event in `.then(event)` block returns with `{"method": "manually"}` - you must keep in mind the human factor it contains.
> </details>


---

### Other Utilities

Embedding template environment variables:
> ```javascript
> const ipc_socket_address = {% LOCAL_BUS_ADDRESS %};
> ```

Closing the application:
> ```javascript
> CLOSE();
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.closeApplication()</nobr></pre></details>
