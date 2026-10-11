---
title: Architettura dei contenuti
description: 'Suggerimenti per l’architettura dei contenuti (suggerimento: tutto è contenuto)'
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%
---
# Architettura dei contenuti{#content-architecture}

## Segui il modello di David {#follow-david-s-model}

Il modello di David è stato scritto da David Nuescheler anni fa, ma le idee sono vere oggi. I principi principali del modello di David sono i seguenti:

* I dati vengono prima, struttura dopo. Forse.
* Guidare la gerarchia dei contenuti, evitare che ciò accada.
* Le aree di lavoro sono per `clone()`, `merge()` e `update()`.
* Attenzione agli stessi fratelli e sorelle.
* I riferimenti sono considerati dannosi.
* I file sono file.
* Gli ID sono malvagi.

Il modello di David si trova nel wiki Jackrabbit all&#39;indirizzo [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Tutto è contenuto {#everything-is-content}

Tutto deve essere archiviato nell’archivio anziché affidarsi a origini dati separate di terze parti, come i database. Questo vale per i contenuti creati, i dati binari come immagini, codice e configurazioni. Questo ci consente di utilizzare un unico set di API per gestire tutti i contenuti e per gestirne la promozione tramite la replica. Inoltre, è possibile ottenere un&#39;unica fonte di backup, registrazione e così via.

### Utilizza il principio di progettazione &quot;prima il modello di contenuto&quot; {#use-the-content-model-first-design-principle}

Quando crei una nuova funzione, inizia sempre progettando prima la struttura del contenuto JCR, quindi cerca di leggere e scrivere il contenuto utilizzando i servlet Sling predefiniti. Questo consente di garantire il corretto funzionamento dell’implementazione con meccanismi di controllo dell’accesso predefiniti, evitando di generare servlet di tipo CRUD non necessari.

### Essere RESTful {#be-restful}

I servlet devono essere definiti in base ai resourceTypes anziché ai percorsi. In questo modo è possibile utilizzare i controlli di accesso JCR, rispettare i principi REST e utilizzare le risorse e il risolutore risorse forniti nella richiesta. Questo consente inoltre di modificare gli script che eseguono il rendering degli URL sul lato server senza dover modificare alcun URL dal lato client, nascondendo al contempo i dettagli di implementazione lato server dal client per una maggiore sicurezza.

### Evita di definire nuovi tipi di nodo {#avoid-defining-new-node-types}

I tipi di nodo funzionano a un livello basso nel livello dell&#39;infrastruttura e la maggior parte dei requisiti può essere soddisfatta utilizzando un sling:resourceType assegnato a un tipo di nodo nt:unstructured, oak:Unstructured, sling:Folder o cq:Page. I tipi di nodo equivalgono allo schema nell’archivio e la modifica dei tipi di nodo può risultare costosa in qualsiasi momento.

### Rispettare le convenzioni di denominazione nel JCR {#adhere-to-naming-conventions-in-the-jcr}

Il rispetto delle convenzioni di denominazione aggiunge coerenza alla base di codice, riducendo il tasso di incidenza dei difetti e aumentando la velocità degli sviluppatori che lavorano nel sistema. Adobe utilizza le seguenti convenzioni per lo sviluppo di AEM:

* Nomi di nodo

  * Tutte minuscole
  * Separazione delle parole mediante trattini

* Nomi di proprietà

  * Camel case, a partire da una lettera minuscola

* Componenti (JSP/HTML)

  * Tutte minuscole
  * Separazione delle parole mediante trattini
