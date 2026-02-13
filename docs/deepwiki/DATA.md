# Bento Data Types Reference

## Overview

This document contains all TypeScript type definitions extracted from the Bento codebase, organized by module.

---

## Core Types (`src/types/bento.ts`)

### TileSize

```typescript
/**
 * Bento grid tile size types.
 * Named by CSS span values (columns x rows).
 * Based on 16-column (desktop) / 8-column (mobile) grid system.
 */
export type TileSize =
  | '2x2'   // Small Square (2 columns x 2 rows)
  | '4x1'   // Mini Horizontal (4 columns x 1 row)
  | '4x2'   // Horizontal (4 columns x 2 rows)
  | '2x4'   // Vertical (2 columns x 4 rows)
  | '4x4'   // Large Square (4 columns x 4 rows)
```

### TileType

```typescript
/**
 * Bento grid tile types.
 */
export type TileType =
  | 'PROFILE'   // User profile tile
  | 'SOCIAL'    // Social media link
  | 'PROJECT'  // Project showcase
  | 'MUSIC'     // Music player
  | 'IMAGE'     // Image gallery
  | 'VIDEO'     // Video thumbnail
  | 'TEXT'      // Text/quote content
  | 'LOCATION'  // Map location
  | 'LINK'      // Generic link
  | 'CHAT'      // AI chat (disabled in current version)
```

### Platform

```typescript
/**
 * Supported social platform types.
 */
export type Platform =
  | 'github'
  | 'twitter'
  | 'instagram'
  | 'spotify'
  | 'youtube'
  | 'figma'
  | 'dribbble'
  | 'linkedin'
```

### BentoItem

```typescript
/**
 * Individual bento grid item configuration.
 */
export interface BentoItem {
  /** Unique identifier for the item */
  id: string;
  
  /** Type of tile to render */
  type: TileType;
  
  /** Size of the tile */
  size: TileSize;
  
  /** Social platform (for SOCIAL type) */
  platform?: Platform;
  
  /** Icon identifier (iconify string or image URL) */
  icon?: string;
  
  /** Primary title text */
  title?: string;
  
  /** Secondary/subtitle text */
  subtitle?: string;
  
  /** Text content (for TEXT type) */
  content?: string;
  
  /** Image URL for thumbnail/preview */
  image?: string;
  
  /** Link URL (for LINK and SOCIAL types) */
  link?: string;
  
  /** Brand accent color (hex) */
  color?: string;
  
  /** Force item to start on new row */
  forceNewRow?: boolean;
  
  /** Explicit column start position (1-8) */
  colStart?: number;
}
```

### BentoSection

```typescript
/**
 * Section containing multiple bento items.
 */
export interface BentoSection {
  /** Unique section identifier */
  id: string;
  
  /** Optional section title */
  title?: string;
  
  /** Array of bento items in this section */
  items: BentoItem[];
}
```

### UserPersona

```typescript
/**
 * User profile information for the bento page.
 */
export interface UserPersona {
  /** Display name */
  name: string;
  
  /** Username/handle (without @) */
  handle: string;
  
  /** Short bio/description */
  bio: string;
  
  /** Avatar image URL */
  avatar: string;
  
  /** Display location */
  location: string;
  
  /** Optional Google Maps embed URL */
  mapEmbed?: string;
}
```

---

## Data Configuration (`src/data/bento.gen.ts`)

### USER_PERSONA

```typescript
export const USER_PERSONA: UserPersona = {
  name: 'Lorem Ipsum',
  handle: 'loremipsum',
  bio: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit...',
  avatar: '/public/images/avatar.png',
  location: 'Lorem City',
  mapEmbed: 'https://www.google.com/maps/embed?pb=...',
};
```

### BENTO_SECTIONS

```typescript
export const BENTO_SECTIONS: BentoSection[] = [
  {
    id: 'hero',
    items: [
      {
        id: 'twitter-top',
        type: 'SOCIAL',
        size: '4x2',
        platform: 'twitter',
        title: 'Twitter',
        subtitle: '@loremipsum',
        link: 'https://twitter.com',
        color: '#1DA1F2',
      },
      // ... more items
    ],
  },
  // ... more sections
];
```

---

## Component Props Types (`src/components/bento/`)

### BentoCardProps

```typescript
interface BentoCardProps extends HTMLMotionProps<'div'> {
  /** Tile size */
  size: TileSize;
  
  /** Force new row (default: undefined) */
  forceNewRow?: boolean;
  
  /** Explicit column start 1-8 (default: undefined) */
  colStart?: number;
}
```

### BentoGridProps

```typescript
interface BentoGridProps {
  /** Array of bento sections to render */
  sections: BentoSection[];
  
  /** Google Maps embed URL (optional) */
  mapEmbed?: string;
}
```

### PlatformIconProps

```typescript
interface PlatformIconProps {
  /** Social platform identifier */
  platform: Platform;
  
  /** Additional CSS classes (default: '') */
  className?: string;
}
```

### ProfileSidebarProps

```typescript
interface ProfileSidebarProps {
  /** User persona data */
  persona: UserPersona;
}
```

---

## Tile Component Props Types (`src/components/bento/tiles/`)

### BaseLinkTileProps

```typescript
interface BaseLinkTileProps {
  /** Bento item data */
  item: BentoItem;
  
  /** Icon React node to display */
  icon: ReactNode;
  
  /** Optional action node (e.g., Follow button) */
  action?: ReactNode;
}
```

### SocialTileProps

```typescript
interface SocialTileProps {
  /** Bento item with SOCIAL type */
  item: BentoItem;
}
```

### LinkTileProps

```typescript
interface LinkTileProps {
  /** Bento item with LINK type */
  item: BentoItem;
}
```

### ImageTileProps

```typescript
interface ImageTileProps {
  /** Bento item with IMAGE type */
  item: BentoItem;
}
```

### VideoTileProps

```typescript
interface VideoTileProps {
  /** Bento item with VIDEO type */
  item: BentoItem;
}
```

### MusicTileProps

```typescript
interface MusicTileProps {
  /** Bento item with MUSIC type */
  item: BentoItem;
}
```

### LocationTileProps

```typescript
interface LocationTileProps {
  /** Bento item with LOCATION type */
  item: BentoItem;
  
  /** Google Maps embed URL */
  mapEmbed?: string;
}
```

### TextTileProps

```typescript
interface TextTileProps {
  /** Bento item with TEXT type */
  item: BentoItem;
}
```

---

## Layout Props Types (`src/layouts/`)

### BaseLayoutProps

```typescript
interface Props {
  /** Page title */
  title: string;
  
  /** Page description (default: 'Astro') */
  description?: string;
}
```

### BentoLayoutProps

```typescript
interface Props {
  /** Page title */
  title: string;
  
  /** User persona for profile display */
  persona: UserPersona;
}
```

---

## UI Component Props (`src/components/ui/Button.tsx`)

### ButtonProps

```typescript
interface ButtonProps extends HTMLMotionProps<'button'> {
  /** Button variant (default: 'primary') */
  variant?: 'primary' | 'secondary';
}
```

---

## OpenGraph Utility Types (`src/utils/opengraph.ts`)

### OpenGraphMetadata

```typescript
/**
 * OpenGraph metadata extracted from a URL.
 */
export interface OpenGraphMetadata {
  /** The page title (from og:title or fallback) */
  title: string;
  
  /** The page description (from og:description or fallback) */
  description: string;
  
  /** The Open Graph image URL */
  image?: string;
  
  /** Alias for image - the Open Graph image URL */
  ogImage?: string;
}
```

### OpenGraphOptions

```typescript
/**
 * Options for fetching OpenGraph metadata.
 */
export interface OpenGraphOptions {
  /** Request timeout in milliseconds (default: 10000) */
  timeout?: number;
  
  /** User agent string for the request */
  userAgent?: string;
  
  /** Whether to generate a screenshot when og:image is missing */
  enableScreenshot?: string;
}
```

### OpenGraphError

```typescript
/**
 * Error class for OpenGraph extraction failures.
 */
export class OpenGraphError extends Error {
  constructor(
    message: string,
    public readonly code: 'TIMEOUT' | 'NOT_FOUND' | 'NETWORK_ERROR' | 'PARSE_ERROR',
    public readonly originalError?: Error
  );
}
```

---

## CSS Custom Properties

### Light Theme (`:root`)

```css
:root {
  --bg-page: #f9fafb;
  --bg-card: #ffffff;
  --bg-card-hover: #f3f4f6;
  --border-card: #e5e7eb;
  --border-card-hover: #d1d5db;
  --text-primary: #111827;
  --text-secondary: #4b5563;
  --shadow-card: 0 2px 8px -2px rgba(0, 0, 0, 0.05);
  --card-shadow-color: rgba(0, 0, 0, 0.1);
}
```

### Dark Theme (`:root.dark`)

```css
:root.dark {
  --bg-page: #000000;
  --bg-card: #0a0a0a;
  --bg-card-hover: #121212;
  --border-card: #1c1c1c;
  --border-card-hover: #333333;
  --text-primary: #ffffff;
  --text-secondary: #a1a1aa;
  --shadow-card: none;
  --card-shadow-color: rgba(0, 0, 0, 0.5);
}
```

---

## Site Configuration (`src/data/site.json`)

```typescript
interface SiteConfig {
  title: string;
  description: string;
  url: string;
  author: {
    name: string;
    email: string;
  };
}
```

---

## OpenGraph Preview Metadata (`src/data/metadata.toml`)

```toml
[[preview]]
url = "https://example.com"
title = "Example Site"
description = "Example site description"
localImage = "filename.png"
```

---

## Tile Size CSS Mapping

```typescript
const sizeClasses: Record<TileSize, string> = {
  '2x2': 'col-span-2 row-span-2',
  '4x1': 'col-span-4 row-span-1',
  '4x2': 'col-span-4 row-span-2',
  '2x4': 'col-span-2 row-span-4',
  '4x4': 'col-span-4 row-span-4',
};

const colStartClasses: Record<number, string> = {
  1: 'col-start-1',
  2: 'col-start-2',
  3: 'col-start-3',
  4: 'col-start-4',
  5: 'col-start-5',
  6: 'col-start-6',
  7: 'col-start-7',
  8: 'col-start-8',
};
```

---

## Platform Icon Mapping

```typescript
const iconMap: Record<Platform, string> = {
  github: 'logos:github-icon',
  twitter: 'logos:twitter',
  instagram: 'skill-icons:instagram',
  spotify: 'logos:spotify-icon',
  youtube: 'logos:youtube-icon',
  figma: 'skill-icons:figma-dark',
  dribbble: 'logos:dribbble-icon',
  linkedin: 'skill-icons:linkedin',
};
```

---

## Complete Type Hierarchy

```
UserPersona
  ├── name: string
  ├── handle: string
  ├── bio: string
  ├── avatar: string
  ├── location: string
  └── mapEmbed?: string

BentoSection
  ├── id: string
  ├── title?: string
  └── items: BentoItem[]

BentoItem
  ├── id: string
  ├── type: TileType
  ├── size: TileSize
  ├── platform?: Platform
  ├── icon?: string
  ├── title?: string
  ├── subtitle?: string
  ├── content?: string
  ├── image?: string
  ├── link?: string
  ├── color?: string
  ├── forceNewRow?: boolean
  └── colStart?: number
```
