# COMPONENTS — Brutalist Command Snippet Library

Reusable HTML patterns for the "Brutalist Command" design system. Each block below is a copy-ready fragment with a one-line use note. Read `DESIGN.md` for the philosophy. Read `examples/*.html` for full assembled pages.

All snippets assume the page boots Tailwind via CDN, loads Space Grotesk + Material Symbols Outlined, and applies the body baseline:
```html
<body style="background-color:#050505; color:#e5e2e1; font-family:'Space Grotesk', sans-serif;">
```

---

## 1. Color Token Reference

Use these hex values verbatim. Every flash of color must be a meaningful signal.

| Token | Hex | Role |
|---|---|---|
| `background` | `#050505` | Viewport foundation. Dead space. |
| `surface-container-low` | `#0A0A0A` | Primary panel background. |
| `surface-container` | `#131313` | Sub-panel inside a panel. |
| `surface-container-high` | `#2A2A2A` | Inner card / focus area / `<code>`. |
| `surface-container-highest` | `#353534` | Maximum elevation tier. |
| `primary` (cyan) | `#00FFFF` | Active data, interactive states, accents. |
| `on-primary` | `#003737` | Text on solid cyan blocks. |
| `on-surface` | `#e5e2e1` | Default body copy. |
| `on-surface-variant` | `#B9CAC9` | Secondary body copy. |
| `outline` (muted) | `#4B5563` | Inactive metadata, ghost borders (15% opacity). |
| `error` | `#FF0000` | Destructive / failure status. |
| `warning` | `#FFBF00` | Caution status. |

---

## 2. TopNavBar

Use at the top of every page. Fixed; the brand label sits left, page links center, utility icons right. Active link gets the cyan underline.

```html
<header class="flex justify-between items-center w-full px-8 h-16 z-50 bg-[#0A0A0A] fixed top-0 left-0 border-b border-[#4B5563]/15">
    <div class="text-[1.25rem] font-bold text-[#00FFFF] tracking-widest font-['Space_Grotesk'] uppercase">DOCUMENTATION</div>
    <nav class="hidden md:flex items-center space-x-12">
        <a class="font-['Space_Grotesk'] uppercase tracking-[0.1em] text-[0.875rem] text-[#00FFFF] border-b-2 border-[#00FFFF] pb-1" href="index.html">README</a>
        <a class="font-['Space_Grotesk'] uppercase tracking-[0.1em] text-[0.875rem] text-[#4B5563] hover:text-[#00FFFF] transition-colors" href="pages/architecture.html">ARCHITECTURE</a>
        <a class="font-['Space_Grotesk'] uppercase tracking-[0.1em] text-[0.875rem] text-[#4B5563] hover:text-[#00FFFF] transition-colors" href="pages/reference.html">REFERENCE</a>
    </nav>
    <div class="flex items-center space-x-6">
        <span class="material-symbols-outlined text-[#4B5563] hover:text-[#00FFFF] cursor-pointer">search</span>
        <span class="material-symbols-outlined text-[#4B5563] hover:text-[#00FFFF] cursor-pointer">settings</span>
    </div>
</header>
```

---

## 3. SideNavBar with Sectored Nav Items

Use as the page's left rail. Group links under `SECTOR / NN` labels in muted gray; active link uses cyan text on a `#0A0A0A` background.

```html
<aside class="fixed left-0 top-16 h-[calc(100vh-64px)] w-64 bg-[#050505] flex flex-col border-r border-[#4B5563]/15 overflow-y-auto z-40 hidden md:flex">
    <nav class="flex-1 mt-4">
        <div class="px-6 py-2 text-[#4B5563] font-['Space_Grotesk'] uppercase tracking-[0.2em] text-[0.6875rem]">SECTOR / 01</div>
        <a href="index.html" class="block px-6 py-2 text-[#00FFFF] text-[0.875rem] uppercase tracking-[0.1em] bg-[#0A0A0A]">README</a>
        <a href="pages/install.html" class="block px-6 py-2 text-[#4B5563] hover:text-[#00FFFF] hover:bg-[#0A0A0A] text-[0.875rem] uppercase tracking-[0.1em]">INSTALL</a>
        <div class="px-6 py-2 mt-6 text-[#4B5563] font-['Space_Grotesk'] uppercase tracking-[0.2em] text-[0.6875rem]">SECTOR / 02</div>
        <a href="pages/reference.html" class="block px-6 py-2 text-[#4B5563] hover:text-[#00FFFF] hover:bg-[#0A0A0A] text-[0.875rem] uppercase tracking-[0.1em]">REFERENCE</a>
    </nav>
</aside>
```

---

## 4. Hero Header — three variants

Choose by page type. Use exactly one hero per page, immediately below the top nav.

### 4a. Landing-style (readme): solid cyan display headline

Use for landing pages and project entrypoints. The whole title is rendered in primary cyan.

```html
<section class="mb-20">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-end">
        <div class="lg:col-span-8">
            <h1 class="text-[3.5rem] font-extrabold uppercase tracking-[-0.05em] text-[#00FFFF] leading-none mb-6">MY_PROJECT.MD</h1>
        </div>
    </div>
</section>
```

### 4b. Reference-style: side-bordered with crumb label

Use for API or CLI reference pages. The 8px left cyan border anchors the page in the navigation hierarchy.

```html
<div class="mb-16 border-l-8 border-[#00FFFF] pl-8">
    <div class="text-[#4B5563] font-['Space_Grotesk'] uppercase tracking-[0.2em] text-[0.75rem] mb-2">DOCUMENTATION / REFERENCE</div>
    <h1 class="text-[3.5rem] font-black font-['Space_Grotesk'] uppercase tracking-tight text-white leading-tight">MY_PROJECT<span class="text-[#00FFFF]">.MD</span></h1>
</div>
```

### 4c. Architecture-style: white headline with cyan period

Use for system specs, ADRs, design docs. The lone cyan period reinforces the "terminator" aesthetic.

```html
<div class="mb-16">
    <h1 class="text-[3.5rem] font-bold uppercase tracking-tight text-[#e5e2e1] leading-none mb-4">
        MY_PROJECT<span class="text-[#00FFFF]">.</span>
    </h1>
    <div class="flex items-center space-x-4 text-[#4B5563]">
        <span class="font-['Space_Grotesk'] uppercase tracking-[0.2em] text-[0.6rem]">SYSTEM SPECIFICATION</span>
    </div>
</div>
```

---

## 5. Bento Card Grid

Use to lay out non-narrative content blocks (cards, contracts, summaries). Always 12-column, `gap-6` or `gap-8`, mixing column spans for asymmetry.

```html
<div class="grid grid-cols-12 gap-6">
    <!-- Wide card: spans 8 cols on desktop -->
    <div class="col-span-12 lg:col-span-8 bg-[#0A0A0A] p-8 border border-[#4B5563]/10">
        <h2 class="text-[1.25rem] font-bold uppercase tracking-[0.1em] text-[#00FFFF] mb-8">PRIMARY BLOCK</h2>
        <p class="text-[0.875rem] text-[#B9CAC9] leading-relaxed">Dense narrative or list goes here.</p>
    </div>
    <!-- Narrow card: spans 4 cols on desktop -->
    <div class="col-span-12 lg:col-span-4 bg-[#0A0A0A] p-8 border border-[#4B5563]/10">
        <h2 class="text-[1.125rem] font-bold uppercase tracking-[0.1em] text-white mb-8">SIDE BLOCK</h2>
        <p class="text-[0.875rem] text-[#B9CAC9] leading-relaxed">Metadata, flags, or short list.</p>
    </div>
</div>
```

### 5a. Contract Card with top-stripe accent

Use inside the bento grid to surface status or commitments. The 2px top stripe color signals the contract type (cyan = standard, red = critical, muted = informational).

```html
<div class="bg-[#0A0A0A] p-8 border border-[#4B5563]/10 border-t-2 border-t-[#00FFFF]">
    <div class="flex items-center gap-2 mb-4">
        <span class="material-symbols-outlined text-[#00FFFF]">security</span>
        <h3 class="font-bold uppercase tracking-wider text-white text-sm">SECURITY CONTRACT</h3>
    </div>
    <p class="text-[0.875rem] text-[#B9CAC9] leading-relaxed">Short prose stating the guarantee.</p>
</div>
```

---

## 6. Code Blocks

### 6a. Inline `<code>`

Use for short identifiers, paths, or flags inside running prose.

```html
<code class="bg-[#2A2A2A] text-[#00FFFF] px-2 py-0.5 text-[0.75rem]">--verbose</code>
```

### 6b. Block `<pre>` (full-width snippet)

Use for multi-line shell, JSON, or config snippets. Background drops to `#2A2A2A`, text in cyan.

```html
<pre class="bg-[#2A2A2A] text-[#00FFFF] p-4 text-[0.75rem] font-mono overflow-x-auto">
git clone clingy.git
cd clingy &amp;&amp; source ./clingy.sh
clingy --version
</pre>
```

---

## 7. CLI Flag List Item

Use inside reference pages to document a CLI option. The leading `before:` square dot is the meaning carrier — cyan = active default, muted = optional, red = dangerous.

```html
<li class="relative pl-6 before:absolute before:left-0 before:top-2 before:w-1.5 before:h-1.5 before:bg-[#00FFFF]">
    <div class="text-[#00FFFF] font-mono text-sm mb-1">--verbose, -v</div>
    <div class="text-[0.75rem] text-[#4B5563] leading-relaxed">Enables low-level kernel log output for debugging.</div>
</li>
<li class="relative pl-6 before:absolute before:left-0 before:top-2 before:w-1.5 before:h-1.5 before:bg-[#FF0000]">
    <div class="text-[#00FFFF] font-mono text-sm mb-1">--bypass-sec</div>
    <div class="text-[0.75rem] text-[#FFB4AB] leading-relaxed">WARNING: Disables standard security handshake verification.</div>
</li>
```

---

## 8. HTTP Endpoint Item

Use inside an API reference page. The colored verb tag signals the action class (cyan = read, amber = write, red = destructive).

```html
<div class="bg-[#131313] p-6 border border-[#4B5563]/20 hover:border-[#00FFFF]/50 transition-all duration-300">
    <div class="flex items-center gap-4 mb-3">
        <span class="bg-[#00FFFF] text-[#003737] px-2 py-0.5 text-[0.6875rem] font-bold uppercase">GET</span>
        <code class="text-[#00FFFF] font-mono text-sm">/v1/system/heartbeat</code>
    </div>
    <p class="text-sm text-[#B9CAC9] mb-4">Short description of what the endpoint returns.</p>
    <div class="grid grid-cols-2 gap-4 text-[0.75rem] uppercase tracking-wider">
        <div><span class="text-[#4B5563]">Params:</span> <span class="text-white">NODE_ID (UUID)</span></div>
        <div><span class="text-[#4B5563]">Response:</span> <span class="text-white">200 OK [JSON]</span></div>
    </div>
</div>
```

---

## 9. Directory Tree Block

Use on architecture pages to render a project layout. The left cyan border sets it apart as a "system map".

```html
<div class="font-mono text-[0.75rem] text-[#00FFFF]/80 bg-[#050505] p-6 border-l border-[#00FFFF]/30">
    <div class="mb-2">ROOT/</div>
    <div class="ml-4">&#9500;&#9472;&#9472; <span class="text-[#e5e2e1]">bin/</span> [DISPATCHER]</div>
    <div class="ml-8">&#9500;&#9472;&#9472; clingy</div>
    <div class="ml-8">&#9492;&#9472;&#9472; clingy.sh</div>
    <div class="ml-4">&#9492;&#9472;&#9472; <span class="text-[#e5e2e1]">commands/</span> [SECTORS]</div>
</div>
```

---

## 10. Footer

Use at the bottom of every page. Two flavors below; pick by page type.

### 10a. Landing footer

```html
<footer class="mt-24 pt-8 border-t border-[#4B5563]/15">
    <div class="flex flex-col md:flex-row justify-between items-start md:items-center">
        <div class="text-[#4B5563] text-[0.6875rem] uppercase tracking-widest font-mono">END_OF_DOCUMENT</div>
        <div class="flex space-x-8 mt-4 md:mt-0">
            <span class="text-[#00FFFF] text-[0.6875rem] uppercase tracking-[0.2em] cursor-pointer hover:underline">REPORT_ISSUE</span>
            <span class="text-[#00FFFF] text-[0.6875rem] uppercase tracking-[0.2em] cursor-pointer hover:underline">CONTRIBUTE</span>
        </div>
    </div>
</footer>
```

### 10b. Reference / Architecture footer (versioned)

```html
<footer class="mt-24 pt-8 border-t border-[#4B5563]/15 text-[#4B5563]">
    <div class="flex flex-wrap justify-between items-center gap-4">
        <div class="text-[0.75rem] uppercase tracking-widest">LAST UPDATED: 2026-05-01 &bull; VERSION 1.2.0-STABLE</div>
        <div class="flex gap-6">
            <a class="text-[0.75rem] uppercase tracking-widest hover:text-white transition-none" href="#">HELP</a>
            <a class="text-[0.75rem] uppercase tracking-widest hover:text-white transition-none" href="#">SUPPORT</a>
        </div>
    </div>
</footer>
```

---

## 11. CRT Overlay + Vignette (architecture-only)

Use ONLY on architecture pages. Place the two divs immediately inside `<body>` before any other content. The fixed `z-index` keeps them above the content layer but non-interactive.

```html
<style>
    .crt-overlay {
        position: fixed; top: 0; left: 0;
        width: 100vw; height: 100vh;
        background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.15) 50%),
                    linear-gradient(90deg, rgba(255, 0, 0, 0.03), rgba(0, 255, 0, 0.01), rgba(0, 0, 255, 0.03));
        background-size: 100% 2px, 3px 100%;
        pointer-events: none;
        z-index: 100;
    }
    .vignette {
        position: fixed; top: 0; left: 0;
        width: 100%; height: 100%;
        box-shadow: inset 0 0 150px rgba(0,0,0,0.8);
        pointer-events: none;
        z-index: 101;
    }
</style>

<div class="crt-overlay"></div>
<div class="vignette"></div>
```

---

## 12. The "No-Line" Rule in Practice

The design forbids 1px structural borders. Hierarchy is built from background steps. The pattern below shows the correct way to nest a focus area inside a panel.

```html
<!-- WRONG: relies on a 1px outline ring -->
<div class="border border-white p-4">...</div>

<!-- RIGHT: tonal stack — the inner block is one tier brighter than its parent -->
<div class="bg-[#0A0A0A] p-8">                 <!-- surface-container-low -->
    <div class="bg-[#131313] p-6">             <!-- surface-container -->
        <div class="bg-[#2A2A2A] p-4">         <!-- surface-container-high (focus) -->
            Inner content sits here without ever drawing a line.
        </div>
    </div>
</div>
```

When a hairline is unavoidable for accessibility, use the `outline-variant` token at 15% opacity:

```html
<div class="border border-[#4B5563]/15 p-8 bg-[#0A0A0A]">Ghost border fallback.</div>
```

That is the only sanctioned 1px line in the system.
