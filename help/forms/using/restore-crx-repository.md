---
title: Impossibile ripristinare l'archivio CRX danneggiato applicabile al server cluster JEE
description: Passaggi per ripristinare l'archivio CRX danneggiato
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: c4f776b08cb8cc8c6eea78a3757735e063bec20c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# Impossibile ripristinare l&#39;archivio CRX corrotto {#unable-to-restore-corrupt-crx-repository}

## Problema   {#issue}

Per AEM Forms su JEE che utilizza un database relazionale, il tempo sul computer che ospita AEM Forms e il database relazionale deve sempre essere in sincronia assoluta. Se il tempo su questi computer non è sincronizzato, l&#39;archivio CRX di AEM Forms sul server JEE può diventare inaccessibile. Potrebbe apparire danneggiato e diventare inaccessibile tramite URL. La `AuthenticationsupportService missing` errore registrato.

## Prerequisiti {#prerequisites}

Esegui il backup del tuo archivio CRX prima di eseguire i passaggi indicati di seguito.

## Soluzione {#solution}

Esegui i seguenti passaggi per risolvere il problema:
1. Passa a  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Individua il `oak-core` e controlla se è in esecuzione.

1. Riavvia `oak-core` se non è in esecuzione. Se  ![Pulsante Pausa](/help/forms/using/assets/stop.png) l&#39;icona è presente di fronte alla `oak-core` bundle, quindi indica che il bundle è in esecuzione.

1. Se il problema non è ancora risolto, ripristina dall&#39;archivio CRX dal backup o ricostruisci l&#39;archivio CRX se il backup non è disponibile.


## Si applica a {#applies-to}

Questa soluzione si applica a:

* AEM Forms su cluster JEE