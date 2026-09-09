---
title: Sviluppare AEM Commerce
description: Scopri come generare un progetto AEM abilitato per il commerce utilizzando l’archetipo di progetto AEM. Scopri come generare e distribuire il progetto in un ambiente di sviluppo locale.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 33%

---

# Sviluppo di AEM Commerce {#develop}

Lo sviluppo di progetti AEM Commerce basati su Commerce integration framework (CIF) per AEM segue le stesse regole e best practice di altri progetti AEM. Rivedi prima questi:

- [Guida utente allo sviluppo in AEM 6.5](/help/sites-developing/getting-started.md)
- [Concetti di base di AEM](/help/sites-developing/the-basics.md)
- [Sviluppo AEM - Linee guida e best practice](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md)

## Sviluppo locale per AEM Commerce {#local}

Si consiglia di utilizzare un ambiente di sviluppo locale con progetti CIF.

>[!NOTE]
>
>Le istruzioni seguenti sono utili per configurare un ambiente di sviluppo AEM locale per AEM Commerce utilizzando CIF (con particolare attenzione per AEM 6.5). Se utilizzi AEM as a Cloud Service, consulta la documentazione di [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html?lang=it).

Il componente aggiuntivo AEM Commerce per AEM 6.5, alias. Il componente aggiuntivo CIF è disponibile anche per lo sviluppo locale e viene fornito come pacchetto AEM. Può essere scaricato dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html) come feature pack.

### Software richiesto

È necessario installare localmente quanto segue:

- AEM locale 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html) 7 o versione successiva
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o successivo)
- [Nodo LTS](https://nodejs.org/it/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Accesso al componente aggiuntivo CIF

Il componente aggiuntivo CIF può essere scaricato dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html), cercare &#39;componente aggiuntivo AEM Commerce&#39;.

>[!TIP]
>
>Occorre utilizzare sempre la versione più recente del componente aggiuntivo CIF.

### Configurazione locale

Per lo sviluppo di progetti CIF locali utilizzando i componenti aggiuntivi AEM e CIF, procedere come segue:

1. Scarica AEM 6.5 e installa AEM 6.5 Service Pack. È richiesto AEM 6.5 Service Pack 7, tuttavia Adobe consiglia di installare l’ultimo service pack disponibile.

1. Decomprimi il file AEM.jar per creare la cartella `crx-quickstart` ed esegui:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Crea una cartella `crx-quickstart/install`.

1. Copiare il pacchetto del componente aggiuntivo CIF scaricato dal portale di distribuzione software nella cartella `crx-quickstart/install`.

>[!TIP]
>
>In alternativa, il pacchetto del componente aggiuntivo CIF può essere installato anche tramite Gestione pacchetti.

1. Avvia quickstart di AEM

Verifica la configurazione tramite la console OSGI:`http://localhost:4502/system/console/osgi-installer`. L’elenco deve includere i bundle relativi al componente aggiuntivo CIF, il pacchetto di contenuti e le configurazioni OSGI. Assicurati che tutti i bundle siano avviati.

## Configurazione del progetto {#project}

Esistono due modi per avviare il progetto AEM Commerce utilizzando CIF.

### Usare AEM Project Archetype

Il [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) è lo strumento principale per avviare un progetto preconfigurato con cui iniziare a utilizzare CIF. I Componenti core CIF e tutte le configurazioni richieste possono essere inclusi in un progetto generato con un’opzione aggiuntiva.

>[!TIP]
>
>Usa [AEM Project Archetype 25 o versioni successive](https://github.com/adobe/aem-project-archetype/releases) per generare il progetto.

Consulta le [istruzioni d’uso](https://github.com/adobe/aem-project-archetype#usage) di AEM Project Archetype per la generazione di un progetto AEM. Per includere CIF nel progetto, usa l’opzione `includeCommerce`.

Esempio:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

I componenti core CIF possono essere utilizzati in qualsiasi progetto includendo il pacchetto `all` fornito o singoli utenti tramite il pacchetto di contenuti CIF e i bundle OSGI correlati. Per aggiungere manualmente componenti core CIF a un progetto, usa le seguenti dipendenze:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Usare AEM Venia Reference Store

Una seconda opzione per avviare un progetto CIF è clonare e utilizzare [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store è un esempio di applicazione di vetrina di riferimento che illustra l’utilizzo dei componenti core CIF di AEM. Si tratta di un insieme di esempi di best practice e di un potenziale punto di partenza per sviluppare le tue funzionalità.

Per iniziare a utilizzare Venia Reference Store, è sufficiente clonare l&#39;archivio [Git](https://github.com/adobe/aem-cif-guides-venia) e iniziare a personalizzare il progetto in base alle tue esigenze.

>[!NOTE]
>
>Il progetto Venia Reference Store contiene due profili di build per AEM as a Cloud Service e AEM 6.5. Controlla il [file readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) del progetto per vedere come vengono utilizzati. Per AEM 6.5 utilizzare il profilo `classic`.

### Collegare AEM al sistema Commerce

Per collegare il progetto al sistema commerce, AEM deve essere configurato con l’endpoint GraphQL del sistema commerce.

Entrambi, un progetto generato da [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype) o [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia), include già una [configurazione predefinita](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) che deve essere modificata.

Sostituire il valore di `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con l&#39;endpoint GraphQL del sistema commerce utilizzato dal progetto.

Il componente aggiuntivo AEM Commerce e i componenti core CIF si connettono all’endpoint commerce GraphQL tramite il server AEM e direttamente tramite il browser. Per impostazione predefinita, i componenti core CIF lato client e gli strumenti di creazione dei componenti aggiuntivi CIF si connettono a `/api/graphql`. Se necessario, questo può essere regolato tramite la configurazione di CIF Cloud Service (vedi sotto).

Il componente aggiuntivo CIF fornisce un servlet proxy GraphQL in `/api/graphql`. Se non prevedi di utilizzare un Dispatcher AEM locale, è consigliabile configurare anche il servlet proxy di GraphQL.

Passare a http://localhost:4502/system/console/configMgr e creare una configurazione OSGI per il servizio `Adobe CIF GraphQL Proxy Configuration`. Utilizza lo stesso endpoint GraphQL del sistema commerce utilizzato per il client GraphQL di cui sopra.

## Risorse aggiuntive

- [Archetipo di progetto AEM](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
