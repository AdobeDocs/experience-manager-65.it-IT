---
title: Convenzioni di denominazione
seo-title: Convenzioni di denominazione
description: I nodi nell'archivio sono soggetti alle convenzioni di denominazione dell'archivio dei contenuti Java
seo-description: I nodi nell'archivio sono soggetti alle convenzioni di denominazione dell'archivio dei contenuti Java
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---


# Convenzioni di denominazione{#naming-conventions}

I nodi nel repository sono soggetti alle convenzioni di denominazione di [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). Tuttavia AEM ulteriori convenzioni per il nome dei nodi di pagina.

## Convenzioni di denominazione per le pagine {#naming-conventions-for-pages}

Queste convenzioni di denominazione sono implementate a vari livelli:

* JcrUtil: l&#39;implementazione AEM delle utility [JCR](#jcr-utilities).
* PageManager: [Page Manager](#page-manager) fornisce metodi per le operazioni a livello di pagina.
* In base all’interfaccia in uso:

   * [Interfaccia touch standard](#standard-ui)
   * [Interfaccia classica](#classic-ui)

### Utilità JCR {#jcr-utilities}

[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) JcrUtilis l&#39;implementazione AEM delle utility JCR. Di particolare interesse per la convalida dei nomi sono le mappature dei caratteri che controlla e le seguenti convalide:

* `isValidName`

   * Controlla se il nome non è vuoto e contiene solo caratteri validi.
   * Può essere utilizzato per verificare se un nome proposto è valido.

* `createValidName`

   * In questo modo viene creata un&#39;etichetta valida da una stringa arbitraria.
   * Può essere utilizzato per creare un nome da un titolo.

### Page Manager {#page-manager}

[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) PageManager fornisce metodi per le operazioni a livello di pagina, in base a  [JCRUtil](#jcr-utilities).

### Interfaccia standard {#standard-ui}

Interfaccia touch standard:

* Convalida il nome in base alle restrizioni imposte da PageManager quando:

   * un titolo di pagina è fornito per la conversione nel nome del nodo
   * viene fornito un nome di nodo esplicito

### Interfaccia classica {#classic-ui}

L&#39;interfaccia classica impone maggiori restrizioni:

* Convalida il nome quando un nome di nodo esplicito è:

   * un titolo di pagina è fornito per la conversione nel nome del nodo
   * viene fornito un nome di nodo esplicito

* Caratteri validi (solo questi caratteri sono effettivamente validi quando una pagina viene creata dall&#39;interfaccia classica, anche se `PageManagerImpl` consentirebbe caratteri aggiuntivi):

   * Da “a” a “z”
   * Da “A” a “Z”
   * da “0” a “9”
   * _ (trattino basso)
   * `-` (trattino/meno)

