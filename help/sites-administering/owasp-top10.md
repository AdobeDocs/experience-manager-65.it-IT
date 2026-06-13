---
title: OWASP Top 10
description: Scopri come AEM gestisce i dieci principali rischi per la sicurezza di OWASP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 4%

---

# OWASP Top 10{#owasp-top}

Il [progetto di sicurezza dell&#39;applicazione Web aperta](https://owasp.org/) (OWASP) mantiene un elenco dei [principali dieci rischi di sicurezza dell&#39;applicazione Web](https://owasp.org/www-project-top-ten/).

Questi sono elencati di seguito, insieme a una spiegazione di come CRX li gestisce.

## &#x200B;1. Iniezione {#injection}

* SQL - Impedito dalla progettazione: la configurazione predefinita dell’archivio non include né richiede un database tradizionale; tutti i dati vengono memorizzati nell’archivio dei contenuti. Tutti gli accessi sono limitati agli utenti autenticati e possono essere eseguiti solo tramite l’API JCR. SQL è supportato solo per le query di ricerca (SELECT). SQL offre inoltre il supporto per l&#39;associazione dei valori.
* LDAP - L&#39;iniezione LDAP non è possibile perché il modulo di autenticazione filtra l&#39;input ed esegue l&#39;importazione dell&#39;utente utilizzando il metodo bind.
* Sistema operativo: non viene eseguita alcuna esecuzione della shell dall’interno dell’applicazione.

## &#x200B;2. Script tra siti (XSS) {#cross-site-scripting-xss}

La procedura di mitigazione generale consiste nel codificare tutti gli output di contenuti generati dall&#39;utente utilizzando una libreria di protezione XSS lato server basata su [OWASP Encoder](https://owasp.org/www-project-java-encoder/) e [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS è una priorità assoluta durante sia il test che lo sviluppo e tutti i problemi riscontrati vengono (in genere) risolti immediatamente.

## &#x200B;3. Autenticazione e gestione delle sessioni interrotte {#broken-authentication-and-session-management}

AEM utilizza tecniche di autenticazione valide e collaudate, basate su [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) e [Apache Sling](https://sling.apache.org/). Le sessioni browser/HTTP non vengono utilizzate in AEM.

## &#x200B;4. Riferimenti diretti agli oggetti non sicuri {#insecure-direct-object-references}

Tutti gli accessi agli oggetti dati sono mediati dall’archivio e pertanto limitati dal controllo degli accessi basato sul ruolo.

## &#x200B;5. CSRF (Cross-Site Request Forgery) {#cross-site-request-forgery-csrf}

La funzione Cross-Site Request Forgery (CSRF) viene mitigata inserendo automaticamente un token di crittografia in tutti i moduli e le richieste di AJAX e verificando tale token sul server per ogni POST.

Inoltre, AEM viene fornito con un filtro basato sull&#39;intestazione del referente, che può essere configurato in modo da consentire *solo* richieste POST da host specifici (definiti in un elenco).

## &#x200B;6. Configurazione errata della sicurezza {#security-misconfiguration}

È impossibile garantire che tutto il software sia sempre configurato correttamente. Tuttavia, Adobe si impegna a fornire quante più linee guida possibili e a semplificare il più possibile la configurazione. Inoltre, AEM viene fornito con [controlli di integrità della sicurezza integrati](/help/sites-administering/operations-dashboard.md) che consentono di monitorare immediatamente la configurazione della sicurezza.

Esaminare l&#39;[elenco di controllo protezione](/help/sites-administering/security-checklist.md) per ulteriori informazioni che forniscono istruzioni dettagliate sulla protezione avanzata.

## &#x200B;7. Archiviazione crittografica non sicura {#insecure-cryptographic-storage}

Le password vengono memorizzate come hash di crittografia nel nodo utente. Per impostazione predefinita, tali nodi sono leggibili solo dall’amministratore e dall’utente stesso.

I dati sensibili, come le credenziali di terze parti, vengono archiviati in formato crittografato utilizzando una libreria di crittografia certificata FIPS 140-2.

## &#x200B;8. Errore nel limitare l’accesso agli URL {#failure-to-restrict-url-access}

L&#39;archivio consente l&#39;impostazione di [privilegi granulari (come specificato da JCR)](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) per qualsiasi utente o gruppo specificato in un determinato percorso, tramite le voci di controllo di accesso. Le restrizioni di accesso vengono applicate dall’archivio.

## &#x200B;9. Protezione livello di trasporto insufficiente {#insufficient-transport-layer-protection}

Mitigato dalla configurazione del server (ad esempio, utilizza solo HTTPS).

## &#x200B;10. Reindirizzamenti e inoltri non convalidati {#unvalidated-redirects-and-forwards}

Attenuata limitando tutti i reindirizzamenti a destinazioni interne fornite dall’utente.
