---
title: Console Rapporti
seo-title: Reports Console
description: Scopri come accedere ai rapporti
seo-description: Learn how to access reports
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# Console Rapporti {#reports-console}

## Panoramica {#overview}

Per AEM Communities, è possibile accedere a diversi rapporti in diversi modi dall’ambiente di authoring.

In generale, le varie relazioni sono:

* [Rapporto visualizzazioni](#views-report)

   Fornisce un grafico dei contenuti dei membri della community e dei visitatori del sito per qualsiasi sito della community.

* [Rapporto sui post](#posts-report)

   Fornisce un grafico dei vari tipi di post dei membri della community su qualsiasi sito della community.

I rapporti tabulari possono essere esportati in formato .csv per successive elaborazioni.

## Console di reporting {#reporting-consoles}

### Rapporti per siti della community {#reports-for-community-sites}

* Dalla navigazione globale: **[!UICONTROL Navigazione]** > **[!UICONTROL Community]** >  **[!UICONTROL Rapporti]**

* Scegli tra:

   * **[!UICONTROL Rapporto assegnazioni]**

      * Genera un report per la sede, l&#39;utente o il gruppo della community selezionati e l&#39;assegnazione.
   * **[!UICONTROL Rapporto sui post]**

      * Genera un report per il sito della community selezionato, il tipo di contenuto e il periodo di tempo.
   * **[!UICONTROL Rapporto visualizzazioni]**

      * genera un rapporto per il sito della community, il tipo di contenuto e il periodo di tempo selezionati.



![rapporti](assets/reports1.png)

## Rapporto visualizzazioni {#views-report}

La console Visualizzazioni consente di generare rapporti sulle visualizzazioni di pagina in base alle funzioni della community per un determinato periodo di tempo.

![rapporto visivo](assets/view-report.png)

Seleziona i criteri per il rapporto:

* **[!UICONTROL Sito]**

   Seleziona un sito community.

* **[!UICONTROL Tipo di contenuto]**

   È possibile scegliere Tutti i contenuti o selezionare una delle funzioni presenti sul sito.

* **[!UICONTROL Intervallo temporale]**

   Seleziona una delle seguenti opzioni:

   * Ultimi 7 giorni
   * Ultimi 30 giorni
   * Ultimi 90 giorni
   * Ultimo anno

Seleziona **[!UICONTROL Genera]** per creare il rapporto.

![generate-views](assets/generate-views.png)

## Rapporto sui post {#posts-report}

La console Post consente di generare rapporti sul numero di post nelle funzioni della community per un determinato periodo di tempo.

![post-report](assets/posts-report.png)

Seleziona i criteri per il rapporto:

* **[!UICONTROL Sito]**

   Seleziona un sito community.

* **[!UICONTROL Tipo di contenuto]**

   È possibile scegliere Tutti i contenuti o selezionare una delle funzioni presenti sul sito.

* **[!UICONTROL Intervallo temporale]**

   Seleziona una delle seguenti opzioni:

   * Ultimi 7 giorni
   * Ultimi 30 giorni
   * Ultimi 90 giorni
   * Ultimo anno

Seleziona **[!UICONTROL Genera]** per creare il rapporto.

![genera rapporto](assets/generate-posts-report.png)

## Risoluzione dei problemi {#troubleshooting}

### Nessun sito community elencato {#no-community-sites-listed}

Se non sono elencati siti della community, assicurati che Adobe Analytics sia stato abilitato per un sito. Se si selezionano i rapporti relativi alle assegnazioni, verificare che la funzione delle assegnazioni si trovi nella struttura del sito della community.

### I rapporti non vengono visualizzati nell’istanza di AEM Author {#reports-do-not-show-in-aem-author-instance}

Se i rapporti non vengono visualizzati nell’istanza di authoring di AEM, controlla le personalizzazioni, ad esempio la mappatura degli URL sull’istanza di pubblicazione. Se la mappatura URL viene eseguita solo sull’istanza di pubblicazione AEM del sito Communities, assicurati che lo stesso sia stato configurato nell’istanza di authoring AEM in **Report Trend del sito Social Component Factory** configurazione.

![Mappatura URL su AEM Author](assets/sitetrend.png)
