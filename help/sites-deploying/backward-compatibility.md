---
title: Compatibilità con le versioni precedenti in AEM 6.5
seo-title: Compatibilità con le versioni precedenti in AEM 6.5
description: Scopri come mantenere le tue app e configurazioni compatibili con AEM 6.5
seo-description: Scopri come mantenere le tue app e configurazioni compatibili con AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
translation-type: tm+mt
source-git-commit: c863e438df45fd54c29c1b99114eea07aaeb6162

---


# Compatibilità con le versioni precedenti in AEM 6.5{#backward-compatibility-in-aem}

## Panoramica {#overview}

>[!NOTE]
>
>Per un elenco delle modifiche al contenuto e alla configurazione che non rientrano nell’ambito del pacchetto di compatibilità, consultate Ristrutturazione [repository in AEM](/help/sites-deploying/repository-restructuring.md).

In AEM 6.5, tutte le funzioni sono state sviluppate tenendo presente la compatibilità con le versioni precedenti.

Nella maggior parte dei casi, i clienti che eseguono AEM 6.3 non devono cambiare il codice o le personalizzazioni durante l&#39;aggiornamento. Per i clienti di AEM 6.1 e 6.2 non vi sono modifiche di interruzione aggiuntive rispetto a quelle apportate durante un aggiornamento alla versione 6.3.

Per le eccezioni per le quali le funzionalità non potevano essere mantenute compatibili con le versioni precedenti, i problemi di incompatibilità arretrata per i bundle e i contenuti possono essere attenuati installando un pacchetto di compatibilità per la versione 6.4 (vedere come impostare di seguito per i dettagli su dove scaricare). Questo pacchetto di supporto consentirà di ripristinare la compatibilità nella maggior parte dei casi per le applicazioni conformi con AEM 6.4.

Il pacchetto di compatibilità consente di eseguire AEM in modalità di compatibilità e di differire lo sviluppo personalizzato rispetto alle nuove funzioni di AEM:

>[!NOTE]
>
>Il pacchetto di compatibilità è solo una soluzione temporanea per posticipare lo sviluppo necessario per essere compatibile con AEM 6.5. È consigliato solo come ultima opzione se non siete in grado di risolvere problemi di compatibilità tramite lo sviluppo subito dopo l’aggiornamento. È fortemente consigliato passare alla modalità nativa e disinstallare il pacchetto di compatibilità una volta che si decide di procedere con lo sviluppo personalizzato basato su 6.5 e sfruttare la funzionalità completa 6.5.

![sase](assets/sase.png)

Il pacchetto di compatibilità presenta due modalità: **Routing abilitato** e **Routing disattivato**.

Questo consente di eseguire AEM 6.5 in tre modalità:

**Modalità nativa:**

La modalità nativa è per i clienti che desiderano utilizzare tutte le nuove funzioni di AEM 6.5 e sono pronti a sviluppare qualcosa per far sì che le loro personalizzazioni funzionino con tutte le nuove funzioni.

Ciò significa che potrebbe essere necessario apportare modifiche all&#39;applicazione subito dopo l&#39;aggiornamento.

**Modalità compatibilità: Pacchetto di compatibilità installato con Routing abilitato**

La modalità di compatibilità è per i clienti che hanno personalizzazioni di interfacce non compatibili con le versioni precedenti. Questo consente ad AEM di essere eseguito in modalità di compatibilità e di posticipare lo sviluppo personalizzato richiesto rispetto alle nuove funzioni di AEM non compatibili con alcuni codici personalizzati.

**Modalità legacy: Pacchetto di compatibilità installato con Routing disattivato**

La modalità legacy è per i clienti con interfacce personalizzate basate su codice legacy o obsoleto di AEM spostato nel pacchetto di compatibilità.

![sapone](assets/sapte.png)

## Come impostare {#how-to-set-up}

Il pacchetto di compatibilità di AEM 6.3 verrà installato come pacchetto tramite Gestione pacchetti al [collegamento](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-compat-cq64-to-cq63).

Una volta installato il pacchetto di compatibilità, il routing può essere abilitato o disabilitato utilizzando uno switch nella configurazione OSGI come mostrato di seguito:

![screen_shot_2017-11-27at122421pm](assets/screen_shot_2017-11-27at122421pm.png)

Una volta installato e configurato il pacchetto di compatibilità, le funzioni verranno utilizzate in base alla modalità di compatibilità scelta.
