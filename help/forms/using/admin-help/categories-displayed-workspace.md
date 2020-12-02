---
title: Gestione delle categorie visualizzate in Workspace
seo-title: Gestione delle categorie visualizzate in Workspace
description: In Workspace, i processi che un utente può avviare vengono visualizzati in categorie nel riquadro di navigazione a sinistra. Scopri come gestire queste categorie visualizzate in Workspace.
seo-description: In Workspace, i processi che un utente può avviare vengono visualizzati in categorie nel riquadro di navigazione a sinistra. Scopri come gestire queste categorie visualizzate in Workspace.
uuid: c2a275f5-872e-467f-9f07-4b130631e8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d1536a2-10ac-4031-bd7f-264b02d0d75f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Gestione delle categorie visualizzate in Workspace {#managing-the-categories-displayed-in-workspace}

In Workspace, i processi che un utente può avviare vengono visualizzati in categorie nel riquadro di navigazione a sinistra. È possibile impostare le categorie nella console di amministrazione oppure i progettisti di processi possono configurarle in Workbench. Quando i progettisti di processi creano dei processi, li assegnano a categorie.

Quando si specificano i nomi delle categorie, crearli in modo che vengano visualizzati correttamente nel riquadro di navigazione Area di lavoro. Per impostazione predefinita, il riquadro di navigazione a sinistra ha una larghezza fissa di 210 pixel, che è di circa 24 caratteri. Se il nome della categoria specificato è troppo lungo per adattarsi alla larghezza fissa del riquadro di navigazione a sinistra, viene troncato. Il nome completo viene visualizzato solo quando il puntatore del mouse viene messo in pausa. Cercate di evitare nomi di categoria che verranno troncati. Gli esempi seguenti illustrano i nomi delle categorie che possono essere inseriti e troncati:

**Nome categoria adatto:** Partecipazione e uscita

**Nome categoria troncato:** Partecipazione e uscita (Stati Uniti)

In Workspace, i processi all&#39;interno di una categoria vengono generalmente visualizzati come schede nella pagina Avvia processo. In generale, sei schede possono essere visualizzate sullo schermo per una categoria prima che l&#39;utente sia tenuto a scorrere per visualizzare le schede rimanenti. Poiché lo scorrimento rende più difficile trovare un processo, è consigliabile limitare ciascuna categoria a sei processi oppure, a seconda della risoluzione, limitare il numero di processi che possono essere visualizzati sullo schermo senza richiedere alcuno scorrimento.

Se si utilizza MySQL come database di moduli AEM, la console di amministrazione non può distinguere tra due nomi di categoria che differiscono solo nell&#39;uso di caratteri estesi. Ad esempio, se si crea una categoria denominata abcde e una denominata âbcdè, vengono considerate uguali.

## Aggiungere una categoria {#add-a-category}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione categorie.
1. Fate clic su Aggiungi. Se desiderate aggiungere una sottocategoria, selezionate una categoria e fate clic su Aggiungi.
1. Nella casella Nome, digitare un nome per la categoria e digitare una descrizione della categoria nella casella Descrizione.
1. Fate clic su Aggiungi. La categoria viene visualizzata nella pagina Gestione categorie.

   ***nota **: Durante la creazione di categorie è possibile aggiungere fino a cinque livelli di gerarchia.*

## Modificare una categoria {#edit-a-category}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione categorie.
1. Selezionate la categoria da modificare e fate clic su Modifica. In alternativa, potete fare doppio clic su una categoria da modificare.
1. Modificate il nome della categoria nella casella Nome.

## Rimuovere una categoria {#remove-a-category}

È possibile rimuovere solo le categorie non utilizzate.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione categorie.
1. Nella pagina Gestione categorie selezionare la casella di controllo per la categoria da rimuovere e fare clic su Rimuovi. La categoria non viene più visualizzata.

