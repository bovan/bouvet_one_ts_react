---
layout: page
title: Oppsett
permalink: /oppsett/
nav_order: 3
---

# Oppsett

Når create-react-app er ferdig må vi gjøre klar et par ting til før vi kan starte.

## Proxy

Det første vi må gjøre er å sørge for at utviklingsserveren vår kan nå backend-tjenesten vår. Dette gjør vi ved å legge til en linje på øverste nivå i package.json:

    {
        "name": ...
        ...
        "proxy": "http://127.0.0.1:5000",
        ...
    }

## Redux

For å lagre data fra backend bruker vi i denne guiden Redux, vi må
da installere et par pakker til kodebasen vår:

    yarn add redux react-redux @types/react-redux typesafe-actions

Spesielt for TypeScript er at vi trenger å installere types for pakker
som ikke inkluderere disse. Mange pakker har inkludert types og da trenger
man ikke å legge disse til. `react-redux` oppdaterer ikke sine egne types
og vi må derfor hente dette fra DefinitelyTyped sin pakke.

## Redux Dev Tools

For å lettere kunne følge med på hva som foregår bruker vi redux-devtools

Plugin/Extension for Chrome og Firefox er tilgjengelig via [http://extension.remotedev.io/](http://extension.remotedev.io/)

For å koble opp appen vår mot denne kan vi bruke `redux-devtools-extension`

    yarn add redux-devtools-extension

## Oppstart

Med alle endringer vi ønsker å gjøre i `package.json` utført, kan vi nå
starte frontend-serveren

    yarn start
