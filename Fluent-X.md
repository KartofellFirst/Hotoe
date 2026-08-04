# Fluent-X Native Capabilities API
Official shorthand is fxAPI. In JS it is named `fx`. <br>
`fxAPI` is fully supported by Hotoe engine and shipped within every EWA built with it<br>

Fluent-X API v1.0.0 toolkit contains 5 categories of methods:<br>
*absolute necessary* -> [visit](#basics) <br>
<sup>input regions management, closing an application and etc</sup><br>
*IPC related* -> [visit](#ipc-related-methods) <br>
<sup>communicate your JS backend to whatever other backend you want through local IPC</sup><br>
*Filesystem related* -> [visit](#file-system-api) <br>
<sup>write, open and remove files from disk right from your JS backend</sup><br>
*Local database* -> [visit](#json-atabase) <br>
<sup>store and read values from cache without managing files</sup><br>
*other* -> [visit](#other) <br>
<sup>global shortcuts and terminal commands execution</sup><br>

## Basics
Setting up the input region:<br>
<sup>SIR - Set as Input Region</sup>
> ```html
> <mytag SIR>
> ```
> Now application grabs focus as `<mytag>` hovered. Alternatively, you can add the `.hotoe-input-region-regulator-box` class to your tag to have the same effect without sacrificing classes.
>
> <details><summary>parses into (click):</summary>
> <pre><nobr>&lt;mytag class="hotoe-input-region-regulator-box"></nobr></pre></details>

Recalculating input regions after DOM updates:<br>
<sup>after resizing/moving/destroying elements</sup>
> ```javascript
> SIRs()
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.recalculateInputRegions()</nobr></pre></details>

Closing the application:

> ```javascript
> CLOSE()
> ```
> 
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.closeApplication()</nobr></pre></details> 


Managing focus events globally: <br>
<sup>when any of your input regions is receives or looses the pointer focus, this triggers</sup>
> ```javascript
> focus {
>     if (!focus) console.log("Cursor left the input region");
> }
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>window.addEventListener('focusEvent', function(event) {
>     const focus = event.detail;
>     if (!focus) console.log("Cursor left the input region");
> });</nobr></pre></details>

---

## IPC Related Methods

Publishing string into IPC:<br>
<sup>data will be stringified, no matter what you put there</sup>
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

Adding IPC message listener:<br>
<sup>`const message` will be pre-defined</sup>
> ```javascript
> receive {
>     push({"Got your message, dear backend!": message});
> }
> ```
> 
> <details><summary>parses into (click):</summary>
> <pre><nobr>window.addEventListener('busMessage', function(event) {
>     const message = event.detail;
>     fx.pushString({"Got your message, dear backend!": message})
> });</nobr></pre></details>

---

## File System API

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
<sup>this, of course, works with global paths too</sup>
> ```javascript
> read("essay.txt")
>     .then(file => console.log(file.content))
>     .catch(err => console.log("File missing or unreadable:", err));
> ```
> 
> In this usecase `file` contains:
> 1. `type` *(string)* — text
> 2. `mime` *(string)* — mimetype of the file
> 3. `content` *(string)* — raw file content
>
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.requestFileContent("essay.txt")</nobr></pre></details>

Reading binary files / Opening images:
> To load local images or binary assets into the DOM, put their content as URI in source:
> ```javascript
> read("$PICTURES/bg.png").then(file => document.querySelector('img').src = file.content);
> ```
>
> In this usecase `file` contains:
> 1. `type` *(string)* — binary
> 2. `mime` *(string)* — mimetype of the file
> 3. `encoded` *(string)* — raw base64-encoded string
> 4. `content` *(string)* — complete data URI, ready to be assigned to `src` or `href`
>
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.requestFileContent("$PICTURES/bg.png")</nobr></pre></details>

Creating or writing files (String or Base64):<br>
<sup>`.then()` and `.catch()` also work here if needed</sup>
> ```javascript
> // Write plain text
> write("~/MY_APP/main.txt", "Hello World!");
>
> // Write raw binary/image data from a Base64 string (3rd argument = true)
> write("$CACHE/MY_APP/saved_image.png", base64String, true);
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.writeFile(&lt;arguments>)</nobr></pre></details>

Deleting a file:<br>
<sup>`.then()` and `.catch()` also work here if needed</sup>
> ```javascript
> remove("$CACHE/MY_APP/temp.txt");
> ```
> <details><summary>parses into (click):</summary>
> <pre><nobr>fx.removeFile("$CACHE/MY_APP/temp.txt")</nobr></pre></details>

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

## Other Utilities
Setting up a global hotkey combination:<br>
<sup>works even when your app loses focus</sup>
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

Embedding template environment variables:
> ```javascript
> const ipc_socket_address = {% LOCAL_BUS_ADDRESS %};
> ```
