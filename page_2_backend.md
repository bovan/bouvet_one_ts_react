---
layout: page
title: Backend mock
permalink: /backend/
nav_order: 2
---

# Backend

Vi trenger en backend-tjeneste for å serve testdata. En enkel
server i express.js som leverer JSON holder for dette eksempelet.

Først installerer vi express:

    yarn add express

Vi lager en ny mappe `server` og oppretter en ny javascript fil `./server/server.js`

{% gist 2f9a563712ffec222194afe28a5c0de4 %}

Det denne gjør er bare å lytte på port 5000, og svare på http-requests
til `http://localhost:5000/api/fjell`, og så returnere en liste over fjell
i bymarka.

Denne kan senere byttes ut med en mer nyttig backend i valgfritt språk.

Vi kan nå også starte backend-serveren vår:

    node server.js
