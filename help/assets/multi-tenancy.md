---
title: Multi-tenancy per raccolte, snippet e modelli di snippet
description: Scopri in che modo la funzione di multi-tenancy consente di segregare i contenuti nell’archivio CRX in base all’organizzazione del cliente per evitare accessi non autorizzati.
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---

# Multi-tenancy per raccolte, snippet e modelli di snippet {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La funzione di multi-tenancy consente di segregare il contenuto in CRX in base al prefisso dell’organizzazione e all’ID dell’organizzazione, per proteggere il contenuto dall’accesso non autorizzato da parte degli utenti di altre organizzazioni.

[!DNL Adobe Experience Manager Assets] memorizza i dati per ogni organizzazione in un percorso diverso. Ogni percorso specifico dell’organizzazione è identificato dal prefisso dell’organizzazione e dall’ID dell’organizzazione inclusi nella posizione tradizionale in cui sono memorizzati diversi tipi di risorse in CRX.

Ad esempio, se crei una cartella denominata `Demo`, [!DNL Experience Manager] la cartella viene tradizionalmente memorizzata in `../content/dam/Demo`. Se è abilitata la multi-tenancy, ora puoi archiviare i dati in `../content/dam/<organization prefix>/<organization id>Demo`

Ad esempio, se per [!DNL Adobe Marketing Cloud] utenti di [!DNL Assets] (su richiesta) assegnati al `aodpremium` organizzazione, puoi utilizzare la funzione multi-tenancy per configurare `../content/dam/<mac>/<aodpremium>Demo` per segregarne il contenuto. In questo esempio, `mac` è il prefisso dell’organizzazione e `aodpremium` è l’ID organizzazione.

In base all’organizzazione e all’ID dell’utente, questo percorso qualificato viene visualizzato in [!DNL Assets] e varie procedure guidate, incluse quelle per la creazione di snippet e di spostamenti per applicare la segregazione.

La funzione Multi-tenancy consente di segregare i seguenti tipi di risorse e componenti:

* Raccolte
* Raccolte pubbliche
* Cataloghi (inclusa la procedura guidata Aggiungi/Seleziona pagina)
* Modelli
* Modelli di snippet
* Lightbox
