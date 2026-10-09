![error logo not found path: https://github.com/tromoSM/better-jellyfin-ui/blob/main/Assets/fullbannergit.png?raw=true . DEV NOTE DO NOT CHANGE TO RELATIVE.PROJECT MANAGER WILL FAIL](https://github.com/tromoSM/better-jellyfin-ui/blob/main/Assets/fullbannergit.png?raw=true)
===
# Better Jellyfin UI

A modern UI enhancement theme for Jellyfin focused on cleaner layout, smoother animations, and ios like design.

> [!IMPORTANT]
> **This is a fork of [`tromoSM/better-jellyfin-ui`](https://github.com/tromoSM/better-jellyfin-ui).**
> All design credit belongs to tromoSM (Apache 2.0). This fork patches one thing —
> the play button on media cards — see [What this fork changes](#what-this-fork-changes).

---
[![](https://data.jsdelivr.com/v1/package/gh/skysstst/better-jellyfin-ui/badge?style=rounded)](https://www.jsdelivr.com/package/gh/skysstst/better-jellyfin-ui)
[![](https://img.shields.io/jsdelivr/gh/hy/skysstst/better-jellyfin-ui?style=flat&label=jsDelivr&color=f25a30)](https://www.jsdelivr.com/package/gh/skysstst/better-jellyfin-ui)

## Installation

Go to:

Dashboard → General → Branding → Custom CSS

Paste:

```css
@import url("https://cdn.jsdelivr.net/gh/skysstst/better-jellyfin-ui@main/theme.css");
```
Click **Save** and refresh the page.

> [!NOTE]
> Use the `skysstst` URL above, not the upstream one. The fix lives in `theme.css`,
> so importing `tromoSM/...` gives you the unpatched original. The optional add-ons
> below are unchanged and still load from upstream.

> [!TIP]
> ### For firefox users
> make sure to enable `layout.css.backdrop-filter.enabled` and `gfx.webrender.all` to true in `about:config` to be able to see the blur effect. [detailed tutorial on how to enable backdrop blur](https://shounak.hashnode.dev/how-to-enable-backdrop-filter-in-firefox)

## What this fork changes

**One thing only: the play button on media cards.** Everything else is upstream, unmodified.

### The problem

On Jellyfin 12 library views the covers had no play button at all. Two independent
bugs, both in `theme.css`:

1. **`scale: 0`** — upstream hides the centred FAB until the card is hovered, and it
   pops in with no transition.
2. **`position: relative`** — upstream flips `.cardOverlayContainer` to
   `position: relative`, which drops the natively `position: absolute` FAB back into
   normal flow. The button then renders *below* the cover instead of on it.

Bug 2 is the one that makes the button unfindable: fixing bug 1 alone leaves the
control outside the card artwork, still invisible.

### The fix

All of it sits in a single commented block at the end of `theme.css`
(`LIQUID GLASS PLAY BUTTON - fork patch`), so it can be rebased or dropped cleanly:

- **Re-centred** — pinned back to the middle of the card with `position: absolute`
  plus `translate(-50%, -50%)`, sized at `2.9em`.
- **Fades in on hover** — sits at `opacity: 0` / `scale: 0.88` and reveals on
  `:hover` over 0.22 s. `pointer-events` are disabled while hidden, so it cannot be
  clicked blind.
- **Liquid-glass styling** — frosted blur, translucent tint, white inset rim light and
  a soft drop shadow, reusing the recipe upstream already applies to `.countIndicator`
  and `.paper-icon-button-light`. No solid fill, no accent colour.
- **Fallbacks** — `@media (hover: none)` keeps it visible on touch devices, which have
  no hover state at all; `:focus-within` reveals it for keyboard navigation.

### For JellyFrame users

This fork is also registered as a standalone theme (`better-jellyfin-ui-glass`), so it
can be picked in JellyFrame instead of being injected as custom CSS. JellyFrame caches
both the theme manifest and the compiled CSS, so after any change to `theme.css` you
must bump the theme version **and** purge the jsDelivr cache:

```bash
curl https://purge.jsdelivr.net/gh/skysstst/better-jellyfin-ui@main/theme.css
```
 
---

# Optional Add-ons

All add-ons require the main theme to be installed first.

You can combine multiple add-ons together.

---
<details>
  <summary><strong>Custom cover images</strong></summary>
  <img width="1284" height="148" alt="plugin-isprimCov" src="https://github.com/user-attachments/assets/c5e3cf83-aace-4f67-8600-8d006ad063ee" />

  <ul>
    <li>Go <a href="https://github.com/tromoSM/better-jellyfin-ui/tree/main/images">Images</a></li>
    <li>Download and Replace the jellyfin libraries primary cover images with the images in <a href="https://github.com/tromoSM/better-jellyfin-ui/tree/main/images">Images</a></li>
  </ul>
</details>
<details>
<summary><strong> Floating Header</strong></summary>

### Description
Makes the top navigation header float with improved spacing and cleaner visual separation.

### Preview
![Floating Header](https://github.com/tromoSM/better-jellyfin-ui/blob/main/options/screenshots/headr.png?raw=true)

### Installation

Add below the main theme import:

```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/Floating-header.css");
```

</details>


<details>
<summary><strong> High Contrast Interface</strong></summary>

### Description
Improves readability by increasing contrast across interface elements.

### Preview


https://github.com/user-attachments/assets/bb46422f-92ae-41e6-8535-e02880d1867a


### Installation

```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/High-contrast-interface.css");
```

</details>


<details>
<summary><strong> Scale Up Background Animation on Card Hover</strong></summary>

### Description
Adds a subtle scale animation effect to card backgrounds on hover.

### Preview


https://github.com/user-attachments/assets/899687a8-5201-43ab-9ec6-7efa10e8d3a8



### Installation

```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/Scale-up-animation-on-hover-card.css");
```

</details>


<details>
<summary><strong> Remove Liquid Glass Borders</strong></summary>

### Description
Removes glass-style border effects for a flatter visual appearance.

### Preview


https://github.com/user-attachments/assets/56181924-8a25-4a21-b272-642b82cead16



### Installation

```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/no-liquid-glass-borders.css");
```

</details>
<details>
  <summary><Strong>Alternative navigation bar</Strong></summary>

  > **For Jellyfin v12+ users** : this plugin won't work with jellyfin v12 or later versions  
  > ###### this plugin wont work on jellyfin v12 or later version because it is already being used by default
  >  

  ### Preview
  ![igv](https://github.com/tromoSM/better-jellyfin-ui/blob/main/options/screenshots/altrNav.png?raw=true)

  ### Installation

  ```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/alternative-navigation-bar.css");
```
  
</details>
<details>
  <summary><strong>Remove jellyfin logo from header</strong></summary>

> For Jellyfin v12+ users : this plugin might not work as great in v12 compared other versions

  ### Preview
 | before | after |
 |-|-|
 | ![better jellyfin ui plugin #7 : remove jellyfin logo from header](https://github.com/user-attachments/assets/704dda3e-baa1-4e03-aa67-d6794345d05f) | ![better jellyfin ui plugin #7 : remove jellyfin logo from header](https://github.com/user-attachments/assets/50b566cf-7b77-4777-8567-fe492fb11692) |

  ### Installation

  ```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/Remove-jellyfin-logo-from-header.css");
```

</details>
<details>
  <summary><Strong>Alternative detail logo</Strong></summary>

  ### Preview
  | before | after |
  |-|-|
  | ![better jellyfin ui plugin #7 : remove jellyfin logo from header](https://github.com/user-attachments/assets/02854392-10a5-475a-aa9a-4648e1e37de2) | ![better jellyfin ui plugin #7 : remove jellyfin logo from header](https://github.com/user-attachments/assets/a4820e12-8557-4dd8-ade1-412bdf39e3e9) |

  ### Installation

  ```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/alternative-detail-logo.css");
```
  
</details>
<details>
  <summary><Strong>TrickPlay support</Strong></summary>
 
  ##### reported by [@0belous](https://github.com/0belous)
  ### Installation

  ```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/Trickplay-support.css");
```
  
</details>

<details>
  <summary><Strong>iOS Toggle styling</Strong></summary>

  ### Preview
  | before | after |
  |-|-|
  | ![better jellyfin ui plugin #11 : ios toggle styling](https://github.com/user-attachments/assets/ba565761-c1c9-4051-9da8-c88604506845) | ![better jellyfin ui plugin #11 : ios toggle styling](https://github.com/user-attachments/assets/043af9ea-c502-4c67-83aa-e031799b00c0) |

  ### Installation
  ```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/iOS-toggle-styling.css");
```
  
</details>
<br>
<details id='manual'>
  <summary><strong>Manual options</strong></summary>
  <p>
    Customize the variables below to suit your preferences. Once edited, paste the code after all existing imports in <strong>Dashboard → General → Branding → Custom CSS</strong>.</p>
  
  ```css
:root{
  /*active card indicators*/
  --card-indicate-bg:rgba(255, 169, 184, 0.534);
  --card-indicate-liquid-glass:rgba(253, 185, 255, 0.39) ;
  --card-indicate-shadow:rgba(255, 154, 238, 0.329);
  --card-indicate-icon-fill:#ffb0d9;
  /*Backgound*/
  --background-glow-color:#240000;
  /*Backdrop image styling*/
  --backdrop-bg-color:rgba(0, 0, 0, 0.87);
  --backdrop-filter:blur(20px) saturate(120%) contrast(120%) brightness(110%);

  /*Blur value - requested by @Aceman67*/
  --extra-frosted:50px; /*extra frosted ui: panels,headers etc*/
  --medium-frosted:20px;
  --largeui-frosted:15px;/*mostly used by large ui*/
  --smallui-frosted:10px;/*mostly used by smaller ui*/
  --lite-frosted:5px;/*also used by card animation*/
  --extrathin-frostlayer:2px;
}
  ```
</details>

# Example Combined Setup

```css
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/theme.css");
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/Floating-header.css");
@import url("https://cdn.jsdelivr.net/gh/tromoSM/better-jellyfin-ui@main/options/Scale-up-animation-on-hover-card.css");
```

---



# Compatibility


• Designed for Jellyfin Web, desktop and mobile client  
• Some animations might not work as expected on desktop(not web) client.  
• TV client does not support custom css  
• Add-ons can be combined freely    
• Now works with Jellyfin v12   

---



###### [send feedback or request features](https://tromosm.gt.tc/?feedback=true&utm_source=jellyreadmenew)
###### Fork maintained by [skysstst](https://github.com/skysstst) — see [What this fork changes](#what-this-fork-changes).
###### © 2026 - tromoSM. Licensed under Apache 2.0.
