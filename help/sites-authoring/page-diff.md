---
title: Differenze tra pagine
description: È possibile confrontare in modalità affiancata i contenuti di due pagine, evidenziandone le differenze rilevate.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 3beea5cd-5ae0-485b-8dfc-8b3a23c11586
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 80%

---

# Differenze tra pagine {#page-diff}

## Introduzione {#introduction}

La creazione dei contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. La visualizzazione separata di due versioni di una pagina è inefficiente e soggetta a errori. L’autore desidera poter confrontare facilmente la pagina corrente affiancata a un’altra sua versione.

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

Consulta i rispettivi argomenti su come avviare la funzione per il rilevamento delle differenze all’interno di questi contesti.

### Presentazione delle differenze   {#presentation-of-differences}

Indipendentemente dal contenuto confrontato, la presentazione della differenza rimane la stessa.

* Il contenuto selezionato all’avvio della funzione per il rilevamento delle differenze viene visualizzato a sinistra (il punto di ingresso).
* Il contenuto con cui viene confrontato viene visualizzato a destra (rispetto a cosa viene confrontato il contenuto selezionato).

Ad esempio, se si confrontano le versioni, la versione corrente viene visualizzata a sinistra e la versione precedente a destra.

L’origine di entrambe le pagine viene visualizzata in modo chiaro nella barra dell’intestazione nella parte superiore della finestra del browser.

![Origine mostrata nell’intestazione](assets/chlimage_1-109.png)

La differenza rileva le modifiche apportate a livello di componente e HTML. Gli elementi che sono stati modificati sono evidenziati con colori diversi.

**Modifiche ai componenti**

* Verde chiaro: componente aggiunto
* Rosa: componente rimosso

**Modifiche HTML**

* Verde scuro: HTML aggiunto
* Rosso - HTML rimosso

>[!NOTE]
>
>Quando si confrontano le copie per lingua, l’evidenziazione viene disattivata in quanto in una traduzione cambia tutto e l’evidenziazione non avrebbe alcun vantaggio.

### Modalità a schermo intero e Uscita   {#fullscreen-and-exiting}

Per concentrarti su un contenuto particolare, puoi fare clic sull’icona a schermo intero di entrambi i &quot;lati&quot; di side-by-side diff (differenze affiancate) per ingrandirla fino alla finestra del browser completa.

![Icona modalità a tutto schermo](do-not-localize/chlimage_1-18.png)

Il lato selezionato occupa l’intera finestra, ma nella parte superiore rimane visualizzata la barra che consente di alternare tra le due pagine.

![La barra in alto consente di passare da una pagina all’altra](assets/chlimage_1-110.png)

Per chiudere la visualizzazione a schermo intero, fai clic sull’icona per uscire dalla modalità a tutto schermo.

![Chiudi schermo intero](do-not-localize/chlimage_1-19.png)

Puoi uscire dalla modalità di confronto affiancato delle differenze in qualsiasi momento facendo clic sul pulsante Chiudi, nell’intestazione.

## Limiti   {#limitations}

In alcune situazioni, il confronto delle differenze della pagina potrebbe non essere in grado di rilevare una differenza nel modo previsto.

* Quando si distinguono versioni e avvii, la diff non tiene conto dei componenti dinamici come breadcrumb, menu, elenchi di prodotti o loghi (componenti che si basano sulla struttura del sito per il rendering dei contenuti).
* Per le versioni, non viene ricreato il criterio per il controllo degli accessi e le relazioni Live Copy.
* Se una pagina viene spostata, non sarà più possibile eseguire una rilevazione delle differenze con qualsiasi versione creata prima dello spostamento.

   * Se riscontri problemi con un confronto, controlla la [Timeline](/help/sites-authoring/basic-handling.md#timeline) per la pagina per verificare se la pagina è stata spostata.

>[!NOTE]
>
>Le versioni non possono essere confrontate tra loro. Solo la versione corrente può essere confrontata con altre versioni della pagina. La versione corrente è sempre la versione con le modifiche evidenziate.

>[!NOTE]
>
>Per ulteriori dettagli sul funzionamento del meccanismo di differenze tra pagine e sulle limitazioni che possono influenzare tale meccanismo, vedi [documentazione per sviluppatori](/help/sites-developing/pagediff.md) di questa funzione.
