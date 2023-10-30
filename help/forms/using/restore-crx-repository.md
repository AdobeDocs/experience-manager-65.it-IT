---
title: Impossibile ripristinare l’archivio CRX danneggiato applicabile al server cluster JEE
description: Passaggi per ripristinare l’archivio CRX danneggiato.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# Impossibile ripristinare l’archivio CRX danneggiato {#unable-to-restore-corrupt-crx-repository}

## Problema   {#issue}

Per AEM Forms su JEE che utilizza un database relazionale, il tempo sul computer che ospita AEM Forms e il database relazionale deve sempre essere sincronizzato in modo assoluto. Se l’ora su questi computer non è sincronizzata, l’archivio CRX di AEM Forms sul server JEE può diventare inaccessibile. Potrebbe apparire danneggiato e diventare inaccessibile tramite URL. Il `AuthenticationsupportService missing` l&#39;errore viene registrato.

## Prerequisiti {#prerequisites}

Esegui il backup dell’archivio CRX prima di eseguire i passaggi indicati di seguito.

## Soluzione {#solution}

Per risolvere il problema, effettua le seguenti operazioni:
1. Passa a  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Individua il `oak-core` e controlla se è in esecuzione.

1. Riavvia il `oak-core` se non è in esecuzione. Se  ![Pulsante Pausa](/help/forms/using/assets/stop.png) presente davanti al `oak-core` indica che il bundle è in esecuzione.

1. Se il problema non è ancora stato risolto, eseguire il ripristino dall&#39;archivio CRX dal backup o rigenerare l&#39;archivio CRX se il backup non è disponibile.


## Si applica a {#applies-to}

Questa soluzione si applica a:

* AEM Forms su cluster JEE