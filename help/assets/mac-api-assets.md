---
title: API HTTP [!DNL Assets].
description: Creazione, lettura, aggiornamento, eliminazione, gestione di risorse digitali tramite l'API HTTP in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: add8be813ce377384ee4d90600f54a1455a1ab0d
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 1%

---


# [!DNL Assets] API HTTP {#assets-http-api}

## Panoramica {#overview}

L&#39;API [!DNL Assets] HTTP consente di creare-leggere-aggiornare-eliminare (CRUD) le operazioni sulle risorse digitali, inclusi i metadati, sulle rappresentazioni e sui commenti, nonché il contenuto strutturato utilizzando i frammenti di [!DNL Experience Manager] contenuto. È esposto in `/api/assets` e viene implementato come REST API. Include [il supporto per i frammenti](/help/assets/assets-api-content-fragments.md)di contenuto.

Per accedere all&#39;API:

1. Aprite il documento del servizio API in `https://[hostname]:[port]/api.json`.
1. Seguite il collegamento [!DNL Assets] del servizio `https://[hostname]:[server]/api/assets.json`.

La risposta API è un file JSON per alcuni tipi MIME e un codice di risposta per tutti i tipi MIME. La risposta JSON è facoltativa e potrebbe non essere disponibile, ad esempio per i file PDF. Per ulteriori analisi o azioni, fai affidamento sul codice di risposta.

Dopo la [!UICONTROL disattivazione], una risorsa e le relative rappresentazioni non sono disponibili tramite l&#39;interfaccia [!DNL Assets] Web e l&#39;API HTTP. L&#39;API restituisce un messaggio di errore 404 se l&#39;ora [!UICONTROL di] attivazione è futura o [!UICONTROL Ora] di disattivazione è passata.

>[!CAUTION]
>
>[L&#39;API HTTP aggiorna le proprietà](#update-asset-metadata) dei metadati nello `jcr` spazio dei nomi. Tuttavia, l&#39;interfaccia utente del Experience Manager  aggiorna le proprietà dei metadati nello `dc` spazio dei nomi.

## Frammenti di contenuto {#content-fragments}

Un frammento [di](/help/assets/content-fragments/content-fragments.md) contenuto è un tipo speciale di risorsa. Può essere utilizzato per accedere a dati strutturati, come testi, numeri, date, ecc. Poiché le `standard` risorse presentano diverse differenze (ad esempio immagini o documenti), per la gestione dei frammenti di contenuto si applicano alcune regole aggiuntive.

Per ulteriori informazioni, consulta Supporto per i frammenti di [contenuto nell’API](/help/assets/assets-api-content-fragments.md)HTTP  Experience Manager Assets.

## Dati, modello {#data-model}

L&#39;API [!DNL Assets] HTTP espone due elementi principali, cartelle e risorse (per le risorse standard).

Inoltre, espone elementi più dettagliati per i modelli di dati personalizzati che descrivono il contenuto strutturato nei frammenti di contenuto. Per ulteriori informazioni, consulta Modelli [di dati per frammenti di](/help/assets/assets-api-content-fragments.md#content-fragments) contenuto.

### Cartelle {#folders}

Le cartelle sono come directory nei file system tradizionali. Sono contenitori per altre cartelle o asserzioni. Le cartelle hanno i seguenti componenti:

**Entità**: Le entità di una cartella sono gli elementi secondari, che possono essere cartelle e risorse.

**Proprietà**:

* `name` è il nome della cartella. Equivale all’ultimo segmento nel percorso dell’URL senza estensione.
* `title` è un titolo facoltativo della cartella che può essere visualizzato al posto del nome.

>[!NOTE]
>
>Alcune proprietà della cartella o della risorsa vengono mappate con un prefisso diverso. Il `jcr` prefisso `jcr:title`, `jcr:description`, e `jcr:language` viene sostituito con `dc` prefisso. Quindi nel JSON restituito `dc:title` e `dc:description` contengono rispettivamente i valori di `jcr:title` e `jcr:description`.

**Le cartelle dei collegamenti** presentano tre collegamenti:

* `self`: Collegarsi a se stesso.
* `parent`: Collegare la cartella principale.
* `thumbnail`: (Facoltativo) collegamento alla miniatura di una cartella.

### Assets {#assets}

In  Experience Manager una risorsa contiene i seguenti elementi:

* Proprietà e metadati della risorsa.
* Rappresentazioni multiple, ad esempio la rappresentazione originale (che è la risorsa caricata originariamente), una miniatura e varie altre rappresentazioni. Rappresentazioni aggiuntive possono essere immagini di dimensioni diverse, codifiche video diverse o pagine estratte da PDF o [!DNL Adobe InDesign] file.
* Commenti facoltativi.

Per informazioni sugli elementi nei frammenti di contenuto, consulta Supporto frammenti di [contenuto in  API](/help/assets/assets-api-content-fragments.md#content-fragments)HTTP delle risorse di Experience Manager.

In [!DNL Experience Manager] una cartella sono presenti i seguenti componenti:

* Entità: Gli elementi secondari delle risorse sono le relative rappresentazioni.
* Proprietà.
* Collegamenti.

L&#39;API [!DNL Assets] HTTP include le seguenti funzionalità:

* [Recuperate un elenco](#retrieve-a-folder-listing)di cartelle.
* [Creare una cartella](#create-a-folder).
* [Creare una risorsa](#create-an-asset).
* [Aggiorna binario](#update-asset-binary)risorse.
* [Aggiornare i metadati](#update-asset-metadata)delle risorse.
* [Creare una rappresentazione](#create-an-asset-rendition)di una risorsa.
* [Aggiornare una rappresentazione](#update-an-asset-rendition)di una risorsa.
* [Create un commento](#create-an-asset-comment)sulla risorsa.
* [Copiate una cartella o una risorsa](#copy-a-folder-or-asset).
* [Spostate una cartella o una risorsa](#move-a-folder-or-asset).
* [Eliminate una cartella, una risorsa o una rappresentazione](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Per semplificare la leggibilità, gli esempi seguenti omettono la notazione cURL completa. In realtà la notazione è correlata con [Resty](https://github.com/micha/resty) che è un wrapper di script per `cURL`.

**Prerequisiti**

* Accesso `https://[aem_server]:[port]/system/console/configMgr`.
* Andate a **[!UICONTROL Adobe Filtro]** CSRF Granite.
* Accertatevi che la proprietà **[!UICONTROL Filter Methods]** includa: `POST`, `PUT`, `DELETE`.

## Recuperare un elenco di cartelle {#retrieve-a-folder-listing}

Recupera una rappresentazione Siren di una cartella esistente e delle relative entità figlie (sottocartelle o risorse).

**Richiesta**: `GET /api/assets/myFolder.json`

**Codici** di risposta: I codici di risposta sono:

* 200 - Ok - successo.
* 404 - NON TROVATO - la cartella non esiste o non è accessibile.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

**Risposta**: La classe dell&#39;entità restituita è una risorsa o una cartella. Le proprietà delle entità contenute sono un sottoinsieme dell&#39;intero insieme di proprietà di ciascuna entità. Per ottenere una rappresentazione completa dell&#39;entità, i clienti devono recuperare il contenuto dell&#39;URL indicato dal collegamento con un `rel` di `self`.

## Crea una cartella . {#create-a-folder}

Crea un nuovo `sling`: `OrderedFolder` nel percorso specificato. Se `*` viene fornito un nome di nodo al posto del nome di un nodo, il servlet utilizza il nome del parametro come nome del nodo. Accettato come dati della richiesta è una rappresentazione Siren della nuova cartella o un set di coppie nome-valore, codificate come `application/www-form-urlencoded` o `multipart`/ `form`- `data`, utile per creare una cartella direttamente da un modulo HTML. Inoltre, le proprietà della cartella possono essere specificate come parametri di query URL.

Una chiamata API non riesce con un codice di `500` risposta se il nodo padre del percorso fornito non esiste. Una chiamata restituisce un codice di risposta `409` se la cartella esiste già.

**Parametri**: `name` è il nome della cartella.

**Richiesta**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - sulla creazione di successo.
* 409 - CONFLICT - se la cartella esiste già.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Creare una risorsa {#create-an-asset}

Posizionate il file fornito nel percorso specificato per creare una risorsa nell’archivio DAM. Se `*` viene fornito un nome di nodo al posto del nome di un nodo, il servlet utilizza il nome del parametro o il nome del file come nome del nodo.

**Parametri**: I parametri sono `name` per il nome della risorsa e `file` per il riferimento al file.

**Richiesta**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se la risorsa è stata creata con successo.
* 409 - CONFLITTO - se il bene esiste già.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Aggiornare un binario di una risorsa {#update-asset-binary}

Aggiorna il binario di una risorsa (rappresentazione con nome originale). Un aggiornamento attiva il flusso di lavoro di elaborazione delle risorse predefinito da eseguire, se configurato.

**Richiesta**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - se la risorsa è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o a cui non è stato possibile accedere all&#39;URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Aggiornare i metadati delle risorse {#update-asset-metadata}

Aggiorna le proprietà dei metadati della risorsa. Se aggiornate una qualsiasi proprietà nello `dc:` spazio dei nomi, l&#39;API aggiorna la stessa proprietà nello `jcr` spazio dei nomi. L&#39;API non sincronizza le proprietà sotto i due spazi dei nomi.

**Richiesta**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - se la risorsa è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o a cui non è stato possibile accedere all&#39;URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

### Sincronizzare l&#39;aggiornamento dei metadati tra `dc` `jcr` e lo spazio dei nomi {#sync-metadata-between-namespaces}

Il metodo API aggiorna le proprietà dei metadati nello `jcr` spazio dei nomi. Gli aggiornamenti effettuati utilizzando l&#39;interfaccia touch modificano le proprietà dei metadati nello `dc` spazio dei nomi. Per sincronizzare i valori dei metadati tra `dc` e lo `jcr` spazio dei nomi, potete creare un flusso di lavoro e configurare  Experience Manager in modo da eseguire il flusso di lavoro dopo la modifica della risorsa. Utilizzate uno script ECMA per sincronizzare le proprietà di metadati richieste. Lo script di esempio seguente sincronizza la stringa del titolo tra `dc:title` e `jcr:title`.

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

Create una nuova rappresentazione di risorsa per una risorsa. Se il nome del parametro della richiesta non viene fornito, il nome del file viene utilizzato come nome di rappresentazione.

**Parametri**: I parametri sono `name` per il nome della rappresentazione e `file` come riferimento del file.

**Richiesta**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se la rappresentazione è stata creata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o a cui non è stato possibile accedere all&#39;URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Aggiornare una rappresentazione di una risorsa {#update-an-asset-rendition}

Gli aggiornamenti sostituiscono rispettivamente una rappresentazione di risorsa con i nuovi dati binari.

**Richiesta**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - se la rappresentazione è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o a cui non è stato possibile accedere all&#39;URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Aggiungere un commento a una risorsa {#create-an-asset-comment}

Crea un nuovo commento sulla risorsa.

**Parametri**: I parametri sono `message` per il corpo del messaggio del commento e `annotationData` per i dati di annotazione in formato JSON.

**Richiesta**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se il commento è stato creato correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o a cui non è stato possibile accedere all&#39;URI fornito.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Copiare una cartella o una risorsa {#copy-a-folder-or-asset}

Copia una cartella o una risorsa disponibile nel percorso fornito in una nuova destinazione.

**Richiedi intestazioni**: I parametri sono:

* `X-Destination` - un nuovo URI di destinazione nell&#39;ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` - `infinity` o `0`. Utilizzando viene copiata `0` solo la risorsa e le relative proprietà e non i relativi elementi secondari.
* `X-Overwrite` - Consente `F` di evitare la sovrascrittura di una risorsa nella destinazione esistente.

**Richiesta**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NESSUN CONTENUTO - se la cartella o la risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un&#39;intestazione di richiesta.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Spostare una cartella o una risorsa {#move-a-folder-or-asset}

Sposta una cartella o una risorsa nel percorso specificato in una nuova destinazione.

**Richiedi intestazioni**: I parametri sono:

* `X-Destination` - un nuovo URI di destinazione nell&#39;ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` - `infinity` o `0`. Utilizzando viene copiata `0` solo la risorsa e le relative proprietà e non i relativi elementi secondari.
* `X-Overwrite` - Utilizzare `T` per forzare l&#39;eliminazione di una risorsa esistente o `F` per impedire la sovrascrittura di una risorsa esistente.

**Richiesta**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

Non usate `/content/dam` nell’URL. Un comando di esempio per spostare le risorse e sovrascrivere quelle esistenti è:

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: http://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**Codici** di risposta: I codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NESSUN CONTENUTO - se la cartella o la risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un&#39;intestazione di richiesta.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Eliminare una cartella, una risorsa o una rappresentazione {#delete-a-folder-asset-or-rendition}

Elimina una risorsa (-tree) nel percorso specificato.

**Richiesta**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Codici** di risposta: I codici di risposta sono:

* 200 - OK - Se la cartella è stata eliminata correttamente.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE SERVER INTERNO - se qualcos&#39;altro va storto.

## Suggerimenti e limitazioni {#tips-best-practices-limitations}

* [L&#39;API HTTP aggiorna le proprietà](#update-asset-metadata) dei metadati nello `jcr` spazio dei nomi. Tuttavia, l&#39;interfaccia utente del Experience Manager  aggiorna le proprietà dei metadati nello `dc` spazio dei nomi.

* L&#39;API della risorsa non restituisce i metadati completi. Nell&#39;API gli spazi dei nomi sono codificati e vengono restituiti solo questi. Se avete bisogno di metadati interi, consultate il percorso della risorsa `/jcr_content/metadata.json`.
