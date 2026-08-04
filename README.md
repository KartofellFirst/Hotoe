<img alt="demonstration">

# Hotoe
<!-- <sub><i>Add some extra sugar</i></sub> -->
The main repo of every Hotoe Engine. 
<br><br>

## Navigator: 
What is Hotoe [1 min](#description) <br>
When do I pick Hotoe [3 min](#is-hotoe-better) <br>
Switching to Hotoe is not a problem [2 min](#switching-to-hotoe-is-not-a-problem) <br>
Read the documentation [10 min](Fluent-X.md) <br>
Start with Hotoe [1 min](#one-minute-separates-you-from-your-hello-world-app) + Manners and stuff [4 min](#second-step-to-become-hotoe-user) <br>
Popular questions -> [here](DeveloperQA.md) <br>
**Pages version of the repo** -> [link](https://KartofellFirst.github.io/Hotoe)
<br><br>

## Available platforms:
- [Linux (Wayland Session)](https://github.com/KartofellFirst/Hotoe-Wayland) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{darkgreen}stable}$$
- [MacOS](https://github.com/KartofellFirst/Hotoe-MacOS) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{yellow}planned}$$
- [Windows](https://github.com/FaultedSapiens/Hotoe-Windows) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{orange}alpha}$$
<br><br><br>

## Description

**Hotoe** is a lightweight cross-platform application engine designed specifically for building desktop HUDs, bars, menus, and [EWAs](PHILOSOPHY.md) using standard Web technologies.

It abstracts low-level display layers (like Wayland's `layer_shell` or OS-native overlay surfaces) into a unified, zero-config HTML/CSS/JS runtime, powered by [Fluent-X Native Capabilities API](Fluent-X.md).

## Is Hotoe better?
For
- A frontend guy that just wants to build something native already
- Newbies in programming who want to customize their systems
- A tired appdev who’s done with big Electron/Tauri APIs and 20-minute “quick starts”
- Someone whose frontend is already a 10k+ line file and doesn’t want to figure out how to bolt Node or Rust on top of it

— YES.

The main thing we want you to understand about Hotoe is that this is not just another framework. Hotoe is built **specifically** for its type of applications. 

That is why our API is way shorter than whatever other frameworks can provide you with — we just don’t put any tools there that are not supposed to be.

You don’t learn ~~Node~~, don’t learn ~~Rust~~. **You already know basic JS and that's enough for an application**.

You won't find any other framework where the whole app fits into one .html file. It's either:
> "we have built a whole new language on top of JS"

or

> "build your pseudo-browser on Node to run your HTML frontend as an app"

because they don’t have the same approach as ours. **Hotoe ships its standards into the industry**

### Switching to Hotoe is not a problem
You may be thinking you are losing tools by switching to Hotoe. But you don’t have to lose your `npm`... 

[How to connect any additional backend to Hotoe in 2 lines](Extensions.md)

Hotoe does not require you to lock inside of its API. Hotoe built to build EWAs. And EWAs are embeddable and able to cooperate with normal apps. **We don’t restrict that, we provide toolkit for that.**

Switching to Hotoe is not a problem, it's the solution for the problem.

## The Alternatives
Here is our alternatives to compare and make sure we are better:

| Framework | Desktop Layer Support | DX (Web Tech) | Cross-Platform HUDs | The Catch |
| :--- | :---: | :---: | :---: | :--- |
| *Electron / Tauri / Wails* | No | **Great** | Limited | No native layer-shell / overlay support on Wayland |
| *GTK / Qt + Bindings* | **Native** | Painful | Linux Only | Much worse DX than web-tech stacks. Wayland-chained |
| **Hotoe** | **Native** | **Great** | **Yes** | Built only for EWAs — not for standard windowed apps |

That means in some cases Hotoe provides more flexibility than a normal framework.

<br><br>

## Quick start 
*Requirements:*  
- Hotoe  
- Basic HTML skills (optional)
<br><br>

**ONE minute separates you from your Hello World app** 
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
*Add `SIR` at the end of the `<body>` tag. And `CLOSE()` somewhere:*<br>
<sup>CLOSE() to close the application. SIR - Set as Input Region. Minimal requirements for every application: at least one way to close it + area to interact with it</sup>
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
Limit your body's width and height<br>

```html 
<body style="max-width: 50%; max-height: 30%;" SIR>
```

**Great!** Now, as your application does not cover full screen, you can call it <u>EWA</u>.  
EWAs are Hotoe applications that follow *Hotoe manners* list.  

<details>
<summary>Read manners list</summary>
<br>
<blockquote>
<br><ol>
<li>EWA <b>does not</b> cover full screen for a long time without giving user an opportunity to temporarily hide it or collapse it into something small — <br><hr> 
Your application has an advantage of user's system. It's above everything. As the carriers of such responsibility, we should always give user a choice.</li><br>
<li>EWA <b>preferably</b> is not managing external applications lifecycle. We always try to keep content on the surface (inside the box) we've been given<br><hr>
Exceptions: app launchers, docks or every other application whose main purpose is to help opening external windowed software or webpages.</li><br>
<li>EWA <b>does not</b> interact with the WM.<br><hr>Leave it to normal apps. If you want a normal window use other frameworks.<br>Things like exclusive zone are not allowed too (if you even know what is it). Think of a EWA more like a guest in user's system.</li><br>
<li>Everything that can be localized <b>must</b> be localized<br><hr>To keep your application snappy, sources must be pre-loaded. Ideally, your application has to be able to open offline.</li><br>
<li>No <b>embedded content</b> should have access to the API<br><hr>The only rule that secures your application. You must open external links in user's standard browser where they are sandboxed. <br>Things like JS libraries and iframe content better be pre-loaded, so no one can inject fxAPI calls into them unnoticed.</li><br>
<li>EWA decides itself how its UI looks. EWA's shapes are not necessarily rectangular. Minimize button might collapse, close button might minimize. We dont style your application with frames, dont tile them. We fight for EWA's beauty being untouched and we appreciate artists that bring life in their rises with our framework. <b>Don’t be scared</b> of making something unusual.</li><br>
<br></ol>
</blockquote>
</details>

[What else features do we have?](Fluent-X.md)<br>
Oh, we have.. **everything**. Except windows. You'll like it. Welcome to the community!

<br><br>

## Contributing
We are always open to new ideas, bug reports, and contributions! If you want to help build the EWA ecosystem, feel free to submit a Pull Request or open an Issue.

Everyone who helps with the project get added to [NOTICE](NOTICE)

<br><br>

## License
This project is licensed under the [MIT License](LICENSE)

<br><br>

$${\color{gray}\sim\ With\ love\ from\ Hotoe\ Team\ \sim}$$

