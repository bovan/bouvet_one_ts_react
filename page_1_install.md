---
layout: page
title: Installasjon
permalink: /installasjon/
nav_order: 1
---

Jeg går ut fra at man har følgende installert:

- [node 8.10.0](https://nodejs.org)
- [yarn 1.13.0](https://yarnpkg.com/lang/en/docs/install/)

Du kan enkelt sjekke versjonen av disse:

    node --version
    yarn --version

# Installasjon

Kjør [create-react-app](https://github.com/facebook/create-react-app)

    yarn create react-app bouvet-fjell --typescript

Dette vil opprette de nødvendige filene for et utviklingsmiljø for React
i TypeScript.

Dette kan vi lett utvide til å bruke en valgfri backend

Gå inn i prosjekt-mappen vi har opprettet:

    cd bouvet-fjell

## NPM

Hvis du ønsker å bruke npm i stedet for yarn trenger du npm version 5.2+.

Du kan da kjøre:

    npx create-react-app my-app --typescript --use-npm
