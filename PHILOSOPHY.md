
> [!TIP]
> Estimated reading time: *~10 mins*.  
> Dont be scared of big page length, we just have a lot of linebreaks ☺️  
> *(It is actually **more comfortable** to read if you've used to sit in Group chats / Comments / Forums)*

> [!CAUTION]
> Some parts of this .md can be displayed wrong on mobile devices. <a href="https://github.com/KartofellFirst/Hotoe/blob/main/PHILOSOPHY.md">Open in browser</a>
> 
> This text has been fact‑checked by AI. Feel free to open issues if you spot a mistake.
>
> <details><summary>additional pre-word</summary>Everything without a graphical presence at all (some CLI tools or background daemons) or web applications did not take place in our applications classification. This is not a blind spot –– it is just for simplification</details>


> [!IMPORTANT]
> **Terminology Guide**
>
> - **WM** - Window Manager (<a href="https://google.com/search?q=What Window Manager is as the type of software?">read more</a> if you're not familiar with the concept)  
> - **GTK application** - Application built with Gimp Toolkit (most likely cross-platform)
> - **HE** — Hotoe Engine (project shorthand)
> - **WA** — Workspace Application (core concept)
> - **SWA** - A WA that has been built with system-specific framework and not designed to be cross-platform 
> - **EWA** — Enhanced WA. Like games separated from apps, EWAs separated from WAs (core concept)
>
> *Some wise words at the end of the note:*  
> $${\color{gray}\""WAs\ developer\"\ is\  cringe\ to\ pronounce\ \text{—}\ nobody\ is\ going\ to\ call\ themselves\ that\.}$$  
> $\qquad$ $\qquad$ $\qquad$ $\qquad$ $\qquad$ $\qquad$ $\qquad$ $${\color{gray}Okay\,\ EWAs\ is\ a\ little\ better" \sim\ Drunk\ DeepSeek}$$ 
 
# PHILOSOPHY: *What cross-platform means. Window-centric model. New type of applications.*

When you're about to start a new project, you probably ask yourself one question before choosing a framework.

**Am I building an application, or am I building a game?**

Nobody finds that question strange.

Games have their own engines. Applications have their own frameworks. We've accepted this separation for decades.

But have you ever asked yourself **why**?

Is it because games need physics? 

3D rendering? 

Shaders? 

Networking?

No.

Those are consequences, not the reason why games have been separated long ago. 

The real difference is much simpler. **Games don't think in windows.**

You can't find `window.setAlwaysOnTop()` or `window.openPopup()` in Unity, Unreal or Godot.   

Why?  

Because they can't provide that kind of API? No &mdash;

Because they have realized that you dont need to fight every WM to create your own UI.

And this is actually the right solution. This separation has given games their own input handlers, their own focus management, and even their own graphics renderer. Games became stronger as a category of applications after they gave up some native functionality.

> Imagine your Minecraft inventory is opening in a separate window? That would look wildly exotic nowadays... 

Games became their own category the moment developers stopped thinking of a window as the application.

---

Now ask yourself another question.

**If I'm building a native cross-platform application...  
why does it automatically have to be a window?**

Not *can* be. *Has* to be.

Every modern framework quietly assumes exactly that &mdash;

Electron. 

Tauri.

GTK. 

Qt. 

Flutter. 

Different languages, different architectures, exactly the same assumption:

> Your application is managed by a Window Manager.

For most software, that's completely reasonable.  

A browser should have a window. A code editor should have a window. A spreadsheet should have a window.  

They're supposed to participate in the desktop. Users move them, resize them, tile them, fullscreen them, switch between them. The Window Manager is doing exactly what it's designed to do.

---

But what if your application doesn't belong there?

Suppose you want to build a beautiful clock that permanently lives in the corner of the screen. 

Or a system monitor. 

A desktop companion. 

A floating music widget. 

An ambient utility.

Why is the first thing every framework gives you a rectangular window? 

Why are you suddenly negotiating with a Window Manager **you never wanted to interact with**?

*Keep that question in mind, we'll get to the answer in a minute*

<br><br>

## You dont know what those apps that you call "system-specific" are actually built with
<!-- made it look like waybar were not designed to be only for Wayland. Sorry guys, i needed an example-->
Look at <a href="https://google.com/search?q=What is Waybar and analogs in MacOS / Windows">Waybar</a>. 

Does it look like a GTK application? &mdash; Not at all.

It looks like some privileged desktop component &mdash; something built with a special framework provided by the operating system *(SWA)*.

That's the illusion.

Underneath, Waybar is just another GTK application.

The interesting part isn't what it's built with.

The interesting part is what it has to become.

The moment these applications stop behaving like a normal window, every cross-platform abstraction disappears. 

Developers suddenly fall back to platform-specific APIs — Wayland's layer-shell, Windows overlays, macOS widgets. 

The application didn't fundamentally change. Only its relationship with the Window Manager did.

<br><br>

## Redefining the problem

So, the simplest application possible — a round analog clock. 

It doesn't need tabs. 

It doesn't need resize handles. 

It doesn't need tiling. 

It doesn't need fullscreen. 

It barely even needs focus. It simply exists.

Today, writing that clock means implementing it three different ways: a macOS widget, a Wayland layer-shell surface, a Windows desktop overlay. 

Not because clocks are platform-specific — because **our frameworks only know how to build windows.**

Ironically, the moment you wrap the exact same clock inside a normal rectangular frame and let the Window Manager control it, Electron, Tauri, Flutter and GTK suddenly become excellent cross-platform solutions again. 

The application didn't become more portable. It became more window-like.

---

This isn't a failure of Electron, GTK, or Qt. 

They're solving the problem they were created to solve: windowed applications.

The real problem sits one level higher:  

*We don't even have a mental category for software that intentionally avoids participating in window management.*

That's why desktop bars, overlays, floating widgets, HUDs and etc always feel like exceptions

---

Maybe we've been asking the wrong question all along.

Instead of asking *"Which framework should I use?"* — maybe we should first ask:

> **"Does my application actually want to be managed by a Window Manager?"**

If the answer is yes, today's frameworks are fantastic.  

If the answer is no... why do we pretend it's still the same kind of application?

Games earned their own engines because they separated application logic from window management. Our category deserves exactly the same shift — not because it needs another renderer or another programming language, but because it represents a fundamentally different relationship with the desktop.

Abstractly:  
**A window is not an application. A window is a service provided by a Window Manager. And not every application needs that service.**

Maybe applications that intentionally live **with** your workspace instead of **inside** it deserve a runtime of their own.

Not another <a href="https://google.com/search?q=What Electron is in short and what famous applications are built with it?">Electron</a>. A new category.

<br><br>

## What We're Building

We're building **Hotoe** — a cross-platform runtime for that missing category. 

Throughout this document, we'll refer to this category as **workspace applications**: something that renders on screen without asking the Window Manager to treat it as a normal window, and without contesting windowed apps for space or window-level status.

Hotoe is not an attempt to set up a WA monopoly &mdash;  

**Our goal is to define the philosophy and terminology and give it to the next generations of engines.**

Our ideas might not be revolutionary, they are just "in time". Watch Wayland-layer-shell documentation &mdash;

They have already separated WAs from Native applications and moving in the same direction as we are. 

Maybe in a decade Windows will get there too.

Maybe macOS will follow even later.

and Hotoe will be waiting, aged like a fine wine...

<details><summary>See Software classification diagram (click to expand)</summary>
  WAs will have their undercategory: EWAs  
  
  We cant call Waybar, Conky or Rainmeter EWAs because, unlike WAs, EWAs must be cross-platform. 
  ```mermaid
    graph TD
        Software[Software] --> A["Windowed Application: Software that interacts with the WM (has GUI). Can be cross-platform"]
        A --> N["Native application: operating different types of windows, surfaces and tiling options. Can be cross-platform"]
        A --> G["Game: only need one window. Operates Surfaces inside that window. Does not talk to the WM. Accent on being cross-platform"]
        A --> WA["Workspace Application: operates windows and surfaces in specific layers. Can be built with cross-platform framework, but cant be cross-platform due to the large range of system-specific funtions it has to contain"]
        WA --> EWA[EWA: only need one window in specific layer. Operates Surfaces inside that window. Does not talk to the WM. Accent on being cross-platform]
        EWA --> Hotoe["Hotoe EWA: only allowed to sit in overlay"]
        EWA --> E["Different Engine EWAs : Soon may appear engines that provide toolkits for other window layers"]
        Software --> SWA["SWA: WAs that built with system specific frameworks. Not made to be cross-platform"]
  ```
</details>

> [!NOTE]
> If you are building your own engine and want to adopt our philosophy, or even name your project something like "Better Hotoe" or "Hotoe - MyVision", let us know! We will gladly add a link to your project in our repository.

<br><br>

### What is Hotoe Engine after what we just defined?

Hotoe Engine is a framework for building **EWAs** (cross-platform workspace applications), that uses the world well-known HTML, CSS and JS stack with your system's native webview as its rendering engine

What limitations Hotoe applies to EWAs to make them cross-platform:
  1. EWA does not interact with WM at all. Not even  <a href="https://google.com/search?q=What is exclusive zone (wayland layer shell definition)">Exclusive zone</a>

What limitations Hotoe applies to its EWAs:
  1. Hotoe EWA lives in an overlay
  2. Hotoe EWA does not have fullscreen
  3. Hotoe EWA is not required to be rectangular
  4. Hotoe EWA receives full keyboard and pointer focus when the pointer enters the predefined region on your screen or when a predefined hotkey is triggered
  5. Hotoe EWA does not have system-provided window decorations. If you want to create exit button: you make it on your own (like in game engines)


<sub>With great attention to detail (and written in our best broken English), the Hotoe team thanks everyone who read this file all the way to this line. Welcome to the community! ♡</sub>

<!--Hotoe does not attempt to cover every possible kind of Workspace applications – it deliberately focuses on one subset: **overlay** workspace applications.
So Hotoe will NOT be supporting \<overlaysurface\>, \<backgroundsurface\> and \<lockscreensurface\> tags yet, as they must have different approach in their restrictions philosophy and probably different engines.  
For now it's just cleaner to have one \<surface\> tag in your index.html

$${\color{red}\text{With great attention to detail (and written in our best broken English),}}$$  
$${\color{red}\text{the Hotoe team thanks everyone who read this file all the way to this line.}}$$  
$${\color{red}\text{Welcome to the community!}}$$
-->
