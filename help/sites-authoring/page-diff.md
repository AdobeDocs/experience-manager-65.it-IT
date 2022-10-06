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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 100%

---

# Differenze tra pagine {#page-diff}

## Introduzione {#introduction}

La creazione di contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. La visualizzazione separata di due versioni di una pagina è inefficiente e soggetta a errori. L’autore desidera poter confrontare facilmente la pagina corrente affiancata a un’altra sua versione.

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

Consulta i rispettivi argomenti su come avviare la funzione per il rilevamento delle differenze in questi contesti.

### Presentazione delle differenze   {#presentation-of-differences}

A prescindere dal contenuto, la presentazione delle differenze rimane la stessa.

* Il contenuto selezionato viene visualizzato a sinistra (punto di ingresso per il rilevamento delle differenze).
* Il contenuto con cui viene confrontato è visualizzato a destra.

Ad esempio, se si confrontano due versioni, la versione corrente è a sinistra e quella precedente a destra.

L’origine di entrambe le pagine è indicata chiaramente nella barra dell’intestazione, nella parte superiore della finestra del browser.

![chlimage_1-109](assets/chlimage_1-109.png)

Vengono rilevate le modifiche apportate a livello di componente e di codice HTML. Gli elementi che sono stati modificati sono evidenziati con colori diversi.

**Modifica componenti**

* Verde chiaro - Componente aggiunto
* Rosa - Componente rimosso

**Modifiche HTML**

* Verde scuro - HTML aggiunto
* Rosso - HTML rimosso

>[!NOTE]
>
>Quando si confrontano le copie per lingua, l’evidenziazione è disattivata poiché in una traduzione tutto cambia.

### Modalità a schermo intero e Uscita   {#fullscreen-and-exiting}

Per concentrarti su un contenuto particolare, fai clic sull’icona schermo intero di entrambi i “lati” a confronto, per ingrandire il contenuto nella finestra del browser a schermo intero.

![](do-not-localize/chlimage_1-18.png)

Il lato selezionato occupa l’intera finestra, ma nella parte superiore rimane visualizzata la barra che consente di alternare tra le due pagine.

![chlimage_1-110](assets/chlimage_1-110.png)

Per chiudere la visualizzazione a schermo intero, fai clic sull’icona per uscire dalla modalità a tutto schermo.

![](do-not-localize/chlimage_1-19.png)

Puoi uscire dalla modalità di confronto affiancato delle differenze in qualsiasi momento facendo clic sul pulsante Chiudi, nell’intestazione.

## Limiti   {#limitations}

Esistono alcune situazioni in cui il confronto delle differenze della pagina non è in grado di rilevare una differenza nel modo previsto.

* Nel confronto di versioni e lanci, la funzione non prende in considerazione le differenze dinamiche, come i componenti breadcrumb, i menu, gli elenchi di prodotti o i loghi (componenti che si basano sulla struttura del sito per eseguire il rendering del contenuto).
* Per le versioni, non viene ricreato il criterio per il controllo degli accessi e le relazioni Live Copy.
* Se una pagina viene spostata, non ti sarà più possibile eseguire una rilevazione delle differenze con qualsiasi versione creata prima dello spostamento.

   * Se rilevi dei problemi con una differenza, controlla la [Timeline](/help/sites-authoring/basic-handling.md#timeline) per verificare se la pagina è stata spostata.

>[!NOTE]
>
>Le versioni non possono essere confrontate tra di loro. Solo la versione corrente può essere confrontata con altre versioni della pagina. La versione corrente è sempre la versione con le modifiche evidenziate.

>[!NOTE]
>
>Per ulteriori informazioni sull’operazione del meccanismo di differenze tra pagine e sui limiti che possono influenzare tale meccanismo, consulta la [documentazione per gli sviluppatori](/help/sites-developing/pagediff.md) per questa funzione.
