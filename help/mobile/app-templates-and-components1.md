---
title: Modelli e componenti per app
seo-title: Modelli e componenti per app
description: Segui questa pagina per saperne di più su Modelli e componenti per app. Fornisce informazioni dettagliate sulla struttura dei modelli.
seo-description: Segui questa pagina per saperne di più su Modelli e componenti per app. Fornisce informazioni dettagliate sulla struttura dei modelli.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---


# Modelli e componenti app{#app-templates-and-components}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Un modello viene utilizzato per creare una pagina e definisce quali componenti possono essere utilizzati all’interno dell’ambito selezionato. Un modello è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.

Ogni modello vi presenta una selezione di componenti disponibili per l’uso.

* I modelli sono composti di [Componenti](/help/sites-developing/components.md);
* I componenti utilizzano e consentono l&#39;accesso ai Widget e questi vengono utilizzati per il rendering del contenuto.

>[!NOTE]
>
>Per informazioni su come sviluppare l&#39;applicazione AEM utilizzando il CRXDE Lite, vedere [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Un modello è la base di una pagina.

Per creare una pagina, il modello deve essere copiato (node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**) nella posizione corrispondente nella struttura del sito: questo è ciò che accade se una pagina viene creata utilizzando la scheda **Siti Web**.

Questa azione di copia assegna alla pagina anche il contenuto iniziale (in genere Contenuto di livello principale) e la proprietà sling:resourceType, il percorso del componente della pagina utilizzato per eseguire il rendering della pagina (tutto nel nodo figlio jcr:content).

## Struttura di un modello {#structure-of-a-template}

Occorre considerare due aspetti:

* la struttura del modello stesso
* la struttura del contenuto prodotto quando viene utilizzato un modello

Un modello viene creato sotto un nodo di tipo **cq:Template**.

È possibile impostare diverse proprietà, in particolare:

* **jcr:title** - title per il modello; viene visualizzata nella finestra di dialogo durante la creazione di una pagina.
* **jcr:description** - descrizione del modello; viene visualizzata nella finestra di dialogo durante la creazione di una pagina.

Questo nodo contiene *un nodo jcr:content (cq:PageContent)* che può essere utilizzato come base per il nodo di contenuto delle pagine risultanti; questo fa riferimento, utilizzando *sling:resourceType*, al componente da utilizzare per il rendering del contenuto effettivo di una nuova pagina.

>[!NOTE]
>
>Per informazioni di base sui modelli e componenti in AEM, consulta le risorse seguenti:
>
>* [Modelli](/help/sites-developing/templates.md)
>* [Componenti](/help/sites-developing/components.md)

>



Dopo aver compreso i modelli e i componenti di base, consulta le risorse seguenti:

* [Creazione e aggiunta di modelli e componenti](/help/mobile/mobile-ondemand-app-templates.md)
* [Utilizzo delle proprietà di contenuto per esportare il contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Best practice  ](/help/mobile/best-practices-aem-mobile.md)
* [Sviluppo  AEM Mobile Content Services](//help/mobile/developing-content-services.md)

### Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni su argomenti aggiuntivi sulle app mobili, consulta i collegamenti di seguito:

* [Mobile con sincronizzazione dei contenuti](/help/mobile/mobile-ondemand-contentsync.md)
* [Verifica delle app mobili](/help/mobile/develop-mobile-apps-testing.md)

