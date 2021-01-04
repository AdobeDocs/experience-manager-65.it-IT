---
title: Aggiornamento ad AEM 6.5 Communities
seo-title: Aggiornamento ad AEM 6.5 Communities
description: Come effettuare l’aggiornamento da una versione precedente a AEM community 6.5
seo-description: Come effettuare l’aggiornamento da una versione precedente a AEM community 6.5
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: 612d102b5925704ce459ad818554e487ec0d5355
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Aggiornamento ad AEM 6.5 Communities {#upgrading-to-aem-communities}

A seconda della topologia e delle caratteristiche di ciascun sito, per effettuare l&#39;aggiornamento ad AEM Communities 6.5 o installare l&#39;ultimo pacchetto di funzioni potrebbero essere necessarie le azioni seguenti.

Questa sezione è specifica per Communities e completa le informazioni fornite in [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md) (piattaforma).

## Aggiornamento da AEM 6.1 o successivo {#upgrading-from-aem-or-later}

### Reindicizzare Solr {#reindex-solr}

Durante l&#39;installazione di un nuovo pacchetto di funzionalità Community su una distribuzione configurata con MSRP, sarà necessario:

1. Installare il [pacchetto di funzionalità più recente](/help/communities/deploy-communities.md#latestfeaturepack).
1. Installate i [file di configurazione Solr più recenti](/help/communities/msrp.md#upgrading).
1. Reindicizza MSRP
vedere la sezione [MSRP Reindex Tool](/help/communities/msrp.md#msrp-reindex-tool).

### Attivazione 2.0 {#enablement}

A partire da AEM 6.3, le funzioni di abilitazione non memorizzano più le informazioni di reporting in MySQL. La dipendenza MySQL è presente solo per il tracciamento del contenuto SCORM.

Per assistenza durante la migrazione dei contenuti da Enablement 1.0, contattate l&#39; [Assistenza clienti](https://helpx.adobe.com/it/marketing-cloud/contact-support.html).

## Aggiornamento da AEM 6.0 {#upgrading-from-aem}

Se è necessario mantenere l&#39;UGC preesistente, i mezzi per farlo dipendono dal fatto che la distribuzione abbia memorizzato UGC [locale](#on-premise-storage) o nel [ Adobe cloud](#adobe-cloud-storage).

###  Adobe di archiviazione cloud {#adobe-cloud-storage}

Se il sito aggiornato è stato configurato per l&#39;utilizzo  Adobe di archiviazione cloud, potrebbe apparire (in modo non corretto) come se tutti gli UGC fossero andati persi in quanto i metodi SRP non sarebbero in grado di individuare gli UGC preesistenti nella vecchia posizione.

Di conseguenza, è possibile indicare ad ASRP di utilizzare `AEM 6.0 compatability-mode` per accedere a UGC.

Per tutte le istanze di creazione e pubblicazione AEM 6.3:

* Effettuate l&#39;accesso con privilegi di amministratore.
* Configurare [ASRP](/help/communities/asrp.md).
* Per rendere visibile l’UGC preesistente, effettuate le seguenti operazioni:

   * Passate alla console Web:

      * Ad esempio, [https://&lt;host>:&lt;porta>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Individuare la configurazione **AEM Communities Utilities**.
      * Selezionare per espandere il pannello di configurazione:

         * *Deseleziona* `Cloud Storage`

         * Seleziona **Salva**

      ![utilità](assets/utilities.png)


### Storage locale {#on-premise-storage}

Se il sito aggiornato non ha utilizzato l&#39;archiviazione cloud, qualsiasi UGC preesistente deve essere convertito in conformità alla nuova struttura introdotta in AEM 6.1 Communities a supporto dello store comune.

A questo scopo, su GitHub è disponibile uno strumento di migrazione open source:
[ AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API Java {#java-apis}

Quando eseguite l&#39;aggiornamento da AEM 6.0 social community a AEM community 6.3, tenete presente che molte API sono state riorganizzate in pacchetti diversi. La maggior parte dovrebbe essere facilmente risolta quando si utilizza un IDE per la personalizzazione delle funzionalità di Communities.

Per informazioni dettagliate sul pacchetto SocialUtils obsoleto, visitate [SocialUtils Refactoring](/help/communities/socialutils.md).

Vedere anche [Utilizzo di Paradiso per Communities](/help/communities/maven.md).

### Nessun modello di componente JSP {#no-jsp-component-templates}

Il [social component framework](/help/communities/scf.md) (SCF) utilizza il linguaggio HTML [HandlebarsJS](https://www.handlebarsjs.com/) (HBS) anziché Java Server Pages (JSP) utilizzato prima del AEM 6.0.

In AEM 6.0, i componenti JSP sono rimasti accanto ai nuovi componenti framework HBS nella stessa posizione, con i componenti HBS generalmente situati in sottocartelle denominate &quot;hbs&quot;.

A partire dal AEM 6.1, i componenti JSP sono stati completamente rimossi. Per Communities, si consiglia di sostituire tutti gli usi dei componenti JSP con i componenti SCF.

##  AEM Communities UGC Migration Tool {#aem-communities-ugc-migration-tool}

[ AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) è uno strumento di migrazione open source, disponibile su GitHub, che può essere personalizzato per esportare UGC da versioni precedenti di AEM social community e importare  AEM Communities 6.1 o versioni successive.

Oltre a spostare UGC da versioni precedenti, è anche possibile utilizzare lo strumento per spostare UGC da un [SRP](/help/communities/working-with-srp.md) a un altro, ad esempio da MSRP a DSRP.

## Aggiornamento da AEM 5.6.1 o versioni precedenti {#upgrading-from-aem-or-earlier}

Concettualmente, esistono tre generazioni di componenti per comunità:

**Gen 1**: CQ 5.4 e AEM 5.6.0 circa, questi sono i componenti  **** collabcomponents che hanno memorizzato UGC nell&#39;archivio locale utilizzando la replica come mezzo per sincronizzare UGC tra piattaforme. Altre differenze riguardano l’implementazione tramite Java Server Pages (JSP), nonché la funzione blog che consiste nell’authoring solo nell’ambiente di authoring.

**Gen 2**: Da AEM 5.6.1 a AEM 6.1, questo è un mix di  **** colletti e componenti  **** sociali. AEM 6.0 ha introdotto il nuovo [social component framework](/help/communities/scf.md) (SCF) e AEM 6.2 ha introdotto un [archivio UGC comune](/help/communities/working-with-srp.md) in cui è possibile accedere a UGC utilizzando un [provider di risorse di storage](/help/communities/srp.md) (SRP).

**Gen 3**: A partire dal AEM 6.2, vi sono solo componenti  **** socialistici, implementati in SCF come componenti Handlebars (HBS) che richiedono una scelta di SRP per UGC.
