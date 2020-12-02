---
title: Amministrazione di siti Web
seo-title: Amministrazione di siti Web
description: Scopri come gestire siti Web multilingue in AEM.
seo-description: Scopri come gestire siti Web multilingue in AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
translation-type: tm+mt
source-git-commit: 0885fb6eb6b6a6b8fefd522b2656c8f64e0a537e
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 4%

---


# Amministrazione di siti Web{#website-administration}

I seguenti strumenti di amministrazione sono disponibili per la gestione di siti Web e pagine:

* Multi Site Manager (MSM) consente di utilizzare lo stesso contenuto del sito in più posizioni, consentendo allo stesso tempo l&#39;utilizzo di varianti:

   * [Riutilizzo del contenuto: Multi-Site Manager e Live Copy](/help/sites-administering/msm.md)

* La traduzione consente di automatizzare la traduzione di contenuti di una pagina, risorse e contenuti generati dagli utenti per creare e gestire siti Web multilingue:

   * [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md)

* Queste due funzioni possono essere combinate per gestire siti Web che sono [Multilinazionali e Multilingue](#multinational-and-multilingual-sites).

## Siti multinazionali e multilingue {#multinational-and-multilingual-sites}

È possibile creare contenuti per siti multinazionali e multilingue in modo efficiente grazie all&#39;utilizzo combinato di Multi Site Manager e al flusso di lavoro di traduzione. Create un sito master in una lingua, per un paese specifico, quindi utilizzate tale contenuto come base per gli altri siti, utilizzando la traduzione ove necessario:

* [Tradurre ](/help/sites-administering/translation.md) il sito principale in diverse lingue.

* Utilizzate [Multi Site Manager](/help/sites-administering/msm.md) per:

   * Riutilizzate i contenuti del sito principale e le traduzioni per creare siti per altri paesi e culture.
   * Assicuratevi di limitare l&#39;uso di Multi Site Manager ai contenuti in una lingua, ad esempio master inglese -> filiali in lingua inglese in siti di paese, master francese -> filiali in lingua francese in siti di paese.
   * Se necessario, staccate gli elementi delle copie in diretta per aggiungere dettagli sulla localizzazione.

Il diagramma seguente illustra l’intersezione dei concetti principali (ma non mostra tutti i livelli/elementi coinvolti):

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>In questo e in altri scenari, MSM non gestisce le diverse versioni in quanto tale.
>
>* [MSM ](/help/sites-administering/msm.md) gestisce la distribuzione di contenuto convertito da un blueprint (ad esempio, un master globale) alle Live Copy (ad esempio i siti locali), entro i limiti di una lingua.
>* Le funzionalità di [traduzione](/help/sites-administering/translation.md) integrazione di AEM, insieme ai servizi di gestione della traduzione di terze parti, gestiscono le lingue e traducono i contenuti in queste diverse lingue.

>
>
Per casi d&#39;uso più avanzati, MSM può essere utilizzato anche nelle lingue master.

>[!NOTE]
>
>Per tutti i casi di utilizzo si consiglia di consultare le best practice seguenti:
>
>* [Best practice per MSM](/help/sites-administering/msm-best-practices.md); in particolare:
   >
   >   
   * [Crea sito](/help/sites-administering/msm-best-practices.md#create-site)
   >   * [MSM e siti Web multilingue](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [Best practice per la traduzione](/help/sites-administering/tc-bp.md)

