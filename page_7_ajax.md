---
layout: page
title: Ajax
permalink: /ajax/
nav_order: 7
---

# Ajax

For å hente data fra backend trenger vi en middleware. Det finnes mange alternativer her (f.eks Redux-Saga)
man kan benytte seg av.

Dette eksemplet er en veldig minimalistisk (og potensielt sett ikke bugfri) variant for å
letter se hva som foregår internt.

```typescript
// ./src/store/fjell/middleware.ts
import { fetchSuccess } from "./actions";
import { FjellActionTypes } from "./types";
import { Middleware, MiddlewareAPI } from 'redux';

// fetch data og dispatch success
const fetchFjell = (api: MiddlewareAPI) => fetch("/api/fjell")
    .then(response => response.json())
    .then(json => {
        api.dispatch(fetchSuccess(json));
    });

// fang opp fetch request og start fetchFjell
const middleware: Middleware = api => next => action => {
    if (action.type === FjellActionTypes.FETCH_REQUEST) fetchFjell(api);

    return next(action);
}

export { middleware as fjellMiddleware }
```

Vi aktiverer så middleware i store:

```typescript
// ./src/store/index.ts
...
import { applyMiddleware /* ny import */, createStore } from 'redux';
...

const store = createStore(
    fjellReducer,
    composeWithDevTools(
        applyMiddleware(fjellMiddleware) // ny linje
    )
);
```