---
title: Quadro di riferimento per la protezione del CSRF
seo-title: The CSRF Protection Framework
description: Il framework utilizza i token per garantire che la richiesta del cliente sia legittima
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Quadro di riferimento per la protezione del CSRF{#the-csrf-protection-framework}

Oltre al filtro di riferimento Apache Sling, l&#39;Adobe fornisce anche un nuovo quadro di protezione CSRF per proteggere da questo tipo di attacco.

Il framework utilizza i token per garantire che la richiesta del cliente sia legittima. I token vengono generati quando il modulo viene inviato al client e convalidato quando il modulo viene inviato nuovamente al server.

>[!NOTE]
>
>Non ci sono token nelle istanze di pubblicazione per gli utenti anonimi.

## Requisiti  {#requirements}

### Dipendenze {#dependencies}

Qualsiasi componente che si basa sul `granite.jquery` La dipendenza beneficerà automaticamente del quadro di protezione CSRF. In caso contrario, è necessario dichiarare una dipendenza in `granite.csrf.standalone` prima di poter utilizzare il framework.

### Replicazione della chiave Crypto {#replicating-crypto-keys}

Per utilizzare i token, è necessario replicare il `/etc/keys/hmac` binario per tutte le istanze nella distribuzione. Un modo pratico per copiare la chiave HMAC in tutte le istanze è quello di creare un pacchetto contenente la chiave e installarla tramite Gestione pacchetti su tutte le istanze.

>[!NOTE]
>
>Assicurati anche di fare il necessario [Modifiche alla configurazione del dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) per utilizzare il quadro di protezione CSRF.

>[!NOTE]
>
>Se utilizzi la cache del manifesto con la tua applicazione web, assicurati di aggiungere &quot;**&amp;ast;**&quot; al manifesto per assicurarti che il token non prenda offline la chiamata di generazione del token CSRF. Per ulteriori informazioni, consulta [collegamento](https://www.w3.org/TR/offline-webapps/).
>
>Per ulteriori informazioni sugli attacchi CSRF e sui modi per attenuarli, consulta la sezione [Pagina OWASP della struttura di richiesta tra siti](https://owasp.org/www-community/attacks/csrf).
