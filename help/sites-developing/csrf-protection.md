---
title: Quadro di protezione CSRF
seo-title: Quadro di protezione CSRF
description: Il framework utilizza i token per garantire che la richiesta del cliente sia legittima
seo-description: Il framework utilizza i token per garantire che la richiesta del cliente sia legittima
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
translation-type: tm+mt
source-git-commit: c83c77c5c313099944dd73c8cbe63d429d84a518

---


# Quadro di protezione CSRF{#the-csrf-protection-framework}

Oltre al filtro Apache Sling Referrer, Adobe fornisce un nuovo quadro di protezione CSRF per la protezione contro questo tipo di attacchi.

Il framework utilizza i token per garantire che la richiesta del cliente sia legittima. I token vengono generati quando il modulo viene inviato al client e convalidato al momento del ritorno del modulo al server.

>[!NOTE]
>
>Nelle istanze pubblicate non sono presenti token per gli utenti anonimi.

## Requisiti {#requirements}

### Dipendenze {#dependencies}

Qualsiasi componente che si basa sulla `granite.jquery` dipendenza beneficerà automaticamente del CSRF Protection Framework. Se questo non è il caso di uno dei componenti, è necessario dichiarare una dipendenza per `granite.csrf.standalone` poter utilizzare il framework.

### Replica della chiave di crittografia {#replicating-crypto-keys}

Per poter utilizzare i token, è necessario replicare il `/etc/keys/hmac` binario a tutte le istanze nella distribuzione. Un modo pratico per copiare la chiave HMAC in tutte le istanze consiste nel creare un pacchetto contenente la chiave e installarlo tramite Gestione pacchetti in tutte le istanze.

>[!NOTE]
>
>Per utilizzare CSRF Protection Framework, è inoltre necessario apportare le modifiche [necessarie alla configurazione del](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) dispatcher.

>[!NOTE]
>
>Se utilizzate la cache del manifesto con l’applicazione Web, accertatevi di aggiungere &quot;**&amp;ast;**&quot; al manifesto per assicurarvi che il token non porti offline la chiamata di generazione del token CSRF. Per ulteriori informazioni, consulta questo [collegamento](https://www.w3.org/TR/offline-webapps/).
>
>Per ulteriori informazioni sugli attacchi CSRF e sui modi per attenuarli, consultate la pagina [OWASP sulla richiesta](https://owasp.org/www-community/attacks/csrf)intersito.
