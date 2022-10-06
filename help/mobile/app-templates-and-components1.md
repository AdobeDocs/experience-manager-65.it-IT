---
title: Modelli e componenti per app
seo-title: App Templates and Components
description: Leggi questa pagina per scoprire di più sui modelli e i componenti delle app. Fornisce informazioni dettagliate sulla struttura dei modelli.
seo-description: Follow this page to learn about App Templates and Components. It provides detailed information on the structure of templates.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Modelli e componenti per app{#app-templates-and-components}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Un modello viene utilizzato per creare una pagina e definisce quali componenti possono essere utilizzati all’interno dell’ambito selezionato. Un modello è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.

Ogni modello presenta una selezione di componenti disponibili per l’uso.

* I modelli sono costituiti da [Componenti](/help/sites-developing/components.md);
* I componenti utilizzano e consentono l’accesso ai Widget e questi vengono utilizzati per il rendering del contenuto.

>[!NOTE]
>
>Per informazioni su come sviluppare l’applicazione AEM utilizzando CRXDE Lite, consulta [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Un modello è la base di una pagina.

Per creare una pagina, il modello deve essere copiato (node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**) nella posizione corrispondente nell&#39;albero del sito: questo è ciò che accade se una pagina viene creata utilizzando **Siti Web** scheda .

Questa azione di copia dà alla pagina anche il suo contenuto iniziale (di solito solo contenuto di livello principale) e la proprietà sling:resourceType, il percorso del componente della pagina che viene utilizzato per eseguire il rendering della pagina (tutto nel nodo figlio jcr:content).

## Struttura di un modello {#structure-of-a-template}

Ci sono due aspetti da considerare:

* la struttura del modello stesso
* la struttura del contenuto prodotto quando viene utilizzato un modello

Un modello viene creato sotto un nodo di tipo **cq:Template**.

È possibile impostare varie proprietà, in particolare:

* **jcr:title** - titolo del modello; viene visualizzata nella finestra di dialogo durante la creazione di una pagina.
* **jcr:description** - descrizione del modello; viene visualizzata nella finestra di dialogo durante la creazione di una pagina.

Questo nodo contiene *a jcr:content (cq:PageContent)* nodo utilizzato come base per il nodo del contenuto delle pagine risultanti; riferimenti, utilizzando *sling:resourceType*, il componente da utilizzare per il rendering del contenuto effettivo di una nuova pagina.

>[!NOTE]
>
>Per informazioni di base sui modelli e i componenti in AEM, consulta le risorse seguenti:
>
>* [Modelli](/help/sites-developing/templates.md)
>* [Componenti](/help/sites-developing/components.md)
>


Dopo aver acquisito le nozioni di base su Modelli e componenti, consulta le risorse seguenti:

* [Creazione e aggiunta di modelli e componenti](/help/mobile/mobile-ondemand-app-templates.md)
* [Utilizzo delle proprietà di contenuto per esportare il contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Best practice  ](/help/mobile/best-practices-aem-mobile.md)
* [Sviluppo di servizi per contenuti AEM Mobile](/help/mobile/developing-content-services.md)

### Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sugli argomenti relativi alle app per dispositivi mobili, consulta i collegamenti seguenti:

* [Mobile con sincronizzazione dei contenuti](/help/mobile/mobile-ondemand-contentsync.md)
* [Verifica delle app mobili](/help/mobile/develop-mobile-apps-testing.md)
