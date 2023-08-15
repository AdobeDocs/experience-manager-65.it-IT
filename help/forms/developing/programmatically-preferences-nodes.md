---
title: Gestione programmatica di PreferencesNodes
seo-title: Programmatically managing the PreferencesNodes
description: Utilizza l’API del servizio Preferences Manager (Java) per gestire in modo programmatico i nodi delle preferenze.
seo-description: Use the Preferences Manager Service API (Java) to programmatically manage the Preferences Nodes.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Gestione programmatica dei nodi delle preferenze {#programmatically-managing-the-preferencesnodes}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

In questo argomento viene descritto come utilizzare l&#39;API del servizio Preferences Manager (Java) per gestire in modo programmatico i nodi Preferences.

Puoi modificare manualmente le impostazioni di configurazione dall’interfaccia utente di Amministrazione. Per modificare le opzioni, passa a `Home>Settings>User Management> Configuration>Manual Configuration`. Importa `config.xml` dopo aver apportato le modifiche, noterai che tutte le modifiche tranne quelle apportate al nodo `/Adobe/Adobe Experience Manager Forms/Config/UM persist` sono persi. L&#39;anteprima di Importazione ed esportazione gestione utenti non supporta la modifica delle impostazioni di configurazione per altri componenti. Ora è possibile apportare queste modifiche utilizzando `PreferencesManagerServiceClient` API.

**Riepilogo dei passaggi** Per gestire in modo programmatico i nodi delle preferenze, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PreferencesManagerService
1. Richiama le operazioni di ruolo o autorizzazione appropriate

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client PreferencesManagerService**

Prima di poter eseguire a livello di programmazione un&#39;operazione PreferencesManagerService di User Management, è necessario creare un client PreferencesManagerService. Con l’API Java questo viene effettuato creando un oggetto PreferencesManagerServiceClient.

**Richiama le operazioni di ruolo o autorizzazione appropriate**

Dopo aver creato il client del servizio, è possibile richiamare le operazioni di Gestione preferenze. Il client del servizio consente di leggere e impostare le autorizzazioni.
