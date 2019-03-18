---
layout: page
title: Klargjøre app
permalink: /klargjore/
nav_order: 4
---

# Klargjøring

Før vi starter tar vi bort det vi ikke trenger, slik at det er plass til
vår app.

Vi kan slette hele `<header></header>` tag i `src/App.js`, og ta bort importeringen av logo. Vi står da igjen med:

```typescript
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        { /* slett innhold her */ }
      </div>
    );
  }
}

export default App;
```

Vi kan også rydde bort CSS som vi ikke trenger i `App.css` slik at vi står igjen med de øverste 3 linjene:

```css
.App {
  text-align: center;
}
```