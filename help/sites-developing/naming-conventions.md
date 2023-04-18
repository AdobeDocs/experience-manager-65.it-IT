---
title: Convenzioni di denominazione dei nodi nell’archivio dei contenuti Jave
description: I nodi nell’archivio sono soggetti a denominazioni convenzionali del Java Content Repository
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 7%

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

L’interfaccia classica impone restrizioni più restrittive:

* Convalida il nome quando un nome di nodo esplicito è presente quando:

   * viene fornito un titolo di pagina per la conversione nel nome del nodo
   * viene fornito un nome di nodo esplicito

* Caratteri validi (solo questi caratteri sono effettivamente validi quando una pagina viene creata dall’interno dell’interfaccia classica, anche se `PageManagerImpl` consentirebbe caratteri aggiuntivi):

   * da &quot;a&quot; a &quot;z&quot;
   * Da &quot;A&quot; a &quot;Z&quot;
   * Da &quot;0&quot; a &quot;9&quot;
   * _ (trattino basso)
   * `-` (trattino/segno meno)
