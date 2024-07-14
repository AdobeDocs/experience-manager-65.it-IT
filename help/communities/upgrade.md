---
title: Aggiornamento alle community AEM 6.5
description: Come effettuare l’aggiornamento da una versione precedente a AEM 6.5 Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Aggiornamento alle community AEM 6.5 {#upgrading-to-aem-communities}

A seconda della topologia e delle funzionalità di ciascun sito, potrebbe essere necessario eseguire le azioni seguenti durante l’aggiornamento ad AEM Communities 6.5 o l’installazione del feature pack più recente.

Questa sezione è specifica per Communities e integra le informazioni fornite in [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md) (piattaforma).

## Aggiornamento da AEM 6.1 o versione successiva {#upgrading-from-aem-or-later}

### Reindicizza Solr {#reindex-solr}

Quando si installa un nuovo feature pack Communities in una distribuzione configurata con MSRP, è necessario:

1. Installa il [pacchetto di funzionalità più recente](/help/communities/deploy-communities.md#latestfeaturepack).
1. Installa i [file di configurazione Solr più recenti](/help/communities/msrp.md#upgrading).
1. Reindicizza MSRP
vedere la sezione [Strumento di reindicizzazione MSRP](/help/communities/msrp.md#msrp-reindex-tool).

## Aggiornamento da AEM 6.0 {#upgrading-from-aem}

Se è necessario mantenere un UGC preesistente, i mezzi per farlo dipendono dal fatto che la distribuzione abbia memorizzato un UGC [on-premise](#on-premise-storage) o nel [cloud Adobe](#adobe-cloud-storage).

### Adobe Cloud Storage {#adobe-cloud-storage}

Se il sito aggiornato è stato configurato per l’utilizzo dell’archiviazione cloud Adobe, potrebbe sembrare (erroneamente) che tutti i contenuti generati dagli utenti siano stati persi, in quanto i metodi SRP non saranno in grado di individuare i contenuti generati dagli utenti preesistenti nella posizione precedente.

È quindi possibile istruire ASRP a utilizzare `AEM 6.0 compatability-mode` per accedere a UGC.

Per tutte le istanze di authoring e pubblicazione di AEM 6.3:

* Accedi con privilegi di amministratore.
* Configura [ASRP](/help/communities/asrp.md).
* Per rendere visibili contenuti generati dagli utenti preesistenti, segui la procedura riportata di seguito:

   * Passa alla console Web:

      * Ad esempio, [https://&lt;host>:&lt;porta>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Individua la configurazione di **Utilità AEM Communities**.
      * Seleziona per espandere il pannello di configurazione:

         * *Deseleziona* `Cloud Storage`

         * Seleziona **Salva**

     ![utilità](assets/utilities.png)

### Archiviazione locale {#on-premise-storage}

Se il sito aggiornato non utilizzava l’archiviazione cloud, eventuali contenuti UGC preesistenti devono essere convertiti per essere conformi alla nuova struttura introdotta nelle community AEM 6.1 a supporto dello store comune.

A questo scopo, su GitHub è disponibile uno strumento di migrazione open source:
[Strumento di migrazione UGC per AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API Java {#java-apis}

Durante l’aggiornamento dalle social community AEM 6.0 alle community AEM 6.3, molte API sono state riorganizzate in pacchetti diversi. La maggior parte dovrebbe essere facilmente risolta quando si utilizza un IDE per personalizzare le funzioni di Communities.

Per informazioni dettagliate sul pacchetto SocialUtils obsoleto, visita [Refactoring SocialUtils](/help/communities/socialutils.md).

Vedi anche [Utilizzo di Maven per le community](/help/communities/maven.md).

### Nessun modello di componente JSP {#no-jsp-component-templates}

Il [framework dei componenti social](/help/communities/scf.md) (SCF) utilizza il linguaggio di modelli [HandlebarsJS](https://handlebarsjs.com/) (HBS) al posto delle Java Server Pages (JSP) utilizzate prima di AEM 6.0.

In AEM 6.0, i componenti JSP sono rimasti accanto ai nuovi componenti framework HBS nella stessa posizione, con i componenti HBS in genere nelle sottocartelle denominate &quot;hbs&quot;.

A partire da AEM 6.1, i componenti JSP sono stati completamente rimossi. Per le community, si consiglia di sostituire tutti gli utilizzi di componenti JSP con componenti SCF.

## Strumento di migrazione UGC per AEM Communities {#aem-communities-ugc-migration-tool}

Lo strumento di migrazione UGC [AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) è uno strumento di migrazione open source, disponibile su GitHub, che può essere personalizzato per esportare UGC da versioni precedenti delle social community AEM e importarlo in AEM Communities 6.1 o versione successiva.

Oltre a spostare UGC da versioni precedenti, è anche possibile utilizzare lo strumento per spostare UGC da un [SRP](/help/communities/working-with-srp.md) a un altro, ad esempio da MSRP a DSRP.

## Aggiornamento da AEM 5.6.1 o versioni precedenti {#upgrading-from-aem-or-earlier}

Concettualmente, esistono tre generazioni di componenti community :

**Gen 1**: Circa da CQ 5.4 a AEM 5.6.0, questi sono i componenti **collab** che hanno archiviato UGC nell&#39;archivio locale utilizzando la replica come mezzo per sincronizzare UGC tra le piattaforme. Altre differenze riguardano l’implementazione tramite Java Server Pages (JSP) e la funzione di blog che consiste nell’authoring solo nell’ambiente di authoring.

**Gen 2**: Da AEM 5.6.1 a AEM 6.1, è una combinazione di **collab** e **social** componenti. AEM 6.0 ha introdotto il nuovo [framework per componenti social](/help/communities/scf.md) (SCF) e AEM 6.2 ha introdotto un [archivio UGC comune](/help/communities/working-with-srp.md) in cui è possibile accedere a UGC utilizzando un [provider di risorse di archiviazione](/help/communities/srp.md) (SRP).

**Gen 3**: a partire da AEM 6.2, sono presenti solo **componenti social**, implementati in SCF come componenti Handlebars (HBS) che richiedono la scelta di SRP per UGC.
