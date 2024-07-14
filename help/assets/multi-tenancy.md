---
title: Multi-tenancy per raccolte, snippet e modelli di snippet
description: Scopri in che modo la funzione di multi-tenancy consente di segregare i contenuti nell’archivio CRX in base all’organizzazione del cliente per evitare accessi non autorizzati.
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---

# Multi-tenancy per raccolte, snippet e modelli di snippet {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La funzione multi-tenancy consente di segregare il contenuto in CRX in base al prefisso e all’ID organizzazione, per proteggere il contenuto dall’accesso non autorizzato da parte degli utenti di altre organizzazioni.

[!DNL Adobe Experience Manager Assets] memorizza i dati per ogni organizzazione in un percorso diverso. Ogni percorso specifico dell’organizzazione è identificato dal prefisso e dall’ID organizzazione
incluso nella posizione tradizionale in cui sono memorizzati diversi tipi di risorse in CRX.

Ad esempio, se crei una cartella denominata `Demo`, [!DNL Experience Manager] risorse archivia tradizionalmente la cartella in `../content/dam/Demo`. Se è abilitata la multi-tenancy, è ora possibile archiviare i dati in `../content/dam/<organization prefix>/<organization id>Demo`

Ad esempio, se per [!DNL Adobe Marketing Cloud] utenti di [!DNL Assets] (su richiesta) assegnati all&#39;organizzazione `aodpremium`, è possibile utilizzare la funzione multi-tenancy per configurare il percorso `../content/dam/<mac>/<aodpremium>Demo` per segregarne il contenuto. In questo esempio, `mac` è il prefisso dell&#39;organizzazione e `aodpremium` è l&#39;ID organizzazione.

In base all&#39;organizzazione e all&#39;ID dell&#39;utente, questo percorso qualificato viene visualizzato nell&#39;interfaccia [!DNL Assets] e in varie procedure guidate, incluse quelle per la creazione di spostamenti e frammenti di codice, per applicare la segregazione.

La funzione Multi-tenancy consente di segregare i seguenti tipi di risorse e componenti:

* Raccolte
* Raccolte pubbliche
* Cataloghi (inclusa la procedura guidata Aggiungi/Seleziona pagina)
* Modelli
* Modelli di snippet
* Lightbox
