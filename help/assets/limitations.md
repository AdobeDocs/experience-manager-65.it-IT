---
title: Limiti di Dynamic Media
description: Scopri le best practice e i limiti applicati quando crei un set di immagini o un set 360 gradi o carichi un PDF. Scopri anche le combinazioni di browser web e sistemi operativi non supportate per Dynamic Media.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: c12bda38-aa1a-4647-b62e-42cd4537dac6
    internal-label: Dynamic Media Classic
  - id: e2dc1259-9034-40fc-a518-b92a34fe6642
    internal-label: Image sets
  - id: cb008a68-9156-4b10-9c66-391409a53067
    internal-label: Spin Sets
  - id: fb5874db-3110-450a-b647-a5c2ce139bef
    internal-label: eCatalog
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 8%
---
# Limitazioni per elementi multimediali dinamici

Le sezioni seguenti descrivono le limitazioni di Dynamic Media.

Questo argomento include le sezioni seguenti:

* [Best practice e limiti applicati da Dynamic Media ai tipi di risorse](#best-practice-enforced-limits)
* [Combinazioni di browser web e sistemi operativi non supportate per Dynamic Media](#unsupported-browser-os)

## Best practice e limiti applicati da Dynamic Media ai tipi di risorse {#best-practice-enforced-limits}

Quando crei un set 360 gradi o un set di immagini o carichi PDF per l’estrazione di pagine, Adobe consiglia le seguenti best practice e applica i seguenti limiti:

| Risorsa - Tipo di limite | Best practice | Limite imposto |
| --- | --- | --- |
| **Immagine** - Numero di ritagli avanzati per immagine | 5 | 100 |
| **Tutti i set** - Numero di risorse duplicate per set | Nessun duplicato | 20‡ |
| **Tutti i set** - Numero massimo di risorse per set | 5-10 immagini per set | 1000 |
| **Set 360 gradi** - Numero massimo di righe/colonne per set 2D | 12-18 immagini per set | 1000 |
| **PDF** - Numero massimo di pagine per un PDF da considerare per l&#39;estrazione |  | 100 (per tutti i PDF) |

‡ best practice prevede di non avere risorse duplicate in un set. Il limite è di 20 duplicati per una singola risorsa. Se aggiungi un altro duplicato per quella risorsa, all’interno di quel set, la richiesta restituisce un errore o ignora il duplicato.
<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Combinazioni di browser web e sistemi operativi non supportate per Dynamic Media {#unsupported-browser-os}

Dynamic Media non supporta le seguenti combinazioni di browser web e sistemi operativi.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Aggiornamento Internet Explorer 11 + Windows Phone 8.1
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## Fine del supporto per Secure Socket Layer 2.0 e 3.0 e Transport Layer Security 1.0 e 1.1 {#tls}

<!--
CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)
-->

A partire dal 30 aprile 2024, Adobe Dynamic Media terminerà il supporto per i seguenti elementi:

* SSL (Secure Socket Layer) 2.0
* SSL 3.0
* TLS (Transport Layer Security) 1.0 e 1.1
* Le seguenti crittografie deboli in TLS 1.2:
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_RSA_WITH_AES_256_GCM_SHA384`
  * `TLS_RSA_WITH_AES_256_CBC_SHA256`
  * `TLS_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_AES_128_GCM_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

