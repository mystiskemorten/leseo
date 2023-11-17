# Reliable, Scalable, and Maintainable Applications

Formålet med kapittel 1 er å etablere begrepene som brukes i resten av boka. Det første begrepet er Data System, som jeg kanskje heller ville kalt Data Architecture(?). Et Data System er samlingen av komponenter som samlet sett tilbyr en tjeneste eller utfører en funksjon basert på data. For eksempel vil et enkelt CRUD API Data System kunne se slik ut:

```
┌Data-System────────┐
│  ┌────────┐       │
│  │Postgres│┌─────┐│
│  └───┬────┘│Redis││
│      │▲    └─┬───┘│
│      ▼│      ▼ ▲  │
│┌──────┴────────┴─┐│
││Flask Applikasjon││
│└─────────────────┘│
└───────────────────┘
```

Her kan data hentes og skrives fra databasen (Postgres) eller cache (Redis). Hvilket av de to systemene man bruker vil for eksempel kunne avhenge av hvor lang kjøretid en spørring har i databasen versus hvor viktig det er at dataene er helt sanntidige. Disse spørsmålene inngår i designprosessen når man skal lage et Data System. Data Systems må designes, fordi bruksmønstre og dataenes karakter vil påvirke hvor godt egna ulike teknologier er for å håndtere traffikk.

## Reliability Scalability, Maintainability

Boka etablerer tre begreper som (jeg regner med) dukker opp mye senere: Reliability, Scalability og Maintainability. Dette er egenskaper ved Data Systems:

Et Data System har Reliability hvis det fungerer som forventet under bruk. Dette betyr både at systemet må kunne tilgjengeliggjøre data, og må kunne begrense tilgang til data, avhengig av kravene som stilles til systemet. 

Et Data System har Scalability hvis det kan tilpasse seg økte menger bruk. Det som gjør scalability vanskeligere enn man kanskje først antar er at den økte mengden bruk kan ha en form som gjør det nødvendig å tilpasse systemet utover å bare horisontalt eller vertikalt skalere det opp, for eksempel ved å legge til replikaer eller kjøpe større servere. Boka har et interessant eksempel på hvordan Twitter gjorde sitt system skalerbart i møte med enorme mengder traffikk. Dette gjorde de ved å implementere en ganske komplisert løsning som støttet to typer storskalatraffikk: Fra brukere med svært mange følgere, og fra brukere med færre følgere. Det som er nøkkelen til å kunne gjøre et system skalerbart er å forstå Load Parameters, altså hvilke parametre i systemet som påvirker den totale lasten. I Twitters tilfelle var et nøkkelparameter "antall følgere per bruker". Siden systemers last kan antas å utvikle seg over tid er det viktig å følge opp viktige Load Parameters med god monitorering.

Et Data System har Maintainability hvis det er rimelig enkelt å vedlikeholde. Kompleksitet gjør det vanskeligere å oppnå Scalability og Reliability, siden det gjør det vanskeligere å videreutvikle systemet, og forutsi og/eller oppdage problemer. Samtidig vil det gjerne være komplekst å løse Scalability, noe som gjør at man kan bli nødt til å ofre noe Maintainability.
