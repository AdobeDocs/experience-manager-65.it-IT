---
title: Distribuzione EAR non riuscita sul server WebLogic JEE
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Passaggi per risolvere un errore di distribuzione EAR nel server JEE WebLogic
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
source-git-commit: 45bb54a2666c2c196a8fb52795a7f428aa751e4d
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 6%

---


# Distribuzione EAR non riuscita sul server WebLogic JEE {#ear-deployment-failing-on-jee-weblogic-server}

## Problema   {#issue}

Quando un utente tenta di distribuire il `adobe-livecycle-weblogic.ear`, il `Null Pointer` è stata riscontrata un&#39;eccezione.

## Applicabile a {#applies-to}

Questa soluzione si applica a:

* AEM Forms sul server WebLogic JEE versione 12.2.1.x.

## Soluzione {#solution}

Per risolvere il problema, effettua le seguenti operazioni:

1. Vai a `<domain_home>\bin` directory del server WebLogic JEE installato.

1. Modifica il `setDomainEnv.cmd` o `setDomainEnv.sh` file, come `applicable`.

1. Cerca l&#39;ultima occorrenza di `JAVA_OPTS` e aggiungi `-DANTLR_USE_DIRECT_CLASS_LOADING=true` ad esso. Ad esempio, la stringa aggiornata viene visualizzata come:

       set `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Salva le modifiche.


