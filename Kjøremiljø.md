# Kjøremiljø

## Valg av plattform

- Jeg har mest erfaring med klassisk serverarkitektur
- For et enkelt API ville jeg brukt Docker for å unngå kompleksitet
- Skal det være en mikrotjenestearkitektur, kan Kubernetes være et godt valg

## CI/CD-pipeline

- Min nr. 1-preferanse:
  - Azure DevOps som kode-repo
  - TeamCity for bygg
  - Octopus for deployment
- Alternativt:
  - GitHub eller Azure DevOps som kode-repo
  - GitHub Actions eller Azure Pipelines for bygg og deployment
- Ønsket repo-policy:
  - Låst main-gren
  - Feature-grener for utvikling
    - Pull request med krav om kodegjennomgang (bidrar til bedre kodekvalitet og kunnskapsdeling)
  - Release-grener for deployment til produksjon

## Miljøhåndtering

- Development
  - Lokal utviklermaskin
- DevTest
  - Relativt stabilt miljø
  - Både main-, release- og feature-grener kan enkelt deployes for testing
- Staging
  - Svært likt produksjon, men med testdata
  - Stabilt miljø
  - Ingen feature-gren-deployments
  - Deployments må koordineres og kommuniseres med andre team for å sikre stabilitet
- Produksjon
  - Hovedmiljøet
  - Begrenset utviklertilgang
  - Kun deployment av main- og release-grener etter tilstrekkelig testing i forkant
  - Kontrollerte og planlagte deployments

## Tilgjengelighet og skalerbarhet

- Health-check (kan integreres med Kubernetes for automatisk restart)
- Load balancing og autoskalering basert på CPU

## Sikkerhet og secrets-håndtering

- Azure Key Vault til håndtering av secrets
- Miljøvariabler for å håndtere Azure Key Vault-secrets og andre kritiske nøkler
- OWASP Top 10 som sikkerhetsreferanse
- SAST og DAST-kodeskanning (Snyk, Veracode, ...)
- Regelmessig pentest
