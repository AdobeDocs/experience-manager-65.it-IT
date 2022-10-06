---
title: Aggiornamento ad AEM 6.5 Communities
seo-title: Upgrading to AEM 6.5 Communities
description: Come effettuare l’aggiornamento da una versione precedente a AEM community 6.5
seo-description: How to upgrade from an earlier version to AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# Aggiornamento ad AEM 6.5 Communities {#upgrading-to-aem-communities}

A seconda della topologia e delle funzioni di ogni sito, possono essere necessarie le seguenti azioni durante l’aggiornamento ad AEM Communities 6.5 o l’installazione del pacchetto di funzioni più recente.

Questa sezione è specifica delle Comunità e integra le informazioni fornite in [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md) (piattaforma).

## Aggiornamento da AEM 6.1 o versione successiva {#upgrading-from-aem-or-later}

### Solr reindicizzazione {#reindex-solr}

Quando installi un nuovo pacchetto di funzioni di Communities su una distribuzione configurata con MSRP, sarà necessario:

1. Installa il [pacchetto di funzionalità più recente](/help/communities/deploy-communities.md#latestfeaturepack).
1. Installa il [file di configurazione Solr più recenti](/help/communities/msrp.md#upgrading).
1. Reindicizzazione MSRP vedi sezione [Strumento di reindicizzazione MSRP](/help/communities/msrp.md#msrp-reindex-tool).

### Abilitazione 2.0 {#enablement}

A partire da AEM 6.3, le funzioni di abilitazione non memorizzano più le informazioni di reporting in MySQL. La dipendenza MySQL è presente solo per il tracciamento del contenuto SCORM.

Contattare [assistenza clienti](https://helpx.adobe.com/it/marketing-cloud/contact-support.html) per assistenza nella migrazione dei contenuti da Abilitazione 1.0.

## Aggiornamento da AEM 6.0 {#upgrading-from-aem}

Se è necessario mantenere UGC preesistente, i mezzi per farlo dipendono dal fatto che la distribuzione memorizzi UGC [on-premise](#on-premise-storage) o [Adobe cloud](#adobe-cloud-storage).

### Adobe Cloud Storage {#adobe-cloud-storage}

Se il sito aggiornato è stato configurato per l’utilizzo dell’archiviazione cloud di Adobe, potrebbe apparire (in modo errato) come se tutto l’UGC fosse stato perso, in quanto i metodi SRP non saranno in grado di individuare l’UGC preesistente nella vecchia posizione.

Quindi, c&#39;è la possibilità di istruire l&#39;ASRP per utilizzare `AEM 6.0 compatability-mode` per accedere a UGC.

Per tutte le istanze di authoring e pubblicazione AEM 6.3:

* Accedi con privilegi di amministratore.
* Configura [ASRP](/help/communities/asrp.md).
* Segui questi passaggi per rendere visibile un UGC preesistente :

   * Passa alla console Web:

      * Ad esempio: [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Individua **Utilità AEM Communities** configurazione.
      * Seleziona per espandere il pannello di configurazione:

         * *Deseleziona* `Cloud Storage`

         * Seleziona **Salva**

      ![servizi](assets/utilities.png)


### Storage on-premise {#on-premise-storage}

Se il sito aggiornato non ha utilizzato l’archiviazione cloud, qualsiasi UGC preesistente deve essere convertito in conformità alla nuova struttura introdotta in AEM 6.1 Communities a supporto dello store comune.

A questo scopo, su GitHub è disponibile uno strumento di migrazione open source:
[Strumento di migrazione UGC di AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API Java {#java-apis}

Quando esegui l’aggiornamento da AEM 6.0 social community a AEM 6.3 Communities, molte API sono state riorganizzate in pacchetti diversi. La maggior parte dovrebbe essere facilmente risolta quando si utilizza un IDE per la personalizzazione delle funzioni di Communities.

Per informazioni dettagliate sul pacchetto SocialUtils obsoleto, visita [Refactoring di SocialUtils](/help/communities/socialutils.md).

Vedi anche [Utilizzo di Maven per Communities](/help/communities/maven.md).

### Nessun modello di componente JSP {#no-jsp-component-templates}

La [quadro della componente sociale](/help/communities/scf.md) (SCF) utilizza [HandlebarsJS](https://handlebarsjs.com/) (HBS) linguaggio di template al posto di Java Server Pages (JSP) utilizzato prima di AEM 6.0.

Nella AEM 6.0, i componenti JSP sono rimasti accanto ai nuovi componenti del framework HBS nella stessa posizione, con i componenti HBS generalmente situati in sottocartelle denominate &quot;hbs&quot;.

A partire AEM 6.1, i componenti JSP sono stati rimossi completamente. Per Communities, si consiglia di sostituire tutti gli usi dei componenti JSP con i componenti SCF.

## Strumento di migrazione UGC di AEM Communities {#aem-communities-ugc-migration-tool}

La [Strumento di migrazione UGC di AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) è uno strumento di migrazione open source disponibile su GitHub, che può essere personalizzato per esportare contenuti generati dagli utenti generati dagli utenti da versioni precedenti di AEM social community e importarli in AEM Communities 6.1 o versioni successive.

Oltre a spostare UGC da versioni precedenti, è anche possibile utilizzare lo strumento per spostare UGC da uno [SRP](/help/communities/working-with-srp.md) a un altro, ad esempio da MSRP a DSRP.

## Aggiornamento da AEM 5.6.1 o versioni precedenti {#upgrading-from-aem-or-earlier}

Concettualmente, ci sono tre generazioni di componenti di comunità:

**Gen.**: Da CQ 5.4 a AEM 5.6.0 circa, questi sono i **collare** componenti che hanno memorizzato UGC nell’archivio locale utilizzando la replica come mezzo per sincronizzare UGC tra piattaforme. Altre differenze riguardano l’implementazione tramite Java Server Pages (JSP) e la funzione blog che consiste nell’authoring solo nell’ambiente di authoring.

**Gen.**: Da AEM 5.6.1 a AEM 6.1, questo è un mix di **collare** e **sociale** componenti. AEM 6.0 introduce la nuova [quadro della componente sociale](/help/communities/scf.md) (SCF) e AEM 6.2 hanno introdotto un [archivio UGC comune](/help/communities/working-with-srp.md) in cui è possibile accedere a UGC utilizzando un [provider di risorse di archiviazione](/help/communities/srp.md) (SRP).

**Gen.**: A partire da AEM 6.2, **sociale** componenti, implementati in SCF come componenti Handlebars (HBS) che richiedono una scelta di SRP per UGC.
