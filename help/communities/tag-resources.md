---
title: Assegnazione tag alle risorse di abilitazione
seo-title: Assegnazione tag alle risorse di abilitazione
description: L’assegnazione di tag alle risorse di abilitazione consente di filtrare le risorse e i percorsi di apprendimento come membri di un catalogo di ricerca
seo-description: L’assegnazione di tag alle risorse di abilitazione consente di filtrare le risorse e i percorsi di apprendimento come membri di un catalogo di ricerca
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# Assegnazione tag alle risorse di abilitazione {#tagging-enablement-resources}

## Panoramica {#overview}

L’assegnazione di tag alle risorse di abilitazione consente di filtrare le risorse e i percorsi di apprendimento come membri di [cataloghi](functions.md#catalog-function)di ricerca.

Essenzialmente:

* [Creare uno spazio dei nomi](../../help/sites-administering/tags.md#creating-a-namespace) tag per ciascun catalogo

   * [Impostare le autorizzazioni dei tag](../../help/sites-administering/tags.md#setting-tag-permissions)
   * Solo per i membri della comunità (comunità chiusa)

      * Consenti accesso in lettura al gruppo di membri del sito [community](users.md#publish-group-roles)
   * Per qualsiasi visitatore del sito, che abbia effettuato l’accesso o sia anonimo (community aperta)

      * Consenti accesso in lettura per il `Everyone` gruppo
   * [Pubblicare i tag](../../help/sites-administering/tags.md#publishing-tags)



* [Definire l&#39;ambito dei tag per un sito community](sites-console.md#tagging)

   * [Configurare i cataloghi esistenti nella struttura del sito](functions.md#catalog-function)

      * Può aggiungere tag all’istanza del catalogo per controllare l’elenco di tag presenti nei filtri dell’interfaccia utente.
      * Può aggiungere [pre-filtri](catalog-developer-essentials.md#pre-filters), per limitare le risorse incluse in un catalogo.

* [Pubblicare il sito della community](sites-console.md#publishing-the-site)
* [Applicare tag alle risorse](resources.md#create-a-resource) di abilitazione in modo che possano essere filtrate in modo categorico
* [Pubblicare le risorse di abilitazione](resources.md#publish)

## Tag sito community {#community-site-tags}

Quando create o modificate un sito community, l&#39;impostazione [](sites-console.md#tagging) Tagging imposta l&#39;ambito dei tag disponibili per le funzioni del sito selezionando un sottoinsieme di spazi dei nomi dei tag esistenti.

Anche se i tag possono essere creati e aggiunti al sito della community in qualsiasi momento, si consiglia di progettare in anticipo una tassonomia, simile alla progettazione di un database. Consultate [Utilizzo dei tag](../../help/sites-authoring/tags.md).

Quando successivamente si aggiungono tag a un sito community esistente, è necessario salvare la modifica prima di poter aggiungere il nuovo tag a una funzione catalogo nella struttura del sito.

Per un sito community, dopo la pubblicazione del sito e la pubblicazione dei tag, è necessario consentire l&#39;accesso in lettura ai membri della community. Consultate [Impostazione delle autorizzazioni](../../help/sites-administering/tags.md#setting-tag-permissions)per i tag.

Di seguito viene illustrato come viene visualizzato in CRXDE quando un amministratore applica le autorizzazioni di lettura `/etc/tags/ski-catalog` per il gruppo `Community Enable Members`.

![site-tags](assets/site-tags.png)

## Spazi dei nomi dei tag del catalogo {#catalog-tag-namespaces}

La funzione del catalogo utilizza i tag per definirsi. Quando si configura la funzione del catalogo in un sito community, l&#39;insieme di spazi dei nomi dei tag tra cui scegliere viene definito dall&#39;ambito degli spazi dei tag impostati per il sito community.

La funzione Catalog include un&#39;impostazione di tag che definisce i tag elencati nell&#39;interfaccia utente del filtro per il catalogo. L&#39;impostazione &quot;Tutti i namespace&quot; fa riferimento all&#39;ambito degli spazi dei nomi dei tag selezionati per il sito della community.

![catalog-namespace](assets/catalog-namespace.png)

## Applicazione dei tag alle risorse di abilitazione {#applying-tags-to-enablement-resources}

Le risorse di abilitazione e i percorsi di apprendimento verranno visualizzati in tutto il catalogo quando `Show in Catalog` è selezionato. L’aggiunta di tag a risorse e percorsi di apprendimento consentirà di prefiltrare in cataloghi specifici e di filtrare l’interfaccia utente del catalogo.

Limitando le risorse di abilitazione e i percorsi di apprendimento per cataloghi specifici, potete creare [pre-filtri](catalog-developer-essentials.md#pre-filters).

L’interfaccia utente del catalogo consente ai visitatori di applicare un filtro tag all’elenco delle risorse e dei percorsi di apprendimento visualizzati in tale catalogo.

L’amministratore che applica i tag alle risorse di abilitazione deve essere a conoscenza degli spazi dei nomi dei tag associati ai cataloghi, nonché della tassonomia, al fine di selezionare un tag secondario per una classificazione più precisa.

Ad esempio, se uno `ski-catalog` spazio nomi è stato creato e impostato su un catalogo denominato `Ski Catalog`, potrebbe avere due tag secondari: `lesson-1` e `lesson-2`.

Di conseguenza, qualsiasi risorsa di abilitazione con un tag tra:

* ski-catalog:session-1
* ski-catalog:session-2

verrà visualizzato in `Ski Catalog` dopo la pubblicazione della risorsa di abilitazione.

![basic-info](assets/applytags-basicinfo.png)

## Visualizzazione del catalogo in Pubblica {#viewing-catalog-on-publish}

Una volta che tutto è stato configurato dall’ambiente di authoring e pubblicato, nell’ambiente di pubblicazione è possibile utilizzare il catalogo per trovare le risorse di abilitazione.

Se nell’elenco a discesa non vengono visualizzati spazi dei nomi dei tag, accertatevi che le autorizzazioni siano state impostate correttamente nell’ambiente di pubblicazione.

Se gli spazi dei nomi dei tag sono stati aggiunti e mancano, accertatevi che i tag e il sito siano stati ripubblicati.

Se non vengono visualizzate risorse di abilitazione dopo aver selezionato un tag durante la visualizzazione del catalogo, accertatevi che sia presente un tag dagli spazi dei nomi del catalogo applicato alla risorsa di abilitazione.

![view-catalog](assets/viewcatalog.png)

