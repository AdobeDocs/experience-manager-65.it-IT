---
title: Controlli di coerenza e di transito
seo-title: Controlli di coerenza e di transito
description: Scopri come eseguire controlli di coerenza e di attraversamento.
seo-description: Scopri come eseguire controlli di coerenza e di attraversamento.
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Verifiche di coerenza e di transito{#consistency-and-traversal-checks}

Quando si esegue l’aggiornamento possono verificarsi problemi a causa di incoerenze nell’area di lavoro. È possibile eseguire un aggiornamento di test per verificare se si tratta di un problema, oppure eseguire controlli di coerenza come azione preventiva.

Se eseguite un aggiornamento di prova che non riesce a causa di incoerenze nell’area di lavoro, vengono visualizzate voci simili a quelle riportate di seguito in crx-quickstart/logs/crx/error.log:

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Eseguire un controllo di coerenza {#perform-a-consistency-check}

Per eseguire una verifica di coerenza, andate alla pagina di amministrazione per il file MBeia JMX** com.adobe.granite (Repository)**. Dalla schermata principale AEM, passate a:

**Strumenti > Console Web > Principale (nella barra dei menu) > JMX > com.adobe.granite (Repository)**

In un&#39;installazione predefinita, si trova qui:  **[|Mostra|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

Nella sezione **Operazioni** della pagina sono disponibili due metodi: **`traversalCheck`** e **`consistencyCheck`**. Per eseguire un controllo, fare clic sull&#39;operazione e immettere i parametri desiderati.

![chlimage_1-117](assets/chlimage_1-117.png)

