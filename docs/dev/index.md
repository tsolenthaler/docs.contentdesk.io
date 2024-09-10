# Entwicklung


## Übersicht

### IST
``` mermaid
flowchart LR

    contentdesk[fa-solid fa-database Contentdesk]-->docs.contentdesk.io
    contentdesk-->app.contentdesk.io
    contentdesk-->outdooractive
    contentdesk-->discover.swiss

    guidle-->contentdesk
    eventfrog-->contentdesk
```

### SOLL
``` mermaid
flowchart LR

    contentdesk[fa-solid fa-database Contentdesk]-->docs.contentdesk.io
    contentdesk-->app.contentdesk.io
    contentdesk-->outdooractive
    contentdesk-->discover.swiss

    guidle-->discover.swiss
    eventfrog-->discover.swiss
```