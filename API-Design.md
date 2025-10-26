# API Design

## Valg av teknology og rammeverk

- Siste stable versjonen av .net (net9.0 for øyeblikket)
- ASP.NET Core til API webben
- EntityFramework.Core til DB intraksjoner

## Struktur og arkitektur

- Lagdeling (tilpasses av kompleksitet)
  - Data lag
    - Data entiteter som speiler DB
    - DB migrasjoner
    - EF.Core konfigrasjoner
    - Eventuelle sql skripter som bør kjøres ved deployment kan også ligge her
    - Repository mønster for DB transaksjoner
  - Forretning lag
    - Forretning relaterte entiteter (kan ligne eller være forskjellig av Data laget sin entiteter)
    - Facade mønster for koordinere DB, eksterne systemer og forretningsrelaterte logikk
  - Web
    - ASP.NET Core applikasjonen
    - API endepunkter
    - Autentisering og autorisasjons policierne.
    - API kontrakter (Request, Response)

## Autentisering og autorisasjon

### Autentisering

- API-et brukes av kun en Frontend tjeneste (BFF)
  - OIDC autentisering
  - Webben (API) tar imot id token fra IDP of lager applikasjon cookie
  - Endepunktene er beskytet av cookie
- API-er brukes av andre systemer
  - Proxy autentisering for Server to server kaller
  - OIDC JWT token for alle andre type requester

### Autorisasjon

- Første beskyttelse lag: Autorisasjon policy + ASP.NET Core autorisasjons middelware
- Domenespesifikke autorisasjon bør ligge i forretningslaget.
- Kritiske data relaterte autorisasjon bør ligge nær databasen (Data laget - repository)
