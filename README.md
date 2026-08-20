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

### Navigator:
What is Hotoe [1 min](#core-concept) <br>
Why would I choose it? [2 min](#why-would-i-choose-it) <br>
Start with Hotoe [1 min](#one-minute-separates-you-from-your-hello-world-app) + Manners and stuff [4 min](#second-step-to-become-hotoe-user) <br>
Read the documentation [10 min](Fluent-X.md) <br>
Popular questions -> [here](DeveloperQA.md) <br>
Showcase gallery -> [here](Showcase.md) <br>
<b><sub>recommended</sub><br>Pages version of the repo -> [link](https://KartofellFirst.github.io/Hotoe)</b>
<br><br>

## Available platforms:
- [Linux (Wayland Session)](https://github.com/KartofellFirst/Hotoe-Wayland) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{darkgreen}stable}$$
- [MacOS](https://github.com/KartofellFirst/Hotoe-MacOS) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{yellow}planned}$$
- [Windows](https://github.com/FaultedSapiens/Hotoe-Windows) &nbsp;&nbsp;&nbsp;&nbsp; $${\color{orange}alpha}$$
<br><br><br>

## Core concept

**Hotoe** is a quickshell alternative, built for fast creation and prototyping of the [EWAs](EWAs.md) (HUD's, bars, menus, etc) between systems using HTML. 

Despite the normal applications, widgets creation starts from the frontend and needs a frontend-first language — such as HTML.

<br><br>


## Why would I choose it?
This section will be more personal, because I'm going to talk directly to you

<a href="https://google.com/search?q=Why%20should%20I%20value%20my%20time?">Do you value your time?</a> — <br>
<br>
。<br>
。<br>
。<br>
<br>
Seriously, people stopped to value their time. You start it as a fan project, but after 2-3 month of debugging/updating/improving/growing a community around it — the time you could save on writing it with HTML is starting to count in *weeks*. 

Now, does at least **one week** of your time / time of your contributors worth **100MiB** RAM usage difference? Or even a **1000MiB**? 

> **1000MiB** of DDR5 RAM is about $15 in the RAM shortage period in case you want actual numbers

But you waste not one week, not two.

HTML is optimized for its job, it has one of the largest communities to join. But what are QML pros to compare? — RAM? Something else? You really think that covers on a normal PC?

Use Quickshell for your old laptop and Hotoe for actual projects. Don’t waste your and your contributors time if you respect them

<br>

### Also
If you have chosen Hotoe, here are other advantages we give you:
+ Connect any backend you want to your project in 2 lines. (We don’t require one specific language like Node/Rust/C)
+ Contributors from WEB (The oldest design community is now your community too)
+ Minimalistic JS API (you want to just poll fastfetch? Yes, you can. Without C++, right from your frontend)

<br><br>

## Quick start 
*Requirements:*  
- Hotoe [<— how to install?](Installation.md)
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

**Great!**<br>
But we're finishing this quick start here. It was really quick, as it should be. <br> 
For further instructions check [API docs](Fluent-X.md) or give it to your agent to study. <br>
Additionally, you can read Hotoe manners list: 

<details>
<summary>Read manners list</summary>
<br>
<blockquote>
<br><ol>
<li>EWA <b>does not</b> cover full screen for a long time without giving user an opportunity to temporarily hide it or collapse it into something small — <br><hr> 
Your application has an advantage of user's system. It's above everything. As the carriers of such responsibility, we should always give user a choice.</li><br>
<li>EWA <b>preferably</b> is not managing external applications lifecycle. We always try to keep content on the surface (inside the box we've been given)<br><hr>
Exceptions: app launchers, docks or every other application whose main purpose is to help opening external windowed software or webpages.</li><br>
<li>EWA <b>does not</b> interact with the WM.<br><hr>Leave it to normal apps. If you want a normal window use other frameworks.<br>Things like exclusive zone are not allowed too (if you even know what is it). Think of a EWA more like a guest in user's system.</li><br>
<li>Everything that can be localized <b>must</b> be localized<br><hr>To keep your application snappy, sources must be pre-loaded. Ideally, your application has to be able to open offline.</li><br>
<li>No <b>embedded content</b> should have access to the API<br><hr>The only rule that secures your application. You must open external links in user's standard browser where they are sandboxed. <br>Things like JS libraries and iframe content better be pre-loaded, so no one can inject fxAPI calls into them unnoticed.</li><br>
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

