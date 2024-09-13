# Entwicklung


## Übersicht

### IST
``` mermaid
flowchart LR
    contentdesk[fa:fa-database Contentdesk]-->discover.swiss
    contentdesk-->app.contentdesk.io
    contentdesk-->outdooractive
    contentdesk-->docs.contentdesk.io

    excel[Excel / CSV]-->contentdesk
    onboarding-->contentdesk
    app.contentdesk.io-->contentdesk
    docs.contentdesk.io-->contentdesk

    guidle-->contentdesk
    eventfrog-->contentdesk
```

### VISION
``` mermaid
flowchart LR

    contentdesk[fa:fa-database Contentdesk]-->docs.contentdesk.io
    contentdesk-->app.contentdesk.io
    contentdesk-->outdooractive
    contentdesk-->discover.swiss

    onboarding-->contentdesk

    guidle-->discover.swiss
    eventfrog-->discover.swiss
```