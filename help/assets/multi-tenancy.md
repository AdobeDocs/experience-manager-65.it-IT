---
title: Multi-tenancy per raccolte, snippet e modelli di snippet
description: Scopri come la funzione di multi-tenancy ti consente di separare i contenuti nell’archivio CRX in base all’organizzazione del cliente per impedire l’accesso non autorizzato.
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

La funzione di multi-tenancy consente di separare i contenuti in CRX in base al prefisso dell’organizzazione e all’ID organizzazione per proteggere il contenuto dall’accesso non autorizzato da parte degli utenti di altre organizzazioni.

[!DNL Adobe Experience Manager Assets] memorizza i dati per ogni organizzazione in un percorso diverso. Ciascun percorso specifico per l’organizzazione è identificato dal prefisso dell’organizzazione e dall’ID organizzazione inclusi nella posizione tradizionale in cui vengono memorizzati in CRX diversi tipi di risorse.

Ad esempio, se crei una cartella denominata `Demo`, [!DNL Experience Manager] in genere la cartella viene memorizzata in `../content/dam/Demo`. Con l’opzione multi-tenancy abilitata, è ora possibile memorizzare i dati in `../content/dam/<organization prefix>/<organization id>Demo`

Ad esempio, se [!DNL Adobe Marketing Cloud] utenti di [!DNL Assets] (su richiesta) che sono assegnati al `aodpremium` per configurare `../content/dam/<mac>/<aodpremium>Demo` percorso per separare il contenuto. In questo esempio, `mac` è il prefisso dell’organizzazione e `aodpremium` è l&#39;ID organizzazione.

In base all’organizzazione e all’ID dell’utente, questo percorso qualificato viene visualizzato nel [!DNL Assets] Interfaccia e varie procedure guidate, incluse le procedure guidate per la creazione di Sposta e Frammento per applicare la segregazione.

La funzione Multi-tenancy consente di separare i seguenti tipi di risorse e componenti:

* Raccolte
* Raccolte pubbliche
* Cataloghi (inclusa la procedura guidata Aggiungi/Seleziona pagina )
* Modelli
* Modelli per snippet
* Lightbox
