---
title: OWASP Top 10
seo-title: OWASP Top 10
description: Scopri come AEM gestire i 10 principali rischi di protezione OWASP.
seo-description: Scopri come AEM gestire i 10 principali rischi di protezione OWASP.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
translation-type: tm+mt
source-git-commit: cd7331f5f57ec90ea72d41d467891dc832347a3c
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# OWASP Top 10{#owasp-top}

Il [Open Web Application Security Project](https://www.owasp.org) (OWASP) mantiene un elenco dei 10 rischi per la sicurezza delle applicazioni Web considerati come [primi 10 rischi per la sicurezza delle applicazioni Web](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

Questi sono elencati di seguito, insieme a una spiegazione di come CRX si occupa di loro.

## 1. Iniezione {#injection}

* SQL - Prevenzione della progettazione: La configurazione predefinita del repository non include né richiede un database tradizionale, tutti i dati vengono memorizzati nell&#39;archivio dei contenuti. L&#39;accesso è limitato agli utenti autenticati e può essere eseguito solo tramite l&#39;API JCR. SQL è supportato solo per le query di ricerca (SELECT). Inoltre, SQL offre il supporto per il binding dei valori.
* LDAP - L’inserimento LDAP non è possibile, poiché il modulo di autenticazione filtra l’input ed esegue l’importazione dell’utente tramite il metodo bind.
* Sistema operativo: nessuna esecuzione shell eseguita dall&#39;interno dell&#39;applicazione.

## 2. Script tra siti (XSS) {#cross-site-scripting-xss}

La pratica generale di mitigazione consiste nel codificare tutti gli output di contenuto generato dall&#39;utente utilizzando una libreria di protezione XSS lato server basata su [OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) e [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS è una priorità assoluta sia durante il test che durante lo sviluppo, e tutti i problemi rilevati vengono (generalmente) risolti immediatamente.

## 3. Autenticazione e gestione delle sessioni interrotte {#broken-authentication-and-session-management}

AEM utilizza tecniche di autenticazione sonore e collaudate, affidandosi a [Apache Jackrabbit](https://jackrabbit.apache.org/) e [Apache Sling](https://sling.apache.org/). Le sessioni browser/HTTP non vengono utilizzate in AEM.

## 4. Riferimenti agli oggetti diretti non sicuri {#insecure-direct-object-references}

L&#39;accesso agli oggetti dati è gestito dall&#39;archivio e pertanto limitato da un controllo di accesso basato su ruoli.

## 5. Modulo di richiesta intersito (CSRF) {#cross-site-request-forgery-csrf}

Il CSRF (Cross-Site Request Forgery) è attenuato dall&#39;invio automatico di un token di crittografia in tutti i moduli e le richieste di AJAX e dalla verifica del token sul server per ogni POST.

Inoltre, AEM viene fornito con un filtro basato sull&#39;intestazione del referente, che può essere configurato su *only* per consentire le richieste di POST da host specifici (definiti in un elenco).

## 6. Configurazione errata della sicurezza {#security-misconfiguration}

È impossibile garantire che tutto il software sia sempre configurato correttamente. Tuttavia, ci sforziamo di fornire il maggior numero possibile di indicazioni e rendere la configurazione il più semplice possibile. Inoltre, AEM navi con [controlli di sicurezza integrati](/help/sites-administering/operations-dashboard.md) che consentono di monitorare rapidamente la configurazione di sicurezza.

Per ulteriori informazioni, consultare la [lista di controllo della sicurezza](/help/sites-administering/security-checklist.md), che fornisce istruzioni dettagliate per l&#39;applicazione del livello di protezione.

## 7. Archiviazione crittografia non sicura {#insecure-cryptographic-storage}

Le password sono memorizzate come hash crittografici nel nodo utente; per impostazione predefinita tali nodi sono leggibili solo dall&#39;amministratore e dall&#39;utente stesso.

I dati sensibili, come le credenziali di terze parti, vengono memorizzati in un modulo crittografato utilizzando una libreria di crittografia certificata FIPS 140-2.

## 8. Errore durante la limitazione dell&#39;accesso all&#39;URL {#failure-to-restrict-url-access}

L&#39;archivio consente di impostare [privilegi finemente granulati (come specificato da JCR)](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html) per qualsiasi utente o gruppo in qualsiasi percorso, attraverso le voci di controllo degli accessi. Le restrizioni di accesso sono applicate dall&#39;archivio.

## 9. Protezione livello di trasporto insufficiente {#insufficient-transport-layer-protection}

Mitigato dalla configurazione del server (ad esempio, usa solo HTTPS).

## 10. Reindirizzamenti e inoltri non convalidati {#unvalidated-redirects-and-forwards}

Mitigato limitando tutti i reindirizzamenti alle destinazioni fornite dall&#39;utente alle posizioni interne.

