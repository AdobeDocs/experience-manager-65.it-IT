---
title: Compatibilità con le versioni precedenti della AEM 6.5
seo-title: Compatibilità con le versioni precedenti della AEM 6.5
description: Scoprite come mantenere le app e le configurazioni compatibili con AEM 6.5
seo-description: Scoprite come mantenere le app e le configurazioni compatibili con AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
translation-type: tm+mt
source-git-commit: 303841896717448947aa48ece7ae86519a5450d5
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Compatibilità con le versioni precedenti di AEM 6.5{#backward-compatibility-in-aem}

## Panoramica {#overview}

>[!NOTE]
>
>Per un elenco delle modifiche di contenuto e configurazione che non rientrano nell&#39;ambito del pacchetto di compatibilità, vedere [Ristrutturazione del repository in AEM](/help/sites-deploying/repository-restructuring.md).

In AEM 6.5, tutte le funzioni sono state sviluppate tenendo presente la compatibilità con le versioni precedenti.

Nella maggior parte dei casi, i clienti che eseguono AEM 6.3 non devono cambiare il codice o le personalizzazioni durante l&#39;aggiornamento. Per i clienti AEM 6.1 e 6.2 non sono previste modifiche di rottura aggiuntive rispetto a quelle che si verificavano durante un aggiornamento alla versione 6.3.

Per le eccezioni per le quali le funzionalità non potevano essere mantenute compatibili con le versioni precedenti, i problemi di incompatibilità arretrata per i bundle e i contenuti possono essere attenuati installando un pacchetto di compatibilità per la versione 6.4 (vedere come impostare di seguito per i dettagli su dove scaricare). Questo pacchetto di componenti aiuterà a ripristinare la compatibilità nella maggior parte dei casi per le applicazioni conformi a AEM 6.4.

Il pacchetto di compatibilità consente di eseguire AEM in modalità di compatibilità e differire lo sviluppo personalizzato rispetto alle nuove funzioni di AEM:

>[!NOTE]
>
>Il pacchetto di compatibilità è solo una soluzione temporanea per posticipare lo sviluppo necessario per essere compatibile con AEM 6.5. Questa opzione è consigliata solo come ultima opzione se non siete in grado di risolvere i problemi di compatibilità attraverso lo sviluppo subito dopo l&#39;aggiornamento. È fortemente consigliato passare alla modalità nativa e disinstallare il pacchetto di compatibilità una volta che si decide di procedere con lo sviluppo personalizzato basato su 6.5 e sfruttare la funzionalità completa 6.5.

![sase](assets/sase.png)

Il pacchetto di compatibilità presenta due modalità: **Routing abilitato** e **Routing disattivato**.

Questo consente di eseguire AEM 6.5 in tre modalità:

**Modalità nativa:**

La modalità nativa è per i clienti che desiderano utilizzare tutte le nuove funzionalità di AEM 6.5 e sono pronti a sviluppare le proprie personalizzazioni in modo che funzionino con tutte le nuove funzioni.

Ciò significa che potrebbe essere necessario apportare modifiche all&#39;applicazione subito dopo l&#39;aggiornamento.

**Modalità compatibilità: Pacchetto di compatibilità installato con Routing abilitato**

La modalità di compatibilità è per i clienti che hanno personalizzazioni di interfacce non compatibili con le versioni precedenti. Questo consente di eseguire AEM in modalità di compatibilità e differire lo sviluppo personalizzato richiesto rispetto alle nuove funzionalità AEM non compatibili con alcuni codici personalizzati.

**Modalità legacy: Pacchetto di compatibilità installato con Routing disattivato**

La modalità legacy è per i clienti con interfacce personalizzate basate su codice legacy o obsoleto AEM spostato nel pacchetto di compatibilità.

![sapone](assets/sapte.png)

## Configurazione {#how-to-set-up}

Il pacchetto di compatibilità AEM 6.3 può essere installato come pacchetto utilizzando Package Manager. È possibile scaricare il pacchetto di compatibilità [AEM 6.3 dal sito di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/compatpack/aem-compat-cq64-to-cq63).

Una volta installato il pacchetto di compatibilità, il routing può essere abilitato o disabilitato utilizzando uno switch nella configurazione OSGI come mostrato di seguito:

![screen_shot_2017-11-27at122421pm](assets/screen_shot_2017-11-27at122421pm.png)

Una volta installato e configurato il pacchetto di compatibilità, le funzioni verranno utilizzate in base alla modalità di compatibilità scelta.
