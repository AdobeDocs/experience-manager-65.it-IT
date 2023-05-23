---
title: Compatibilità con le versioni precedenti in AEM 6.5
seo-title: Backward Compatibility in AEM 6.5
description: Scopri come mantenere le app e le configurazioni compatibili con AEM 6.5
seo-description: Learn how to keep your apps and configurations compatible with AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: 50a11e30ccd720065962e8dd03cbcc71ec9f715a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# Compatibilità con le versioni precedenti in AEM 6.5{#backward-compatibility-in-aem}

## Panoramica {#overview}

>[!NOTE]
>
>Per un elenco delle modifiche al contenuto e alla configurazione che non rientrano nell’ambito del pacchetto di compatibilità, consulta [Ristrutturazione dell’archivio dell’AEM](/help/sites-deploying/repository-restructuring.md).

Con AEM 6.5, tutte le funzioni sono state sviluppate tenendo presente la retrocompatibilità.

Nella maggior parte dei casi, i clienti che eseguono AEM 6.3 non devono essere costretti a modificare il codice o le personalizzazioni durante l’aggiornamento. Per i clienti AEM 6.1 e 6.2 non vi sono ulteriori modifiche che causerebbero interruzioni rispetto a quelle che si verificherebbero durante un aggiornamento alla versione 6.3.

Per le eccezioni in cui le funzionalità non potevano essere mantenute compatibili con le versioni precedenti, i problemi di incompatibilità con le versioni precedenti per bundle e contenuti possono essere attenuati installando un pacchetto di compatibilità per 6.4 (vedi come impostare di seguito per i dettagli su dove scaricare). Questo pacchetto di compatibilità aiuterà a ripristinare la compatibilità nella maggior parte dei casi per le applicazioni conformi a AEM 6.4.

Il pacchetto di compatibilità consente di eseguire AEM in modalità di compatibilità e di posticipare lo sviluppo personalizzato rispetto alle nuove funzioni AEM:

>[!NOTE]
>
>Il pacchetto di compatibilità è solo una soluzione temporanea per posticipare lo sviluppo necessario per la compatibilità con AEM 6.5; consigliato solo come ultima opzione se non è possibile risolvere i problemi di compatibilità tramite lo sviluppo immediatamente dopo l’aggiornamento. Si consiglia vivamente di passare alla modalità nativa e disinstallare il pacchetto di compatibilità una volta che si decide di procedere con lo sviluppo personalizzato basato sulla versione 6.5 e di avvalersi della funzionalità completa 6.5.

![sase](assets/sase.png)

Il pacchetto di compatibilità prevede due modalità: **Indirizzamento abilitato** e **Indirizzamento disabilitato**.

Questo consente di eseguire AEM 6.5 in tre modalità:

**Modalità nativa:**

La modalità nativa è per i clienti che desiderano utilizzare tutte le nuove funzioni di AEM 6.5 e sono pronti a fare qualche sviluppo per far funzionare le loro personalizzazioni con tutte le nuove funzioni.

Ciò significa che potrebbe essere necessario apportare modifiche all&#39;applicazione immediatamente dopo l&#39;aggiornamento.

**Modalità di compatibilità: pacchetto di compatibilità installato con il routing abilitato**

La modalità di compatibilità è rivolta ai clienti che dispongono di personalizzazioni di interfacce non compatibili con le versioni precedenti. Questo consente di eseguire AEM in modalità di compatibilità e di posticipare lo sviluppo personalizzato richiesto per le nuove funzionalità AEM non compatibili con alcuni codici personalizzati.

**Modalità legacy: pacchetto di compatibilità installato con routing disabilitato**

La modalità legacy è destinata ai clienti che dispongono di interfacce personalizzate basate su codice legacy o obsoleto proveniente da AEM che è stato spostato all’esterno del pacchetto di compatibilità.

![sapte](assets/sapte.png)

## Configurazione {#how-to-set-up}

Il **AEM 6.4 Compatability Pack per 6.5** può essere installato come pacchetto utilizzando Gestione pacchetti. È possibile scaricare [AEM 6.4 Compatability Pack per 6.5 da Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) sito.

Una volta installato il pacchetto di compatibilità, il routing può essere abilitato o disabilitato utilizzando uno switch nella configurazione OSGI, come illustrato di seguito:

![Opzioni compatibilità](assets/compat-switches.png)

Una volta installato e configurato il pacchetto di compatibilità, le funzioni verranno utilizzate in base alla modalità di compatibilità scelta.
