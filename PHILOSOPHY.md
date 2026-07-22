
> [!CAUTION]
> This text has been partically refactored by AI to put my brainstorms into a single English markdown file.
> 
> It has also been fact‑checked by AI, so feel free to open issues if you spot a mistake.
>
> <details><summary>additional pre-word</summary>Everything without a graphical presence at all (some CLI tools or background daemons) or web applications did not take place in our applications classification. This is not a blind spot –– it is just for simplification</details>


# Stop Thinking About Windows

When you're about to start a new project, you probably ask yourself one question before choosing a framework.

**Am I building an application, or am I building a game?**

Nobody finds that question strange.

Games have their own engines. Applications have their own frameworks. We've accepted this separation for decades.

But have you ever asked yourself **why**?

Is it because games need physics? 3D rendering? Shaders? Networking?

No. Those are consequences.

The real difference is much simpler. **Games don't think in windows.**

Unity, Unreal and Godot never ask you to create a popup window for your inventory. They don't expose APIs like `window.openPopup()` or `window.setAlwaysOnTop()` because game UI isn't something the operating system manages. The game owns its own interaction model. The operating system simply gives it a surface to draw on. Everything else belongs to the engine.

Games became their own category the moment developers stopped thinking of a window as the application.

---

Now ask yourself another question.

**If I'm building a native cross-platform application... why does it automatically have to be a window?**

Not *can* be. *Has* to be.

Every modern framework quietly assumes exactly that. Electron. Tauri. GTK. Qt. Flutter. Different languages, different architectures, exactly the same assumption:

> Your application is managed by a Window Manager.

For most software, that's completely reasonable. A browser should have a window. A code editor should have a window. A spreadsheet should have a window. They're supposed to participate in the desktop. Users move them, resize them, tile them, fullscreen them, switch between them. The Window Manager is doing exactly what it's designed to do.

---

But what if your application doesn't belong there?

Suppose you want to build a beautiful clock that permanently lives in the corner of the screen. Or a system monitor. A desktop companion. A floating music widget. An ambient utility.

Why is the first thing every framework gives you a rectangular window? Why are you suddenly negotiating with a Window Manager you never wanted to interact with?

---

Look at Waybar. Does it look like a GTK application? Not at all. It looks like some privileged desktop component — something built with a special framework provided by the operating system.

That's the illusion. Because underneath, Waybar is just another GTK application. GTK applications don't normally look like that. Yet Waybar proves they can.

The same is true for Conky. Rainmeter. Übersicht. None of them are powered by some magical "widget engine." They all begin life as ordinary applications built with ordinary technologies — GTK, Qt, WebViews, native toolkits. The surprising part isn't what they're built with. The surprising part is what they have to become.

The moment these applications stop behaving like windows, every cross-platform abstraction disappears. Developers suddenly fall back to platform-specific APIs — Wayland's layer-shell, Windows overlays, macOS widgets. The application didn't fundamentally change. Only its relationship with the Window Manager did.

---

Think about how strange that is.

Imagine the simplest application possible — a round analog clock. It doesn't need tabs. It doesn't need resize handles. It doesn't need tiling. It doesn't need fullscreen. It barely even needs focus. It simply exists.

Today, writing that clock means implementing it three different ways: a macOS widget, a Wayland layer-shell surface, a Windows desktop overlay. Not because clocks are platform-specific — because **our frameworks only know how to build windows.**

Ironically, the moment you wrap the exact same clock inside a normal rectangular frame and let the Window Manager control it, Electron, Tauri, Flutter and GTK suddenly become excellent cross-platform solutions again. The application didn't become more portable. It became more window-like.

---

This isn't a failure of Electron, GTK, or Qt. They're solving the problem they were created to solve: windowed applications.

The real problem sits one level higher. We don't even have a mental category for software that intentionally avoids participating in window management.

Today we recognize three kinds of graphical software: games, windowed desktop applications, and terminal applications. Everything else gets awkwardly squeezed into one of them. That's why desktop bars, overlays, floating widgets, HUDs and ambient utilities always feel like exceptions instead of first-class citizens.

---

Maybe we've been asking the wrong question all along.

Instead of asking *"Which framework should I use?"* — maybe we should first ask:

> **"Does my application actually want to be managed by a Window Manager?"**

If the answer is yes, today's frameworks are fantastic. If the answer is no... why do we pretend it's still the same kind of application?

Games earned their own engines because they separated application logic from window management. Desktop utilities deserve exactly the same shift — not because they need another renderer, not because they need another programming language, not because they need HTML or WebViews, but because they represent a fundamentally different relationship with the desktop.

A window is not an application. A window is a service provided by a Window Manager. And not every application needs that service.

Maybe applications that intentionally live **with** your workspace instead of **inside** it deserve a runtime of their own.

Not another Electron. A new category.

---

> [!NOTE]
> **Terminology Guide**
>
> - **HE** — Hotoe Engine (project shorthand)
> - **WA** — Workspace Application (core concept)
> - **EWA** — Enhanced WA / Enhanced Web Application
>
>   *We'll use EWA going forward — it sounds better, fits both contexts, and is easily memorable to those familiar with PWA.*
>   $${\color{gray}\"WAs\ \-\ cringe\ to\ pronounce\.\ EWAs\ \-\ sounds\ perfect\ to\ me\"\ \sim\ Kidai}$$
>
> *Names are not final — open issues to discuss.*
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

*Hotoe is not an attempt to own this category. Our goal is to define the philosophy and terminology, not to prevent alternative runtimes from existing.*

So which existing applications, that are not system built-in, are already **workspace applications**?
Waybar is a workspace application, Conky too...   
See? They are **not cross-platform, but still considered workspace applications** – mark that  
*We are not inventing this kind of software. We are giving it a name.*

### What is Hotoe Engine after what we just defined?

Hotoe Engine is a framework for building cross-platform workspace applications, that uses world the well-known HTML, CSS and JS stack with your system's native webview as its rendering engine

Hotoe does not attempt to cover every possible kind of Workspace applications – it deliberately focuses on one subset: **overlay** workspace applications.

What limitations Hotoe applies for your application, so we can define a standard:
1. HE Workspace application lives in an overlay (above system UI)
2. HE Workspace application does not interact with WM at all. Not even Exclusive zone
3. HE Workspace application does not have fullscreen
4. HE Workspace application is not required to be rectangular
5. HE Workspace application receives full keyboard and pointer focus when the pointer enters the predefined region on your screen or when a predefined hotkey is triggered
6. HE Workspace application does not have system-provided window decorations. If you want to create exit button: you make it on your own (like in game engines)

HE workspace application is now an encanced conception of WA, so they are going to be called $${\color{aquamarine}EWAs}$$.

~ AGAIN –– Hotoe will NOT be supporting \<overlaysurface\>, \<backgroundsurface\> and \<locksccreensurface\> tags, because from my (creator) point of view, they must have different approach in their restrictions philosophy (maybe you would want an exclusive zone on a bg widget?) and it's just cleaner to have one <surface> tag in your .html  
So Hotoe ONLY serves OVERLAY applications

> [!NOTE]
> Want to start building your own engine for background layer and put its link or philosophy here?
>
> – open a discussion
