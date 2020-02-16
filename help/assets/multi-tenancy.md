---
title: Più tenant per raccolte, snippet e modelli snippet
description: Scoprite come la funzione multi-tenant consente di separare i contenuti nell'archivio CRX in base all'organizzazione del cliente per impedire accessi non autorizzati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Più tenant per raccolte, snippet e modelli snippet {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La funzione multi-tenant consente di separare i contenuti in CRX in base al prefisso dell’organizzazione e all’ID organizzazione per proteggere i contenuti dall’accesso non autorizzato da parte degli utenti di altre organizzazioni.

Risorse Adobe Experience Manager (AEM) memorizza i dati per ogni organizzazione in un percorso diverso. Ciascun percorso specifico per l’organizzazione è identificato dal prefisso dell’organizzazione e dall’ID organizzazione inclusi nella posizione tradizionale in cui sono memorizzati in CRX diversi tipi di risorse.

Ad esempio, se create una cartella denominata `Demo`, le risorse AEM memorizzano la cartella in `../content/dam/Demo`. Con l&#39;opzione multi-tenant abilitata, ora è possibile archiviare i dati in `../content/dam/<organization prefix>/<organization id>Demo`

Ad esempio, se per [!DNL Adobe Marketing Cloud] gli utenti di Risorse AEM (su richiesta) assegnati all’ `aodpremium` organizzazione, potete utilizzare la funzione multi-tenant per configurare il `../content/dam/<mac>/<aodpremium>Demo` percorso per la separazione del contenuto. In questo esempio `mac` è il prefisso dell&#39;organizzazione e `aodpremium` l&#39;ID organizzazione.

In base all’organizzazione e all’ID dell’utente, questo percorso completo viene visualizzato nell’interfaccia di Risorse AEM e in varie procedure guidate, comprese le procedure guidate per la creazione di Sposta e Snippet, al fine di applicare la segregazione.

La funzione Multi-Tenancy permette di separare i seguenti tipi di risorse e componenti:

* Raccolte
* Raccolte pubbliche
* Cataloghi (inclusa la procedura guidata Aggiungi/Seleziona pagina)
* Modelli
* Modelli per snippet
* Lightbox
