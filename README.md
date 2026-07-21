
> [!CAUTION]
> This text has been refactored by AI to put my brainstorms into English markdown file.
> 
> Also, it has been fact-checked by the AI, so feel free to open issues if you see a mistake
>
> <details><summary>additional pre-word</summary>Everything without a graphical presence at all (some CLI tools or background daemons) or web applications did not take place in our applications classification. It's not a blind spot, it is just for simplification</details>


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
> N - placeholder for an actual product name
> 
> Namings are changable, open issues


## What We're Building

We're building **N** — a cross-platform runtime for that missing category. Not a replacement for Electron, Tauri, GTK, or Qt; those remain the right tool the moment an application genuinely wants to be a window. N exists for the applications that don't.

We call that category a **workspace component**: something that renders on screen without asking the Window Manager to treat it as a normal window, and without contesting windowed apps for space or window-level status.

We do not stop you from building your own workspace component engine, we want to build a philosophy and define some definitions.

What is N – N is a workspace component applications building framework, that uses world well-known HTML, CSS and JS stack with your system's native webview as the core

What N defines as a workspace component, so we can keep it cross-platform:
1. Workspace component lives in overlay (above system UI)
2. Workspace component does not interact with WM at all. Not even Exclusive zone
3. Workspace component does not have fullscreen
4. Workspace component is not necessary rectangular-shaped
5. Workspace component takes full keyboard and cursor focus when you enter defined region on your screen or use prebuilt hotkey
6. Workspace component is not surrounded by styled a window border. If you want to create exit button: you make it on your own (like in game engines)

Other conceptions like background-layer Workspace components are most likely going to be realised in separated repositories and frameforks, with their own conceptions. Technical part is going to be in another readme in the project, or even in the separate repository, i'll update later
