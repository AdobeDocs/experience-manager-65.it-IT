---
title: OWASP Top 10
seo-title: OWASP Top 10
description: Scopri in che modo AEM gestisce i 10 principali rischi per la sicurezza OWASP.
seo-description: Scopri in che modo AEM gestisce i 10 principali rischi per la sicurezza OWASP.
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

Il [Open Web Application Security Project](https://www.owasp.org) (OWASP) mantiene un elenco dei 10 [principali rischi](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)per la sicurezza delle applicazioni Web.

Questi sono elencati di seguito, insieme a una spiegazione di come CRX si occupa di loro.

## 1. Iniezione {#injection}

* SQL - Prevenzione della progettazione: La configurazione predefinita del repository non include né richiede un database tradizionale, tutti i dati vengono memorizzati nell&#39;archivio dei contenuti. L&#39;accesso è limitato agli utenti autenticati e può essere eseguito solo tramite l&#39;API JCR. SQL è supportato solo per le query di ricerca (SELECT). Inoltre, SQL offre il supporto per il binding dei valori.
* LDAP - L’inserimento LDAP non è possibile, poiché il modulo di autenticazione filtra l’input ed esegue l’importazione dell’utente tramite il metodo bind.
* Sistema operativo: nessuna esecuzione shell eseguita dall&#39;interno dell&#39;applicazione.

## 2. Cross-Site Scripting (XSS) {#cross-site-scripting-xss}

La pratica generale di mitigazione consiste nel codificare tutti gli output di contenuto generato dall&#39;utente utilizzando una libreria di protezione XSS lato server basata su [OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) e [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS è una priorità assoluta sia durante il test che durante lo sviluppo, e tutti i problemi rilevati vengono (generalmente) risolti immediatamente.

## 3. Autenticazione e gestione delle sessioni interrotte {#broken-authentication-and-session-management}

AEM utilizza tecniche di autenticazione sonore e collaudate, affidandosi a [Apache Jackrabbit](https://jackrabbit.apache.org/) e [Apache Sling](https://sling.apache.org/). Le sessioni browser/HTTP non vengono utilizzate in AEM.

## 4. Riferimenti diretti oggetti non sicuri {#insecure-direct-object-references}

L&#39;accesso agli oggetti dati è gestito dall&#39;archivio e pertanto limitato da un controllo di accesso basato su ruoli.

## 5. Modulo di richiesta intersito (CSRF) {#cross-site-request-forgery-csrf}

Il CSRF (Cross-Site Request Forgery) è attenuato dall&#39;inserimento automatico di un token di crittografia in tutti i moduli e le richieste AJAX e dalla verifica del token sul server per ogni POST.

Inoltre, AEM viene fornito con un filtro basato sull’intestazione del referente, che può essere configurato per consentire *solo* richieste POST da host specifici (definito in un elenco).

## 6. Protezione non configurata {#security-misconfiguration}

È impossibile garantire che tutto il software sia sempre configurato correttamente. Tuttavia, ci sforziamo di fornire il maggior numero possibile di indicazioni e rendere la configurazione il più semplice possibile. Inoltre, AEM viene fornito con controlli di sicurezza [integrati](/help/sites-administering/operations-dashboard.md) che consentono di monitorare rapidamente la configurazione di sicurezza.

Per ulteriori informazioni, consulta l&#39;elenco [di controllo](/help/sites-administering/security-checklist.md) della sicurezza che fornisce istruzioni dettagliate per l&#39;inasprimento delle procedure.

## 7. Archiviazione crittografia non sicura {#insecure-cryptographic-storage}

Le password sono memorizzate come hash crittografici nel nodo utente; per impostazione predefinita tali nodi sono leggibili solo dall&#39;amministratore e dall&#39;utente stesso.

I dati sensibili, come le credenziali di terze parti, vengono memorizzati in un modulo crittografato utilizzando una libreria di crittografia certificata FIPS 140-2.

## 8. Errore di limitazione dell&#39;accesso all&#39;URL {#failure-to-restrict-url-access}

L&#39;archivio consente di impostare privilegi [finemente granulati (come specificato da JCR)](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html) per qualsiasi utente o gruppo in un determinato percorso, attraverso le voci di controllo degli accessi. Le restrizioni di accesso sono applicate dall&#39;archivio.

## 9. Protezione dello strato di trasporto insufficiente {#insufficient-transport-layer-protection}

Mitigato dalla configurazione del server (ad esempio, usa solo HTTPS).

## 10. Reindirizzamenti e inoltri non convalidati {#unvalidated-redirects-and-forwards}

Mitigato limitando tutti i reindirizzamenti alle destinazioni fornite dall&#39;utente alle posizioni interne.

