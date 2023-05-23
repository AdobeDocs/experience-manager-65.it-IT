---
title: "[!DNL Assets] API HTTP."
description: Creare, leggere, aggiornare, eliminare e gestire le risorse digitali tramite API HTTP in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer
feature: APIs,Assets HTTP API,Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 1%

---

# [!DNL Assets] API HTTP {#assets-http-api}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=en) |
| AEM 6.5 | Questo articolo |

## Panoramica {#overview}

Il [!DNL Assets] API HTTP consente di eseguire operazioni CRUD (create-read-update-delete) su risorse digitali, inclusi metadati, rappresentazioni e commenti, insieme a contenuti strutturati tramite [!DNL Experience Manager] Frammenti di contenuto. Viene esposto in corrispondenza di `/api/assets` e viene implementato come API REST. Include [Supporto per frammenti di contenuto](/help/assets/assets-api-content-fragments.md).

Per accedere all’API:

1. Apri il documento del servizio API in `https://[hostname]:[port]/api.json`.
1. Segui le [!DNL Assets] collegamento del servizio che porta a `https://[hostname]:[server]/api/assets.json`.

La risposta API è un file JSON per alcuni tipi MIME e un codice di risposta per tutti i tipi MIME. La risposta JSON è facoltativa e potrebbe non essere disponibile, ad esempio per i file PDF. Utilizza il codice di risposta per ulteriori analisi o azioni.

Dopo il [!UICONTROL Ora di disattivazione], una risorsa e le relative rappresentazioni non sono disponibili tramite [!DNL Assets] tramite l’interfaccia web e l’API HTTP. L’API restituisce il messaggio di errore 404 se [!UICONTROL Ora di attivazione] è nel futuro o [!UICONTROL Ora di disattivazione] è nel passato.

>[!CAUTION]
>
>[API HTTP aggiorna le proprietà dei metadati](#update-asset-metadata) nel `jcr` spazio dei nomi. Tuttavia, l’interfaccia utente di Experience Manager aggiorna le proprietà dei metadati nel `dc` spazio dei nomi.

## Frammenti di contenuto {#content-fragments}

A [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Può essere utilizzato per accedere a dati strutturati, tra cui testi, numeri, date. Poiché esistono diverse differenze `standard` risorse (come immagini o documenti), si applicano alcune regole aggiuntive alla gestione dei frammenti di contenuto.

Per ulteriori informazioni, consulta [Supporto per frammenti di contenuto nell’API HTTP di Experience Manager Assets](/help/assets/assets-api-content-fragments.md).

## Modello dati {#data-model}

Il [!DNL Assets] L’API HTTP espone due elementi principali, cartelle e risorse (per le risorse standard).

Inoltre, espone elementi più dettagliati per i modelli di dati personalizzati che descrivono i contenuti strutturati nei frammenti di contenuto. Consulta [Modelli dati per frammenti di contenuto](/help/assets/assets-api-content-fragments.md#content-fragments) per ulteriori informazioni.

### Cartelle {#folders}

Le cartelle sono simili alle directory dei file system tradizionali. Sono contenitori per altre cartelle o asserzioni. Le cartelle hanno i seguenti componenti:

**Entità**: le entità di una cartella sono i relativi elementi secondari, che possono essere cartelle e risorse.

**Proprietà**:

* `name` è il nome della cartella. È lo stesso dell’ultimo segmento nel percorso URL senza estensione.
* `title` è un titolo facoltativo della cartella che può essere visualizzato al posto del nome.

>[!NOTE]
>
>Alcune proprietà della cartella o della risorsa sono mappate a un prefisso diverso. Il `jcr` prefisso di `jcr:title`, `jcr:description`, e `jcr:language` sono sostituiti con `dc` prefisso. Quindi nel JSON restituito, `dc:title` e `dc:description` contengono i valori di `jcr:title` e `jcr:description`, rispettivamente.

**Collegamenti** Le cartelle espongono tre collegamenti:

* `self`: collegamento a se stesso.
* `parent`: collegamento alla cartella principale.
* `thumbnail`: (facoltativo) collegamento a un’immagine di miniatura della cartella.

### Risorse {#assets}

Ad Experience Manager, una risorsa contiene i seguenti elementi:

* Proprietà e metadati della risorsa.
* Più rappresentazioni, ad esempio la rappresentazione originale (la risorsa caricata originariamente), una miniatura e varie altre rappresentazioni. Rappresentazioni aggiuntive possono essere immagini di dimensioni diverse, codifiche video diverse o pagine estratte da PDF o [!DNL Adobe InDesign] file.
* Commenti facoltativi.

Per informazioni sugli elementi nei frammenti di contenuto, consulta [Supporto dei frammenti di contenuto nell’API HTTP di Experience Manager Assets](/help/assets/assets-api-content-fragments.md#content-fragments).

In entrata [!DNL Experience Manager] una cartella contiene i seguenti componenti:

* Entità: i figli delle risorse ne sono le rappresentazioni.
* Proprietà.
* Collegamenti.

Il [!DNL Assets] L’API HTTP include le seguenti funzionalità:

* [Recuperare un elenco di cartelle](#retrieve-a-folder-listing).
* [Creare una cartella](#create-a-folder).
* [Creare una risorsa](#create-an-asset).
* [Aggiorna binario risorsa](#update-asset-binary).
* [Aggiornare i metadati delle risorse](#update-asset-metadata).
* [Creare una rappresentazione di una risorsa](#create-an-asset-rendition).
* [Aggiornare il rendering di una risorsa](#update-an-asset-rendition).
* [Creare un commento della risorsa](#create-an-asset-comment).
* [Copiare una cartella o una risorsa](#copy-a-folder-or-asset).
* [Spostare una cartella o una risorsa](#move-a-folder-or-asset).
* [Eliminare una cartella, una risorsa o una rappresentazione](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Per maggiore leggibilità, gli esempi seguenti omettono la notazione cURL completa. Infatti la notazione è correlata a [Riposa](https://github.com/micha/resty) che è un wrapper di script per `cURL`.

**Prerequisiti**

* Accesso `https://[aem_server]:[port]/system/console/configMgr`.
* Accedi a **[!UICONTROL Filtro CSRF Adobe Granite]**.
* Assicurati che la proprietà **[!UICONTROL Metodi di filtro]** include: `POST`, `PUT`, `DELETE`.

## Recuperare un elenco di cartelle {#retrieve-a-folder-listing}

Recupera una rappresentazione Siren di una cartella esistente e delle relative entità secondarie (sottocartelle o risorse).

**Richiesta**: `GET /api/assets/myFolder.json`

**Codici di risposta**: i codici di risposta sono:

* 200 - OK - operazione riuscita.
* 404 - NON TROVATO - la cartella non esiste o non è accessibile.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

**Risposta**: la classe dell’entità restituita è una risorsa o una cartella. Le proprietà delle entità contenute sono un sottoinsieme dell&#39;insieme completo di proprietà di ciascuna entità. Per ottenere una rappresentazione completa dell’entità, i clienti devono recuperare il contenuto dell’URL a cui fa riferimento il collegamento con un `rel` di `self`.

## Crea una cartella . {#create-a-folder}

Crea un nuovo `sling`: `OrderedFolder` nel percorso specificato. Se un `*` viene fornito al posto del nome di un nodo, il servlet utilizza il nome del parametro come nome di nodo. Accettati come dati della richiesta è una rappresentazione Siren della nuova cartella o un set di coppie nome-valore, codificate come `application/www-form-urlencoded` o `multipart`/ `form`- `data`, utile per creare una cartella direttamente da un modulo HTML. Inoltre, è possibile specificare le proprietà della cartella come parametri di query URL.

Una chiamata API non riesce e viene visualizzato un messaggio `500` codice di risposta se il nodo principale del percorso specificato non esiste. Una chiamata restituisce un codice di risposta `409` se la cartella esiste già.

**Parametri**: `name` è il nome della cartella.

**Richiesta**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**Codici di risposta**: i codici di risposta sono:

* 201 - CREATO - su creazione riuscita.
* 409 - CONFLITTO - se la cartella esiste già.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Creare una risorsa {#create-an-asset}

Posiziona il file fornito nel percorso fornito per creare una risorsa nell’archivio DAM. Se un `*` viene fornito al posto del nome di un nodo, il servlet utilizza il nome del parametro o il nome del file come nome del nodo.

**Parametri**: i parametri sono `name` per il nome della risorsa e `file` come riferimento del file.

**Richiesta**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**Codici di risposta**: i codici di risposta sono:

* 201 - CREATO - se la risorsa è stata creata correttamente.
* 409 - CONFLITTO - se la risorsa esiste già.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiornare un binario di risorse {#update-asset-binary}

Aggiorna il file binario di una risorsa (rappresentazione con nome originale). Un aggiornamento attiva il flusso di lavoro predefinito di elaborazione delle risorse da eseguire, se configurato.

**Richiesta**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**Codici di risposta**: i codici di risposta sono:

* 200 - OK - se la risorsa è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiornare i metadati delle risorse {#update-asset-metadata}

Aggiorna le proprietà dei metadati della risorsa. Se aggiorni una proprietà in `dc:` , l&#39;API aggiorna la stessa proprietà nella sezione `jcr` spazio dei nomi. L’API non sincronizza le proprietà nei due spazi dei nomi.

**Richiesta**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**Codici di risposta**: i codici di risposta sono:

* 200 - OK - se la risorsa è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

### Sincronizza aggiornamento metadati tra `dc` e `jcr` namespace {#sync-metadata-between-namespaces}

Il metodo API aggiorna le proprietà dei metadati nel `jcr` spazio dei nomi. Gli aggiornamenti apportati tramite l’interfaccia utente modificano le proprietà dei metadati nel `dc` spazio dei nomi. Per sincronizzare i valori dei metadati tra `dc` e `jcr` namespace, puoi creare un flusso di lavoro e configurare Experience Manager per eseguirlo in seguito alla modifica della risorsa. Utilizza uno script ECMA per sincronizzare le proprietà dei metadati richieste. Lo script di esempio seguente sincronizza la stringa del titolo tra `dc:title` e `jcr:title`.

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## Creare una rappresentazione di una risorsa {#create-an-asset-rendition}

Crea una nuova rappresentazione della risorsa. Se non viene fornito il nome del parametro della richiesta, il nome del file viene utilizzato come nome della rappresentazione.

**Parametri**: i parametri sono `name` per il nome della rappresentazione e `file` come riferimento di file.

**Richiesta**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Codici di risposta**: i codici di risposta sono:

* 201 - CREATO - se la rappresentazione è stata creata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiornare il rendering di una risorsa {#update-an-asset-rendition}

Gli aggiornamenti sostituiscono rispettivamente una rappresentazione di una risorsa con i nuovi dati binari.

**Richiesta**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Codici di risposta**: i codici di risposta sono:

* 200 - OK - se la rappresentazione è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiungere un commento a una risorsa {#create-an-asset-comment}

Crea un nuovo commento per la risorsa.

**Parametri**: i parametri sono `message` per il corpo del messaggio del commento e `annotationData` per i dati di Annotation in formato JSON.

**Richiesta**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Codici di risposta**: i codici di risposta sono:

* 201 - CREATO - se il commento è stato creato correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Copiare una cartella o una risorsa {#copy-a-folder-or-asset}

Copia in una nuova destinazione una cartella o una risorsa disponibile nel percorso specificato.

**Intestazioni richiesta**: i parametri sono:

* `X-Destination` : nuovo URI di destinazione nell’ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` - oppure `infinity` o `0`. Utilizzo di `0` copia solo la risorsa e le relative proprietà e non i relativi elementi figlio.
* `X-Overwrite` - Utilizzo `F` per evitare la sovrascrittura di una risorsa nella destinazione esistente.

**Richiesta**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Codici di risposta**: i codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NESSUN CONTENUTO - se la cartella/risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un’intestazione di richiesta.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Spostare una cartella o una risorsa {#move-a-folder-or-asset}

Sposta una cartella o una risorsa nel percorso specificato in una nuova destinazione.

**Intestazioni richiesta**: i parametri sono:

* `X-Destination` : nuovo URI di destinazione nell’ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` - oppure `infinity` o `0`. Utilizzo di `0` copia solo la risorsa e le relative proprietà e non i relativi elementi figlio.
* `X-Overwrite` - Utilizzare `T` per forzare l’eliminazione di una risorsa esistente o `F` per evitare la sovrascrittura di una risorsa esistente.

**Richiesta**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

Non usi `/content/dam` nell’URL. Un comando di esempio per spostare le risorse e sovrascrivere quelle esistenti è:

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**Codici di risposta**: i codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NESSUN CONTENUTO - se la cartella/risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un’intestazione di richiesta.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Eliminare una cartella, una risorsa o una rappresentazione {#delete-a-folder-asset-or-rendition}

Elimina una risorsa (-tree) nel percorso specificato.

**Richiesta**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Codici di risposta**: i codici di risposta sono:

* 200 - OK - se la cartella è stata eliminata correttamente.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Suggerimenti e limitazioni {#tips-best-practices-limitations}

* [API HTTP aggiorna le proprietà dei metadati](#update-asset-metadata) nel `jcr` spazio dei nomi. Tuttavia, l’interfaccia utente di Experience Manager aggiorna le proprietà dei metadati nel `dc` spazio dei nomi.

* L’API HTTP delle risorse non restituisce i metadati completi. Gli spazi dei nomi sono hardcoded e vengono restituiti solo tali spazi dei nomi. Per i metadati completi, vedi il percorso della risorsa `/jcr_content/metadata.json`.
