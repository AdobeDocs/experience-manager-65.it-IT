---
title: Configurazione delle posizioni per Forms
description: Scopri come configurare la posizione per il modulo AEM. È possibile specificare le posizioni degli attributi dei file, la posizione del modulo, il file dei PDF di seed e la posizione della cache.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---

# Configurazione delle posizioni per Forms {#configuring-locations-for-forms}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

È possibile specificare l&#39;URL, l&#39;URI e le posizioni di file di attributi quali la directory principale del Web, la posizione dei moduli da recuperare, il file dei PDF di inizializzazione utilizzato nelle trasformazioni del modulo PDF e la posizione della cache.

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Posizioni (Locations), specificate le opzioni appropriate. Le opzioni sono descritte di seguito.
1. Fai clic su Salva.

## Impostazioni posizioni {#locations-settings}

**URL di base:** l&#39;URL di base in cui si trovano le risorse del modulo come immagini e script. Questo valore è necessario per le trasformazioni HTML che includono riferimenti HREF a dipendenze esterne, come immagini o script. Uno di questi script è xfasubset.js, necessario affinché i moduli HTML possano eseguire le funzioni di intelligence XFA. Questo valore deve essere l’equivalente HTTP dell’URI della directory principale dei contenuti.

>[!NOTE]
>
>L&#39;URL di base supporta solo i protocolli HTTP o del repository. Non supporta protocolli come file:///. Se devi accedere a una risorsa come un URI di firma digitale o CSS personalizzato, specifica la posizione assoluta utilizzando il valore del parametro API appropriato.

Quando un percorso di dipendenza è assoluto, il valore dell&#39;URL di base viene ignorato. In caso contrario, il percorso di dipendenza viene combinato con l’URL di base.

Il valore predefinito è una stringa vuota.

L’esempio seguente punta allo stesso contenuto (utilizzando l’URI della directory principale del contenuto e l’URL di base):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI radice Web FS:** URL dell&#39;applicazione Web Forms. È possibile lasciare vuota questa casella se l&#39;applicazione Web Forms e l&#39;applicazione client vengono distribuite sullo stesso server applicazioni; viene utilizzato l&#39;URL radice Web API di Forms.

Se l&#39;applicazione Web Forms e l&#39;applicazione client non sono distribuite nello stesso server applicazioni, specificare l&#39;URL per l&#39;applicazione Web Forms in questa casella, come illustrato nell&#39;esempio seguente:

`https://<host name>:<port>/FormServer`

Dove `host name` e `port` sono il nome del server e il numero di porta del server che ospita l&#39;applicazione Web Forms.

Il valore predefinito è una stringa vuota.

**Web Root URI:** Web root dell&#39;applicazione. Questo valore viene combinato con il parametro sTargetURL (quando sTargetURL viene fornito come relativo), specificato tramite l’AEM Forms SDK, per creare un URL assoluto per accedere a contenuti web specifici per l’applicazione.

Il valore predefinito è una stringa vuota.

**URI radice contenuto:** URI o posizione assoluta da cui vengono recuperati i moduli. Questo valore viene combinato con il parametro sFormQuery, specificato tramite l’API, per costruire il percorso assoluto del modulo recuperato. Questo valore può fare riferimento a una directory o a un percorso web accessibile tramite HTTP.

Il valore predefinito è una stringa vuota.

**URI configurazione XCI:** Percorso relativo o assoluto in cui è stato trovato il file XCI utilizzato per il rendering. Per un valore relativo, si presume che il file XCI risieda nel file EAR dei moduli AEM distribuibili.

Il valore predefinito è `com/adobe/formServer/PA/pa.xci`.

**URI mappa caratteri:** La posizione relativa o assoluta del file di mappatura caratteri. Per un valore relativo, si presume che questo file risieda nel file EAR dei moduli AEM distribuibili.

Il file di mappatura dei font viene utilizzato per creare mappature dei font personalizzate per le trasformazioni dei HTML nei moduli, consentendo quindi di specificare quale font verrà sostituito quando un font non è disponibile sul computer del client.

Il valore predefinito è `com/adobe/formServer/client-font-map.properties`.

La voce seguente è un esempio di una voce nel file di mappatura dei caratteri:

`Arial=Arial,Helvetica,sans-serif`

**File di seed PDF:** il file di PDF iniziale utilizzato in una trasformazione PDFForm per ottimizzare la consegna. Il file PDF di seed specifica un file PDF personalizzato (contenente solo le risorse flusso XFA, immagine e font) che viene aggiunto alla struttura e ai dati del modulo. Il modulo viene renderizzato da Acrobat 7 o versione successiva e si applica alla trasformazione PDFForm.

Il valore predefinito è una stringa vuota.

**Posizione cache:** Specifica la posizione della cache del disco di Forms. Quando si modifica questa impostazione, tutte le informazioni della cache esistenti dalla posizione corrente vengono reimpostate e viene creata una nuova cache nella nuova posizione. Selezionare una delle opzioni seguenti:

**Posizione predefinita:** Questa è la selezione predefinita. Quando questa opzione è selezionata, la cache viene creata in una posizione dipendente dal server applicazioni in uso:

* **JBoss:** [JBoss Home]\server\[tipo installazione]\svcdata\FormServer\Cache
* **WebLogic:** [Home WebLogic]\user_projects\domains\[nome dominio aem-forms]\adobe\[nome server Forms]\FormServer\Cache
* **WebSphere:** [Home di IBM]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Directory temporanea LC:** La cache viene creata in una sottodirectory della directory temporanea dei moduli AEM, specificata nella console di amministrazione in Impostazioni > Impostazioni sistema core > Configurazioni > Posizione della directory temporanea. La sottodirectory è denominata adobeform_[servername].

>[!NOTE]
>
>Se si utilizza un&#39;utilità di pulizia temporanea, anche se l&#39;eliminazione di queste directory non influisce sulla funzionalità, può avere un impatto significativo sulle prestazioni per un breve periodo di tempo fino alla creazione della nuova cache. Per evitare questo problema, non eliminare queste directory mentre si cancella la directory temporanea dei moduli AEM.
