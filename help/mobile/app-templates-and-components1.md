---
title: Modelli di app e componenti
description: Segui questa pagina per scoprire di più sui modelli e i componenti dell’app. Fornisce informazioni dettagliate sulla struttura dei modelli.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 1%

---

# Modelli di app e componenti{#app-templates-and-components}

{{ue-over-mobile}}

Un modello viene utilizzato per creare una pagina e definisce quali componenti possono essere utilizzati all’interno dell’ambito selezionato. Un modello è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.

Ogni Modello presenta una selezione di componenti disponibili per l’uso.

* I modelli sono costituiti da [Componenti](/help/sites-developing/components.md);
* I componenti utilizzano i widget e ne consentono l’accesso; questi vengono utilizzati per eseguire il rendering del contenuto.

>[!NOTE]
>
>Per informazioni su come sviluppare l&#39;applicazione Adobe Experience Manager (AEM) utilizzando CRXDE Lite, vedere [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Un modello è la base di una pagina.

Per creare una pagina, è necessario copiare il modello (albero dei nodi **/apps/&lt;myapp>/templates/&lt;mytemplate>**) nella posizione corrispondente nell&#39;albero del sito: questo è ciò che accade se si crea una pagina utilizzando la scheda **Siti Web**.

Questa azione di copia fornisce anche alla pagina il suo contenuto iniziale (in genere solo Contenuto di primo livello) e la proprietà sling:resourceType, il percorso del componente pagina utilizzato per il rendering della pagina (tutto ciò che si trova nel nodo figlio jcr:content).

## Struttura di un modello {#structure-of-a-template}

Vi sono due aspetti da considerare:

* la struttura del modello stesso
* la struttura del contenuto prodotto quando viene utilizzato un modello

Un modello viene creato in un nodo di tipo **cq:Template**.

È possibile impostare varie proprietà, in particolare:

* **jcr:title** - titolo del modello; viene visualizzato nella finestra di dialogo durante la creazione di una pagina.
* **jcr:description** - descrizione del modello; viene visualizzato nella finestra di dialogo durante la creazione di una pagina.

Questo nodo contiene *un nodo jcr:content (cq:PageContent)* che viene utilizzato come base per il nodo di contenuto delle pagine risultanti. Questo fa riferimento, utilizzando *sling:resourceType*, al componente da utilizzare per il rendering del contenuto effettivo di una nuova pagina.

>[!NOTE]
>
>Per informazioni di base sui modelli e i componenti in AEM, consulta le risorse seguenti:
>
>* [Modelli](/help/sites-developing/templates.md)
>* [Componenti](/help/sites-developing/components.md)
>

Dopo aver acquisito le nozioni di base su Modelli e componenti, consulta le risorse seguenti:

* [Creazione e aggiunta di modelli e componenti](/help/mobile/mobile-ondemand-app-templates.md)
* [Utilizzo delle proprietà del contenuto per esportare il contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Best practice](/help/mobile/best-practices-aem-mobile.md)
* [Sviluppo di AEM Mobile Content Services](/help/mobile/developing-content-services.md)

### Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sulle app per dispositivi mobili, consulta i collegamenti seguenti:

* [Dispositivi mobili con sincronizzazione contenuti](/help/mobile/mobile-ondemand-contentsync.md)
* [Verifica delle app mobili](/help/mobile/develop-mobile-apps-testing.md)
