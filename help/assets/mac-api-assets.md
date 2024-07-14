---
title: "[!DNL Assets] API HTTP."
description: Crea, leggi, aggiorna, elimina, gestisci le risorse digitali tramite API HTTP in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer
feature: Assets HTTP API,Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 1%

---

# API HTTP [!DNL Assets] {#assets-http-api}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=en) |
| AEM 6.5 | Questo articolo |

## Panoramica {#overview}

L&#39;API HTTP [!DNL Assets] consente operazioni di creazione-lettura-aggiornamento-eliminazione (CRUD) sulle risorse digitali, inclusi i metadati, sulle rappresentazioni e sui commenti, insieme a contenuti strutturati che utilizzano [!DNL Experience Manager] frammenti di contenuto. È esposto in `/api/assets` ed è implementato come API REST. Include [supporto per frammenti di contenuto](/help/assets/assets-api-content-fragments.md).

Per accedere all’API:

1. Aprire il documento del servizio API in `https://[hostname]:[port]/api.json`.
1. Segui il collegamento al servizio [!DNL Assets] che porta a `https://[hostname]:[server]/api/assets.json`.

La risposta API è un file JSON per alcuni tipi MIME e un codice di risposta per tutti i tipi MIME. La risposta JSON è facoltativa e potrebbe non essere disponibile, ad esempio, per i file PDF. Utilizza il codice di risposta per ulteriori analisi o azioni.

Dopo l&#39;[!UICONTROL Ora di disattivazione], una risorsa e le relative rappresentazioni non sono disponibili tramite l&#39;interfaccia Web [!DNL Assets] e tramite l&#39;API HTTP. L&#39;API restituisce il messaggio di errore 404 se [!UICONTROL Ora di attivazione] è nel futuro o [!UICONTROL Ora di disattivazione] è nel passato.

>[!CAUTION]
>
>[API HTTP aggiorna le proprietà dei metadati](#update-asset-metadata) nello spazio dei nomi `jcr`. Tuttavia, l&#39;interfaccia utente di Experience Manager aggiorna le proprietà dei metadati nello spazio dei nomi `dc`.

## Frammenti di contenuto {#content-fragments}

Un [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Può essere utilizzato per accedere a dati strutturati, ad esempio testi, numeri, date e così via. Poiché esistono diverse differenze rispetto alle risorse `standard` (ad esempio immagini o documenti), alla gestione dei frammenti di contenuto si applicano alcune regole aggiuntive.

Per ulteriori informazioni, vedere [Supporto per frammenti di contenuto nell&#39;API HTTP Experience Manager Assets](/help/assets/assets-api-content-fragments.md).

## Modello dati {#data-model}

L&#39;API HTTP [!DNL Assets] espone due elementi principali, cartelle e risorse (per le risorse standard).

Inoltre, espone elementi più dettagliati per i modelli di dati personalizzati che descrivono i contenuti strutturati nei frammenti di contenuto. Per ulteriori informazioni, consulta [Modelli dati per frammenti di contenuto](/help/assets/assets-api-content-fragments.md#content-fragments).

### Cartelle {#folders}

Le cartelle sono simili alle directory dei file system tradizionali. Sono contenitori per altre cartelle o asserzioni. Le cartelle hanno i seguenti componenti:

**Entità**: le entità di una cartella sono i relativi elementi secondari, che possono essere cartelle e risorse.

**Proprietà**:

* `name` è il nome della cartella. È lo stesso dell’ultimo segmento nel percorso URL senza estensione.
* `title` è un titolo facoltativo della cartella che può essere visualizzato al posto del nome.

>[!NOTE]
>
>Alcune proprietà della cartella o della risorsa sono mappate a un prefisso diverso. Il prefisso `jcr` di `jcr:title`, `jcr:description` e `jcr:language` viene sostituito con il prefisso `dc`. Pertanto, nel JSON restituito, `dc:title` e `dc:description` contengono rispettivamente i valori di `jcr:title` e `jcr:description`.

**I collegamenti** nelle cartelle espongono tre collegamenti:

* `self`: collegamento a se stesso.
* `parent`: collegamento alla cartella principale.
* `thumbnail`: (facoltativo) collegamento a un&#39;immagine di miniatura della cartella.

### Risorse {#assets}

Ad Experience Manager, una risorsa contiene i seguenti elementi:

* Proprietà e metadati della risorsa.
* Più rappresentazioni, ad esempio la rappresentazione originale (la risorsa caricata originariamente), una miniatura e varie altre rappresentazioni. Altre rappresentazioni possono essere immagini di dimensioni diverse, codifiche video diverse o pagine estratte da file PDF o [!DNL Adobe InDesign].
* Commenti facoltativi.

Per informazioni sugli elementi nei frammenti di contenuto, vedere [Supporto dei frammenti di contenuto nell&#39;API HTTP Experience Manager Assets](/help/assets/assets-api-content-fragments.md#content-fragments).

In [!DNL Experience Manager] una cartella contiene i seguenti componenti:

* Entità: i figli delle risorse ne sono le rappresentazioni.
* Proprietà.
* Collegamenti.

L&#39;API HTTP [!DNL Assets] include le seguenti funzionalità:

* [Recuperare un elenco di cartelle](#retrieve-a-folder-listing).
* [Creare una cartella](#create-a-folder).
* [Crea una risorsa](#create-an-asset).
* [Aggiorna binario risorsa](#update-asset-binary).
* [Aggiorna metadati risorsa](#update-asset-metadata).
* [Crea una rappresentazione di una risorsa](#create-an-asset-rendition).
* [Aggiorna una rappresentazione di risorsa](#update-an-asset-rendition).
* [Crea un commento risorsa](#create-an-asset-comment).
* [Copia una cartella o una risorsa](#copy-a-folder-or-asset).
* [Spostare una cartella o una risorsa](#move-a-folder-or-asset).
* [Eliminare una cartella, una risorsa o una copia trasformata](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Per maggiore leggibilità, gli esempi seguenti omettono la notazione cURL completa. La notazione è correlata a [Resty](https://github.com/micha/resty), che è un wrapper di script per `cURL`.

**Prerequisiti**

* Accedi a `https://[aem_server]:[port]/system/console/configMgr`.
* Passa a **[!UICONTROL Filtro CSRF Adobe Granite]**.
* Assicurarsi che la proprietà **[!UICONTROL Metodi filtro]** includa: `POST`, `PUT`, `DELETE`.

## Recuperare un elenco di cartelle {#retrieve-a-folder-listing}

Recupera una rappresentazione Siren di una cartella esistente e delle relative entità secondarie (sottocartelle o risorse).

**Richiesta**: `GET /api/assets/myFolder.json`

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - operazione riuscita.
* 404 - NON TROVATO - la cartella non esiste o non è accessibile.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

**Risposta**: la classe dell&#39;entità restituita è una risorsa o una cartella. Le proprietà delle entità contenute sono un sottoinsieme dell&#39;insieme completo di proprietà di ciascuna entità. Per ottenere una rappresentazione completa dell&#39;entità, i client devono recuperare il contenuto dell&#39;URL indicato dal collegamento con `rel` di `self`.

## Crea una cartella {#create-a-folder}

Crea un nuovo `sling`: `OrderedFolder` nel percorso specificato. Se viene fornito un `*` invece del nome di un nodo, il servlet utilizza il nome del parametro come nome di nodo. Accettati come dati della richiesta è una rappresentazione Siren della nuova cartella o un set di coppie nome-valore, codificate come `application/www-form-urlencoded` o `multipart`/ `form`- `data`, utili per la creazione di una cartella direttamente da un modulo HTML. Inoltre, è possibile specificare le proprietà della cartella come parametri di query URL.

Una chiamata API non riesce con un codice di risposta `500` se il nodo principale del percorso specificato non esiste. Una chiamata restituisce un codice di risposta `409` se la cartella esiste già.

**Parametri**: `name` è il nome della cartella.

**Richiesta**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**Codici di risposta**: I codici di risposta sono:

* 201 - CREATO - su creazione riuscita.
* 409 - CONFLITTO - se la cartella esiste già.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Creare una risorsa {#create-an-asset}

Posiziona il file fornito nel percorso fornito per creare una risorsa nell’archivio DAM. Se viene fornito un `*` invece del nome di un nodo, il servlet utilizza il nome del parametro o il nome del file come nome di nodo.

**Parametri**: parametri `name` per il nome della risorsa e `file` per il riferimento al file.

**Richiesta**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**Codici di risposta**: I codici di risposta sono:

* 201 - CREATO - se la risorsa è stata creata correttamente.
* 409 - CONFLITTO - se la risorsa esiste già.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiornare un binario di risorse {#update-asset-binary}

Aggiorna il file binario di una risorsa (rappresentazione con nome originale). Un aggiornamento attiva il flusso di lavoro predefinito di elaborazione delle risorse da eseguire, se configurato.

**Richiesta**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - se la risorsa è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiornare i metadati delle risorse {#update-asset-metadata}

Aggiorna le proprietà dei metadati della risorsa. Se si aggiorna una proprietà nello spazio dei nomi `dc:`, l&#39;API aggiorna la stessa proprietà nello spazio dei nomi `jcr`. L’API non sincronizza le proprietà nei due spazi dei nomi.

**Richiesta**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - se la risorsa è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

### Aggiornamento dei metadati di sincronizzazione tra `dc` e lo spazio dei nomi `jcr` {#sync-metadata-between-namespaces}

Il metodo API aggiorna le proprietà dei metadati nello spazio dei nomi `jcr`. Gli aggiornamenti apportati tramite l&#39;interfaccia utente modificano le proprietà dei metadati nello spazio dei nomi `dc`. Per sincronizzare i valori dei metadati tra lo spazio dei nomi `dc` e `jcr`, è possibile creare un flusso di lavoro e configurare Experience Manager per eseguire il flusso di lavoro in seguito alla modifica della risorsa. Utilizza uno script ECMA per sincronizzare le proprietà dei metadati richieste. Lo script di esempio seguente sincronizza la stringa del titolo tra `dc:title` e `jcr:title`.

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

Creare una rappresentazione di una risorsa. Se non viene fornito il nome del parametro della richiesta, il nome del file viene utilizzato come nome della rappresentazione.

**Parametri**: i parametri sono `name` per il nome della rappresentazione e `file` come riferimento di file.

**Richiesta**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Codici di risposta**: I codici di risposta sono:

* 201 - CREATO - se la rappresentazione è stata creata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiornare il rendering di una risorsa {#update-an-asset-rendition}

Gli aggiornamenti sostituiscono rispettivamente una rappresentazione di una risorsa con i nuovi dati binari.

**Richiesta**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - se la rappresentazione è stata aggiornata correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Aggiungere un commento a una risorsa {#create-an-asset-comment}

Crea un nuovo commento per la risorsa.

**Parametri**: i parametri sono `message` per il corpo del messaggio del commento e `annotationData` per i dati di annotazione in formato JSON.

**Richiesta**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Codici di risposta**: I codici di risposta sono:

* 201 - CREATO - se il commento è stato creato correttamente.
* 404 - NON TROVATO - se la risorsa non è stata trovata o non è stato possibile accedervi all’URI specificato.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Copiare una cartella o una risorsa {#copy-a-folder-or-asset}

Copia in una nuova destinazione una cartella o una risorsa disponibile nel percorso specificato.

**Intestazioni richiesta**: i parametri sono:

* `X-Destination` - Nuovo URI di destinazione nell&#39;ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` - `infinity` o `0`. Se si utilizza `0`, verranno copiate solo la risorsa e le relative proprietà e non i relativi elementi figlio.
* `X-Overwrite` - Utilizzare `F` per impedire la sovrascrittura di una risorsa nella destinazione esistente.

**Richiesta**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Codici di risposta**: I codici di risposta sono:

* 201 - CREATO - se la cartella/risorsa è stata copiata in una destinazione non esistente.
* 204 - NESSUN CONTENUTO - se la cartella/risorsa è stata copiata in una destinazione esistente.
* 412 - PRECONDIZIONE NON RIUSCITA - se manca un’intestazione di richiesta.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Spostare una cartella o una risorsa {#move-a-folder-or-asset}

Sposta una cartella o una risorsa nel percorso specificato in una nuova destinazione.

**Intestazioni richiesta**: i parametri sono:

* `X-Destination` - Nuovo URI di destinazione nell&#39;ambito della soluzione API in cui copiare la risorsa.
* `X-Depth` - `infinity` o `0`. Se si utilizza `0`, verranno copiate solo la risorsa e le relative proprietà e non i relativi elementi figlio.
* `X-Overwrite` - Utilizzare `T` per forzare l&#39;eliminazione di una risorsa esistente oppure `F` per impedire la sovrascrittura di una risorsa esistente.

**Richiesta**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

Non utilizzare `/content/dam` nell&#39;URL. Un comando di esempio per spostare le risorse e sovrascrivere quelle esistenti è:

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**Codici di risposta**: I codici di risposta sono:

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

**Codici di risposta**: I codici di risposta sono:

* 200 - OK - se la cartella è stata eliminata correttamente.
* 412 - PRECONDIZIONE NON RIUSCITA - se non è possibile trovare o accedere alla raccolta radice.
* 500 - ERRORE INTERNO DEL SERVER - se si verificano altri errori.

## Suggerimenti e limitazioni {#tips-best-practices-limitations}

* [API HTTP aggiorna le proprietà dei metadati](#update-asset-metadata) nello spazio dei nomi `jcr`. Tuttavia, l&#39;interfaccia utente di Experience Manager aggiorna le proprietà dei metadati nello spazio dei nomi `dc`.

* L’API HTTP di Assets non restituisce i metadati completi. Gli spazi dei nomi sono hardcoded e vengono restituiti solo tali spazi dei nomi. Per i metadati completi, vedere il percorso della risorsa `/jcr_content/metadata.json`.
