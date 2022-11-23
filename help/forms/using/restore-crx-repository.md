---
title: Impossibile ripristinare l'archivio CRX danneggiato applicabile al server cluster JEE
description: Passaggi per ripristinare l'archivio CRX danneggiato
source-git-commit: a7d125503b0bd3c52cb3a959e2f0dde1a69cbe2b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# Impossibile ripristinare l&#39;archivio CRX corrotto {#unable-to-restore-corrupt-crx-repository}

## Problema   {#issue}

Per AEM Forms distribuito su JEE con persistenza RDB, è necessario che le macchine host e le macchine database AEM Forms siano in sincronia temporale assoluta. Tuttavia, se per qualche motivo gli orologi escono dalla sincronizzazione, allora l&#39;archivio CRX viene corrotto e i suoi URL diventano inaccessibili. L&#39;errore è `AuthenticationsupportService missing` si verifica nei file di registro.

## Soluzione {#solution}

Esegui i seguenti passaggi per risolvere il problema:
1. Vai a  [https://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. Individua il `oak-core` e controlla se è in esecuzione.

1. Riavvia `oak-core` se non è in esecuzione. Se il pulsante di pausa è presente davanti al `oak-core` bundle, quindi indica che il bundle è in esecuzione.

1. Se il problema non è ancora risolto, ripristina dall&#39;archivio CRX dal backup o ricostruisci l&#39;archivio CRX se il backup non è disponibile.

   >[!NOTE]
   >
   >Esegui il backup del tuo archivio CRX prima di eseguire i passaggi precedenti.

## Si applica a {#applies-to}

Questa soluzione si applica a:

* AEM Forms su JEE Cluster Server


