---
title: Distribuzione EAR non riuscita sul server WebLogic JEE
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Passaggi per risolvere un errore di distribuzione EAR nel server JEE WebLogic
exl-id: 109d9182-5e3f-477e-9417-abc83d5ea3bc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 14%
---
# Distribuzione EAR non riuscita sul server WebLogic JEE {#ear-deployment-failing-on-jee-weblogic-server}

## Problema {#issue}

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
