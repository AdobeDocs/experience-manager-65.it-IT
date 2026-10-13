---
title: Impossibile ripristinare l’archivio CRX danneggiato applicabile al server cluster JEE
description: Scopri come ripristinare un archivio CRX danneggiato.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%
---
# Impossibile ripristinare l’archivio CRX danneggiato {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Per AEM Forms su JEE che utilizza un database relazionale, il tempo sul computer che ospita AEM Forms e il database relazionale deve sempre essere sincronizzato in modo assoluto. Se l’ora su questi computer non è sincronizzata, l’archivio CRX di AEM Forms sul server JEE può diventare inaccessibile. Potrebbe apparire danneggiato e diventare inaccessibile tramite URL. Errore `AuthenticationsupportService missing` registrato.

## Prerequisiti {#prerequisites}

Esegui il backup dell’archivio CRX prima di eseguire i passaggi indicati di seguito.

## Soluzione {#solution}

1. Vai a `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Individuare il bundle `oak-core` e verificare che sia in esecuzione.

1. Riavviare il bundle `oak-core` se non è in esecuzione. Se l&#39;icona ![Pause button](/help/forms/using/assets/stop.png) è presente davanti al bundle `oak-core`, indica che il bundle è in esecuzione.

1. Se il problema non è ancora stato risolto, eseguire il ripristino dall&#39;archivio CRX dal backup o ricreare l&#39;archivio CRX se il backup non è disponibile.


## Si applica a {#applies-to}

Questa soluzione si applica ad AEM Forms su cluster JEE.
