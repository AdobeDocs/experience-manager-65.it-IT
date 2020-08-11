---
title: Console Rapporti
seo-title: Console Rapporti
description: Scopri come accedere ai rapporti
seo-description: Scopri come accedere ai rapporti
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 7%

---


# Console Rapporti {#reports-console}

## Panoramica {#overview}

Per  AEM Communities, esistono diversi rapporti a cui è possibile accedere in diversi modi dall’ambiente di authoring.

In generale, le relazioni sono le seguenti:

* [Rapporto assegnazioni](#assignments-report)

   Per una comunità di [abilitazione](/help/communities/overview.md#enablement-community), fornisce una panoramica dei progressi compiuti dagli studenti nelle loro mansioni, inclusa una valutazione associata nell&#39;implementazione dello standard SCORM.

* [Rapporto visualizzazioni](#views-report)

   Fornisce un grafico del contenuto visualizzato dai membri della community e dai visitatori del sito per qualsiasi sito della community.

* [Rapporto sui post](#posts-report)

   Fornisce un grafico dei vari tipi di post dei membri della community in qualsiasi sito della community.

Quando [Adobe Analytics è abilitato](/help/communities/sites-console.md#analytics), i rapporti includeranno il numero di visualizzazioni, riproduzioni, commenti e valutazioni per ciascuna risorsa di abilitazione nel tempo.

I rapporti tabulari possono essere esportati in formato .csv per l’elaborazione successiva.

## Console di reporting {#reporting-consoles}

### Report per siti community {#reports-for-community-sites}

* Dalla navigazione globale: **[!UICONTROL Navigazione]** > **[!UICONTROL Community]** > **[!UICONTROL Rapporti]**

* Scegli tra:

   * **[!UICONTROL Rapporto assegnazioni]**

      * Genera un report per il sito, l&#39;utente o il gruppo community selezionato e l&#39;assegnazione.
   * **[!UICONTROL Rapporto sui post]**

      * Genera un rapporto per il sito community selezionato, il tipo di contenuto e il periodo di tempo.
   * **[!UICONTROL Rapporto visualizzazioni]**

      * genera un rapporto per il sito community selezionato, il tipo di contenuto e il periodo di tempo.



![report](assets/reports1.png)

### Rapporti per risorse di abilitazione e percorsi di apprendimento {#reports-for-enablement-resources-and-learning-paths}

* Dalla navigazione globale: **[!UICONTROL Navigazione]** > **[!UICONTROL Community]** > **[!UICONTROL Risorse]**

* Selezionate un sito community di abilitazione esistente:

   * Selezionate l’icona **Rapporto** per generare rapporti che coprono tutte le risorse di abilitazione.
   * Selezionate un percorso di apprendimento per l’abilitazione.
   * Selezionate l’icona **Rapporto** per generare i rapporti per:

      * Risorse di abilitazione incluse.
      * Gli studenti assegnati al percorso di apprendimento.

* Tali rapporti forniscono:

   * Dati tabella, scaricabili come CSV:

      * Identificazione dello studente
      * Il loro status
      * Assegnazione o accesso tramite catalogo
      * Numero di osservazioni fatte
      * Valutazione a stella

Per ulteriori dettagli, consultate la sezione [](/help/communities/resources.md#report) Rapporti della console Risorse.

## Rapporto assegnazioni {#assignments-report}

La console Assegnazioni consente di filtrare i rapporti in base all&#39;abilitazione del sito community, degli utenti o dei gruppi e dell&#39;assegnazione.

Il rapporto fornisce informazioni sui loro progressi, nonché eventuali commenti o valutazioni forniti.

![rapporto sulle assegnazioni](assets/assignment-report.png)

Seleziona i criteri per il rapporto:

* **Sito**

   Selezionate un sito community di abilitazione.

* **Utente o gruppo**
   * Selezionate Utente per generare un rapporto per uno studente.
   * Selezionate Gruppo per generare un rapporto per un gruppo di utenti in formazione.

   Il servizio tunnel accederà ai membri e ai gruppi di membri dall&#39;ambiente di pubblicazione.

* **Assegnazione**

   Scegliete tra le risorse di abilitazione assegnate agli studenti selezionati.

Selezionate **Genera** per creare il rapporto:

![generate-report](assets/generate-assignment-report.png)

## Rapporto visualizzazioni {#views-report}

La console Visualizzazioni consente di generare rapporti sulle visualizzazioni di pagina in base alle funzioni per community per un determinato periodo di tempo.

![view-report](assets/view-report.png)

Seleziona i criteri per il rapporto:

* **[!UICONTROL Sito]**

   Selezionate un sito community.

* **[!UICONTROL Tipo di contenuto]**

   Può scegliere Tutto il contenuto o selezionare una delle funzioni presenti sul sito.

* **[!UICONTROL Time frame]**

   Selezionate una delle seguenti opzioni:

   * Ultimi 7 giorni
   * Ultimi 30 giorni
   * Ultimi 90 giorni
   * Ultimo anno

Selezionate **[!UICONTROL Genera]** per creare il rapporto.

![generate-views](assets/generate-views.png)

## Rapporto sui post {#posts-report}

La console Post consente di generare rapporti sul numero di post alle funzioni della community per un determinato periodo di tempo.

![post-report](assets/posts-report.png)

Seleziona i criteri per il rapporto:

* **[!UICONTROL Sito]**

   Selezionate un sito community.

* **[!UICONTROL Tipo di contenuto]**

   Può scegliere Tutto il contenuto o selezionare una delle funzioni presenti sul sito.

* **[!UICONTROL Time frame]**

   Selezionate una delle seguenti opzioni:

   * Ultimi 7 giorni
   * Ultimi 30 giorni
   * Ultimi 90 giorni
   * Ultimo anno

Selezionate **[!UICONTROL Genera]** per creare il rapporto.

![generate-report](assets/generate-posts-report.png)

## Risoluzione dei problemi {#troubleshooting}

### Nessun sito community elencato {#no-community-sites-listed}

Se non è presente alcun sito community, accertatevi che  Adobe Analytics sia stato abilitato per un sito. Se scegli rapporti sulle assegnazioni, assicurati che la funzione delle assegnazioni sia nella struttura del sito della community.

### I rapporti non vengono visualizzati nell&#39;istanza di AEM Author {#reports-do-not-show-in-aem-author-instance}

Se i rapporti non vengono visualizzati nell&#39;istanza di AEM Author, controllate se sono disponibili personalizzazioni, ad esempio la mappatura URL sull&#39;istanza di Publish. Se la mappatura URL viene effettuata solo sull’istanza AEM Publish del sito community, accertatevi che lo stesso sia stato configurato nell’istanza AEM Author nella configurazione **Site Trend Report Social Component Factory** .

![Mappatura URL su AEM Author](assets/sitetrend.png)