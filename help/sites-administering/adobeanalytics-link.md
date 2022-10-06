---
title: Configurazione del tracciamento dei collegamenti per Adobe Analytics
seo-title: Configuring Link Tracking for Adobe Analytics
description: Scopri come configurare il tracciamento dei collegamenti per SiteCatalyst.
seo-description: Learn about configuring link tracking for SiteCatalyst.
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 1%

---

# Configurazione del tracciamento dei collegamenti per Adobe Analytics{#configuring-link-tracking-for-adobe-analytics}

Quando gli utenti fanno clic sui collegamenti nelle pagine del sito web, è possibile acquisire informazioni correlate in Adobe Analytics. Ad esempio, utilizza il tracciamento dei collegamenti per capire in che modo gli utenti interagiscono con il tuo sito, tracciare i download dei file e i collegamenti di uscita.

## Configurazione del tracciamento dei collegamenti per un framework Adobe Analytics {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. Utilizzo **Navigazione**, via **Distribuzione**, **Cloud Services** al **Adobe Analytics** sezione .

1. Utilizzo **Mostra configurazioni**, apri il framework Adobe Analytics richiesto.
1. Espandi la **Configurazione del tracciamento dei collegamenti** e configura come necessario (questa pagina fornisce ulteriori dettagli):

   ![aa-08](assets/aa-08.png)

## Tracciamento dei download dei file {#tracking-file-downloads}

Configura il framework Adobe Analytics in modo che i file scaricati dalle pagine associate vengano tracciati automaticamente come download in Adobe Analytics. Quando abiliti il tracciamento dei download, vengono tracciati solo i tipi di file specificati.

I download dei seguenti tipi di file sono tracciati per impostazione predefinita:

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

Ad esempio, con il tracciamento del download abilitato per i file PDF, ogni volta che un utente fa clic su un collegamento a file PDF, viene tracciato il download di PDF.

Le proprietà di tracciamento del download del framework sono implementate come codice nel `analytics.sitecatalyst.js` file generato per una pagina. Il seguente codice di esempio rappresenta la configurazione di tracciamento del download predefinita:

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Per abilitare il tracciamento dei download per il framework Adobe Analytics:

1. [Apri il framework Adobe Analytics ed espandi la sezione Configurazione tracciamento collegamenti .](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Abilita **Tracciare i download**.
1. In **Download dei tipi di file** digitare le estensioni del nome file per i tipi di file che si desidera tracciare.

## Tracciamento dei collegamenti esterni {#tracking-external-links}

Puoi tenere traccia dei clic sui collegamenti esterni (collegamenti di uscita) nelle pagine.

Per tenere traccia dei collegamenti esterni per il framework Adobe Analytics:

1. [Apri il framework Adobe Analytics ed espandi il **Configurazione del tracciamento dei collegamenti** sezione](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configura le seguenti proprietà in base alle tue esigenze.

Proprietà per il tracciamento quando si fa clic su collegamenti esterni:

* **Traccia esterna**
Abilita il tracciamento dei collegamenti esterni.

* **Filtri esterni**
(Facoltativo) Definisce i filtri per la corrispondenza con gli URL esterni delle destinazioni di collegamento. Quando le destinazioni di collegamento corrispondono al filtro, il collegamento viene tracciato. I filtri esterni sono utili per tenere traccia solo di alcuni collegamenti esterni sulle pagine.

   Per specificare i collegamenti esterni da tracciare, digita tutto o parte dell’URL della destinazione del collegamento. Separa più filtri con una virgola. Racchiudere i letterali stringa tra virgolette singole. Nessun valore (il valore predefinito di `''`, due virgolette singole) fa sì che tutti i collegamenti esterni siano tracciati.

* **Filtri interni**
Definisce i filtri per la corrispondenza con gli URL dei collegamenti interni. Quando il collegamento esegue il targeting di URL che corrispondono a questo filtro, il collegamento non viene tracciato. Il valore predefinito è un comando javascript che restituisce il nome host dell&#39;URL per l&#39;indirizzo della finestra corrente.

   Per specificare i collegamenti interni non tracciati, digita tutto o parte dell’URL interno della destinazione del collegamento. Separa più filtri con una virgola. Racchiudere i letterali stringa tra virgolette singole.

   Il valore predefinito è `'javascript:,'+window.location.hostname`

* **Lascia stringa di query**
Include i parametri URL durante la valutazione delle corrispondenze con filtri interni ed esterni.

   Abilita per includere i parametri URL durante la valutazione degli URL di destinazione del collegamento rispetto a filtri esterni e interni.

Le proprietà di tracciamento dei collegamenti esterni vengono implementate come codice nel `analytics.sitecatalyst.js` file generato per una pagina. Il seguente codice di esempio viene generato per una pagina associata a un framework che ha abilitato il tracciamento dei collegamenti esterni con la seguente configurazione:

* Il filtro esterno è `'google.com'`
* Il filtro interno è il valore predefinito di `'javascript:,'+window.location.hostname`
* Le stringhe di query non vengono incluse durante la valutazione della destinazione del collegamento rispetto ai filtri.

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## Invio di dati a variabili con clic sui collegamenti {#sending-variable-data-with-link-clicks}

Puoi configurare AEM per l’invio di dati di eventi e variabili ad Adobe Analytics quando un utente fa clic su un collegamento. La **Configurazione del tracciamento dei collegamenti** Le proprietà consentono di specificare gli eventi e le variabili di Adobe Analytics da monitorare quando si verificano i clic sul collegamento.

Le mappature del framework determinano i valori dell&#39;evento e della variabile. Puoi mappare le variabili Adobe Analytics alle variabili dei componenti di contenuto che memorizzano i dati da tracciare quando fai clic sui collegamenti.

Per inviare dati variabili con clic sul collegamento:

1. [Apri il framework Adobe Analytics ed espandi la sezione Configurazione tracciamento collegamenti .](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configura le seguenti proprietà in base alle tue esigenze.

Proprietà per l’invio di dati variabili con clic sul collegamento:

* **Tracciare i collegamenti**
Immetti le variabili dell&#39;evento Adobe Analytics che desideri utilizzare per contare i clic sui collegamenti.

   Separa i nomi di più variabili con una virgola.

   Il valore predefinito di `None` non causa il tracciamento degli eventi.

* **Varie traccia collegamenti**
Immetti le variabili Adobe Analytics da inviare ad Adobe Analytics quando fai clic sui collegamenti. Separa i nomi di più variabili con una virgola.

   Il valore predefinito di `None` non invia dati variabili.

Quando specifichi gli eventi e le variabili da inviare, la configurazione viene implementata come codice nel `analytics.sitecatalyst.js` file generato per una pagina. Il seguente codice di esempio viene generato per una pagina quando il framework traccia il `event10` e `prop4` proprietà:

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## Esempio di configurazione del tracciamento dei collegamenti {#example-link-tracking-configuration}

Esegui le seguenti procedure per esplorare il comportamento di tracciamento dei collegamenti dell’integrazione Adobe Analytics. Le procedure mostrano i risultati [Debugger Adobe Marketing Cloud](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html).

### Configurazione generale {#general-configuration}

Questo esempio illustra come funziona la mappatura nel contesto del tracciamento e del debugger:

1. Apri il framework associato a una pagina web.
1. Trascina **Pagina** nell&#39;area delle mappature del framework. La **Pagina** il componente appartiene al **Generale** gruppo di componenti nella barra laterale.

   >[!NOTE]
   >
   >Il componente da utilizzare in uno scenario reale dipende dal componente ereditato da (se del caso).
   >
   >In caso contrario, esponete il vostro componente (definendo un sottonodo di analytics nel suo componente pagina).

   Configura la mappatura in base alla tabella seguente, trascinando la variabile Analytics (SiteCatalyst) dal pannello laterale sinistro:

<table>
 <tbody>
  <tr>
   <th>Variabile CQ<br /> </th>
   <th>Voce nel browser delle variabili<br /> </th>
   <th>Variabile Adobe Analytics</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>eVar personalizzato 1 (eVar1)</td>
   <td>eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>Personalizzato 1 (evento1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. Trascina il componente Ricerca nell’area delle mappature del framework. Il componente Ricerca appartiene al gruppo di componenti Generale nella barra laterale. Configura la mappatura in base alla tabella seguente, trascinando la variabile Analytics (SiteCatalyst) dal pannello laterale sinistro:

<table>
 <tbody>
  <tr>
   <th>Variabile CQ<br /> </th>
   <th>Voce nel browser delle variabili</th>
   <th>Variabile Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>eVar personalizzato 2 (eVar2)</td>
   <td>eVar 2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>eVar personalizzato 3 (eVar3)</td>
   <td>eVar 3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>Personalizzato 2 (event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### Configurare il tracciamento dei collegamenti esterni {#configure-external-link-tracking}

1. Nel framework, espandi la **Configurazione del tracciamento dei collegamenti** area.
1. Deseleziona **Tracciare i download**.

1. Seleziona **Traccia esterna**.
1. Deseleziona **Lascia stringa di query**.
1. Utilizza il seguente valore per **Filtri esterni** elenco per identificarlo come URL esterno:

   `‘yahoo.com’`

1. Aggiungi il seguente valore al **Tracciare i collegamenti** campo:

   ```
       event1,event2
   ```

1. Aggiungi il seguente valore al **Varie di tracciamento dei collegamenti** campo:

   ```
       eVar1,eVar2
   ```

1. Nella pagina associata al framework, aggiungi un **Testo** componente. Dentro **Testo** aggiungi un collegamento ipertestuale al seguente indirizzo:

   `https://search.yahoo.com/?p=this`

1. Passa a **Modalità Anteprima** e fai clic sul collegamento.

La chiamata effettuata avrà questo aspetto quando viene visualizzata con Adobe Marketing Cloud Debugger:

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>L’URL non contiene la stringa di query: `?p=this`

### Includere il parametro URL {#include-the-url-parameter}

1. Nel framework, espandi il **Configurazione del tracciamento dei collegamenti** area.
1. Abilita **Lascia stringa di query**.
1. Ricarica l’anteprima della pagina e fai clic sul collegamento.

I dettagli della chiamata visualizzati in Adobe Marketing Cloud Debugger sono simili al seguente esempio:

![aa-leavequerysearch-active](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>Questa volta l’URL contiene la stringa Query: `?p=this`

## Tracciamento dei collegamenti ad hoc {#ad-hoc-link-tracking}

Il tracciamento dei collegamenti ad hoc consente agli autori di contenuti di configurare il tracciamento dei collegamenti per un componente. La configurazione del componente sostituisce la **Configurazione del tracciamento dei collegamenti** del framework, in particolare sulle pagine associate al framework, **Testo** I componenti possono essere configurati per il tracciamento dei collegamenti degli URL.

Il tracciamento dei collegamenti ad hoc consente di tenere traccia dei collegamenti per il download, dei collegamenti esterni e dei dati relativi a eventi e variabili.

Per abilitare il tracciamento dei collegamenti ad hoc devi:

* [Associa la pagina contenente la **Testo** componente del quadro](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Configurare il framework Adobe Analytics per abilitare il tracciamento dei collegamenti ad hoc](#enabling-ad-hoc-link-tracking).
* [Configurare il tracciamento dei collegamenti per un componente Testo](#configuring-link-tracking-for-a-text-component).

### Abilitazione del tracciamento dei collegamenti ad hoc {#enabling-ad-hoc-link-tracking}

Configura il tuo framework Adobe Analytics per abilitare il tracciamento dei collegamenti ad hoc.

1. Apri il framework Adobe Analytics ed espandi il **Configurazione del tracciamento dei collegamenti** sezione .

1. Abilita **Tracciamento dei collegamenti ad hoc**.

   >[!NOTE]
   >
   >Non tutti i tipi di utente hanno accesso a questa casella di controllo. Contatta l’amministratore del sito per richiedere l’accesso.

>[!NOTE]
>
>La configurazione di XSS Antisamy ora è in SLING sotto il percorso **/libs/sling/xss.config.xml** e le seguenti regole devono essere aggiunte a per i collegamenti ad hoc al lavoro:

#### Estensione della regola del tag di ancoraggio {#anchor-tag-rule-extension}

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

### Configurazione del tracciamento dei collegamenti per un componente testo {#configuring-link-tracking-for-a-text-component}

Prima di configurare il tracciamento dei collegamenti ad hoc per **Testo** componenti stessi, le seguenti configurazioni devono essere già state implementate:

* La [Il framework Adobe Analytics è configurato per abilitare il tracciamento dei collegamenti ad hoc](#enabling-ad-hoc-link-tracking).
* La [che contiene **Testo** il componente è associato al framework](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

Segui la procedura seguente per configurare il tracciamento dei collegamenti per un **Testo** componente:

1. Apri la pagina in modalità di modifica e modifica il **Testo** componente.

1. Selezionare il testo da utilizzare come ipertesto e fare clic sul pulsante Collegamento ipertestuale.

   ![](do-not-localize/chlimage_1.png)

1. Aggiungi l’URL di destinazione nella casella Collega a , quindi espandi l’area Tracciamento collegamento .

   >[!NOTE]
   >
   >Il tracciamento dei collegamenti personalizzato è visibile come azione separata, accanto all’azione Collega/Scollega (icona Analytics).
   >
   >Sarà attivato solo se hai selezionato un collegamento valido nell’editor Rich Text.

   ![aa-17](assets/aa-17.png)

1. Abilita **Tracciamento dei collegamenti personalizzati** per ignorare la configurazione di tracciamento dei collegamenti del framework Adobe Analytics e abilitare il tracciamento dei collegamenti per il collegamento corrente.

1. (Facoltativo) Per tenere traccia degli eventi con il clic sul collegamento, aggiungi i nomi degli eventi Adobe Analytics nella sezione **Includi variabili Adobe Analytics** campo . Separa il nome di più eventi con virgole, ad esempio

   `event1, event22`.

1. (Facoltativo) Per tenere traccia dei dati delle variabili con il clic sul collegamento, aggiungi le variabili Adobe Analytics nel **Includi variabili Adobe Analytics** campo . Utilizzare uno dei seguenti formati:

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`‘CONSTANT'`*

   Gli esempi seguenti illustrano ogni formato:

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   Separa più valori con una virgola.

1. Seleziona **OK**.
