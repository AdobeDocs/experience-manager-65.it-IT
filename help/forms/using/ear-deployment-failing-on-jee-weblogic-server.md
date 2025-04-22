---
title: Distribuzione EAR non riuscita sul server WebLogic JEE
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Passaggi per risolvere un errore di distribuzione EAR nel server JEE WebLogic
source-git-commit: 05712cfcef1d9c37b7cd015133abaf6df0e351d2
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 7%

---


# Distribuzione EAR non riuscita sul server WebLogic JEE {#ear-deployment-failing-on-jee-weblogic-server}

## Problema   {#issue}

Quando un utente tenta di distribuire `adobe-livecycle-weblogic.ear`, si verifica l&#39;eccezione `Null Pointer`.

## Applicabile a {#applies-to}

Questa soluzione si applica a:

* AEM Forms sul server WebLogic JEE versione 12.2.1.x.

## Soluzione {#solution}

Per risolvere il problema, effettua le seguenti operazioni:

1. Passare alla directory `<domain_home>\bin` del server WebLogic JEE installato.

1. Modificare il file `setDomainEnv.cmd` o `setDomainEnv.sh` come `applicable`.

1. Cerca l&#39;ultima occorrenza di `JAVA_OPTS` e aggiungi `-DANTLR_USE_DIRECT_CLASS_LOADING=true`. Ad esempio, la stringa aggiornata viene visualizzata come:

       impostare &#39;JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true&#39;
   
1. Salva le modifiche.
