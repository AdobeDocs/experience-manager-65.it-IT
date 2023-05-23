---
title: Architettura dei contenuti
seo-title: Content Architecture
description: 'Suggerimenti per l’architettura dei contenuti (suggerimento: tutto è contenuto)'
seo-description: Tips for architecting your content in Adobe Experience Manager (AEM). (hint - everything is content)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Architettura dei contenuti{#content-architecture}

## Segui il modello di David {#follow-david-s-model}

Il modello di David è stato scritto da David Nuescheler anni fa, ma le idee sono vere oggi. I principi principali del modello di David sono i seguenti:

* I dati vengono prima, struttura dopo. Forse.
* Guidare la gerarchia dei contenuti, non lasciare che accada.
* Le aree di lavoro sono per `clone()`, `merge()`, e `update()`.
* Attenzione ai fratelli con lo stesso nome.
* I riferimenti sono considerati dannosi.
* I file sono file.
* Gli ID sono malvagi.

Il modello di David si trova sul wiki Jackrabbit all&#39;indirizzo [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Tutto è contenuto {#everything-is-content}

Tutto deve essere archiviato nell’archivio anziché affidarsi a origini dati di terze parti separate, come i database. Questo vale per i contenuti creati, i dati binari come immagini, codice, configurazioni, ecc. Questo ci consente di utilizzare un unico set di API per gestire tutti i contenuti e per gestirne la promozione tramite la replica. EMC offre inoltre un&#39;unica fonte di backup, registrazione e così via.

### Utilizza il principio di progettazione &quot;prima il modello di contenuto&quot; {#use-the-content-model-first-design-principle}

Quando crei una nuova funzione, inizia sempre progettando prima la struttura del contenuto JCR, quindi cerca di leggere e scrivere il contenuto utilizzando i servlet Sling predefiniti. Questo ti consentirà di garantire il corretto funzionamento della tua implementazione con meccanismi di controllo degli accessi predefiniti e di evitare di generare servlet di tipo CRUD non necessari.

### Essere RESTful {#be-restful}

I servlet devono essere definiti in base ai resourceTypes anziché ai percorsi. In questo modo è possibile utilizzare i controlli di accesso JCR, rispettare i principi REST e utilizzare le risorse e il risolutore risorse forniti nella richiesta. Questo consente inoltre di modificare gli script che eseguono il rendering degli URL sul lato server senza dover modificare alcun URL dal lato client, nascondendo al contempo i dettagli di implementazione lato server dal client per una maggiore sicurezza.

### Evita di definire nuovi tipi di nodo {#avoid-defining-new-node-types}

I tipi di nodo funzionano a un livello basso nel livello dell’infrastruttura e la maggior parte dei requisiti può essere soddisfatta utilizzando un tipo di nodo sling:resourceType assegnato a un tipo di nodo nt:unstructured, oak:Unstructured, sling:Folder o cq:Page. I tipi di nodo equivalgono allo schema nell’archivio e la modifica dei tipi di nodo può risultare molto costosa.

### Rispettare le convenzioni di denominazione nel JCR {#adhere-to-naming-conventions-in-the-jcr}

Il rispetto delle convenzioni di denominazione aggiungerà coerenza alla base di codice, riducendo il tasso di incidenza dei difetti e aumentando la velocità degli sviluppatori che lavorano nel sistema. Le seguenti convenzioni sono utilizzate per Adobe nello sviluppo dell&#39;AEM:

* Nomi di nodo

   * Tutte minuscole
   * Separazione delle parole mediante trattini

* Nomi di proprietà

   * Camel case, a partire da una lettera minuscola

* Componenti (JSP/HTML)

   * Tutte minuscole
   * Separazione delle parole mediante trattini
