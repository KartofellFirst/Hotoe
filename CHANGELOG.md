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
