---
title: Gestione programmatica di PreferencesNodes
seo-title: Gestione programmatica di PreferencesNodes
description: Utilizza l’API del servizio Preferenze Manager (Java) per gestire in modo programmatico i nodi delle preferenze.
seo-description: Utilizza l’API del servizio Preferenze Manager (Java) per gestire in modo programmatico i nodi delle preferenze.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Gestione programmatica dei nodi delle preferenze {#programmatically-managing-the-preferencesnodes}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

In questo argomento viene descritto come utilizzare l’API del servizio Preferenze Manager (Java) per gestire in modo programmatico i nodi Preferenze.

Puoi modificare manualmente le impostazioni di configurazione dall’interfaccia utente amministratore. Per modificare le opzioni, passa a `Home>Settings>User Management> Configuration>Manual Configuration`. Importa `config.xml` dopo aver apportato le modifiche, noterai che tutte le modifiche eccetto quelle apportate al nodo `/Adobe/Adobe Experience Manager Forms/Config/UM persist` andranno perse. L&#39;anteprima di Importazione ed esportazione di User Management non supporta la modifica delle impostazioni di configurazione per altri componenti. Ora è possibile apportare queste modifiche utilizzando le API `PreferencesManagerServiceClient` .

**Riepilogo dei** passaggiPer gestire in modo programmatico i nodi delle preferenze, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PreferencesManagerService
1. Richiamare le operazioni di ruolo o autorizzazione appropriate

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client PreferencesManagerService**

Prima di eseguire un&#39;operazione di User Management PreferencesManagerService a livello di programmazione, è necessario creare un client PreferencesManagerService. Con l&#39;API Java questo si ottiene creando un oggetto PreferencesManagerServiceClient.

**Richiamare le operazioni di ruolo o autorizzazione appropriate**

Dopo aver creato il client di servizio, puoi richiamare le operazioni di Gestione preferenze. Il client di servizi ti consente di leggere e impostare le autorizzazioni.
