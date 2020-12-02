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
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Quadro di protezione CSRF{#the-csrf-protection-framework}

Oltre al filtro di riferimento Apache Sling,  Adobe fornisce anche un nuovo quadro di protezione CSRF per proteggere contro questo tipo di attacchi.

Il framework utilizza i token per garantire che la richiesta del cliente sia legittima. I token vengono generati quando il modulo viene inviato al client e convalidato al momento del ritorno del modulo al server.

>[!NOTE]
>
>Nelle istanze pubblicate non sono presenti token per gli utenti anonimi.

## Requisiti {#requirements}

### Dipendenze {#dependencies}

Qualsiasi componente che si basa sulla dipendenza `granite.jquery` beneficerà automaticamente del CSRF Protection Framework. Se questo non avviene per uno dei componenti, è necessario dichiarare una dipendenza in `granite.csrf.standalone` prima di poter utilizzare il framework.

### Replica della chiave di crittografia {#replicating-crypto-keys}

Per poter utilizzare i token, è necessario replicare il binario `/etc/keys/hmac` in tutte le istanze della distribuzione. Un modo pratico per copiare la chiave HMAC in tutte le istanze consiste nel creare un pacchetto contenente la chiave e installarlo tramite Gestione pacchetti in tutte le istanze.

>[!NOTE]
>
>Per utilizzare CSRF Protection Framework è inoltre necessario apportare le modifiche [alla configurazione del dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

>[!NOTE]
>
>Se utilizzate la cache del manifesto con l&#39;applicazione Web, accertatevi di aggiungere &quot;**&amp;ast;**&quot; al manifesto per essere certi che il token non porti offline la chiamata di generazione del token CSRF. Per ulteriori informazioni, consultare questo [collegamento](https://www.w3.org/TR/offline-webapps/).
>
>Per ulteriori informazioni sugli attacchi CSRF e sui modi per attenuarli, vedere la pagina [Cross-Site Request Forgery OWASP](https://owasp.org/www-community/attacks/csrf).
