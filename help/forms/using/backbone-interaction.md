---
title: Interazione con il dorso
seo-title: Interazione con il dorso
description: Informazioni concettuali sull'utilizzo di modelli JavaScript di backbone nell'area di lavoro  AEM Forms.
seo-description: Informazioni concettuali sull'utilizzo di modelli JavaScript di backbone nell'area di lavoro  AEM Forms.
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Interazione con la spina dorsale{#backbone-interaction}

Backbone è una libreria che consente di creare e seguire l&#39;architettura MVC nelle applicazioni Web. L&#39;idea di base di Backbone consiste nell&#39;organizzare l&#39;interfaccia in viste logiche, affiancate da modelli, ciascuno dei quali può essere aggiornato indipendentemente quando il modello cambia, senza dover ridisegnare la pagina. Per ulteriori informazioni sulla dorsale, vedere [https://backbonejs.org](https://backbonejs.org/).

Alcuni concetti chiave sono i seguenti:

**Backbone** modelContiene i dati e la maggior parte della logica ad essi correlati.

**Backbone** viewUtilizzato per rappresentare lo stato del modello corrispondente. Una vista dorsale si comporta come un controller, ascoltando eventi dell&#39;interfaccia utente come clic dell&#39;utente o eventi del modello (come i dati modificati) e modificando l&#39;interfaccia utente a seconda delle necessità.

**HTML** templateModello wrapper con segnaposto popolati dal modello.

**** area di lavoro AEM FormsContiene diversi componenti singoli. Ciascun componente:

* Rappresenta un singolo elemento di interfaccia utente logico.
* Può essere un insieme di componenti simili.
* È costituito da un modello Backbone, una vista Backbone e un modello HTML.
* Contiene un riferimento a un servizio.
* Contiene un riferimento alle utility richieste.

Quando un componente viene inizializzato, vengono creati i seguenti oggetti:

* Viene creata una nuova istanza del modello Backbone per il componente. Il servizio è inserito nel modello.
* Viene creata una nuova istanza della vista Backbone.
* Nella vista vengono inserite le istanze del modello, del modello HTML e delle utility corrispondenti.

Nella visualizzazione Backbone è presente una mappa evento che mappa i vari eventi che possono verificarsi a causa delle interazioni dell&#39;interfaccia utente con un gestore corrispondente. Questa mappatura viene avviata una volta inizializzato un componente.

Quando una vista viene inizializzata, la vista richiama il modello corrispondente per recuperare i dati dal server. Quando tutti i dati richiesti da una visualizzazione sono disponibili, la visualizzazione esegue il rendering dei dati nel formato specificato dal modello HTML. Viste multiple possono condividere lo stesso modello per la comunicazione.

![](do-not-localize/aem_forms_workflow.png)

Esempio:

1. L&#39;utente fa clic su un modello di attività nell&#39;elenco delle attività.
1. La visualizzazione Attività ascolta il clic e richiama la funzione di rendering sul modello attività.
1. Il modello di task chiama in seguito il servizio che è un punto comune per tutte le comunicazioni con  server AEM Forms.
1. Chiamate della classe di servizio  endpoint REST di AEM Forms per il metodo di rendering tramite ajax.
1. Il callback di riuscita per questa chiamata Ajax è definito nel modello attività.
1. Il modello di task genera un evento dorsale come notifica del completamento della chiamata di rendering.
1. Un&#39;altra visualizzazione, la visualizzazione dei dettagli dell&#39;attività, ascolta l&#39;evento dal modello dell&#39;attività.
1. La visualizzazione Dettagli attività modifica quindi il modello dei dettagli dell&#39;attività per visualizzare all&#39;utente l&#39;attività di cui è stato effettuato il rendering (modulo, dettagli, allegati, note e così via).
