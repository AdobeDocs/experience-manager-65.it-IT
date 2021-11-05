---
title: Compatibilità con le versioni precedenti in AEM 6.5
seo-title: Backward Compatibility in AEM 6.5
description: Scopri come mantenere le tue app e configurazioni compatibili con AEM 6.5
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
>Per un elenco delle modifiche di contenuto e configurazione che non rientrano nell’ambito del pacchetto di compatibilità, consulta [Ristrutturazione dell’archivio in AEM](/help/sites-deploying/repository-restructuring.md).

Nella AEM 6.5, tutte le funzioni sono state sviluppate pensando alla compatibilità con le versioni precedenti.

Nella maggior parte dei casi, i clienti che eseguono AEM 6.3 non devono modificare il codice o le personalizzazioni durante l&#39;aggiornamento. Per i clienti AEM 6.1 e 6.2 non vi sono modifiche di interruzione aggiuntive rispetto a quelle che si verificherebbero durante un aggiornamento alla versione 6.3.

Per le eccezioni in cui le funzionalità non potevano essere mantenute compatibili con le versioni precedenti, i problemi di incompatibilità con le versioni precedenti per i bundle e i contenuti possono essere attenuati installando un pacchetto di compatibilità per la versione 6.4 (vedi come impostare di seguito per i dettagli su dove scaricare). Questo pacchetto di compattazione aiuterà a ripristinare la compatibilità nella maggior parte dei casi per le applicazioni conformi a AEM 6.4.

Il pacchetto di compatibilità consente di eseguire AEM in modalità di compatibilità e di differire lo sviluppo personalizzato rispetto alle nuove funzioni di AEM:

>[!NOTE]
>
>Nota che il pacchetto di compatibilità è solo una soluzione temporanea per posticipare lo sviluppo necessario per essere compatibile con AEM 6.5. Questa opzione è consigliata solo come ultima se non sei in grado di risolvere i problemi di compatibilità tramite sviluppo immediatamente dopo l’aggiornamento. Si consiglia vivamente di passare alla modalità nativa e disinstallare il pacchetto di compatibilità una volta deciso di procedere con lo sviluppo personalizzato basato su 6.5 e usufruire della funzionalità 6.5 completa.

![sasso](assets/sase.png)

Il pacchetto di compatibilità dispone di due modalità: **Routing abilitato** e **Routing disattivato**.

Questo consente di eseguire AEM 6.5 in tre modalità:

**Modalità nativa:**

La modalità nativa è per i clienti che desiderano utilizzare tutte le nuove funzioni di AEM 6.5 e sono pronti a svolgere alcune attività di sviluppo per far sì che le loro personalizzazioni funzionino con tutte le nuove funzioni.

Ciò significa che potrebbe essere necessario apportare modifiche all&#39;applicazione immediatamente dopo l&#39;aggiornamento.

**Modalità di compatibilità: Pacchetto di compatibilità installato con Routing abilitato**

La modalità di compatibilità è destinata ai clienti che hanno personalizzazioni di interfacce non compatibili con le versioni precedenti. Questo consente di eseguire AEM in modalità di compatibilità e di differire lo sviluppo personalizzato richiesto rispetto alle nuove funzionalità AEM che non sono compatibili con alcuni dei codici personalizzati.

**Modalità legacy: Pacchetto di compatibilità installato con Routing disabilitato**

La modalità legacy è destinata ai clienti con interfacce personalizzate basate su codice legacy o obsoleto di AEM che è stato spostato nel pacchetto di compatibilità.

![sapone](assets/sapte.png)

## Configurazione {#how-to-set-up}

La **Pacchetto di compatibilità AEM 6.4 per 6.5** può essere installato come pacchetto utilizzando Gestione pacchetti. È possibile scaricare [AEM 6.4 Pacchetto di compatibilità per 6.5 dalla Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) sito.

Una volta installato il pacchetto di compatibilità, il routing può essere abilitato o disabilitato utilizzando un interruttore nella configurazione OSGI come mostrato di seguito:

![Interruttori](assets/compat-switches.png)

Una volta installato e configurato il pacchetto di compatibilità, le funzioni verranno utilizzate in base alla modalità di compatibilità scelta.
