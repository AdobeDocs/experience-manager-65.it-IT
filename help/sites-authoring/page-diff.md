---
title: Differenze tra pagine
seo-title: Page Diff
description: È possibile confrontare in modalità affiancata i contenuti di due pagine, evidenziandone le differenze rilevate.
seo-description: The page diff feature allows for the convenient side-by-side comparison of two pages with their differences highlighted.
uuid: 5af8b466-5922-4fe6-9eae-7bad99be23e0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8386a16a-9d47-46d5-bc60-5f290c59e60e
docset: aem65
exl-id: 3beea5cd-5ae0-485b-8dfc-8b3a23c11586
source-git-commit: e85aacd45a2bbc38f10d03915e68286f0a55364e
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 46%

---

# Differenze tra pagine {#page-diff}

## Introduzione {#introduction}

La creazione dei contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. Visualizzare una versione di pagina e l’altra è inefficiente e soggetto a errori. L’autore desidera poter confrontare facilmente la pagina corrente affiancata a un’altra sua versione.

È possibile confrontare in modalità affiancata i contenuti di due pagine, evidenziandone le differenze rilevate.

>[!TIP]
>
>Per ulteriori informazioni tecniche su questa funzione, consulta [Sviluppo e differenze tra pagine](/help/sites-developing/pagediff.md#operation-details).

## Utilizzare {#use}

La visualizzazione affiancata delle differenze permette di confrontare:

* [Versioni](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page) - Versione precedente di una pagina con il relativo stato corrente
* [live Copy](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) - Live Copy con la relativa blueprint
* [Lanci](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page) - Lancio con la rispettiva sorgente
* [Copie per lingua](/help/sites-administering/tc-manage.md#comparing-language-copies) - Una pagina prima e dopo la traduzione o la ritraduzione

Consulta i rispettivi argomenti su come avviare la differenze all’interno di tali contesti.

### Presentazione delle differenze   {#presentation-of-differences}

Indipendentemente dal contenuto confrontato, la presentazione della differenza rimane la stessa.

* Il contenuto selezionato all&#39;avvio della diff viene visualizzato a sinistra (il punto di ingresso della diff).
* Il contenuto di confronto viene visualizzato a destra (a cosa viene confrontato il contenuto selezionato).

Ad esempio, se si confrontano le versioni, la versione corrente viene visualizzata a sinistra e la versione precedente a destra.

L’origine di entrambe le pagine viene visualizzata in modo chiaro nella barra dell’intestazione nella parte superiore della finestra del browser.

![Origine mostrata nell’intestazione](assets/chlimage_1-109.png)

La differenza rileva le modifiche a livello di componente e HTML. Gli elementi che sono stati modificati vengono evidenziati con colori diversi.

**Modifiche ai componenti**

* Verde chiaro - Componente aggiunto
* Rosa - Componente rimosso

**Modifiche HTML**

* Verde scuro - HTML aggiunto
* Rosso - HTML rimosso

>[!NOTE]
>
>Quando si confrontano le copie per lingua, l’evidenziazione viene disattivata in quanto in una traduzione cambia tutto e l’evidenziazione non sarebbe di alcun vantaggio.

### Modalità a schermo intero e Uscita   {#fullscreen-and-exiting}

Per concentrarti su un contenuto particolare, fai clic sull’icona schermo intero di entrambi i “lati” a confronto, per ingrandire il contenuto nella finestra del browser a schermo intero.

![Icona modalità a tutto schermo](do-not-localize/chlimage_1-18.png)

Il lato selezionato occupa l’intera finestra, ma nella parte superiore rimane visualizzata la barra che consente di alternare tra le due pagine.

![La barra in alto consente di passare da una pagina all’altra](assets/chlimage_1-110.png)

Per chiudere la visualizzazione a schermo intero, fai clic sull’icona per uscire dalla modalità a tutto schermo.

![Chiudi schermo intero](do-not-localize/chlimage_1-19.png)

Puoi uscire dalla modalità di confronto affiancato delle differenze in qualsiasi momento facendo clic sul pulsante Chiudi, nell’intestazione.

## Limiti   {#limitations}

In alcune situazioni, la differenza di pagina potrebbe non rilevare una differenza come previsto.

* Quando si differenzia tra versioni e avvii, la diff non tiene conto dei componenti dinamici come breadcrumb, menu, elenchi di prodotti o loghi (componenti che si basano sulla struttura del sito per il rendering dei contenuti).
* Per le versioni, non viene ricreato il criterio per il controllo degli accessi e le relazioni Live Copy.
* Se una pagina viene spostata, non è più possibile eseguire una differenze con le versioni effettuate prima dello spostamento.

   * Se riscontri problemi con una differenza, controlla [Timeline](/help/sites-authoring/basic-handling.md#timeline) affinché la pagina possa vedere se è stata spostata.

>[!NOTE]
>
>Le versioni non possono essere confrontate tra di loro. Solo la versione corrente può essere confrontata con altre versioni della pagina. La versione corrente è sempre la versione con le modifiche evidenziate.

>[!NOTE]
>
>Per ulteriori dettagli sul funzionamento del meccanismo di differenze tra pagine e sui limiti che possono influenzare tale meccanismo, consulta la [documentazione per sviluppatori](/help/sites-developing/pagediff.md) di questa funzione.
