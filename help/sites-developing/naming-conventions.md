---
title: Convenzioni di denominazione
seo-title: Naming Conventions
description: I nodi nell’archivio sono soggetti a denominazioni convenzionali del Java Content Repository
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 17%

---

# Convenzioni di denominazione{#naming-conventions}

I nodi nell&#39;archivio sono soggetti a convenzioni di denominazione [Archivio dei contenuti Java](/help/sites-developing/the-basics.md#java-content-repository). Tuttavia AEM impone ulteriori convenzioni per il nome dei nodi di pagina.

## Convenzioni di denominazione per le pagine {#naming-conventions-for-pages}

Queste convenzioni di denominazione sono implementate a vari livelli:

* JcrUtil: l&#39;attuazione AEM [Utilità JCR](#jcr-utilities).
* PageManager: la [Gestione pagine](#page-manager) fornisce metodi per le operazioni a livello di pagina.
* A seconda dell’interfaccia in uso:

   * [Interfaccia standard con funzionalità touch](#standard-ui)
   * [Interfaccia classica](#classic-ui)

### Utilità JCR {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) è l’implementazione AEM delle utility JCR. Di particolare interesse per la convalida dei nomi sono le mappature dei caratteri che controlla e le seguenti convalide:

* `isValidName`

   * Controlla se il nome non è vuoto e contiene solo caratteri validi.
   * Può essere utilizzato per verificare se un nome proposto è valido.

* `createValidName`

   * Questo crea un&#39;etichetta valida da una stringa arbitraria.
   * Può essere utilizzato per creare un nome da un titolo.

### Gestione pagine {#page-manager}

[PageManager](https://helpx.adobe.com/it/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) fornisce metodi per le operazioni a livello di pagina, in base a [JCRUtil](#jcr-utilities).

### Interfaccia standard {#standard-ui}

Interfaccia touch standard:

* Convalida il nome in base alle restrizioni imposte da PageManager quando:

   * viene fornito un titolo di pagina per la conversione nel nome del nodo
   * viene fornito un nome di nodo esplicito

### Interfaccia classica {#classic-ui}

L&#39;interfaccia classica impone maggiori restrizioni:

* Convalida il nome quando un nome di nodo esplicito è presente quando:

   * viene fornito un titolo di pagina per la conversione nel nome del nodo
   * viene fornito un nome di nodo esplicito

* Caratteri validi (solo questi caratteri sono effettivamente validi quando una pagina viene creata dall’interno dell’interfaccia classica, anche se `PageManagerImpl` consentirebbe caratteri aggiuntivi):

   * Da “a” a “z”
   * Da “A” a “Z”
   * da “0” a “9”
   * _ (trattino basso)
   * `-` (trattino/meno)
