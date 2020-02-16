---
title: Configurazione delle posizioni per Forms
seo-title: Configurazione delle posizioni per Forms
description: Scoprite come configurare il percorso per Forms.
seo-description: Scoprite come configurare il percorso per Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurazione delle posizioni per Forms {#configuring-locations-for-forms}

È possibile specificare l&#39;URL, l&#39;URI e i percorsi dei file di attributi come la radice Web, la posizione dei moduli da recuperare, il file PDF di livello inferiore utilizzato nelle trasformazioni PDFForm e il percorso della cache.

1. Nella console di amministrazione, fare clic su Servizi > Moduli.
1. In Posizioni specificare le opzioni appropriate. Le opzioni sono descritte di seguito.
1. Fate clic su Salva.

## Impostazioni posizioni {#locations-settings}

**** URL di base: L&#39;URL di base in cui si trovano le risorse del modulo, ad esempio immagini e script. Questo valore è richiesto per le trasformazioni HTML che includono riferimenti HREF a dipendenze esterne, ad esempio immagini o script. Uno di questi script è xfasubset.js, che è richiesto ai moduli HTML per eseguire funzioni di intelligence XFA. Questo valore deve essere l&#39;equivalente HTTP dell&#39;URI radice del contenuto.

***Nota **: L&#39;URL di base supporta solo protocolli HTTP o repository. Non supporta protocolli come file:///. Se è necessario accedere a una risorsa come un CSS personalizzato o un URI di firma digitale, utilizzare il valore del parametro API appropriato per specificare la posizione assoluta.*

Quando un percorso di dipendenza è assoluto, il valore dell&#39;URL di base viene ignorato. In caso contrario, il percorso di dipendenza viene combinato con l&#39;URL di base.

Il valore predefinito è una stringa vuota.

L&#39;esempio seguente fa riferimento allo stesso contenuto (utilizzando l&#39;URI della directory principale contenuto e l&#39;URL di base):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**** URI radice Web FS: L&#39;URL dell&#39;applicazione Web Forms. È possibile lasciare vuota questa casella se l&#39;applicazione Web Forms e l&#39;applicazione client vengono distribuiti sullo stesso server applicazione; verrà utilizzato l&#39;URL principale Web dell&#39;API Forms.

Se l&#39;applicazione Web Forms e l&#39;applicazione client non sono distribuiti nello stesso server applicazione, fornire l&#39;URL per l&#39;applicazione Web Forms in questa casella, come illustrato nell&#39;esempio seguente:

`https://<host name>:<port>/FormServer`

Dove `host name`e `port` sono il nome del server e il numero della porta del server che ospita l&#39;applicazione Web Forms.

Il valore predefinito è una stringa vuota.

**** URI radice Web: Radice Web dell&#39;applicazione. Questo valore viene combinato con il parametro sTargetURL (quando sTargetURL viene fornito come relativo), specificato tramite l’SDK dei moduli AEM, per creare un URL assoluto per accedere al contenuto Web specifico dell’applicazione.

Il valore predefinito è una stringa vuota.

**** URI radice contenuto: URI o posizione assoluta da cui vengono recuperati i moduli. Questo valore è combinato con il parametro sFormQuery, specificato tramite l&#39;API, per costruire il percorso assoluto del modulo che viene recuperato. Questo valore può fare riferimento a una directory o a una posizione Web accessibile tramite HTTP.

Il valore predefinito è una stringa vuota.

**** URI di configurazione XCI: Posizione relativa o assoluta in cui viene trovato il file XCI utilizzato per il rendering. Per un valore relativo, si presume che il file XCI risieda nel file EAR dei moduli AEM distribuibile.

Il valore predefinito è `com/adobe/formServer/PA/pa.xci`.

**** URI mappa font: Posizione relativa o assoluta del file di mappatura dei font. Per un valore relativo, si presume che il file risieda nel file EAR dei moduli AEM distribuibile.

Il file di mappatura dei font viene utilizzato per creare mappature dei font personalizzate per le trasformazioni HTML nei moduli, consentendo di specificare quale font verrà sostituito quando un font non sarà disponibile nel computer client.

Il valore predefinito è `com/adobe/formServer/client-font-map.properties`.

La voce seguente è un esempio di una voce nel file di mappatura dei font:

`Arial=Arial,Helvetica,sans-serif`

**** File PDF seed: Il file PDF iniziale utilizzato in una trasformazione PDFForm per ottimizzare la distribuzione. Il file PDF di livello inferiore specifica un file PDF personalizzato (contenente solo il flusso XFA, l&#39;immagine e le risorse di font) che viene aggiunto alla struttura del modulo e ai dati. Il rendering del modulo viene eseguito da Acrobat 7 o versione successiva e viene applicato alla trasformazione PDFForm.

Il valore predefinito è una stringa vuota.

**** Posizione cache: Specifica il percorso della cache del disco di Forms. Quando modificate questa impostazione, tutte le informazioni cache esistenti provenienti dalla posizione corrente vengono reimpostate e viene creata una nuova cache nella nuova posizione. Selezionare una delle seguenti opzioni:

**** Posizione predefinita: Questa è la selezione predefinita. Quando questa opzione è selezionata, la cache viene creata in una posizione che dipende dal server applicazione in uso:

* **** JBoss: Home [JBoss]\server\[tipo di installazione]\svcdata\FormServer\Cache
* **** WebLogic: Home [WebLogic]\user_projects\domains\[nome dominio moduli aem]\adobe\[nome server moduli]\FormServer\Cache
* **** WebSphere: Home [IBM]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**** Directory temporanea LC: La cache viene creata in una sottodirectory della directory temporanea dei moduli AEM, specificata nella console di amministrazione in Impostazioni > Impostazioni sistema di base > Configurazioni > Posizione della directory temporanea. La sottodirectory è denominata adobeform_[servername].

>[!NOTE]
>
>Se si utilizza un&#39;utilità di pulizia temporanea, tenere presente che mentre si eliminano queste directory non influisce sulla funzionalità, può avere un impatto significativo sulle prestazioni per un breve periodo di tempo fino alla creazione della nuova cache. Per evitare questo problema, non eliminate queste directory durante la cancellazione della directory temporanea dei moduli AEM.

