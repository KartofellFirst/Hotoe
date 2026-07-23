
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
> - **GTK application** - Application bult with Gimp Toolkit (most likely cross-platform)
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

Is it because games need physics? 3D rendering? Shaders? Networking?

No. Those are consequences, not the reason why games have been separated long ago. 

The real difference is much simpler. **Games don't think in windows.**

You cant find `window.setAlwaysOnTop()` or `window.openPopup()` in Unity, Unreal or Godot.   
Why? Because they cant provide that kind of API? No - because they have realised that you dont need to fight every WM to create your own UI.

And this is actualy the right solution, this separation has given games their own input handlers, their own focus management and even their own graphics renderer. Games has became stronger as the type of applications after they gave up some of their native functionality.

> Imagine your Minecraft inventory is opening in a separated window? That would look wildly exotic nowadays... 

Games became their own category the moment developers stopped thinking of a window as the application.

---

Now ask yourself another question.

**If I'm building a native cross-platform application...  
why does it automatically have to be a window?**

Not *can* be. *Has* to be.

Every modern framework quietly assumes exactly that. Electron. Tauri. GTK. Qt. Flutter. Different languages, different architectures, exactly the same assumption:

> Your application is managed by a Window Manager.

For most software, that's completely reasonable.  
A browser should have a window. A code editor should have a window. A spreadsheet should have a window.  
They're supposed to participate in the desktop. Users move them, resize them, tile them, fullscreen them, switch between them. The Window Manager is doing exactly what it's designed to do.

---

But what if your application doesn't belong there?

Suppose you want to build a beautiful clock that permanently lives in the corner of the screen. Or a system monitor. A desktop companion. A floating music widget. An ambient utility.

Why is the first thing every framework gives you a rectangular window? Why are you suddenly negotiating with a Window Manager you never wanted to interact with?

---

Look at <a href="https://google.com/search?q=What is Waybar and analogs in MacOS / Windows">Waybar</a>. Does it look like a GTK application? Not at all. It looks like some privileged desktop component — something built with a special framework provided by the operating system.

That's the illusion. Because underneath, Waybar is just another GTK application. GTK applications don't normally look like that. Yet Waybar proves they can.

The same is true for Conky. Rainmeter. Übersicht. None of them are powered by some magical "widget engine." They all begin life as ordinary applications built with ordinary technologies — GTK, Qt, WebViews.  

The surprising part isn't what they're built with. The surprising part is what they have to become.

The moment these applications stop behaving like windows, every cross-platform abstraction disappears. Developers suddenly fall back to platform-specific APIs — Wayland's layer-shell, Windows overlays, macOS widgets. The application didn't fundamentally change. Only its relationship with the Window Manager did.

---

Think about how strange that is.

Imagine the simplest application possible — a round analog clock. It doesn't need tabs. It doesn't need resize handles. It doesn't need tiling. It doesn't need fullscreen. It barely even needs focus. It simply exists.

Today, writing that clock means implementing it three different ways: a macOS widget, a Wayland layer-shell surface, a Windows desktop overlay. 

Not because clocks are platform-specific — because **our frameworks only know how to build windows.**

Ironically, the moment you wrap the exact same clock inside a normal rectangular frame and let the Window Manager control it, Electron, Tauri, Flutter and GTK suddenly become excellent cross-platform solutions again. The application didn't become more portable. It became more window-like.

---

This isn't a failure of Electron, GTK, or Qt. They're solving the problem they were created to solve: windowed applications.

The real problem sits one level higher:  
*We don't even have a mental category for software that intentionally avoids participating in window management.*

Today we recognize two kinds of cross-platform graphical software: games and windowed desktop applications. Everything else gets awkwardly squeezed into one of them. That's why desktop bars, overlays, floating widgets, HUDs and etc always feel like exceptions instead of first-class citizens.

---

Maybe we've been asking the wrong question all along.

Instead of asking *"Which framework should I use?"* — maybe we should first ask:

> **"Does my application actually want to be managed by a Window Manager?"**

If the answer is yes, today's frameworks are fantastic.  

If the answer is no... why do we pretend it's still the same kind of application?

Games earned their own engines because they separated application logic from window management. Our category deserve exactly the same shift — not because it needs another renderer or another programming language, but because they represent a fundamentally different relationship with the desktop.

Abstractive:  
**A window is not an application. A window is a service provided by a Window Manager. And not every application needs that service.**

Maybe applications that intentionally live **with** your workspace instead of **inside** it deserve a runtime of their own.

Not another Electron. A new category.

---

<!--
> [!NOTE]
> Decrypt:
> <details><summary> HE, WA, EWA, EWAs</summary>
> HE - Hotoe Engine shortening
>
> WA - Workspace Application abbreviation
>
> EWA - Enchanced WA. We're going to use this word later because it sounds a lot better and it technically fits
> ALSO: EWA - Enchanced Web Application. Can be used since our main stack rn contains web technologies. Easely memorazable to the people who are familiar with PWA term.
> </details>
> Namings are changable, open issues
-->


## What We're Building

We're building **Hotoe** — a cross-platform runtime for that missing category. Not a replacement for Electron, Tauri, GTK, or Qt; those remain the right tool the moment an application genuinely wants to be a window. Hotoe exists for the applications that don't.

Throughout this document, we'll refer to this category as **workspace applications**: something that renders on screen without asking the Window Manager to treat it as a normal window, and without contesting windowed apps for space or window-level status.

Hotoe is not an attempt to own this category. Our goal is to define the philosophy and terminology, not to prevent alternative runtimes from existing.

*We are not first to invent this kind of software. We are giving it a name.* 

<details><summary>What existing software already considered WA or EWA?</summary>
  WAs will have their undercategory: EWAs  
  
  We cant call Waybar, Conky or Rainmeter EWAs because, unlike WAs, EWAs must be cross-platform. 
  ```mermaid
    graph TD
        Software[Software] --> A["Windowed Application: Software that interacts with the WM (has GUI). Can be cross-platform"]
        A --> N["Native application: operating different types of windows, surfaces and tiling options. Can be cross-platform"]
        A --> G["Game: only need one window. Operates Surfaces inside that window. Does not talk to the WM. Accent on being cross-platform"]
        A --> WA["Workspace Application: operates windows and surfaces in specific layers. Can be build with cross-platform framework, but cant be cross-platform due to the large range of system-specific funtions it has to contain"]
        WA --> EWA[EWA: only need one window in specific layer. Operates Surfaces inside that window. Does not talk to the WM. Accent on being cross-platform]
        EWA --> Hotoe["Hotoe EWA: only allowed to sit in overlay"]
        EWA --> E["Different Engine EWAs : Soon may appear engines that provide toolkits for other window layers"]
        Software --> SWA["SWA: WAs that built with system specific frameworks. Not made to be cross-platform"]
  ```
</details>

> [!NOTE]
> If you're making an engine for background / lockscreen / whatever else layer and want to name it like.. "Better Hotoe" or "Hotoe Background' - let us know, we'll add link to your project to the repository


### What is Hotoe Engine after what we just defined?

Hotoe Engine is a framework for building **EWAs** (cross-platform workspace applications), that uses world the well-known HTML, CSS and JS stack with your system's native webview as its rendering engine

What limitations Hotoe applies to EWAs to make them cross-platform:
  1. EWA does not interact with WM at all. Not even  <a href="https://google.com/search?q=What is exclusive zone (wayland layer shell definition)">Exclusive zone</a>

What limitations Hotoe applies to its EWAs:
  1. Hotoe EWA lives in an overlay
  2. Hotoe EWA does not have fullscreen
  3. Hotoe EWA is not required to be rectangular
  4. Hotoe EWA receives full keyboard and pointer focus when the pointer enters the predefined region on your screen or when a predefined hotkey is triggered
  5. Hotoe EWA does not have system-provided window decorations. If you want to create exit button: you make it on your own (like in game engines)

Hotoe does not attempt to cover every possible kind of Workspace applications – it deliberately focuses on one subset: **overlay** workspace applications.
So Hotoe will NOT be supporting \<overlaysurface\>, \<backgroundsurface\> and \<lockscreensurface\> tags yet, as they must have different approach in their restrictions philosophy and probably different engines.  
For it's just cleaner to have one \<surface\> tag in your index.html ()

