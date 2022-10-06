---
title: Controlli di coerenza e di transito
seo-title: Consistency and Traversal Checks
description: Scopri come eseguire controlli di coerenza e di attraversamento.
seo-description: Learn how to perform consistency and traversal checks.
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Controlli di coerenza e di transito{#consistency-and-traversal-checks}

Durante l’aggiornamento possono verificarsi problemi a causa di incongruenze nell’area di lavoro. Puoi eseguire un aggiornamento del test per verificare se si tratta di un problema, oppure eseguire i controlli di coerenza come azione preventiva.

Se esegui un aggiornamento del test che non riesce a causa di incongruenze nell’area di lavoro, vedrai voci simili alle seguenti in crx-quickstart/logs/crx/error.log:

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Eseguire un controllo di coerenza {#perform-a-consistency-check}

Per eseguire un controllo di coerenza, passa alla pagina di amministrazione per JMX Mbean** com.adobe.granite (Repository)**. Dalla schermata principale AEM, vai a:

**Strumenti > Console web > Principale (nella barra dei menu) > JMX > com.adobe.granite (Repository)**

In un&#39;installazione predefinita, si trova qui:  **[|Mostra utente|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

In **Operazioni** nella sezione della pagina sono disponibili due metodi: **`traversalCheck`** e **`consistencyCheck`**. Per eseguire un controllo, fai clic sull’operazione e immetti i parametri desiderati.

![chlimage_1-117](assets/chlimage_1-117.png)
