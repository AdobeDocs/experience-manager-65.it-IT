---
title: OWASP Top 10
seo-title: OWASP Top 10
description: Scopri come AEM gestire i principali 10 rischi di sicurezza OWASP.
seo-description: Learn how AEM deals with the top 10 OWASP security risks.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# OWASP Top 10{#owasp-top}

Il [Progetto di sicurezza di un&#39;applicazione Web aperta](https://www.owasp.org) (OWASP) mantiene un elenco dei 10 principali rischi di sicurezza dell&#39;applicazione Web [principali.](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)

Questi sono elencati di seguito, insieme a una spiegazione di come CRX tratta con loro.

## 1. Iniezione {#injection}

* SQL - Preventivo della progettazione: La configurazione predefinita dell’archivio non include né richiede un database tradizionale, tutti i dati vengono memorizzati nell’archivio dei contenuti. L’accesso è limitato agli utenti autenticati e può essere eseguito solo tramite l’API JCR. SQL supportato solo per le query di ricerca (SELECT). Inoltre, SQL offre il supporto per il binding dei valori.
* LDAP - L&#39;inserimento LDAP non è possibile, in quanto il modulo di autenticazione filtra l&#39;input ed esegue l&#39;importazione dell&#39;utente utilizzando il metodo bind.
* Sistema operativo: nessuna esecuzione della shell eseguita dall&#39;interno dell&#39;applicazione.

## 2. Script tra siti (XSS) {#cross-site-scripting-xss}

La pratica generale di mitigazione è quella di codificare tutti gli output di contenuti generati dall&#39;utente utilizzando una libreria di protezione XSS lato server basata su [OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) e [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS è una priorità assoluta sia durante i test che durante lo sviluppo e tutti i problemi rilevati vengono (in genere) risolti immediatamente.

## 3. Autenticazione non riuscita e gestione delle sessioni {#broken-authentication-and-session-management}

AEM utilizza tecniche di autenticazione sonore e comprovate, che si basano su [Apache Jackrabbit](https://jackrabbit.apache.org/) e [Apache Sling](https://sling.apache.org/). Le sessioni browser/HTTP non sono utilizzate in AEM.

## 4. Riferimenti agli oggetti diretti non sicuri {#insecure-direct-object-references}

L’accesso a tutti gli oggetti dati viene mediato dall’archivio e quindi limitato dal controllo degli accessi basato su ruoli.

## 5. Forgeria di richiesta intersito (CSRF) {#cross-site-request-forgery-csrf}

Il CSRF (Cross-Site Request Forgery) è mitigato dall’inserimento automatico di un token di crittografia in tutti i moduli e le richieste di AJAX e dalla verifica di tale token sul server per ogni POST.

Inoltre, AEM viene fornito con un filtro basato sull’intestazione del referente, che può essere configurato su *only* per consentire le richieste POST da host specifici (definito in un elenco).

## 6. Configurazione errata della sicurezza {#security-misconfiguration}

È impossibile garantire che tutto il software sia sempre configurato correttamente. Tuttavia, ci sforziamo di fornire il maggior numero possibile di indicazioni e rendere la configurazione il più semplice possibile. Inoltre, AEM viene fornito con [controlli di sicurezza integrati](/help/sites-administering/operations-dashboard.md) che consentono di monitorare immediatamente la configurazione della sicurezza.

Per ulteriori informazioni, consulta la [Lista di controllo sicurezza](/help/sites-administering/security-checklist.md) che fornisce istruzioni dettagliate per l&#39;indurimento dei passaggi.

## 7. Archiviazione crittografica non sicura {#insecure-cryptographic-storage}

le password sono memorizzate come hash di crittografia nel nodo utente; per impostazione predefinita tali nodi sono leggibili solo dall’amministratore e dall’utente stesso.

I dati sensibili, come le credenziali di terze parti, vengono memorizzati in formato crittografato utilizzando una libreria di crittografia certificata FIPS 140-2.

## 8. Errore nel limitare l&#39;accesso agli URL {#failure-to-restrict-url-access}

L&#39;archivio consente l&#39;impostazione di [privilegi a grana fine (come specificato da JCR)](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) per qualsiasi utente o gruppo in un dato percorso, attraverso le voci di controllo degli accessi. Le restrizioni di accesso sono applicate dall’archivio.

## 9. Protezione insufficiente dello strato di trasporto {#insufficient-transport-layer-protection}

È attenuata dalla configurazione del server (ad esempio, utilizza solo HTTPS).

## 10. Reindirizzamenti e inoltri non convalidati {#unvalidated-redirects-and-forwards}

È possibile attenuare la limitazione di tutti i reindirizzamenti alle destinazioni fornite dall’utente nelle posizioni interne.
