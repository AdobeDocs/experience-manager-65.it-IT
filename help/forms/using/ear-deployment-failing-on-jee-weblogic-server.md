---
title: Distribuzione EAR non riuscita sul server WebLogic JEE
description: Passaggi per risolvere un errore di distribuzione EAR nel server JEE WebLogic
exl-id: b87a9eee-ee56-4dca-b4a3-a42c91db0b4f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
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

       imposta `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Salva le modifiche.
