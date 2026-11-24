<h1><p align=center>v0.3.0</p></h1>

A lot of work has gone into bug fixes in this release, and honestly, it should have been v0.1.0 instead of the original release.

It also brought some cool new features that drastically improved the DX in some projects.

The next version will introduce new concepts and completely reject the old philosophy with EWA rules

<h3><p align=center>Wayland</p></h3>

_Input regions are now declared using HTML attributes instead of classes:_

```html
<mydiv sir></mydiv>
```
<br>

_Added the ability to set input regions manually:_

```js
SIRs({manual: [
    [0, 0, 200, 300],
    [200, 300, 500, 200],
    ...
]})
```
<br>

**Fixed IPC issues** when connecting an additional backend. Added new communication paths with JS.<br>
_Read about it more detailed in [Fluent-X.md](Fluent-X.md#connecting-additional-backend-to-hotoe)_

**Hhotkeys has been removed**. <br>
<sub>For global hotkeys, it is now recommended to create separate daemons and launch them using `exec(..., daemon=true)`. <br>
Alternatively, you can create separate CLI applications and install them on the user's computer using `write()`, then make them executable with `exec("chmod +x ...")`.</sub>

Added support for **complex input regions**, including complex `clip-path` shapes, rounded corners, and rotations. <br>

Input regions can now be disabled not only by removing the attribute, but also by setting `pointer-events: none`, `display: none`, or `visibility: hidden`, or by adding the `active="false"` attribute.

<h3><p align=center>CLI</p></h3>

Fixed an issue where repeated compilation caused recursion and increased the archive size. <br>
_(by adding `app.zip` to `ignore_names` during copying)_

Removed the SIR parser from the CLI. It has been replaced with built-in HTML mechanisms, which should be more reliable.

Added the `update` function to reinstall engine files after updating the CLI. Make sure to run it, or manually remove the old files from `~/.cache/hotoe`.

<br><br><br><br>

<h1><p align=center>v0.2.0</p></h1>

v0.2.0 was focused on improving DX without losing support of the old applications built with hotoe v0.1.0

In most cases, you will be able to just run `hotoe run` in your old project folder and get zero new errors

<h3><p align=center>Wayland</p></h3>

<i>major part of the sugar syntax was replaced with pure JS</i>

now you can 

```js
setInterval(SIRs, 3000);
setTimeout(CLOSE, 200);
// etc
```

instead of wrapping it into another function

new constant added: `SIR = "hotoe-input-region-regulator-box"`

```js
myelement.classList.add(SIR); SIRs();
```
 
to dynamically make your elements interactive

<h3><p align=center>Parser</p></h3>

The `SIR` parser has been updated — you can now add it to elements that already have a class attribute set <br>
e.g.:
```html
<div class="container" SIR>              -> <div class="container hotoe-input-region-regulator-box">
<div class="container" SIR id="kotik">  -> <div class="container hotoe-input-region-regulator-box" id="kotik">
```
