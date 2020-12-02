---
title: Più tenant per raccolte, snippet e modelli snippet
description: Scoprite come la funzione multi-tenant consente di separare i contenuti nell'archivio CRX in base all'organizzazione del cliente per impedire accessi non autorizzati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# Più tenant per raccolte, snippet e modelli snippet {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La funzione multi-tenant consente di separare i contenuti in CRX in base al prefisso dell’organizzazione e all’ID organizzazione per proteggere i contenuti dall’accesso non autorizzato da parte degli utenti di altre organizzazioni.

[!DNL Adobe Experience Manager Assets] archivia i dati per ogni organizzazione in un percorso diverso. Ciascun percorso specifico dell&#39;organizzazione è identificato dal prefisso dell&#39;organizzazione e dall&#39;ID organizzazione
inclusa nella posizione tradizionale in cui sono memorizzati in CRX diversi tipi di risorse.

Ad esempio, se create una cartella denominata `Demo`, le risorse [!DNL Experience Manager] in genere memorizzano la cartella in `../content/dam/Demo`. Con l&#39;opzione multi-tenant abilitata, ora è possibile archiviare i dati in `../content/dam/<organization prefix>/<organization id>Demo`

Ad esempio, se per [!DNL Adobe Marketing Cloud] utenti di [!DNL Assets] (su richiesta) assegnati all&#39;organizzazione `aodpremium`, potete utilizzare la funzione multi-tenant per configurare il percorso `../content/dam/<mac>/<aodpremium>Demo` per la separazione del contenuto. In questo esempio, `mac` è il prefisso dell&#39;organizzazione e `aodpremium` è l&#39;ID organizzazione.

In base all&#39;organizzazione e all&#39;ID dell&#39;utente, questo percorso qualificato viene visualizzato nell&#39;interfaccia [!DNL Assets] e in varie procedure guidate, comprese le procedure guidate per la creazione di Sposta e Snippet per applicare la segregazione.

La funzione Multi-Tenancy permette di separare i seguenti tipi di risorse e componenti:

* Raccolte
* Raccolte pubbliche
* Cataloghi (inclusa la procedura guidata Aggiungi/Seleziona pagina)
* Modelli
* Modelli per snippet
* Lightbox
