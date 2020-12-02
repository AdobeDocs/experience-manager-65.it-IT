---
title: Modelli nell'archivio
seo-title: Modelli nell'archivio
description: 'null'
seo-description: 'null'
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 1%

---


# Modelli in Repository{#models-in-repository}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Un modello contiene un set di tipi di dati che definiscono le proprietà che verranno sottoposte a rendering dai servizi di contenuto. Un modello definisce anche le relazioni tra altri modelli al fine di applicare l&#39;integrità dei dati.

In qualità di Sviluppatore, è necessario avere familiarità con la struttura del modello nella directory archivio. Potete creare modelli ed entità personalizzati in base ai requisiti dell&#39;app.

## Creazione di tipi di modelli {#creating-model-types}

Esistono due tipi di modelli forniti dal sistema in */libs/settings/mobileapps/model-types*. Se si desidera sovrascrivere i tipi di modello di sistema, sarà necessario creare un nodo *mobileapps/model-types* nel nodo di configurazione in cui si desidera eseguire l&#39;override.

Ad esempio, se avete creato configurazioni in */conf/myconf1* e */conf/myconf2* e desiderate ignorare i tipi di modelli di sistema solo in *conf1*, create un nodo *mobileapps/model-types* nelle impostazioni di *conf1*.

Se si desidera consentire l&#39;aggiunta di tipi di dati a un modello, il tipo di modello deve avere un nodo secondario denominato &quot;scaffolding&quot; di tipo &#39;cq:Page&#39; e un tipo di risorsa di *wcm/scaffolding/components/scaffolding*.

La pagina di scaffolding deve includere anche una proprietà *dataTypesConfig* nel nodo PageContent che indica i tipi di dati che i modelli creati da questo tipo saranno consentiti.

>[!NOTE]
>
>Una **Scaffolding** è una pagina che definisce i tipi di dati che possono essere modificati da un&#39;entità basata sul modello. È inoltre possibile configurare ciascun tipo di dati per definire il modo in cui il campo verrà presentato nell&#39;interfaccia utente e il modo in cui il valore dei dati verrà mantenuto.

### Configurazione dei tipi di dati {#data-types-config}

Il nodo di configurazione dei tipi di dati contiene un elenco di elementi dei tipi di dati. Ogni elemento di tipo di dati specifica come apparirà un tipo di dati nell&#39;editor modelli e come dovrà essere persistente per il rendering finale da parte di un&#39;entità.

| **Nome proprietà** | **Descrizione** |
|---|---|
| fieldIcon | Classe dell&#39;icona CoralUI per rappresentare il tipo di dati |
| fieldPropResourceType | componente per il rendering di tutte le proprietà per la configurazione del tipo di dati |
| fieldProperties | elenco multivalore dei componenti di proprietà utilizzati quando fieldPropResourceType è *mobileapps/caas/gui/components/models/editor/dataType/field* |
| fieldResourceType | resourceType del nodo persistente per il tipo di dati (ovvero, il componente che eseguirà il rendering della proprietà nell&#39;editor di entità) |
| fieldViewResourceType | componente da utilizzare per il rendering del tipo di dati nella visualizzazione dell&#39;editor modelli (fieldResourceType verrà utilizzato se questa proprietà viene omessa) |
| fieldTitle | nome del tipo di dati che verrà visualizzato nell&#39;editor modelli |
| multiFieldResourceType | tipo di risorsa da utilizzare sul nodo persistente quando è selezionato più valori |
| renderType | indicatore di rendering per il rendering lato client |

### Sovrapposizione configurazione tipi di dati {#data-types-config-overlay}

La proprietà &#39;dataTypesConfig&#39; supporta l&#39;unione delle risorse Sling. Ciò significa che i tipi di dati utilizzati dai tipi di modelli di sistema (o anche dai tipi di modelli personalizzati) possono essere personalizzati utilizzando i nodi di sovrapposizione.

Sarà necessario creare e personalizzare una sovrapposizione di tipo */libs/settings/mobileapps/models/formbuilderconfig/datatypes*.

Ad esempio, è possibile aggiungere una sovrapposizione per il tipo di dati String per modificare fieldResourceType in un componente personalizzato.

Per ulteriori informazioni sull&#39;unione delle risorse Sling, vedere [Utilizzo dell&#39;unione delle risorse Sling in AEM](/help/sites-developing/sling-resource-merger.md).

![chlimage_1-7](assets/chlimage_1-7.png)

### Tipi di dati {#data-types}

Un tipo di dati modello è un componente modulo in grado di includere i dati da includere durante l&#39;invio di un modulo. Il componente del tipo di dati può essere complicato come desiderato. Un esempio di tipo di dati personalizzato potrebbe essere un blocco indirizzo per un particolare paese, per evitare di doverlo ricreare continuamente utilizzando i tipi di dati primitivi.

Vedere &#39;/libs/mobileapps/caas/components/form/contentreference&#39; come esempio di un tipo di dati personalizzato.

Tutti i tipi di dati di base utilizzano i componenti modulo Granite esistenti. Vedere: [https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

Qualsiasi tipo di dati personalizzato può quindi essere aggiunto a una configurazione di tipo dati da utilizzare nell&#39;editor modelli.

## Creazione di modelli {#creating-models}

È possibile iniziare a creare modelli una volta che tutti i tipi di modelli e i tipi di dati desiderati sono stati sviluppati. Gli autori utilizzeranno infine i modelli per creare entità da cui i servizi di contenuto utilizzano per eseguire il rendering dei propri dati.

La creazione di un modello consiste nel selezionare un tipo di modello consentito in base alla configurazione corrente e quindi fornire un titolo e una descrizione.

Per informazioni sulla creazione e la gestione di un modello dal dashboard, vedere [Creazione di un modello](/help/mobile/administer-mobile-apps.md) nella sezione Authoring per le app mobili.

### Proprietà di un modello {#properties-of-a-model}

La tabella seguente mostra le proprietà definite per un modello:

| **Nome proprietà** | **Descrizione** |
|---|---|
| Titolo modello | nome del modello |
| Descrizione | descrizione del modello |
| Miniatura  | miniatura del modello |
| Tipo di modello | tipo del modello (può essere una semplice stringa o un percorso di un componente effettivo) |
| Elementi figlio consentiti | percorso di un modello che può essere un elemento secondario di questo modello |
| Elementi padre consentiti | percorso di un modello che può essere un elemento padre del modello |

>[!NOTE]
>
>Le proprietà *elementi secondari* e *principali* consentiti seguono le stesse regole dei modelli di pagina. Per ulteriori informazioni, vedere [Modelli di pagina](/help/sites-developing/page-templates-static.md).
>
>In riferimento alla proprietà *Model Type*, tutti i modelli devono avere un super tipo di *mobileapps/caas/components/data/entity*, ma possono avere un sottotipo che consente di personalizzare la distribuzione dei contenuti. Assicurare che tutti i tipi di modelli siano univoci può anche aiutare i client dei servizi di contenuto a distinguere tra gli oggetti nei dati.

### Modifica di un modello {#editing-a-model}

La modifica di un modello prevede l&#39;apertura della finestra di dialogo di scaffolding associata a un modello per la modifica. In genere, lo scaffolding è un nodo secondario del modello, ma può essere posizionato all&#39;esterno del modello, se lo desidera, specificandone il percorso tramite la proprietà &#39;cq:scaffolding&#39;. Questo è utile se desiderate condividere lo stesso scaffolding tra più modelli che necessitano di proprietà diverse.

Quando si trova la pagina di scaffolding del modello, l&#39;editor modelli eseguirà il rendering di tutto ciò che si trova in &#39;jcr:content/cq:dialog/content&#39;. Attualmente solo un layout fisso a 3 colonne è supportato dal motore di generazione dei moduli lato client. A destra della finestra di dialogo del modulo di cui è stato effettuato il rendering verrà visualizzato un elenco di tutti i tipi di dati specificati nella configurazione dei tipi di dati. Per modificare i tipi di dati, fai clic su di essi. La barra a destra passerà quindi alla scheda delle proprietà per il tipo di dati selezionato. È possibile aggiungere nuovi tipi di dati trascinandoli nell&#39;area di visualizzazione dell&#39;anteprima. Facendo clic su Salva, le modifiche vengono propagate al server. Facendo clic su Annulla l&#39;editor modelli viene chiuso.

>[!NOTE]
>
>Tutti i modelli sono Modelli, quindi seguono tutte AEM regole di modello. Questo consente di utilizzare proprietà come le proprietà *allowParents* e *allowChildren*. Sono efficaci durante la creazione di nuove Entità basate su un modello. Le regole del modello garantiscono che le entità possano essere basate solo su determinati modelli a seconda della loro gerarchia.
>
>Per informazioni sulla modifica di un modello dal dashboard, vedere [Creazione di un modello](/help/mobile/administer-mobile-apps.md) nella sezione relativa all&#39;authoring per le app mobili.

### Modelli di sistema {#system-models}

Sono disponibili due tipi di modelli di sistema predefiniti per il semplice riutilizzo dei contenuti. Questi modelli non possono essere modificati.

**Modello** pagineIl modello Pagine fornisce un metodo rapido per riutilizzare il contenuto esistente da Siti per la distribuzione da parte dei servizi contenuto.

resourceType di entità basate sul modello Pages è: mobileapp/caas/components/data/pages

Percorso: Percorso di una pagina Siti. Il contenuto di questo percorso (e dei relativi elementi secondari) verrà rappresentato dai gestori dei servizi di contenuto.

**Modello** risorseIl modello Risorse fornisce un metodo rapido per riutilizzare il contenuto esistente da Risorse per la distribuzione in base ai servizi di contenuto.

resourceType di entità basate sul modello Pages è: *mobileapps/caas/components/data/assets.*

Elenco risorse: Elenco di percorsi da Risorse. Ogni risorsa verrà aggiunta come nodo entità figlio con un resourceType di *wcm/foundation/components/image*.

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;utilizzo di questi modelli per la creazione di modelli dal dashboard, vedere [Creazione di un modello](/help/mobile/administer-mobile-apps.md) nella sezione Authoring per le app mobili.
