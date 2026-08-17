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
What is Hotoe [3 min](#description) <br>
How we solve your problems [3 min](#problems-we-take-care-of) <br>
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

## Description

**Hotoe** is a quickshell alternative, built for fast prototyping between systems and open to new users.

Hotoe provides full web-stack experience, including:
+ sound APIs
+ 3D libraries
+ latest css styles 
+ DOM page structure

Your application will have one-file structure and will stay readable for any frontender. <br>
Hotoe promises you an application without any other backed besides JS, but also admitting that it will not be lightweight. <br>
Hotoe do not promise you anything less than **200mib usage** per app. After you finish your prototyping, if it does not fit your expectations, you can rewrite your app in any other language.

Some things we restrict and highly not recommend doing. Read the conepts of [EWAs](Ewa.md)
<br><br>

## Problems we take care of

<sub>1. Switching to another framework problem</sub><br>
You want to build a HUD, <br>
but learning Hotoe from scratch <br> 
then after prototyping your HUD learning another framework to optimize it might sound too much.<br>

But here's the catch: <br>
Hotoe do not ask you to "learn" anything.<br>
If you know JS — building with hotoe it is literally about aknowlegding existance of the second `navigator` on your page<br>

Hotoe follows this one rule, that is guarantees our minimalism — <br>
__"Prototyping language should be easy and comfortable to use. Comfortable enough to keep choosing it compare to heavy real frameworks"__

<sub>2. Loosing your previous environment</sub>
We storgly tolerate that, and admit that losing your your `npm`, `pip`, etc is not the way.<br>
Instead of trying to replace them, we have made a guide for you on how to bring your familiar toolkit to Hotoe!<br>
You will be able to translate your backend to your next (optimized) versions of the project.<br><br>
[How to connect any additional backend to Hotoe in 2 lines](Extensions.md)

<sub>3. Availability problems</sub><br>
You could not know, but your usual frameworks are not built to create widgets, menus and etc.. <br>
Here's a current situation in short:

| Framework | Layer Shell Support | DX (Web Tech) | Cross-Platform HUDs | The Catch |
| :--- | :---: | :---: | :---: | :--- |
| *Electron / Tauri / Wails* | No | **Great** | Limited | No native layer-shell / overlay support on Wayland |
| *GTK / Qt + Bindings* | **Native** | Painful | Linux Only | Much worse DX than web-tech stacks. Wayland-chained |
| **Hotoe** | **Native** | **Great** | **Yes** | **The catch?** |

No cross-platform solution introduced except Hotoe. That leads us to the next problem

<sub>4. Contributing issues</sub><br>
How my friend from MacOS will contribute if I use `layer_shell_qt`?<br>
He can't. He's forced to use QEMU or make platform bridges (it will still not look the same tho).

But with Hotoe now it is possible, of course. <br>
And this works with not-friends too btw. We expand the range of possible contributors for your project already from "picking a framework" stage of planning.

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

**Great!** It looks like an EWA already! But we're finishing this quick start here. It was really quick, as it should be. <br> 
From now on you are by yourself. Read [API docs](Fluent-X.md) or give it to your agent to study. Also one more gift tho... <br>
Don't treat them as personal limitations. They called manners for a reason —

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

