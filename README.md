# Hotoe

*Add some extra sugar*

The main repo of every Hotoe Engine. 

*Content:*  
Philosophy [6 min](#why) <br>
Read the documentation [10 min](fxAPI.md) <br>
Start with Hotoe [1 min](#1-minute-separates-you-from-your-hello-world-app) + Manners and stuff [4 min](#second-step-to-become-hotoe-user) <br>
Popular questions -> [here](DeveloperQA.md) <br>
Pages version of a website -> [link](https://KartofellFirst.github.io/Hotoe)

## Available platforms:
- [Linux (Wayland Session)](https://github.com/KartofellFirst/Hotoe-Wayland) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{orange}alpha}$$
- [MacOS](https://github.com/KartofellFirst/Hotoe-MacOS) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{yellow}planned}$$
- [Windows](https://github.com/FaultedSapiens/Hotoe-Windows) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{orange}alpha}$$
<br><br>

## Quick start 
*Requirements:*  
- Hotoe  
- Basic HTML skills (optional)
<br><br>

**1 minute separates you from your Hello World app** 
---
*Take your HTML frontend from whatever web app you have or use this default VSCode template below*
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Hello World!</h1>
</body>
</html>
```
---
*Add `SIR` at the end of the `<body>` tag. And `CLOSE()` somewhere:*
```html
<body SIR> <!-- this should do -->
    <h1 onclick="CLOSE()">Hello World!</h1>
</body>
```
---
*Run this in your project's folder:*
```
Hotoe run
```
**Done!**  
Hope you figured out how to close it...

---
### Second step to become Hotoe user
Now try limiting your body's width and height:

```html
<body style="max-width: 50%; max-height: 30%;" SIR>
```
<details>
<summary>SIR?</summary>
<i><code>SIR</code> — Set as Input Region. <br>
<code>SIRs()</code> in JS — Set Input Regions (update them after resize / move / remove IRs)</i>
<br><br>

```javascript
// You can also declare SIR by adding this class to your entity
class="hotoe-input-region-regulator-box"
```

</details>&nbsp; 

Now your application does not cover full screen and you can call it ***EWA***.  
EWAs are Hotoe applications that follow *Hotoe manners* list.  

<details>
<summary>Read manners list</summary>
<br>
<blockquote>
<br><ol>
<li>EWA <b>does not</b> cover full screen for a long time without giving user an opportunity to temporarily hide it or collapse it into something small — <br><hr> 
Your application has an advantage of user's system. Its above everything. As the carriers of such responsibility, we should always give user a choice.</li><br>
<li>EWA <b>preferably</b> is not managing external applications lifecycle. We always try to keep content on the surface (inside the box) we've been given. <br><hr>
Exceptions: app launchers, docks or every other application whose main purpose is to help opening external windowed software or webpages</li><br>
<li>EWA does not interact with the WM. Leave it to normal apps and do your best in the surface you've been given<br><hr>Things like exclusive zone will kill all future cross-platform developing comfort we're planning on creating as they are currently impossible to emulate on other platforms</li><br>
<li>Everything that can be localized should be localized.<br><hr>To keep your application snappy, sources must be pre-loaded. Ideally, your application has to be able to open offline</li><br>
<li>EWA decides itself how its UI looks. EWA's shapes might be unusual. Minimize button might collapse, close button might minimize. We dont style your application with frames, dont tile them. We fight for EWA's beauty being untouched and we appreciate artists that bring life in their rices with our framework</li><br>
<br></ol>
</blockquote>
</details>
<br>

[What else features do we have?](fxAPI.md)
Oh, we have.. **everything**. Except windows. You'll like it. Welcome to the community!

---

<br><br>
## Why?

### The problem
Another day trying to configure my Hyprland rice and thinking of making my own Waybar led me to one issue nobody takes seriously currently — Wayland layer shell protocol. 

No framework supports this thing directly:  
**Electron**, **Tauri**, **Wails**, **Neutralino** cant help you with that <br>
**Qt**, **GTK** have binds, but that's honestly not the ideal. 

Wayland deliberately separated itself from normal application's logic. They say "some applications deserve special treatment and they have to be built specifically using layer_shell protocol"

It's not Electron's fault it doesn't support layers on Wayland. It's not any framework's fault at all. Wayland is one to blame here, because they wanted to show off and be different, and ended up in a situation where half cross-platform applications break on Hyprland as if they were vibecoded.. popups look like windows, buttons fly off the screen (I am not being overdramatic)

But was Wayland wrong? If you think more deeply about that, they actually had a point. There is a type of software that deserves to be treated differently. Maybe it's just that we weren't ready to accept this yet.

### Current solutions are not the solutions
As I said before gtk-layer-shell is not ideal, but I must admit that currently it is the best way to solve layer-shell problem. 

Using these Python GObject binds in a week I've already been able to build most of the visual I needed using GTK renderer. That proves it's not completely garbage and even has its charm, but there is no way this thing is more comfortable than HTML, CSS and JS

You can set up a webview in GTK but that still requires learning signals, GObject, webview features, layer-shell things, GTK styles, etc. 

### Hotoe is the solution. 

Hotoe is a layer_shell wrapper that takes all these responsibilities on itself, providing you with your familiar web renderer as the surface in a non-standard window layer. 

You keep your backend inside of your JS. Hotoe provides a minimal toolkit your application can wish for:  
- local database 
- writing and opening files
- execute terminal commands
- bind global hotkeys

Like [PWAs](https://google.com/search?q=Progressive%20Web%20Application%20cons%20and%20pros%20compare%20to%20Electron-like%20frameworks), but with actual freedom and not browser-dependent.

**OR**

In Hotoe you can connect any backend you want in 2 lines
```javascript
push(data) // to send
receive { console.log(message) } // to receive
```
Simple IPC. Connect Python/Go/Node/Rust, we dont restrict that. Run your scripts right from JS using `exec()`.

### EWA
> [!NOTE]
> EWA - Enhanced Workspace/Web Application <br>
> WM - Window Manager [?](https://google.com/search?q=what%20is%20a%20window%20manager%20in%20every%20desktop%20OS)

Going further — <br>
What if Wayland philosophy isn't that bad? Let me rephrase it so it becomes more clear:

**A window is not an application. A window is a service provided by a Window Manager. And not every application needs that service.**

It's not the exact point, but just my vision of it. And maybe they are right?

Why have to build every app with Tauri and figuring out how to remove decorations in my Rust backend or how to deal with tiling, rect-like windows, etc if I can just use this *framework from Linux called Hotoe*?


### Strategy
If EWAs prove that they are a mature enough category of applications, we will make sure that Hotoe is runnable on other platforms aside from Linux. 

You will be able to develop it on macOS, test on Windows and use on Wayland — that's what Electron is loved for, it's cross-platform, but not built for our cases of use.

Bring unix here
