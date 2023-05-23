---
title: Sviluppare il Commerce AEM
description: Scopri come generare un progetto AEM abilitato per il commercio utilizzando l’archetipo di progetto AEM. Scopri come generare e distribuire il progetto in un ambiente di sviluppo locale.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
source-git-commit: 78359fb8ecbcc0227ab5a3910175aed73d823902
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 34%

---

# Sviluppo del commercio AEM {#develop}

Lo sviluppo di progetti commerciali dell’AEM basati su Commerce Integration Framework (CIF) per l’AEM segue le stesse regole e best practice di altri progetti dell’AEM. Prima di tutto, consulta i seguenti argomenti:

- [Guida utente allo sviluppo in AEM 6.5](/help/sites-developing/home.md)
- [Concetti di base dell’AEM](/help/sites-developing/the-basics.md)
- [Sviluppo AEM - Linee guida e best practice](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Come creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md)

## Sviluppo locale per il commercio AEM {#local}

Si consiglia di utilizzare un ambiente di sviluppo locale con progetti CIF.

>[!NOTE]
>
>Le istruzioni seguenti sono utili per creare un ambiente locale per lo sviluppo AEM per il commercio AEM utilizzando CIF con particolare attenzione per AEM 6.5). Se sta usando AEM as a Cloud Service, consulti il [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html?lang=it) documentazione.

Il componente aggiuntivo AEM Commerce per AEM 6.5, alias. Il componente aggiuntivo CIF è disponibile anche per lo sviluppo locale e fornito come pacchetto AEM. Può essere scaricato da [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html) come feature pack.

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

Il componente aggiuntivo CIF può essere scaricato da [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html), cerca il componente aggiuntivo AEM Commerce.

>[!TIP]
>
>Occorre utilizzare sempre la versione più recente del componente aggiuntivo CIF.

### Configurazione locale

Per lo sviluppo di progetti CIF locali utilizzando l’AEM e il componente aggiuntivo CIF, procedere come segue:

1. Scarica la versione AEM 6.5 e installa il Service Pack AEM 6.5. È richiesto AEM 6.5 Service Pack 7, tuttavia si consiglia di installare l’ultimo service pack disponibile.

1. Decomprimi il file AEM.jar per creare la cartella `crx-quickstart` ed esegui:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Crea una cartella `crx-quickstart/install`.

1. Copiare il pacchetto del componente aggiuntivo CIF, scaricato dal portale di distribuzione software, nella `crx-quickstart/install` cartella.

>[!TIP]
>
>In alternativa, il pacchetto del componente aggiuntivo CIF può essere installato anche tramite Gestione pacchetti.

1. Avviare l’avvio rapido dell’AEM

Verifica la configurazione tramite la console OSGI:`http://localhost:4502/system/console/osgi-installer`. L’elenco deve includere i bundle relativi al componente aggiuntivo CIF, il pacchetto di contenuti e le configurazioni OSGI. Assicurati che tutti i bundle siano avviati.

## Configurazione del progetto {#project}

Esistono due modi per avviare il progetto AEM Commerce utilizzando CIF.

### Usare AEM Project Archetype

Il [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) è lo strumento principale per avviare un progetto preconfigurato con cui iniziare a utilizzare CIF. I componenti core CIF e tutte le configurazioni richieste possono essere inclusi in un progetto generato con un’opzione aggiuntiva.

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

I componenti core CIF possono essere utilizzati in qualsiasi progetto includendo il `all` o singolo utente utilizzando il pacchetto di contenuti CIF e i bundle OSGI correlati. Per aggiungere manualmente componenti core CIF a un progetto, usa le seguenti dipendenze:

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

Per iniziare a usare Venia Reference Store, è sufficiente clonare il file [Archivio Git](https://github.com/adobe/aem-cif-guides-venia) e inizia a personalizzare il progetto in base alle tue esigenze.

>[!NOTE]
>
>Il progetto Venia Reference Store contiene due profili di generazione per AEM as a Cloud Service e AEM 6.5. Controlla il [progetto readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) per vedere come vengono utilizzati. Per l’AEM 6.5 utilizzare il `classic` profilo.

### Collegare l’AEM al sistema Commerce

Per collegare il progetto al sistema commerciale, l’AEM deve essere configurato con l’endpoint GraphQL del sistema commerciale.

Entrambi, un progetto generato da [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype) o [Negozio di riferimento AEM Venia](https://github.com/adobe/aem-cif-guides-venia), include già un [configurazione predefinita](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) che devono essere corretti.

Sostituisci il valore di `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con l’endpoint GraphQL del sistema commerce utilizzato dal progetto.

Il componente aggiuntivo AEM Commerce e i componenti core CIF si connettono all’endpoint commerce GraphQL tramite il server AEM e direttamente tramite il browser. Per impostazione predefinita, i componenti core CIF lato client e gli strumenti di authoring del componente aggiuntivo CIF si connettono a `/api/graphql`. Se necessario, questo può essere regolato tramite la configurazione del Cloud Service CIF (vedi sotto).

Il componente aggiuntivo CIF fornisce un servlet proxy di GraphQL all&#39;indirizzo `/api/graphql`. Se non prevedi di utilizzare un Dispatcher AEM locale, si consiglia di configurare anche il servlet proxy di GraphQL.

Passa a http://localhost:4502/system/console/configMgr e crea una configurazione OSGI per `Adobe CIF GraphQL Proxy Configuration` servizio. Utilizza lo stesso endpoint GraphQL del sistema commerce utilizzato per il client GraphQL di cui sopra.

## Risorse aggiuntive

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
