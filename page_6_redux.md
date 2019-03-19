---
layout: page
title: Redux
permalink: /redux/
nav_order: 6
---

# Redux

For å lagre state til applikasjonen bruker vi redux.
Dette Redux-oppsettet er veldig minimalistisk for å demonstrere hvordan man setter opp
de forskjellige delene med TypeScript.

## Actions

Definerer opp redux actiontypes som enums:

``

```typescript
// ./src/store/fjell/types.ts
export enum FjellActionTypes {
  FETCH_REQUEST = '@@fjell/FETCH_REQUEST',
  FETCH_SUCCESS = '@@fjell/FETCH_SUCCESS',
}
```

Og lager action creators for dem:

```typescript
// ./src/store/fjell/actions.ts
import { action } from 'typesafe-actions';
import { FjellActionTypes, IFjell } from './types';

export const fetchRequest = () => action(FjellActionTypes.FETCH_REQUEST);
export const fetchSuccess = (data: IFjell[]) => action(FjellActionTypes.FETCH_SUCCESS, data);
```

## Reducer

Vi bruker `FjellState` når vi setter opp reducer, dette gjør at
TypeScript kan validere koden vår.

```typescript
// ./store/fjell/reducer.ts
import { Reducer } from 'redux';
import { IFjellState, FjellActionTypes } from "./types";

const initialState: IFjellState = {
    fjell: []
};

const reducer: Reducer<IFjellState> = (state = initialState, action) => {
    switch (action.type) {
        case FjellActionTypes.FETCH_SUCCESS: {
            return { ...state, fjell: action.payload };
        }
        default: {
            return state;
        }
    }
};

export { reducer as fjellReducer };

```

## Store

Vi setter opp store med reducers og dev tools i `store/index.ts`.

```typescript
// ./src/store/index.ts
import { combineReducers, createStore } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import { fjellReducer } from './fjell/reducer';
import { FjellState } from './fjell/types';

export interface IApplicationState {
  fjell: FjellState
}

const reducers = combineReducers<IApplicationState>({
    fjell: fjellReducer
});

export const store = createStore(
    reducers,
    composeWithDevTools()
);
```

## Store i React

For å aktivere store i appen vår må vi legge det inn i React:

```typescript
// ./src/App.tsx
import { Provider } from "react-redux";
...
  render() {
    return (
      <Provider store={store}>
        <div className="App">
          <h1>FjellAppen</h1>
          <Fjell />
        </div>
      </Provider>
    );
  }
...
```