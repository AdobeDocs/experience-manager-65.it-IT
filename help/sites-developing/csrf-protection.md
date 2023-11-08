---
title: Il framework di protezione CSRF
description: Il framework utilizza i token per garantire che la richiesta del cliente sia legittima
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Il framework di protezione CSRF{#the-csrf-protection-framework}

Oltre al filtro Apache Sling Referrer, Adobe fornisce anche un nuovo framework di protezione CSRF per proteggere da questo tipo di attacchi.

Il framework utilizza i token per garantire che la richiesta del cliente sia legittima. I token vengono generati quando il modulo viene inviato al client e convalidati quando il modulo viene inviato nuovamente al server.

>[!NOTE]
>
>Le istanze di pubblicazione non contengono token per gli utenti anonimi.

## Requisiti {#requirements}

### Dipendenze {#dependencies}

Qualsiasi componente che si basa su `granite.jquery` La dipendenza può beneficiare automaticamente del framework di protezione CSRF. In caso contrario, per qualsiasi componente, è necessario dichiarare una dipendenza a `granite.csrf.standalone` prima di poter utilizzare il framework.

### Replica della chiave di crittografia {#replicating-crypto-keys}

Per utilizzare i token, devi replicare il file binario HMAC in tutte le istanze della distribuzione. Consulta [Replica della chiave HMAC](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) per ulteriori dettagli.

>[!NOTE]
>
>Assicurati anche di fare il necessario [Modifiche alla configurazione del Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) per utilizzare il framework di protezione CSRF.

>[!NOTE]
>
>Se utilizzi la cache del manifesto con l’applicazione web, assicurati di aggiungere &quot;**&amp;ast;**&quot; al manifesto per assicurarti che il token non metta offline la chiamata di generazione del token CSRF. Per ulteriori informazioni, consulta [link](https://www.w3.org/TR/offline-webapps/).
>
>Per ulteriori informazioni sugli attacchi CSRF e sui modi per mitigarli, consulta la [Pagina OWASP per false richieste intersito](https://owasp.org/www-community/attacks/csrf).
