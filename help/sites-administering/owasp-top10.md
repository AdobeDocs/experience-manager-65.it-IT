---
title: OWASP Top 10
description: Scopri come l’AEM gestisce i dieci principali rischi per la sicurezza OWASP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# OWASP Top 10{#owasp-top}

Il [Apri progetto di protezione applicazione Web](https://owasp.org/) (OWASP) mantiene un elenco di ciò che considera come [Primi dieci rischi per la sicurezza delle applicazioni web](https://owasp.org/www-project-top-ten/).

Questi sono elencati di seguito, insieme a una spiegazione di come CRX li tratta.

## 1. Iniezione {#injection}

* SQL - Impedito dalla progettazione: la configurazione predefinita dell’archivio non include né richiede un database tradizionale; tutti i dati vengono memorizzati nell’archivio dei contenuti. Tutti gli accessi sono limitati agli utenti autenticati e possono essere eseguiti solo tramite l’API JCR. SQL è supportato solo per le query di ricerca (SELECT). SQL offre inoltre il supporto per l&#39;associazione dei valori.
* LDAP - L&#39;iniezione LDAP non è possibile perché il modulo di autenticazione filtra l&#39;input ed esegue l&#39;importazione dell&#39;utente utilizzando il metodo bind.
* Sistema operativo: non viene eseguita alcuna esecuzione della shell dall’interno dell’applicazione.

## 2. Vulnerabilità cross-site scripting (XSS) {#cross-site-scripting-xss}

La pratica di mitigazione generale consiste nel codificare tutti gli output di contenuti generati dagli utenti utilizzando una libreria di protezione XSS lato server basata su [Codificatore OWASP](https://owasp.org/www-project-java-encoder/) e [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS è una priorità assoluta durante sia il test che lo sviluppo e tutti i problemi riscontrati vengono (in genere) risolti immediatamente.

## 3. Autenticazione e gestione delle sessioni interrotte {#broken-authentication-and-session-management}

L&#39;AEM utilizza tecniche di autenticazione solide e collaudate, basate su [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) e [Apache Sling](https://sling.apache.org/). Le sessioni browser/HTTP non vengono utilizzate nell’AEM.

## 4. Riferimenti diretti agli oggetti non sicuri {#insecure-direct-object-references}

Tutti gli accessi agli oggetti dati sono mediati dall’archivio e pertanto limitati dal controllo degli accessi basato sul ruolo.

## 5. Cross-Site Request Forgery (CSRF) {#cross-site-request-forgery-csrf}

La funzione Cross-Site Request Forgery (CSRF) viene mitigata inserendo automaticamente un token di crittografia in tutti i moduli e le richieste AJAX e verificando tale token sul server per ogni POST.

Inoltre, l’AEM viene fornito con un filtro basato sull’intestazione del referente, che può essere configurato per *solo* consenti richieste POST da host specifici (definiti in un elenco).

## 6. Configurazione errata della sicurezza {#security-misconfiguration}

È impossibile garantire che tutto il software sia sempre configurato correttamente. Tuttavia, Adobe si impegna a fornire il maggior numero possibile di indicazioni e a semplificare il più possibile la configurazione. Inoltre, l&#39;AEM viene fornito con [controlli di integrità e sicurezza integrati](/help/sites-administering/operations-dashboard.md) che consentono di monitorare immediatamente la configurazione della protezione.

Rivedi [Elenco di controllo della sicurezza](/help/sites-administering/security-checklist.md) per ulteriori informazioni sulle istruzioni dettagliate per l&#39;irrigidimento.

## 7. Archiviazione crittografica non sicura {#insecure-cryptographic-storage}

Le password vengono memorizzate come hash di crittografia nel nodo utente. Per impostazione predefinita, tali nodi sono leggibili solo dall’amministratore e dall’utente stesso.

I dati sensibili, come le credenziali di terze parti, vengono archiviati in formato crittografato utilizzando una libreria di crittografia certificata FIPS 140-2.

## 8. Mancata limitazione dell’accesso agli URL {#failure-to-restrict-url-access}

L’archivio consente di impostare [privilegi granulari (come specificato da JCR)](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) per un determinato utente o gruppo in un determinato percorso, tramite le voci di controllo di accesso. Le restrizioni di accesso vengono applicate dall’archivio.

## 9. Protezione insufficiente del livello di trasporto {#insufficient-transport-layer-protection}

Mitigato dalla configurazione del server (ad esempio, utilizza solo HTTPS).

## 10. Reindirizzamenti e inoltri non convalidati {#unvalidated-redirects-and-forwards}

Attenuata limitando tutti i reindirizzamenti a destinazioni interne fornite dall’utente.
