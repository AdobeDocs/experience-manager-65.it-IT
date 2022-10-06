---
title: Struttura dell’interfaccia utente AEM touch
seo-title: Structure of the AEM Touch-Enabled UI
description: L’interfaccia touch, implementata in AEM, presenta diversi principi di base ed è composta da diversi elementi chiave
seo-description: The touch-optimized UI, as implemented in AEM, has several underlying principles and is made up of several key elements
uuid: 9a255238-1adc-4a40-9c37-30cb53ffb26c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 55dba890-4847-4986-b272-33480bc1d573
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 3%

---

# Struttura dell’interfaccia utente AEM touch{#structure-of-the-aem-touch-enabled-ui}

L’interfaccia AEM touch presenta diversi principi di base ed è composta da diversi elementi chiave:

## Console {#consoles}

### Layout di base e ridimensionamento {#basic-layout-and-resizing}

L’interfaccia utente è adatta sia ai dispositivi mobili che a quelli desktop. Invece di creare due stili, l’Adobe ha deciso di utilizzare uno stile che funziona per tutti gli schermi e i dispositivi.

Tutti i moduli utilizzano lo stesso layout di base, AEM può essere visualizzato come segue:

![chlimage_1-142](assets/chlimage_1-142.png)

Il layout aderisce a uno stile di progettazione reattivo e si adatta alle dimensioni del dispositivo o della finestra in uso.

Ad esempio, quando la risoluzione è inferiore a 1024 px (come su un dispositivo mobile), il display viene regolato di conseguenza:

![chlimage_1-143](assets/chlimage_1-143.png)

### Barra intestazione {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

La barra dell’intestazione mostra gli elementi globali, tra cui:

* il logo e lo specifico prodotto/soluzione attualmente in uso; per AEM si tratta anche di un collegamento alla navigazione globale
* Ricerca
* icona per accedere alle risorse dell’Aiuto
* icona per accedere ad altre soluzioni
* un indicatore di (e accesso a) tutti gli avvisi o gli elementi della casella in entrata che ti aspettano
* l’icona utente, insieme a un collegamento alla gestione del profilo

### Barra degli strumenti {#toolbar}

Questo è contestuale agli strumenti di posizione e superfici rilevanti per il controllo della visualizzazione o delle risorse nella pagina sottostante. La barra degli strumenti è specifica per il prodotto, ma esiste una certa comunanza tra gli elementi.

In qualsiasi posizione la barra degli strumenti mostra le azioni attualmente disponibili:

![chlimage_1-145](assets/chlimage_1-145.png)

Dipende anche dal fatto che una risorsa sia attualmente selezionata o meno:

![chlimage_1-146](assets/chlimage_1-146.png)

### Barra a sinistra {#left-rail}

La barra a sinistra può essere aperta o nascosta in base alle esigenze:

* **Timeline**
* **Riferimenti**
* **Filtro**

Il valore predefinito è **Solo contenuto** (barra nascosta).

![chlimage_1-147](assets/chlimage_1-147.png)

## Authoring delle pagine {#page-authoring}

Durante l’authoring delle pagine, le aree strutturali sono le seguenti:

### Frame del contenuto {#content-frame}

Viene eseguito il rendering del contenuto della pagina nel frame del contenuto. La cornice contenuto è completamente indipendente dall’editor, per garantire che non ci siano conflitti dovuti a CSS o javascript.

La cornice contenuto si trova nella sezione destra della finestra, sotto la barra degli strumenti.

![chlimage_1-148](assets/chlimage_1-148.png)

### Frame editor {#editor-frame}

La cornice dell&#39;editor realizza le funzioni di modifica.

Il frame dell&#39;editor è un contenitore (astratto) per tutti i *elementi di authoring delle pagine*. Si trova sopra la cornice del contenuto e include:

* barra degli strumenti superiore
* il pannello laterale
* tutte le sovrapposizioni
* qualsiasi altro elemento di authoring delle pagine; ad esempio, la barra degli strumenti del componente

![chlimage_1-149](assets/chlimage_1-149.png)

### Pannello laterale {#side-panel}

Questa contiene due schede predefinite per la selezione di risorse e componenti; possono essere trascinati da qui e rilasciati sulla pagina.

Il pannello laterale è nascosto per impostazione predefinita. Se selezionata, la finestra verrà visualizzata sul lato sinistro o scivolerà lungo per coprire l&#39;intera finestra (quando la dimensione della finestra è inferiore a 1024 px; come, ad esempio, su un dispositivo mobile).

![chlimage_1-150](assets/chlimage_1-150.png)

### Pannello laterale - Risorse {#side-panel-assets}

Nella scheda Risorse puoi selezionare un intervallo di risorse. Puoi anche filtrare un termine specifico o selezionare un gruppo.

![chlimage_1-151](assets/chlimage_1-151.png)

### Pannello laterale - Gruppi di risorse {#side-panel-asset-groups}

Nella scheda Risorsa è disponibile un elenco a discesa che puoi utilizzare per selezionare i gruppi di risorse specifici.

![chlimage_1-152](assets/chlimage_1-152.png)

### Pannello laterale - Componenti {#side-panel-components}

Nella scheda Componenti puoi selezionare uno dei diversi componenti disponibili. Puoi anche filtrare un termine specifico o selezionare un gruppo.

![chlimage_1-153](assets/chlimage_1-153.png)

### Sovrapposizioni {#overlays}

Sovrappongono il frame del contenuto e vengono utilizzati dal [livelli](#layer) realizzare la meccanica su come interagire (in modo completamente trasparente) con i componenti e i loro contenuti.

Le sovrapposizioni sono presenti nel frame dell’editor (con tutti gli altri elementi di authoring delle pagine), anche se sovrappongono i componenti appropriati nel frame del contenuto.

![chlimage_1-154](assets/chlimage_1-154.png)

### Livello {#layer}

Un livello è un bundle indipendente di funzionalità che può essere attivato per:

* fornire una visualizzazione diversa della pagina
* consente di manipolare e/o interagire con una pagina

I livelli forniscono funzionalità sofisticate per l’intera pagina, anziché azioni specifiche su un singolo componente.

AEM include diversi livelli già implementati per l’authoring delle pagine; ad esempio modifica, anteprima, annotazione.

>[!NOTE]
>
>I livelli sono un concetto potente che influisce sulla visualizzazione e sull’interazione dell’utente con il contenuto della pagina. Quando si sviluppano i propri livelli, è necessario assicurarsi che il livello si ripulisca quando viene lasciato.

### Selettore livello {#layer-switcher}

Lo switcher di livello consente di scegliere il livello da utilizzare. Una volta chiuso, indica il livello attualmente in uso.

Il commutatore di livello è disponibile come un menu a discesa dalla barra degli strumenti (nella parte superiore della finestra, all’interno della cornice dell’editor).

![chlimage_1-155](assets/chlimage_1-155.png)

### Barra degli strumenti del componente {#component-toolbar}

Ogni istanza di un componente mostra la relativa barra degli strumenti quando viene fatto clic su (una volta o con un doppio clic lento). La barra degli strumenti contiene le azioni specifiche (ad esempio copia, incolla, editor aperto) disponibili per l’istanza del componente (modificabile) nella pagina.

A seconda dello spazio disponibile, le barre degli strumenti dei componenti sono posizionate nell’angolo superiore o inferiore destro del componente appropriato.

![chlimage_1-156](assets/chlimage_1-156.png)

## Ulteriori informazioni {#further-information}

Per ulteriori dettagli sui concetti relativi all’interfaccia touch, continua a seguire l’articolo [Concetti dell’interfaccia AEM touch](/help/sites-developing/touch-ui-concepts.md).

Per ulteriori informazioni tecniche consulta la sezione [Set di documentazione JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) per l’editor pagina touch.
