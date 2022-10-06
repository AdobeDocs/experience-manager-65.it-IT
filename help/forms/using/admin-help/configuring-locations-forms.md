---
title: Configurazione delle posizioni per Forms
seo-title: Configuring locations for Forms
description: Scopri come configurare la posizione per Forms.
seo-description: Learn how to configure location for Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# Configurazione delle posizioni per Forms {#configuring-locations-for-forms}

È possibile specificare l’URL, l’URI e le posizioni dei file di attributi quali la radice web, la posizione dei moduli da recuperare, il file PDF seed utilizzato nelle trasformazioni PDFForm e la posizione della cache.

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Posizioni specificare le opzioni appropriate. Le opzioni sono descritte di seguito.
1. Fai clic su Salva.

## Impostazioni delle posizioni {#locations-settings}

**URL di base:** URL di base in cui si trovano le risorse del modulo, ad esempio immagini e script. Questo valore è necessario per le trasformazioni HTML che includono riferimenti HREF a dipendenze esterne, ad esempio immagini o script. Uno di questi script è xfasubset.js , necessario per l’esecuzione di funzioni di intelligenza XFA da parte dei moduli HTML. Questo valore deve essere l’equivalente HTTP dell’URI della directory principale dei contenuti.

>[!NOTE]
>
>L&#39;URL di base supporta solo protocolli HTTP o archivio. Non supporta protocolli come file:///. Se devi accedere a una risorsa, ad esempio un URI CSS o firma digitale personalizzato, utilizza il valore del parametro API appropriato per specificare la posizione assoluta.

Quando un percorso di dipendenza è assoluto, il valore dell&#39;URL di base viene ignorato. In caso contrario, il percorso di dipendenza viene combinato con l&#39;URL di base.

Il valore predefinito è una stringa vuota.

L’esempio seguente fa riferimento allo stesso contenuto (utilizzando l’URI di directory principale dei contenuti e l’URL di base):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI radice Web FS:** URL dell&#39;applicazione Web Forms. È possibile lasciare vuota questa casella se l&#39;applicazione Web Forms e l&#39;applicazione client vengono distribuiti sullo stesso server applicazioni; verrà utilizzato l’URL web root dell’API Forms.

Se l&#39;applicazione Web Forms e l&#39;applicazione client non vengono distribuiti sullo stesso server applicazioni, fornire l&#39;URL per l&#39;applicazione Web Forms in questa casella, come illustrato in questo esempio:

`https://<host name>:<port>/FormServer`

Dove `host name`e `port` sono il nome server e il numero di porta del server che ospita l&#39;applicazione Web Forms.

Il valore predefinito è una stringa vuota.

**URI radice web:** La radice Web dell&#39;applicazione. Questo valore viene combinato con il parametro sTargetURL (quando sTargetURL è fornito come relativo), specificato tramite l’SDK per moduli di AEM, per creare un URL assoluto per accedere al contenuto web specifico per l’applicazione.

Il valore predefinito è una stringa vuota.

**URI radice contenuto:** URI o posizione assoluta da cui vengono recuperati i moduli. Questo valore viene combinato con il parametro sFormQuery, specificato tramite l&#39;API, per creare il percorso assoluto del modulo recuperato. Questo valore può fare riferimento a una directory o a una posizione Web accessibile tramite HTTP.

Il valore predefinito è una stringa vuota.

**URI di configurazione XCI:** Posizione relativa o assoluta in cui viene trovato il file XCI utilizzato per il rendering. Per un valore relativo, si presume che il file XCI risieda nel file EAR dei moduli AEM distribuibili.

Il valore predefinito è `com/adobe/formServer/PA/pa.xci`.

**URI mappa font:** Posizione relativa o assoluta del file di mappatura dei font. Per un valore relativo, si presume che questo file risieda nel file EAR dei moduli AEM distribuibili.

Il file di mappatura dei font viene utilizzato per creare mappature personalizzate dei font per le trasformazioni HTML nei moduli, consentendo quindi di specificare quale font verrà sostituito quando un font non è disponibile nel computer client.

Il valore predefinito è `com/adobe/formServer/client-font-map.properties`.

La voce seguente è un esempio di una voce nel file di mappatura dei font:

`Arial=Arial,Helvetica,sans-serif`

**File PDF di seed:** Il file PDF iniziale utilizzato in una trasformazione PDFForm per ottimizzare la consegna. Il file PDF di seed specifica un file PDF personalizzato (contenente solo risorse di flusso XFA, immagine e font) che viene aggiunto alla struttura del modulo e ai dati. Il rendering del modulo viene eseguito da Acrobat 7 o versione successiva e si applica alla trasformazione PDFForm.

Il valore predefinito è una stringa vuota.

**Posizione cache:** Specifica il percorso della cache del disco Forms. Quando modifichi questa impostazione, tutte le informazioni esistenti sulla cache dalla posizione corrente vengono reimpostate e viene creata una nuova cache nella nuova posizione. Selezionare una delle seguenti opzioni:

**Posizione predefinita:** Questa è la selezione predefinita. Quando questa opzione è selezionata, la cache viene creata in una posizione che dipende dal server dell&#39;applicazione in uso:

* **JBoss:** [Home di JBoss]\server\[tipo di installazione]\svcdata\FormServer\Cache
* **WebLogic:** [Pagina principale WebLogic]\user_projects\domains\[nome di dominio aem-forms]\adobe\[nome server forms]\FormServer\Cache
* **WebSphere:** [Pagina principale di IBM]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Directory temporanea LC:** La cache viene creata in una sottodirectory della directory temporanea dei moduli AEM, specificata nella console di amministrazione in Impostazioni > Impostazioni sistema di base > Configurazioni > Posizione della directory temporanea. La sottodirectory si chiama adobeform_[nome server].

>[!NOTE]
>
>Se si utilizza un&#39;utilità di pulizia temporanea, tenere presente che mentre l&#39;eliminazione di queste directory non influisce sulla funzionalità, può avere un impatto significativo sulle prestazioni per un breve periodo di tempo fino alla creazione della nuova cache. Per evitare questo problema, non eliminare queste directory quando si cancella la directory temporanea dei moduli AEM.
