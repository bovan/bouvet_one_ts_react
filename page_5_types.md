---
layout: page
title: Struktur og types
permalink: /types/
nav_order: 5
---

# Struktur

I denne guiden skal vi gå for følgende filstruktur:

```ascii
-- src
|   |-- components
|   |   `-- Fjell.tsx
|   |-- store
|   |   |-- fjell
|   |   |   |-- actions.ts
|   |   |   |-- middleware.ts
|   |   |   |-- reducer.ts
|   |   |   `-- types.ts
|   |   `-- index.ts
|   |-- App.tsx
-- server
   `-- server.js
```

# Types

For at TypeScript skal kunne hjelpe oss med objektet fra backend definerer
vi hvordan dette ser ut.

`store/fjell/types.ts`

```typescript
export interface IFjell {
   navn: string;
   hoyde: number;
}
```

Vi kan også definere opp hvordan vi ønsker dette skal se ut i Redux store i samme fil:

```typescript
export interface IFjellState {
   // readonly gjør at TypeScript vil klage hvis vi prøver å endre state
   readonly fjell: IFjell[]
}
```