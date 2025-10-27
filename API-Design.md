# API Design

## Valg av teknologi og rammeverk

- Siste stabile versjon av .NET (net9.0 per nå)
- ASP.NET Core for API-webben
- EntityFramework.Core for databaseinteraksjoner

## Struktur og arkitektur

- Lagdeling (tilpasses etter kompleksitet)
  - Data-lag
    - Data-entiteter som speiler databasen
    - Database-migrasjoner
    - EF.Core-konfigurasjoner
    - Eventuelle SQL-skript som bør kjøres ved deployment kan også ligge her
    - Repository-mønster for database-transaksjoner
  - Forretningslag
    - Forretningsrelaterte entiteter (kan ligne på eller være forskjellige fra Data-lagets entiteter)
    - Facade-mønster for å koordinere database, eksterne systemer og forretningsrelatert logikk
  - Web-lag
    - ASP.NET Core-applikasjonen
    - API-endepunkter
    - Autentiserings- og autorisasjonspolicyer
    - API-kontrakter (Request, Response)

## Autentisering og autorisasjon

### Autentisering

- API-et brukes kun av én frontend-tjeneste (BFF)
  - OIDC-autentisering
  - Web-API-et mottar ID-token fra IDP og oppretter applikasjons-cookie
  - Endepunktene er beskyttet av cookie
- API-er som brukes av andre systemer
  - Proxy-autentisering for server-til-server-kall
  - OIDC JWT-token for alle andre typer forespørsler

### Autorisasjon

- Første beskyttelseslag: autorisasjonspolicy + ASP.NET Core-autorisasjonsmiddleware
- Domenespesifikk autorisasjon bør ligge i forretningslaget
- Kritisk datarelatert autorisasjon bør ligge nær databasen (Data-laget / repository)

## Logging, feilhåndtering og overvåking

- Strukturert logging (Serilog)
- Sentralisert loggsystem (Seq, Grafana, etc.)
- Alle håndterte og ikke-håndterte feil bør formidle en beskrivende melding til brukeren:
  - Brukervennlig melding ved håndterte feil
  - Nok informasjon slik at brukeren enkelt kan få hjelp av support (for eksempel CorrelationId)
- Loggene må ha nok informasjon til at hendelser kan gjenskapes
- Hovedaksjoner bør logge tidsbruk for å kunne overvåke ytelse
- Verktøy som Dynatrace, Grafana eller lignende brukes til å overvåke ytelse og produksjonsrelaterte hendelser

## Testing og dokumentasjon

- NUnit/xUnit til unit- og integrasjonstester
- InMemory-testdata og EFCore-database for testene
- Cypress, Playwright eller lignende for frontend end-to-end-testing
- OpenAPI/Swagger for API-skjema og dokumentasjon
- README-filer, wiki-sider eller lignende for dokumentasjon av viktige avgjørelser, arkitektur osv.
