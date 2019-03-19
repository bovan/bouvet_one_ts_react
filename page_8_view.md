---
layout: page
title: Visning
permalink: /visning/
nav_order: 8
---

# Visning

Når alt er satt opp kan vi presentere dataene vi får fra backend i et React-view

```typescript
// ./src/components/Fjell.tsx
import * as React from "react";
import { connect } from "react-redux";
import { IFjell } from "../store/fjell/types";
import { fetchRequest } from "../store/fjell/actions";
import { Dispatch } from "redux";
import { IApplicationState } from "../store";

// definerer separate props for bedre oversikt
interface dispatchProps {
    fetch: () => void;
}

interface stateProps {
    fjell: IFjell[];
}

// merger sammen props for bruk i React.Component
type props = dispatchProps & stateProps;

class Fjell extends React.Component<props> {
    componentDidMount() {
        // når komponenten mountes ønsker vi å starte action
        // som trigger fetch
        this.props.fetch();
    }

    render() {
        return (
            <>
                { this.props.fjell.map(f => (
                    <div key={f.navn}>
                        {f.navn} <em>{f.hoyde} moh</em>
                    </div>
                ))}
            </>
        )
    }
}

// hent state.fjell.fjell fra Redux
const mapStateToProps = (state: IApplicationState) => {
    return {
        fjell: state.fjell.fjell
    }
}

// map inn dispatch for å hente data
const mapDispatchToProps = (dispatch: Dispatch) => {
    return {
        fetch: () => dispatch(fetchRequest())
    }
}

export default connect(mapStateToProps, mapDispatchToProps)(Fjell);
```

For at `connect(state, props)(Fjell)` skal fungere må appen vår ha tilgang til store.
Vi gjør dette med `react-redux`-komponenten, hvor vi legger inn storet.

```typescript
// ./src/app.tsx
import Fjell from "./components/Fjell";
import { Provider } from "react-redux";
import { store } from "./store";

      <Provider store={store}>
        <div className="App">
          <h1>FjellAppen</h1>
          <Fjell />
        </div>
      </Provider>
```