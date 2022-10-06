---
title: Risorse di abilitazione assegnazione tag
seo-title: Tagging Enablement Resources
description: L’assegnazione tag delle risorse di abilitazione consente di filtrare risorse e percorsi di apprendimento durante la navigazione dei membri nei cataloghi
seo-description: Tagging of enablement resources allows for filtering of resources and learning paths as members browse catalogs
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
role: Admin
exl-id: ce58c8e9-8b4a-43fb-a108-ed2ac40268c7
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Risorse di abilitazione assegnazione tag {#tagging-enablement-resources}

## Panoramica {#overview}

L’assegnazione tag delle risorse di abilitazione consente di filtrare le risorse e i percorsi di apprendimento durante la navigazione dei membri [cataloghi](functions.md#catalog-function).

In sostanza:

* [Creare uno spazio dei nomi dei tag](../../help/sites-administering/tags.md#creating-a-namespace) per ogni catalogo

   * [Impostare le autorizzazioni dei tag](../../help/sites-administering/tags.md#setting-tag-permissions)
   * Solo per i membri della comunità (comunità chiusa)

      * Consenti accesso in lettura per [gruppo membro del sito della community](users.md#publish-group-roles)
   * Per qualsiasi visitatore del sito, con accesso o anonimo (community aperta)

      * Consenti accesso in lettura per `Everyone` gruppo
   * [Pubblicare i tag](../../help/sites-administering/tags.md#publishing-tags)



* [Definire l&#39;ambito dei tag per un sito community](sites-console.md#tagging)

   * [Configurare i cataloghi esistenti nella struttura del sito](functions.md#catalog-function)

      * Può aggiungere tag all’istanza di catalogo per controllare l’elenco di tag presentati nei filtri dell’interfaccia utente.
      * Può aggiungere [pre-filtri](catalog-developer-essentials.md#pre-filters), per limitare le risorse incluse di un catalogo.

* [Pubblica il sito della community](sites-console.md#publishing-the-site)
* [Applicare tag alle risorse di abilitazione](resources.md#create-a-resource) in modo che possano essere filtrate in modo categorico
* [Pubblicare le risorse di abilitazione](resources.md#publish)

## Tag del sito community {#community-site-tags}

Quando crei o modifichi un sito community, la [Impostazione dei tag](sites-console.md#tagging) imposta l’ambito dei tag disponibili per le funzioni del sito selezionando un sottoinsieme di spazi dei nomi dei tag esistenti.

Anche se è possibile creare e aggiungere tag al sito della community in qualsiasi momento, è consigliabile progettare in anticipo una tassonomia, simile alla progettazione di un database. Vedi [Utilizzo dei tag](../../help/sites-authoring/tags.md).

In seguito, quando si aggiungono tag a un sito community esistente, è necessario salvare la modifica prima di poter aggiungere il nuovo tag a una funzione catalogo nella struttura del sito.

Per un sito della community, dopo la pubblicazione del sito e la pubblicazione dei tag, è necessario consentire l&#39;accesso in lettura ai membri della community. Vedi [Impostazione delle autorizzazioni dei tag](../../help/sites-administering/tags.md#setting-tag-permissions).

Di seguito è illustrato come viene visualizzato in CRXDE quando un amministratore applica le autorizzazioni di lettura a `/etc/tags/ski-catalog` per il gruppo `Community Enable Members`.

![site-tags](assets/site-tags.png)

## Spazi dei nomi dei tag del catalogo {#catalog-tag-namespaces}

La funzione catalogo utilizza i tag per definirsi. Durante la configurazione della funzione di catalogo in un sito community, il set di namespace tag tra cui scegliere viene definito dall&#39;ambito dei namespace dei tag impostati per il sito community.

La funzione Catalogo include un’impostazione di tag che definisce i tag elencati nell’interfaccia utente del filtro per il catalogo. L&#39;impostazione &quot;Tutti i namespace&quot; fa riferimento all&#39;ambito dei namespace dei tag selezionati per il sito community.

![catalog-namespace](assets/catalog-namespace.png)

## Applicazione dei tag alle risorse di abilitazione {#applying-tags-to-enablement-resources}

Le risorse di abilitazione e i percorsi di apprendimento verranno visualizzati in tutto il catalogo quando `Show in Catalog` è controllata. L’aggiunta di tag alle risorse e ai percorsi di apprendimento consentirà di prefiltrare in cataloghi specifici e di filtrare nell’interfaccia utente del catalogo.

È possibile limitare le risorse di abilitazione e i percorsi di apprendimento per cataloghi specifici creando [pre-filtri](catalog-developer-essentials.md#pre-filters).

L’interfaccia utente del catalogo consente ai visitatori di applicare un filtro tag all’elenco delle risorse e dei percorsi di apprendimento visualizzati nel catalogo.

L’amministratore che applica i tag alle risorse di abilitazione deve conoscere i namespace dei tag associati ai cataloghi e la tassonomia per selezionare un tag secondario per una classificazione più dettagliata.

Ad esempio, se un `ski-catalog` Lo spazio dei nomi è stato creato e impostato su un catalogo denominato `Ski Catalog`, potrebbe avere due tag figlio: `lesson-1` e `lesson-2`.

Pertanto, qualsiasi risorsa di abilitazione taggata con uno dei seguenti tag:

* catalogo sci:lezione-1
* catalogo sci:lezione-2

apparirà in `Ski Catalog` dopo la pubblicazione della risorsa di abilitazione.

![basic-info](assets/applytags-basicinfo.png)

## Visualizzazione del catalogo in Pubblica {#viewing-catalog-on-publish}

Una volta che tutto è stato configurato dall’ambiente di authoring e pubblicato, l’esperienza nell’utilizzo del catalogo per trovare le risorse di abilitazione può essere vissuta nell’ambiente di pubblicazione.

Se nell’elenco a discesa non vengono visualizzati namespace per tag, verifica che le autorizzazioni siano state impostate correttamente nell’ambiente di pubblicazione.

Se sono stati aggiunti e mancanti spazi dei nomi dei tag, assicurati che i tag e il sito siano stati ripubblicati.

Se non vengono visualizzate risorse di abilitazione dopo aver selezionato un tag durante la visualizzazione del catalogo, accertati che alla risorsa di abilitazione sia applicato un tag dai namespace del catalogo.

![catalogo](assets/viewcatalog.png)
