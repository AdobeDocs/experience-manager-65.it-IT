---
title: Impossibile ripristinare l’archivio CRX danneggiato applicabile al server cluster JEE
description: Scopri come ripristinare un archivio CRX danneggiato.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# Impossibile ripristinare l’archivio CRX danneggiato {#unable-to-restore-corrupt-crx-repository}

## Problema   {#issue}

Per AEM Forms su JEE che utilizza un database relazionale, il tempo sul computer che ospita AEM Forms e il database relazionale deve sempre essere sincronizzato in modo assoluto. Se l’ora su questi computer non è sincronizzata, l’archivio CRX di AEM Forms sul server JEE può diventare inaccessibile. Potrebbe apparire danneggiato e diventare inaccessibile tramite URL. Il `AuthenticationsupportService missing` l&#39;errore viene registrato.

## Prerequisiti {#prerequisites}

Esegui il backup dell’archivio CRX prima di eseguire i passaggi indicati di seguito.

## Soluzione {#solution}

1. Vai a  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Individua il `oak-core` e controlla se è in esecuzione.

1. Riavvia il `oak-core` se non è in esecuzione. Se  ![Pulsante Pausa](/help/forms/using/assets/stop.png) presente davanti al `oak-core` indica che il bundle è in esecuzione.

1. Se il problema non è ancora stato risolto, eseguire il ripristino dall&#39;archivio CRX dal backup o rigenerare l&#39;archivio CRX se il backup non è disponibile.


## Si applica a {#applies-to}

Questa soluzione si applica ad AEM Forms su cluster JEE.
