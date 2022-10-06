---
title: Interazione con la colonna vertebrale
seo-title: Backbone interaction
description: Informazioni concettuali sull’utilizzo dei modelli JavaScript di backbone nell’area di lavoro di AEM Forms.
seo-description: Conceptual information about use of Backbone JavaScript models in AEM Forms workspace.
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
exl-id: 8fd9770b-6ec4-4b09-b6b2-47a5e5d40f79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Interazione con la colonna vertebrale{#backbone-interaction}

Backbone è una libreria che aiuta a creare e seguire l&#39;architettura MVC nelle applicazioni web. L’idea di base di Backbone consiste nell’organizzare l’interfaccia in viste logiche, affiancate da modelli, ciascuno dei quali può essere aggiornato in modo indipendente quando il modello cambia, senza dover ridisegnare la pagina. Per ulteriori informazioni sulla colonna vertebrale, consulta [https://backbonejs.org](https://backbonejs.org/).

Alcuni concetti chiave sono i seguenti:

**Modello a spina dorsale** Contiene dati e la maggior parte della logica relativa a tali dati.

**Vista dorsale** Utilizzato per rappresentare lo stato del modello corrispondente. La visualizzazione backbone si comporta come un controller, ascoltando eventi dell&#39;interfaccia utente come i clic dell&#39;utente o per modellare eventi (come i dati modificati) e modifica l&#39;interfaccia utente in base alle necessità.

**Modello HTML** Un modello di wrapper con segnaposto popolati dal modello.

**Area di lavoro di AEM Forms** Contiene diversi componenti singoli. Ogni componente:

* Rappresenta un singolo elemento dell’interfaccia utente logica.
* Può essere una raccolta di componenti simili.
* È costituito da modello Backbone, vista Backbone e modello HTML.
* Contiene un riferimento a un servizio.
* Contiene un riferimento alle utility richieste.

Quando un componente viene inizializzato, vengono creati i seguenti oggetti:

* Viene creata una nuova istanza di modello Backbone per il componente. Il servizio viene inserito nel modello.
* Viene creata una nuova istanza della vista Backbone.
* L&#39;istanza del modello, del modello HTML e delle utility corrispondenti viene inserita nella vista.

Nella vista Backbone è presente una mappa evento che mappa i vari eventi che possono verificarsi a causa delle interazioni dell’interfaccia utente con un gestore corrispondente. Questa mappatura viene avviata una volta inizializzato un componente.

Quando una visualizzazione viene inizializzata, la visualizzazione chiama il modello corrispondente per recuperare i dati dal server. Quando tutti i dati richiesti da una visualizzazione sono disponibili, la visualizzazione esegue il rendering dei dati nel formato specificato dal modello di HTML. Più visualizzazioni possono condividere lo stesso modello per la comunicazione.

![](do-not-localize/aem_forms_workflow.png)

Esempio:

1. L&#39;utente fa clic su un modello di attività nell&#39;elenco delle attività.
1. La visualizzazione attività ascolta il clic e chiama la funzione di rendering sul modello attività.
1. Il modello di task successivamente chiama il servizio che è un punto comune per tutte le comunicazioni con il server AEM Forms.
1. La classe di servizio chiama l’endpoint REST di AEM Forms per il metodo di rendering tramite ajax.
1. Il callback di successo per questa chiamata Ajax è definito nel modello di task.
1. Il modello di task genera un evento di backbone come notifica del completamento della chiamata di rendering.
1. Un&#39;altra visualizzazione, la visualizzazione dei dettagli dell&#39;attività, ascolta l&#39;evento dal modello di task.
1. La visualizzazione dei dettagli dell&#39;attività modifica quindi il modello dei dettagli dell&#39;attività in modo da visualizzare all&#39;utente l&#39;attività di cui è stato eseguito il rendering (modulo, dettagli, allegati, note e così via).
