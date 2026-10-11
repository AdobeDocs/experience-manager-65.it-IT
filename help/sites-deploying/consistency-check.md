---
title: Controlli di coerenza e di attraversamento
description: Scopri come eseguire controlli di coerenza e di attraversamento.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 6%
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

Per eseguire una verifica di coerenza, passare alla pagina di amministrazione per JMX Mbean **com.adobe.granite (repository)**. Dalla schermata principale di AEM, vai a:

**Strumenti > Console Web > Principale (barra dei menu) > JMX > com.adobe.granite (archivio)**

In un&#39;installazione predefinita, si trova qui: **[|Mostra|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

Nella sezione **Operazioni** della pagina sono disponibili due metodi: **`traversalCheck`** e **`consistencyCheck`**. Per eseguire un controllo, fare clic sull&#39;operazione e immettere i parametri desiderati.

![chlimage_1-117](assets/chlimage_1-117.png)
