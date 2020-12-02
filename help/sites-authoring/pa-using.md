---
title: Visualizzazione dei dati analitici sulle pagine
seo-title: Visualizzazione dei dati analitici sulle pagine
description: Utilizza i dati analitici pagina per misurare l'efficacia del contenuto della pagina
seo-description: Utilizza i dati analitici pagina per misurare l'efficacia del contenuto della pagina
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 92%

---


# Visualizzazione dei dati analitici sulle pagine{#seeing-page-analytics-data}

Utilizza i dati analitici pagina per misurare l&#39;efficacia del contenuto della pagina.

## Dati analitici visibili dalla console {#analytics-visible-from-the-console}

![a-10](assets/aa-10.png)

I dati analitici pagina vengono visualizzati nella [Vista a elenco](/help/sites-authoring/basic-handling.md#list-view) della console Sites. Quando le pagine vengono visualizzate nel formato elenco, sono disponibili le colonne seguenti per impostazione predefinita:

* Visualizzazioni pagina
* Visitatori univoci
* Tempo sulla pagina

Ciascuna colonna mostra un valore per il periodo di generazione rapporti in corso e indica anche se tale valore è aumentato o diminuito rispetto al periodo di generazione rapporti precedente. I dati visualizzati vengono aggiornati ogni 12 ore.

>[!NOTE]
>
>Per modificare il periodo di aggiornamento, [configura l&#39;intervallo di importazione](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Apri la console **Sites**, ad esempio [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. Nella parte all&#39;estrema destra della barra degli strumenti (angolo in alto a destra), tocca o fai clic sull&#39;icona per selezionare **Vista a elenco** (l&#39;icona mostrata dipende dalla [vista corrente](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Di nuovo, all&#39;estrema destra della barra degli strumenti (angolo in alto a destra) tocca o fai clic sull&#39;icona **Visualizza impostazioni**. Si aprirà la finestra di dialogo **Configura colonne**. Apporta le modifiche necessarie e conferma con **Aggiorna**.

   ![a-04](assets/aa-04.png)

### Selezione del periodo di generazione rapporti {#selecting-the-reporting-period}

Seleziona il periodo di generazione rapporti per il quale i dati di Analytics vengono visualizzati sulla console Sites:

* Dati degli ultimi 30 giorni
* Dati degli ultimi 90 giorni
* Dati di quest&#39;anno

Il periodo di rigenerazione rapporti corrente viene visualizzato nella barra degli strumenti della console Sites (a destra della barra degli strumenti superiore). Utilizza il menu a discesa per selezionare il periodo di generazione rapporti desiderato.
![a-05](assets/aa-05.png)

### Configurazione delle colonne di dati disponibili {#configuring-available-data-columns}

I membri del gruppo utenti amministratori-analytics possono configurare la console Sites per consentire agli autori di vedere ulteriori colonne di Analytics.

>[!NOTE]
>
>Quando una struttura ad albero di pagine contiene elementi secondari associati a diverse configurazioni cloud di Adobe Analytics, non potrai configurare le colonne di dati disponibili per le pagine.

1. In visualizzazione Elenco, utilizzate i selettori di visualizzazione (a destra della barra degli strumenti), selezionate **Visualizza impostazioni**, quindi **Aggiungi dati di analisi personalizzati**.

   ![a-15](assets/aa-15.png)

1. Seleziona le metriche che desideri esporre agli autori nella console Sites, quindi fai clic su **Aggiungi**.

   Le colonne visualizzate vengono recuperate da  Adobe Analytics.

   ![a-16](assets/aa-16.png)

### Apertura di approfondimenti sui contenuti da Sites {#opening-content-insights-from-sites}

Aprite [Content Insight](/help/sites-authoring/content-insights.md) dalla console Siti per approfondire l&#39;efficacia della pagina.

1. Nella console Sites, seleziona la pagina per la quale desideri visualizzare gli approfondimenti dei contenuti.
1. Nella barra degli strumenti, fai clic sull’icona di Analytics e Recommendations.

   ![](do-not-localize/chlimage_1-16a.png)

## Dati analitici visibili dall’Editor pagine (Mappa attività)  {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>Verranno visualizzati se la [mappa attività è stata configurata](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) per il sito web.

>[!NOTE]
>
>I dati per la mappa attività provengono da Adobe Analytics.

Se il sito web è stato [configurato per Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md), puoi utilizzare la [modalità Mappa attività](/help/sites-authoring/author-environment-tools.md#page-modes) per visualizzare i dati pertinenti. Esempio:

![a-07](assets/aa-07.png)

### Accesso alla mappa attività {#accessing-the-activity-map}

Dopo aver selezionato la modalità [Mappa attività](/help/sites-authoring/author-environment-tools.md#page-modes), ti verrà richiesto di immettere le credenziali di Adobe Analytics.

![a-03](assets/aa-03.png)

Viene visualizzata la barra degli strumenti mobile **Analytics**; qui puoi:

* Modificare il formato della barra degli strumenti mediante le frecce doppie (**>>**)
* Attivare i dettagli pagina (icona occhio)
* Configurare le impostazioni della mappa attività (icona a ingranaggio)
* Selezionare le analisi da visualizzare (vari selettori a discesa)
* Chiudere la mappa attività e la barra degli strumenti (x)

![a-09](assets/aa-09.png)

### Selezione dei dati analitici da visualizzare {#selecting-the-analytics-to-show}

Puoi selezionare i dati analitici da mostrare e come devono essere visualizzati, utilizzando i diversi criteri:

* **Standard**/**Live**

* Tipo di evento
* Gruppo di utenti
* **Bolle**/**Sfumatura**/**Vincenti e perdenti**/**Disattivazione**

* Periodo da visualizzare

![a-13](assets/aa-13.png)

### Configurazione della mappa attività {#configuring-the-activity-map}

Utilizza l’icona **Show Settings** (Mostra impostazioni) per aprire la finestra di dialogo **Mappa attività**.

![a-04-1](assets/aa-04-1.png)

La finestra di dialogo delle **impostazioni della mappa attività** fornisce una serie di opzioni su tre schede:

![a-06](assets/aa-06.png)

* Generale

   * Suite di rapporti
   * Nome pagina
   * Lingua
   * Sovrapposizione etichette con
   * Dimensione font etichetta
   * Colore sfumatura
   * Colore bolle
   * Sfumatura colore basato su
   * Trasparenza sfumatura

* Standard

   * Visualizza (tipo e numero di collegamenti)
   * Nascondi sovrapposizioni per collegamenti che non hanno ricevuto hit

* Live

   * Visualizza i migliori (vincenti o perdenti)
   * Escludi la % inferiore
   * Aggiornamento automatico (dati e periodo)

