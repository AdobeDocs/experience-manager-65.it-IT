---
title: Interazione dorsale
description: Informazioni concettuali sull’utilizzo dei modelli JavaScript per backbone nell’area di lavoro di AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 8fd9770b-6ec4-4b09-b6b2-47a5e5d40f79
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms, Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Interazione dorsale{#backbone-interaction}

Backbone è una libreria che aiuta a creare e seguire l’architettura MVC nelle applicazioni web. L’idea di base di Backbone consiste nell’organizzare l’interfaccia in viste logiche, supportate da modelli, ciascuno dei quali può essere aggiornato in modo indipendente quando il modello cambia, senza dover ridisegnare la pagina. Per ulteriori informazioni su Backbone, consulta [https://backbonejs.org](https://backbonejs.org/).

Alcuni concetti chiave sono i seguenti:

**Modello backbone** Contiene dati e la maggior parte della logica correlata a tali dati.

**Vista backbone** Utilizzato per rappresentare lo stato del modello corrispondente. Una vista backbone si comporta come un controller, ascoltando eventi dell’interfaccia utente come i clic dell’utente o gli eventi del modello (come i dati modificati) e modifica l’interfaccia utente in base alle esigenze.

**Modello HTML** Un modello di wrapper con segnaposto popolati dal modello.

**Area di lavoro di AEM Forms** Contiene diversi componenti singoli. Ciascun componente:

* Rappresenta un singolo elemento dell&#39;interfaccia utente logico.
* Può essere una raccolta di componenti simili.
* Composto da modello Backbone, vista Backbone e modello HTML.
* Contiene un riferimento a un servizio.
* Contiene riferimenti alle utility richieste.

Quando un componente viene inizializzato, vengono creati i seguenti oggetti:

* Viene creata una nuova istanza del modello Backbone per il componente. Servizio inserito nel modello.
* Viene creata una nuova istanza della vista Backbone.
* L&#39;istanza del modello, della maschera HTML e delle utilità corrispondenti viene inserita nella vista.

Nella vista Backbone è disponibile una mappa degli eventi che mappa i vari eventi che possono verificarsi a causa delle interazioni dell’interfaccia utente con un gestore corrispondente. Questa mappatura viene avviata una volta inizializzato un componente.

Quando una vista viene inizializzata, chiama il modello corrispondente per recuperare i dati dal server. Quando tutti i dati richiesti da una visualizzazione sono disponibili, la visualizzazione esegue il rendering dei dati nel formato specificato dal modello HTML. Più viste possono condividere lo stesso modello per la comunicazione.

![L’AEM forma la vista della spina dorsale](do-not-localize/aem_forms_workflow.png)

Ecco un esempio:

1. L&#39;utente fa clic su un modello di operazione nell&#39;elenco delle operazioni.
1. La vista Attività ascolta il clic e chiama la funzione di rendering sul modello di attività.
1. Il modello di attività chiama successivamente il servizio, che è un punto comune per tutte le comunicazioni con il server di AEM Forms.
1. La classe servizio chiama l’endpoint REST di AEM Forms per il metodo di rendering tramite AJAX.
1. Il callback di successo per questa chiamata Ajax è definito nel modello di attività.
1. Il modello di attività genera un evento backbone come notifica del completamento della chiamata di rendering.
1. Un&#39;altra visualizzazione, la visualizzazione dettagli attività, ascolta questo evento dal modello attività.
1. Nella visualizzazione Dettagli attività, il modello dei dettagli attività viene modificato in modo da visualizzare all&#39;utente l&#39;attività di cui è stato eseguito il rendering (modulo, dettagli, allegati, note e così via).
