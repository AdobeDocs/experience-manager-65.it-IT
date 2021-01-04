---
title: Gestione programmatica di PreferencesNodes
seo-title: Gestione programmatica di PreferencesNodes
description: Utilizzate l'API del servizio Preferences Manager (Java) per gestire in modo programmatico i nodi delle preferenze.
seo-description: Utilizzate l'API del servizio Preferences Manager (Java) per gestire in modo programmatico i nodi delle preferenze.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Gestione programmatica dei nodi delle preferenze {#programmatically-managing-the-preferencesnodes}

In questo argomento viene descritto come utilizzare l&#39;API del servizio Preferences Manager (Java) per gestire i nodi delle preferenze in modo programmatico.

Potete modificare manualmente le impostazioni di configurazione dall&#39;interfaccia utente amministratore. Per modificare le opzioni, passare a `Home>Settings>User Management> Configuration>Manual Configuration`. Importa `config.xml` dopo aver apportato le modifiche, noterai che tutte le modifiche tranne quelle apportate al nodo `/Adobe/Adobe Experience Manager Forms/Config/UM persist` vanno perse. L&#39;anteprima di Importazione ed esportazione di Gestione utente non supporta la modifica delle impostazioni di configurazione per altri componenti. Ora, queste modifiche possono essere effettuate utilizzando le `PreferencesManagerServiceClient` API.

**Riepilogo dei** passaggiPer gestire in modo programmatico i nodi delle preferenze, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client PreferencesManagerService
1. Richiama le operazioni di ruolo o autorizzazione appropriate

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un client PreferencesManagerService**

Prima di eseguire un&#39;operazione di Gestione utente in modo programmatico, è necessario creare un client PreferencesManagerService. Con l&#39;API Java questo si ottiene creando un oggetto PreferencesManagerServiceClient.

**Richiama le operazioni di ruolo o autorizzazione appropriate**

Dopo aver creato il client del servizio, potete richiamare le operazioni di Gestione preferenze. Il client del servizio consente di leggere e impostare le autorizzazioni.
