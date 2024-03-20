---
title: Gestione delle categorie visualizzate in Workspace
description: In Workspace, i processi che un utente può avviare vengono visualizzati in categorie nel riquadro di navigazione a sinistra. Scopri come gestire queste categorie visualizzate in Workspace.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 62621fe9-f69f-4bc0-aecc-d7bcc3064516
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Gestione delle categorie visualizzate in Workspace {#managing-the-categories-displayed-in-workspace}

In Workspace, i processi che un utente può avviare vengono visualizzati in categorie nel riquadro di navigazione a sinistra. È possibile impostare le categorie nella console di amministrazione oppure i designer del processo possono impostarle in Workbench. Quando i progettisti di processi creano processi, li assegnano a categorie.

Quando si specificano i nomi delle categorie, crearli in modo che vengano visualizzati correttamente nel riquadro di spostamento di Workspace. Per impostazione predefinita, il riquadro di navigazione sinistro ha una larghezza fissa di 210 pixel, pari a circa 24 caratteri. Se il nome della categoria specificato è troppo lungo per essere contenuto nella larghezza fissa del riquadro di spostamento a sinistra, verrà troncato. Il nome completo viene visualizzato solo quando si posiziona il puntatore del mouse su di esso. Prova ad evitare i nomi di categoria che verranno troncati. Negli esempi seguenti vengono illustrati i nomi delle categorie che possono essere adattati e quelli troncati:

**Nome della categoria:** Partecipazione e congedo

**Nome categoria troncato:** Frequenza e congedo (Stati Uniti)

In Workspace, i processi all’interno di una categoria vengono in genere visualizzati come schede nella pagina Avvia processo. In generale, è possibile visualizzare sullo schermo sei schede per una categoria prima che all&#39;utente venga richiesto di scorrere per visualizzare le schede rimanenti. Poiché lo scorrimento rende più difficile trovare un processo, è consigliabile limitare ogni categoria a sei processi o, a seconda della risoluzione, limitare il numero di processi che possono essere visualizzati sullo schermo senza richiedere alcuno scorrimento.

Se si utilizza MySQL come database di moduli AEM, la console di amministrazione non è in grado di distinguere due nomi di categoria che differiscono solo nell&#39;uso di caratteri estesi. Ad esempio, se crei una categoria denominata abcde e una categoria denominata âbcdè, queste vengono considerate uguali.

## Aggiungi una categoria {#add-a-category}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione categorie.
1. Fai clic su Aggiungi. Per aggiungere una sottocategoria, selezionare una categoria e fare clic su Aggiungi.
1. Nella casella Nome digitare un nome per la categoria e nella casella Descrizione digitare una descrizione della categoria.
1. Fai clic su Aggiungi. La categoria viene visualizzata nella pagina Gestione categorie.

   ***nota **: puoi aggiungere fino a cinque livelli gerarchici durante la creazione delle categorie.*

## Modificare una categoria {#edit-a-category}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione categorie.
1. Seleziona la categoria da modificare e fai clic su Modifica. In alternativa, è possibile fare doppio clic su una categoria da modificare.
1. Modificare il nome della categoria nella casella Nome.

## Rimuovere una categoria {#remove-a-category}

È possibile rimuovere solo le categorie non utilizzate.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione categorie.
1. Nella pagina Gestione categorie selezionare la casella di controllo relativa alla categoria da rimuovere e fare clic su Rimuovi. La categoria non viene più visualizzata.
