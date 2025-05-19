# 🎧 Sounded – Global UI Sound System for React

Sounded is a lightweight, theme-aware sound system for React and Next.js apps. It provides subtle UI feedback using hover and click sounds, with full support for dark/light themes, mute toggles, and accessibility-friendly enhancements.

- 🔊 Click and hover sounds via a single `<Sounded />` wrapper
- 🎨 Theme-based sound packs for dark/light modes
- 🔇 Global mute toggle with persistence
- ⚡️ Fast, typed, and Tailwind-compatible

---

## 📦 Installation

```bash
npm install plebs/sounded
```

or with yarn:

```bash
yarn add plebs/sounded
```

Then import components and hooks directly from the package:

```tsx
import { SoundedProvider, useSoundedContext, useSound, Sounded } from 'plebs/sounded';
```

---

## 🧩 What It Does

- Provides global configuration for UI sound effects
- Enables dark/light theme–specific sound sets
- Offers a persistent mute toggle with `localStorage` support
- Cleanly integrates with React components using a simple `<Sounded>` wrapper
- Works with any interactive component (`button`, `div`, `a`, etc.)

---

## ✅ Core Components

### 1. `SoundedProvider`

Wrap your app in this provider to enable sound context features:

```tsx
import { SoundedProvider } from 'plebs/sounded';

<SoundedProvider theme="dark">
  <App />
</SoundedProvider>
```

- `theme`: `"light"` | `"dark"` – determines which sound pack to use
- Stores the `muted` state in `localStorage` automatically

---

### 2. `useSoundedContext()`

Use this hook anywhere in your app to access or control the sound system:

```tsx
const { muted, toggleMute, sounds, theme } = useSoundedContext();
```

---

### 3. `<Sounded />` Component

Wraps any UI element and injects sound on hover or click automatically:

```tsx
<Sounded>
  <button>Hover and click sound</button>
</Sounded>

<Sounded sound={false}>
  <button>No sound button</button>
</Sounded>

<Sounded hoverSound={false}>
  <div>Hover sound disabled</div>
</Sounded>

<Sounded overrideHover="/custom/hover.mp3">
  <div>Hover here</div>
</Sounded>

<Sounded overrideClick="/custom/click.mp3">
  <a href="#">Custom click sound</a>
</Sounded>
```

#### Props

| Prop           | Type      | Description                                                 |
|----------------|-----------|-------------------------------------------------------------|
| `overrideClick`| `string`  | Optional custom sound file for click events                 |
| `overrideHover`| `string`  | Optional custom sound file for hover events                 |
| `sound`        | `boolean` | Set to `false` to disable all sound                         |
| `clickSound`   | `boolean` | Set to `false` to disable only click sound                  |
| `hoverSound`   | `boolean` | Set to `false` to disable only hover sound                  |

---

### 4. `useSound(urls: string[])`

A lower-level hook for custom playback use cases:

```tsx
const play = useSound(['/sounds/ping.mp3']);

<button onClick={play}>Custom Trigger</button>
```

#### Options

You can pass an optional second argument to `useSound(urls, options)`:

```ts
const play = useSound(['/sounds/ping.mp3'], {
  fallbackToSilence: true, // fallback to silent buffer if all sounds fail
  onLoadError: (url, error) => {
    console.error(`Failed to load sound from ${url}:`, error);
  },
});
```

##### `fallbackToSilence` (default: `true`)
- If all sounds fail to load or decode, a 1-frame silent buffer will be used to avoid crashes.
- If set to `false`, an error will be thrown instead.

##### `onLoadError`
- A callback function that is invoked when a sound fails to fetch or decode.
- Useful for analytics, debugging, or alerting.

---

## 🔧 Features

- ✅ Theme-based sound routing
- ✅ Global mute toggle (with persistence)
- ✅ Shuffle and fallback sound variants
- ✅ One-shot AudioContext support
- ✅ Fully typed and client-safe

---

## 🛠 How To Add Sounds

1. Place your sound files in `/public/sounds/`
2. Update `soundMap` inside `SoundedContext.tsx`:

```ts
const soundMap = {
  dark: {
    click: '/sounds/dark-click.mp3',
    hover: '/sounds/dark-hover.mp3',
  },
  light: {
    click: '/sounds/light-click.mp3',
    hover: '/sounds/light-hover.mp3',
  },
};
```

---

## ⚖️ Pros & Cons

### ✅ Pros

- Easy to integrate and use
- Centralized sound logic for consistent UX
- Fully customizable and theme-aware
- Minimal runtime overhead
- Works seamlessly in Next.js App Router

### ⚠️ Cons

- Requires client-only usage (`'use client'`)
- Not SSR-compatible (by design)
- Must wrap interactive elements manually (or abstract with design system)

---

## 📦 Recommended Use Cases

- Enhanced web apps with rich UIs
- Accessible audio feedback systems
- Design systems that support multimodal interaction
- Games, dashboards, or web-based experiences with hover/click feedback

---

## 🧠 Best Practices

- Keep sounds subtle and under 500ms
- Use low-pass or analog-style tones to avoid fatigue
- Offer mute toggle visibly or inside user settings
- Use `<Sounded>` consistently for accessibility parity

---

## 🧱 Directory Structure

```
/src
  /context
    SoundedContext.tsx     # Global state and provider
  /hooks
    useSound.ts            # Playback logic
  /components
    Sounded.tsx            # Wrapper component for sound-enabled elements
```

---

For bugs, ideas, or enhancements, please reach out or fork this module.