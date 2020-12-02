---
title: Architettura dei contenuti
seo-title: Architettura dei contenuti
description: 'Suggerimenti per l''architettura dei contenuti (suggerimenti: tutto è contenuto)'
seo-description: Suggerimenti per l’architettura dei contenuti in Adobe Experience Manager (AEM). (hint - tutto è contenuto)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Architettura dei contenuti{#content-architecture}

## Segui il modello di David {#follow-david-s-model}

Il Modello di David è stato scritto da David Nuescheler anni fa, ma le idee sono vere oggi. I principali principi del modello di David sono i seguenti:

* I dati vengono prima, la struttura dopo. Forse.
* Guidare la gerarchia dei contenuti, non lasciarla accadere.
* Le aree di lavoro sono `clone()`, `merge()` e `update()`.
* Fai attenzione ai fratelli con lo stesso nome.
* I riferimenti sono considerati dannosi.
* I file sono file.
* Gli ID sono malvagi.

Il modello di David è disponibile sul wiki Jackrabbit all&#39;indirizzo [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Tutto è contenuto {#everything-is-content}

Tutto deve essere memorizzato nell&#39;archivio piuttosto che basarsi su origini dati di terze parti separate, come i database. Questo vale per i contenuti creati, dati binari come immagini, codice, configurazioni, ecc. Questo consente di utilizzare un set di API per gestire tutto il contenuto e per gestire la promozione di tale contenuto tramite la replica. Abbiamo anche un&#39;unica fonte di backup, registrazione, ecc.

### Utilizzare il principio di progettazione &quot;content model first&quot; {#use-the-content-model-first-design-principle}

Quando create una nuova funzione, iniziate sempre progettando la struttura del contenuto JCR, quindi cercate di leggere e scrivere il contenuto utilizzando i servlet Sling predefiniti. Questo vi consentirà di garantire il buon funzionamento dell&#39;implementazione con meccanismi di controllo dell&#39;accesso out-of-box e di evitare la generazione di servlet CRUD non necessari.

### Essere RESTful {#be-restful}

I servlet devono essere definiti in base a resourceTypes anziché ai percorsi. Questo consente di utilizzare i controlli di accesso JCR, aderire ai principi REST e utilizzare il risolutore di risorse e risorse fornito nella richiesta. Questo consente anche di modificare gli script che eseguono il rendering degli URL sul lato server senza dover modificare alcun URL dal lato client, nascondendo al contempo dal client i dettagli di implementazione lato server per una maggiore sicurezza.

### Evitare di definire nuovi tipi di nodo {#avoid-defining-new-node-types}

I tipi di nodo funzionano a un livello basso nel livello dell&#39;infrastruttura e la maggior parte dei requisiti può essere soddisfatta utilizzando un tipo di nodo sling:resourceType assegnato a un tipo di nodo nt:unstructure, oak:Unstructure, sling:Folder o cq:Page. I tipi di nodo equivalgono allo schema nel repository e la modifica dei tipi di nodo può essere molto costoso lungo la strada.

### Conformità alle convenzioni di denominazione in JCR {#adhere-to-naming-conventions-in-the-jcr}

Il rispetto delle convenzioni di denominazione darà coerenza alla base di codice, riducendo il tasso di incidenza dei difetti e aumentando la velocità degli sviluppatori che lavorano nel sistema. Il Adobe utilizza le seguenti convenzioni per sviluppare AEM:

* Nomi nodo

   * Tutte le maiuscole
   * Separazione delle parole mediante trattini

* Nomi proprietà

   * Cassa del cammello, a partire da una lettera minuscola

* Componenti (JSP/HTML)

   * Tutte le maiuscole
   * Separazione delle parole mediante trattini

