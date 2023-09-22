---
title: Controlli di coerenza e di attraversamento
description: Scopri come eseguire controlli di coerenza e di attraversamento.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# Controlli di coerenza e di attraversamento{#consistency-and-traversal-checks}

Durante l&#39;aggiornamento possono verificarsi problemi a causa di incoerenze nell&#39;area di lavoro. Puoi eseguire un aggiornamento dei test per verificare se si tratta di un problema, oppure eseguire i controlli di coerenza come azione preventiva.

Se esegui un aggiornamento dei test che non riesce a causa di incoerenze nell’area di lavoro, trovi voci simili a quelle riportate di seguito in crx-quickstart/logs/crx/error.log:

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Eseguire una verifica di coerenza {#perform-a-consistency-check}

Per eseguire una verifica di coerenza, passare alla pagina di amministrazione per JMX Mbean **com.adobe.granite (Archivio)**. Dalla schermata principale dell’AEM, vai a:

**Strumenti > Console web > Principale (barra dei menu) > JMX > com.adobe.granite (archivio)**

In un’installazione predefinita, si trova qui:  **[|Mostra|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

In **Operazioni** della pagina, sono disponibili due metodi: **`traversalCheck`** e **`consistencyCheck`**. Per eseguire un controllo, fare clic sull&#39;operazione e immettere i parametri desiderati.

![chlimage_1-117](assets/chlimage_1-117.png)
