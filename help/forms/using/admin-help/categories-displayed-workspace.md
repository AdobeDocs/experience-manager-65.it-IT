---
title: Gestire le categorie visualizzate in Workspace
description: Nell’area di lavoro i processi che un utente può avviare vengono visualizzati in categorie nel riquadro di navigazione a sinistra. Scopri come gestire le categorie visualizzate nell’area di lavoro.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 62621fe9-f69f-4bc0-aecc-d7bcc3064516
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '494'
ht-degree: 100%

---

# Gestire le categorie visualizzate in Workspace {#managing-the-categories-displayed-in-workspace}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Nell’area di lavoro i processi che un utente può avviare vengono visualizzati in categorie nel riquadro di navigazione a sinistra. È possibile impostare le categorie nella console di amministrazione oppure gli sviluppatori di processi possono configurarle in Workbench. Quando gli sviluppatori di processi creano processi, li assegnano a delle categorie.

Quando specifichi i nomi delle categorie, creale in modo che vengano visualizzate correttamente nel riquadro di navigazione dell’area di lavoro. Per impostazione predefinita, il riquadro di navigazione a sinistra ha una larghezza fissa di 210 pixel, pari a circa 24 caratteri. Se è troppo lungo per essere contenuto nella larghezza fissa del riquadro di navigazione a sinistra, il nome categoria specificato verrà troncato. Il nome completo viene visualizzato solo quando il cursore del mouse viene posizionato sopra di esso. Evita i nomi di categoria che possono essere troncati. Negli esempi seguenti vengono illustrati i nomi categoria che possono essere contenuti e quelli che vengono troncati:

**Nome categoria adatto:** Frequenza e uscita

**Nome categoria troncato:** Frequenza e uscita (Stati Uniti)

Nell’area di lavoro i processi all’interno di una categoria vengono generalmente visualizzati come schede nella pagina Avvia processo. In generale, è possibile visualizzare sullo schermo sei schede per una categoria prima che l’utente debba scorrere per visualizzare le altre schede. Poiché lo scorrimento rende più difficile trovare un processo, è consigliabile limitare ogni categoria a sei processi o, a seconda della risoluzione, limitare il numero di processi che possono essere visualizzati sullo schermo senza che sia necessario uno scorrimento.

Se utilizzi MySQL come database di AEM Forms, la console di amministrazione non è in grado di distinguere due nomi di categoria che differiscono solo nell’uso di caratteri estesi. Ad esempio, se crei una categoria denominata abcde e una categoria denominata âbcdè, queste vengono considerate uguali.

## Aggiungere una categoria {#add-a-category}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione categorie.
1. Fai clic su Aggiungi. Per aggiungere una sottocategoria, seleziona una categoria e fai clic su Aggiungi.
1. Nella casella Nome digita un nome per la categoria e nella casella Descrizione digita una descrizione della categoria.
1. Fai clic su Aggiungi. La categoria viene visualizzata nella pagina Gestione categorie.

   ***Nota **: puoi aggiungere solo fino a cinque livelli gerarchici durante la creazione delle categorie.*

## Modificare una categoria {#edit-a-category}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione categorie.
1. Seleziona la categoria da modificare e fai clic su Modifica. In alternativa, puoi fare doppio clic su una categoria da modificare.
1. Modifica il nome della categoria nella casella Nome.

## Rimuovere una categoria {#remove-a-category}

Puoi rimuovere solo le categorie non utilizzate.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione categorie.
1. Nella pagina Gestione categorie seleziona la casella di controllo relativa alla categoria da rimuovere e fai clic su Rimuovi. La categoria non verrà più visualizzata.
