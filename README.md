<h1><p align="center">Hotoe <img src="assets/logo/pwt.png" alt="logo" height="30"> <br>
The main repo of every Hotoe Engine. </p>
<p align="center">
    <img src="assets/shield.png" alt="header-logo" height="20">
    <img src="https://img.shields.io/static/v1?label=&message=Wayland&color=darkgreen&">
    <img src="https://img.shields.io/static/v1?label=&message=macOS&color=yellow&">
    <img src="https://img.shields.io/static/v1?label=&message=Windows&color=orange&">
    <img src="https://img.shields.io/static/v1?label=&message=aarch64&color=green&">
    <img src="https://img.shields.io/static/v1?label=&message=AMD64&color=green&">
</p>
</h1>

## Available platforms:
- [Linux (Wayland Session)](https://github.com/KartofellFirst/Hotoe-Wayland) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{darkgreen}stable}$$
- [MacOS](https://github.com/KartofellFirst/Hotoe-MacOS) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{yellow}planned}$$
- [Windows](https://github.com/FaultedSapiens/Hotoe-Windows) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{orange}alpha}$$
<br><br><br>

## Core concept
**Despite the normal applications, widgets creation starts from the frontend and deserves a frontend-first language — such as HTML.**

> [!IMPORTANT]
> Quick terminology guide: <br>
> [EWA](EWAs.md) — Enhanced Web Application (PWA analogy) <br>
> ⤷ _HUDs, menus, bars, floating widgets, etc._

**Hotoe** is a [quickshell](https://quickshell.org) alternative, built for fast creation and prototyping of the EWAs between operating systems. 

+ Minimalistic [JS API](Fluent-X.md) (Enough to build basic widgets (update system state values, open apps, execute scripts))
+ If you need one, connect any backend you want to your project in 2 lines. (We don’t require specific language like Node/Rust/C, connect any using IPC)
+ Real 1 minute [quick start](#one-minute-separates-you-from-your-hello-world-app) followed by further advices to improve your ideas
+ [The biggest](https://google.com/search?q=How%20big%20WEB%20dev%20community%20is?) community (Number of people who know HTML is 10th if not 100th times bigger than people who knows QML. It is way more likely to find contributors with Hotoe)
+ [Save](https://google.com/search?q=Why%20should%20I%20value%20my%20time?) time (Coding with fine-tuned high-level languages saves weeks of time even in medium-long projects and helps prototyping. That is why people choose Python over C/C++)


<br><br>
Popular questions -> [here](DeveloperQA.md) <br>
<b><sub>recommended</sub><br>Pages version of the repo -> [link](https://KartofellFirst.github.io/Hotoe)</b>
<br><br>


## Quick start 
*Requirements:*  
- Hotoe [<— how to install?](Installation.md)
- Basic HTML skills (optional)
<br><br>

**ONE minute separates you from your Hello World app** 
---
*Take your HTML frontend from whatever web app you have or use this default VSCode template below*

<details><summary>I don’t understand</summary>
It's fine, follow step by step: <br>
1. Create a folder for your project somewhere, to keep files organized <br>
2. Create a file named <code>index.html</code> in this folder <br>
3. Right-click it and open with your text editor (not browser) <br>
4. Paste the text from the template below into it and follow further steps
</details>

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
*Save and run this in your project's folder:*
```
hotoe run
```
**Done!**  
If you have figured out how to close it (click the "Hello World!" text if don't), I think we can finish this quickstart right here. <br>
For further instructions check [API docs](Fluent-X.md) or give it to your agent to study. <br>
You can also see our [projects gallery](Showcase.md) <br>

Our next recommendation will be: <br>
Limit your body's width and height<br>

```html 
<body style="max-width: 50%; max-height: 30%;" SIR>
```

and 

<details>
<summary>Read the manners list</summary>
<br>
<blockquote>
<br><ol>
<li>EWA <b>does not</b> cover full screen for a long time without giving user an opportunity to temporarily hide it or collapse it into something small — <br><hr> 
Your application has an advantage of user's system. It's above everything. As the carriers of such responsibility, we should always give user a choice.</li><br>
<li>EWA <b>preferably</b> is not managing external applications lifecycle. We always try to keep content on the surface (inside the box we've been given)<br><hr>
Exceptions: app launchers, docks or every other application whose main purpose is to help opening external windowed software or webpages.</li><br>
<li>EWA <b>does not</b> interact with the WM.<br><hr>Leave it to normal apps. If you want a normal window use other frameworks.<br>Things like exclusive zone are not allowed too (if you even know what is it). Think of a EWA more like a guest in user's system.</li><br>
<li>Everything that can be localized <b>must</b> be localized<br><hr>To keep your application snappy, sources must be pre-loaded. Ideally, your application has to be able to open offline.</li><br>
<li>No <b>embedded content</b> should have access to the API<br><hr>The only rule that secures your application. You must open external links in user's standard browser where they are sandboxed. <br>Things like JS libraries and iframe content better be pre-loaded, so no one can inject fxAPI calls into them unnoticed. </li><br>
<li>EWA decides itself how its UI looks. EWA's shapes are not necessarily rectangular. Minimize button might collapse, close button might minimize. We dont style your application with frames, dont tile them. We fight for EWA's beauty being untouched and we appreciate artists that bring life in their rises with our framework. <b>Don’t be scared</b> of making something unusual.</li><br>
<br></ol>
</blockquote>
</details>

**Welcome to the community!~**

<br><br>

## Contributing
We are always open to new ideas, bug reports, and contributions! If you want to help build the EWA ecosystem, feel free to submit a Pull Request or open an Issue.

Everyone who helps with the project get added to [NOTICE](NOTICE)

<br><br>

## License
This project is licensed under the [MIT License](LICENSE)

<br><br>

$${\color{gray}\sim\ With\ love\ from\ Hotoe\ Team\ \sim}$$

