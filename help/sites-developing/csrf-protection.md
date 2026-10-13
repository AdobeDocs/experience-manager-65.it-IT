---
title: Il framework di protezione CSRF
description: Il framework utilizza i token per garantire che la richiesta del cliente sia legittima
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 6%
---
# Il framework di protezione CSRF{#the-csrf-protection-framework}

Oltre al filtro Apache Sling Referrer, Adobe fornisce anche un nuovo CSRF Protection Framework per la protezione contro questo tipo di attacchi.

Il framework utilizza i token per garantire che la richiesta del cliente sia legittima. I token vengono generati quando il modulo viene inviato al client e convalidati quando il modulo viene inviato nuovamente al server.

>[!NOTE]
>
>Le istanze di pubblicazione non contengono token per gli utenti anonimi.

## Requisiti {#requirements}

### Dipendenze {#dependencies}

Qualsiasi componente che si basa sulla dipendenza `granite.jquery` può beneficiare automaticamente del framework di protezione CSRF. In caso contrario, per qualsiasi componente è necessario dichiarare una dipendenza a `granite.csrf.standalone` prima di poter utilizzare il framework.

### Replica della chiave di crittografia {#replicating-crypto-keys}

Per utilizzare i token, devi replicare il file binario HMAC in tutte le istanze della distribuzione. Per ulteriori dettagli, vedere [Replica della chiave HMAC](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key).

>[!NOTE]
>
>Assicurati anche di apportare le modifiche di configurazione Dispatcher necessarie per utilizzare il framework di protezione CSRF:
>
>* [Configurazione di Adobe Experience Manager Dispatcher per impedire attacchi CSRF](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/configuring/configuring-dispatcher-to-prevent-csrf)
>* [Panoramica di Dispatcher](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/dispatcher)

>[!NOTE]
>
>Se utilizzi la cache del manifesto con l&#39;applicazione Web, assicurati di aggiungere &quot;**&ast;**&quot; al manifesto per assicurarti che il token non metta offline la chiamata di generazione del token CSRF. Per ulteriori informazioni, consulta questo [collegamento](https://www.w3.org/TR/offline-webapps/).
>
>Per ulteriori informazioni sugli attacchi CSRF e sui modi per mitigarli, consulta la [pagina OWASP Cross-Site Request Forgery](https://owasp.org/www-community/attacks/csrf).
