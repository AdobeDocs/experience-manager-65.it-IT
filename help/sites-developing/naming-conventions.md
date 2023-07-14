---
title: Convenzioni di denominazione dei nodi nel Java Content Repository
description: I nodi nell’archivio sono soggetti alle convenzioni di denominazione dell’archivio dei contenuti Java
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: 8cfc42dc8fdf4dc0bfd3f002385f100c81b15993
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 7%

---

# Convenzioni di denominazione {#naming-conventions}

I nodi nell’archivio sono soggetti alle convenzioni di denominazione del [Archivio dei contenuti Java](/help/sites-developing/the-basics.md#java-content-repository). Tuttavia, l’AEM impone ulteriori convenzioni per il nome dei nodi della pagina.

## Convenzioni di denominazione per le pagine {#naming-conventions-for-pages}

Queste convenzioni di denominazione vengono implementate a vari livelli:

* JcrUtil: l&#39;implementazione AEM del [Utilità JCR](#jcr-utilities).
* PageManager: [Gestione pagine](#page-manager) fornisce metodi per le operazioni a livello di pagina.
* In base all’interfaccia utente in uso:

   * [Interfaccia utente touch standard](#standard-ui)
   * [Interfaccia classica](#classic-ui)

### Utilità JCR {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) è l’implementazione AEM delle utilità JCR. Di particolare interesse per la convalida dei nomi sono le mappature di caratteri che controlla e le convalide seguenti:

* `isValidName`

   * Controlla se il nome non è vuoto e contiene solo caratteri validi.
   * Può essere utilizzato per verificare se un nome proposto è valido.

* `createValidName`

   * In questo modo viene creata un&#39;etichetta valida da una stringa arbitraria.
   * Può essere utilizzato per creare un nome da un titolo.

### Gestione pagine {#page-manager}

[PageManager](https://helpx.adobe.com/it/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) fornisce metodi per le operazioni a livello di pagina basati su [JCRUtil](#jcr-utilities).

### Interfaccia standard {#standard-ui}

L’interfaccia utente standard touch:

* Convalida il nome in base alle restrizioni imposte da PageManager quando:

   * viene fornito il titolo della pagina da convertire nel nome del nodo
   * viene fornito un nome di nodo esplicito

### Interfaccia classica {#classic-ui}

L’interfaccia utente classica impone restrizioni più severe:

* Convalida il nome quando un nome di nodo esplicito:

   * viene fornito il titolo della pagina da convertire nel nome del nodo
   * viene fornito un nome di nodo esplicito

* Caratteri validi (solo questi caratteri sono effettivamente validi quando una pagina viene creata dall’interfaccia utente classica, anche se `PageManagerImpl` consentirebbe caratteri aggiuntivi):

   * Da &#39;a&#39; a &#39;z&#39;
   * Da &#39;A&#39; a &#39;Z&#39;
   * Da &#39;0&#39; a &#39;9&#39;
   * _ (trattino basso)
   * `-` (trattino/segno meno)
