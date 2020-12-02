---
title: Configurazione del tracciamento dei collegamenti per  Adobe Analytics
seo-title: Configurazione del tracciamento dei collegamenti per  Adobe Analytics
description: Scopri come configurare il tracciamento dei collegamenti per SiteCatalyst.
seo-description: Scopri come configurare il tracciamento dei collegamenti per SiteCatalyst.
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---


# Configurazione del tracciamento dei collegamenti per  Adobe Analytics{#configuring-link-tracking-for-adobe-analytics}

Quando gli utenti fanno clic sui collegamenti presenti sulle pagine del sito Web, è possibile acquisire informazioni correlate in  Adobe Analytics. Ad esempio, puoi usare il tracciamento dei collegamenti per capire in che modo gli utenti interagiscono con il tuo sito, tenere traccia dei download dei file e dei collegamenti di uscita.

## Configurazione del tracciamento dei collegamenti per un  Adobe Analytics Framework {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. Utilizzando **Navigation**, passare alla sezione **Adobe Analytics** mediante **Cloud Services**.****

1. Utilizzando **Show Configurations**, aprite il framework Adobe Analytics  richiesto.
1. Espandete la sezione **Configurazione tracciamento collegamenti** e configurate come necessario (questa pagina fornisce ulteriori dettagli):

   ![a-08](assets/aa-08.png)

## Tracciamento dei download di file {#tracking-file-downloads}

Configurate il framework Adobe Analytics  in modo che i file scaricati dalle pagine associate vengano tracciati automaticamente come download in  Adobe Analytics. Quando abilitate il tracciamento dei download, vengono tracciati solo i tipi di file specificati.

I download dei seguenti tipi di file vengono tracciati per impostazione predefinita:

* exe
* zip
* wav
* mp3
* mov
* mpg
* avi
* wmv
* doc
* pdf
* xls

Ad esempio, con il tracciamento del download abilitato per i file PDF, ogni volta che l&#39;utente fa clic sui collegamenti ai file PDF, viene tracciato il download del PDF.

Le proprietà di tracciamento del download del framework vengono implementate come codice nel file `analytics.sitecatalyst.js` generato per una pagina. Il seguente esempio di codice rappresenta la configurazione di tracciamento dei download predefinita:

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Per abilitare il tracciamento dei download per il framework Adobe Analytics :

1. [Aprite il framework Adobe Analytics  ed espandete la sezione](#configuring-link-tracking-for-an-adobe-analytics-framework) Configurazione tracciamento collegamenti.
1. Abilita **Track Downloads**.
1. Nella casella **Scarica tipi di file**, digitare le estensioni per i tipi di file da monitorare.

## Tracciamento dei collegamenti esterni {#tracking-external-links}

Potete tenere traccia dei collegamenti esterni (collegamenti di uscita) presenti sulle pagine.

Per tenere traccia dei collegamenti esterni per il framework Adobe Analytics :

1. [Aprite il framework Adobe Analytics  ed espandete la sezione  **Link Tracking** Configuration (Configurazione tracciamento collegamenti)](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configurate le seguenti proprietà in base alle vostre esigenze.

Proprietà per il tracciamento quando si fa clic sui collegamenti esterni:

* **Track**
ExternalAbilita il tracciamento dei collegamenti esterni.

* **Filtri**
 esterni (facoltativo) Definisce i filtri per la corrispondenza con gli URL esterni delle destinazioni di collegamento. Quando le destinazioni di collegamento corrispondono al filtro, il collegamento viene tracciato. I filtri esterni sono utili per tenere traccia solo di alcuni dei collegamenti esterni sulle pagine.

   Per specificare i collegamenti esterni da tracciare, digitate tutto o parte dell’URL della destinazione del collegamento. Separate più filtri con una virgola. Racchiudere i letterali di stringa tra virgolette singole. Nessun valore (il valore predefinito di `''`, due virgolette singole) causa il tracciamento di tutti i collegamenti esterni.

* **Filtri interniDefinisce i filtri per la corrispondenza con gli URL dei collegamenti interni.**
Quando il collegamento ha come destinazione gli URL che corrispondono a questo filtro, il collegamento non viene tracciato. Il valore predefinito è un comando javascript che restituisce il nome host dell&#39;URL per l&#39;indirizzo della finestra corrente.

   Per specificare i collegamenti interni non tracciati, digitate tutto o parte dell’URL interno della destinazione del collegamento. Separate più filtri con una virgola. Racchiudere i letterali di stringa tra virgolette singole.

   Il valore predefinito è `'javascript:,'+window.location.hostname`

* **Lascia**
stringa query: include i parametri URL per la valutazione delle corrispondenze con filtri interni ed esterni.

   Consente di includere i parametri URL durante la valutazione degli URL di destinazione dei collegamenti rispetto ai filtri esterni e interni.

Le proprietà di tracciamento dei collegamenti esterni sono implementate come codice nel file `analytics.sitecatalyst.js` generato per una pagina. Il seguente codice di esempio viene generato per una pagina associata a un framework che ha attivato il tracciamento dei collegamenti esterni con la seguente configurazione:

* Il filtro esterno è `'google.com'`
* Il filtro interno è il valore predefinito di `'javascript:,'+window.location.hostname`
* Le stringhe di query non sono incluse nella valutazione della destinazione del collegamento rispetto ai filtri.

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## Invio di dati variabili con clic di collegamento {#sending-variable-data-with-link-clicks}

Potete configurare AEM per inviare dati di eventi e variabili a  Adobe Analytics quando un utente fa clic su un collegamento. Le proprietà **Configurazione tracciamento collegamenti** consentono di specificare gli eventi e le variabili  Adobe Analytics da monitorare quando si verifica il clic del collegamento.

Le mappature framework determinano i valori di evento e variabile. È possibile mappare  variabili Adobe Analytics alle variabili dei componenti di contenuto che memorizzano i dati da tenere traccia quando si fa clic sui collegamenti.

Per inviare dati variabili con clic sul collegamento:

1. [Aprite il framework Adobe Analytics  ed espandete la sezione](#configuring-link-tracking-for-an-adobe-analytics-framework) Configurazione tracciamento collegamenti.
1. Configurate le seguenti proprietà in base alle vostre esigenze.

Proprietà per l’invio di dati variabili con clic del collegamento:

* **Collega**
eventi di traccia: inserite le variabili di evento Adobe Analytics  che desiderate utilizzare per contare i clic dei collegamenti.

   Separate i nomi di più variabili con una virgola.

   Il valore predefinito di `None` non causa il tracciamento degli eventi.

* **Collega**
variabili di traccia: inserite le  variabili Adobe Analytics che desiderate inviare a  Adobe Analytics quando si fa clic sui collegamenti. Separate i nomi di più variabili con una virgola.

   Il valore predefinito di `None` non invia dati variabili.

Quando si specificano gli eventi e le variabili da inviare, la configurazione viene implementata come codice nel file `analytics.sitecatalyst.js` generato per una pagina. Il seguente codice di esempio viene generato per una pagina quando il framework tiene traccia dell&#39;evento `event10` e della proprietà `prop4`:

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## Esempio di configurazione del tracciamento dei collegamenti {#example-link-tracking-configuration}

Seguite le procedure riportate di seguito per esaminare il comportamento di tracciamento dei collegamenti nell&#39;integrazione  Adobe Analytics. Le procedure mostrano i risultati di [Adobe Marketing Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html).

### Configurazione generale {#general-configuration}

Questo esempio illustra come funziona la mappatura nel contesto del tracciamento e del debugger:

1. Aprite il framework associato a una pagina Web.
1. Trascinare il componente **Page** nell&#39;area delle mappature del framework. Il componente **Page** appartiene al gruppo di componenti **General** nella barra laterale.

   >[!NOTE]
   >
   >Il componente da utilizzare in uno scenario di vita reale dipende dal componente ereditato (se del caso).
   >
   >In caso contrario, il componente deve essere esposto al suo interno (definendo un nodo secondario di analisi nel componente della pagina).

   Configura la mappatura in base alla tabella seguente, trascinando la variabile Analytics (SiteCatalyst) dal pannello laterale sinistro:

<table>
 <tbody>
  <tr>
   <th>Variabile CQ<br /> </th>
   <th>Voce nel browser delle variabili<br /> </th>
   <th> Adobe Analytics Variabile</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>Custom  eVar 1 ( eVar1)</td>
   <td> eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>Custom 1 (event1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. Trascinate il componente Ricerca nell’area delle mappature del framework. Il componente Ricerca appartiene al gruppo di componenti Generale nella barra laterale. Configura la mappatura in base alla tabella seguente, trascinando la variabile Analytics (SiteCatalyst) dal pannello laterale sinistro:

<table>
 <tbody>
  <tr>
   <th>Variabile CQ<br /> </th>
   <th>Voce nel browser delle variabili</th>
   <th> Adobe Analytics Variabile</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>Custom  eVar 2 ( eVar2)</td>
   <td> eVar 2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>Custom  eVar 3 ( eVar3)</td>
   <td> eVar 3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>Custom 2 (event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### Configurare il tracciamento dei collegamenti esterni {#configure-external-link-tracking}

1. Nel framework, espandete l&#39;area **Configurazione tracciamento collegamenti**.
1. Deselezionare **Track Downloads**.

1. Selezionare **Track External**.
1. Deselezionare **Lascia stringa query**.
1. Utilizzate il seguente valore per l&#39;elenco **Filtri esterni** per identificarlo come URL esterno:

   `‘yahoo.com’`

1. Aggiungete il seguente valore al campo **Collega eventi traccia**:

   ```
       event1,event2
   ```

1. Aggiungi il seguente valore al campo **Collega var di traccia**:

   ```
       eVar1,eVar2
   ```

1. Nella pagina associata al framework, aggiungete un componente **Testo**. All&#39;interno del componente **Testo**, aggiungere un collegamento ipertestuale che indichi l&#39;indirizzo seguente:

   `https://search.yahoo.com/?p=this`

1. Passate alla modalità **Anteprima** e fate clic sul collegamento.

La chiamata effettuata sarà simile a quella visualizzata con Adobe Marketing Cloud Debugger:

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>L&#39;URL non contiene la stringa Query: `?p=this`

### Includere il parametro URL {#include-the-url-parameter}

1. Nel framework, espandete l&#39;area **Configurazione tracciamento collegamenti**.
1. Abilitare **Lascia stringa query**.
1. Ricaricate l’anteprima della pagina e fate clic sul collegamento.

I dettagli delle chiamate visualizzati in Adobe Marketing Cloud Debugger sono simili al seguente esempio:

![aa-leavequerysearch-active](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>Questa volta l’URL contiene la stringa Query: `?p=this`

## Tracciamento dei collegamenti ad hoc {#ad-hoc-link-tracking}

Il tracciamento dei collegamenti ad hoc consente agli autori di contenuti di configurare il tracciamento dei collegamenti per un componente. La configurazione del componente ha la priorità su **Configurazione tracciamento collegamenti** del framework, pertanto sulle pagine associate al framework è possibile configurare i componenti **Testo** per il tracciamento dei collegamenti degli URL.

Il tracciamento dei collegamenti ad hoc consente di tenere traccia dei collegamenti per il download, dei collegamenti esterni e dei dati relativi a eventi e variabili.

Per abilitare il tracciamento dei collegamenti ad hoc è necessario:

* [Associate la pagina che contiene il componente  **** Testo al framework](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Configurare il framework Adobe Analytics  per abilitare il tracciamento](#enabling-ad-hoc-link-tracking) dei collegamenti ad hoc.
* [Configurare il tracciamento dei collegamenti per un componente](#configuring-link-tracking-for-a-text-component) Testo.

### Abilitazione del tracciamento dei collegamenti ad hoc {#enabling-ad-hoc-link-tracking}

Configurate il framework Adobe Analytics  per abilitare il tracciamento dei collegamenti ad hoc.

1. Aprite il framework Adobe Analytics  ed espandete la sezione **Configurazione tracciamento collegamenti**.

1. Abilitare il tracciamento dei collegamenti ad hoc **ad hoc**.

   >[!NOTE]
   >
   >Non tutti i tipi di utente hanno accesso a questa casella di controllo. Se necessario, contattate l’amministratore del sito.

>[!NOTE]
>
>La configurazione di XSS Antisamy ora è in SLING nel percorso **/libs/sling/xss.config.xml** e per il collegamento ad hoc al lavoro è necessario aggiungere le seguenti regole:

#### Estensione della regola dei tag di ancoraggio {#anchor-tag-rule-extension}

```xml
<attribute name="onclick">
    <literal-list>
        <literal value="CQ_Analytics.Sitecatalyst.customTrack(this)"/>
    </literal-list>
</attribute>
<attribute name="adhocenable">
    <literal-list>
        <literal value="true"/>
        <literal value="false"/>
    </literal-list>
</attribute>
<attribute name="adhocevents">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
<attribute name="adhocevars">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
```

### Configurazione del tracciamento dei collegamenti per un componente di testo {#configuring-link-tracking-for-a-text-component}

Prima di poter configurare il tracciamento dei collegamenti ad hoc per i componenti **Text**, è necessario che siano già state implementate le seguenti configurazioni:

* Il [ framework Adobe Analytics è configurato per abilitare il tracciamento dei collegamenti ad hoc](#enabling-ad-hoc-link-tracking).
* La pagina [che contiene il componente **Testo** è associata al framework](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

Per configurare il tracciamento dei collegamenti per un componente **Testo**, effettuate le seguenti operazioni:

1. Aprite la pagina in modalità di modifica e modificate il componente **Testo**.

1. Selezionate il testo da usare come ipertesto e fate clic sul pulsante Collegamento ipertestuale.

   ![](do-not-localize/chlimage_1.png)

1. Aggiungete l’URL di destinazione nella casella Collega a, quindi espandete l’area Tracciamento collegamento.

   >[!NOTE]
   >
   >Il tracciamento personalizzato dei collegamenti è visibile come azione separata, accanto all’azione Collegamento/Scollega (icona di Analytics).
   >
   >Sarà attivato solo se hai selezionato un collegamento valido nell’editor Rich Text.

   ![a-17](assets/aa-17.png)

1. Abilitate **Custom Link Tracking** per ignorare la configurazione di tracciamento dei collegamenti del framework Adobe Analytics  e per abilitare il tracciamento dei collegamenti per il collegamento corrente.

1. (Facoltativo) Per tenere traccia degli eventi con il collegamento, fare clic su Aggiungi  nomi degli eventi Adobe Analytics nel campo **Includi  variabili Adobe Analytics**. Separare il nome di più eventi con virgole, ad esempio

   `event1, event22`.

1. (Facoltativo) Per tenere traccia dei dati variabili con il clic del collegamento, aggiungi  variabili Adobe Analytics nel campo **Includi  variabili Adobe Analytics**. Utilizzate uno dei seguenti formati:

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*:  *`‘CONSTANT'`*

   Gli esempi seguenti illustrano ciascun formato:

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   Separate più valori con una virgola.

1. Selezionare **OK**.

