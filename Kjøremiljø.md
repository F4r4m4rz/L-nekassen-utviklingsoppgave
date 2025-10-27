# Kjøremiljø

## Valg av platform

- Jeg selv har mest erfaring med klassik server arkitektur
- For en enkel API ville jeg brukt docker for å unngå kompleksitet
- Skal det være en mikrotjeneste arkitektur da kubernetes kan være lurt å bruke

## CI/CD Pipeline

- Min no.1 preferanse:
  - Azure DevOps som kode repo
  - TeamCity for bygg
  - Octopus for deployment
- Eller:
  - Github/Azure devops som kode repo
  - Github actions/Azure pipelines for bygg og deploy
- Ønsket repo policy
  - Låst main gren
  - feature grener for utvikling
    - Pull request med påbud kode review (Den hjelper med bedre kode kvalitet og å spre kunnskap om koden)
  - release grener for deploymeny til produksjon

## Miljøhåndtering

- Develpment
  - Lokal develper machine
- DevTest
  - Relativt stabil miljø
  - Både main, release og feature grener kan enkelt deployes for testing
- Staging
  - Veldig nær produksjon men med test data
  - Stabil
  - Ingen feature gren deployment
  - Deployments må koordineres og informeres til andre team for å oppnå en stabil miljø
- Produksjon
  - Hoved miljøet
  - Begrenset utvikler tilgang
  - Kun deployment av main og release grener ved tilstrekkelig testing in forkant
  - Kontrollert of planlagt deployments

## Sikkerhet of screts håndtering

- Azure Key-vault til å håndtere secrets
- Env variable til å håndtere azure key-vault secrets og andre super viktige secrets
