---
title: Configurazione del tracciamento dei collegamenti per Adobe Analytics
description: Scopri come configurare il tracciamento dei collegamenti per il SiteCatalyst.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---


# Configurazione del tracciamento dei collegamenti per Adobe Analytics{#configuring-link-tracking-for-adobe-analytics}

Quando gli utenti fanno clic sui collegamenti nelle pagine del sito web, è possibile acquisire informazioni correlate in Adobe Analytics. Ad esempio, utilizza il tracciamento dei collegamenti per scoprire come gli utenti interagiscono con il sito, tracciare i download dei file e tenere traccia dei collegamenti di uscita.

## Configurazione del tracciamento dei collegamenti per un framework Adobe Analytics {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. Utilizzando **Navigazione**, vai tramite **Distribuzione**, **Cloud Service** alla sezione **Adobe Analytics**.

1. Utilizzando **Mostra configurazioni**, apri il framework Adobe Analytics richiesto.
1. Espandi la sezione **Configurazione tracciamento collegamenti** e configura come richiesto (questa pagina fornisce ulteriori dettagli):

   ![Framework di Analytics](assets/aa-08.png)

## Tracciamento dei download di file {#tracking-file-downloads}

Configura il framework Adobe Analytics in modo che i file scaricati dalle pagine associate vengano automaticamente tracciati come download in Adobe Analytics. Quando abiliti il tracciamento dei download, vengono tracciati solo i tipi di file specificati.

Per impostazione predefinita, viene tenuta traccia dei download dei seguenti tipi di file:

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

Ad esempio, con il tracciamento del download abilitato per i file PDF, ogni volta che gli utenti fanno clic su collegamenti a file PDF, viene tracciato il download del PDF.

Le proprietà di tracciamento del download del framework sono implementate come codice nel file `analytics.sitecatalyst.js` generato per una pagina. Il seguente codice di esempio rappresenta la configurazione predefinita di tracciamento del download:

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Per abilitare il tracciamento dei download per il framework Adobe Analytics:

1. [Apri il framework di Adobe Analytics ed espandi la sezione Configurazione di tracciamento collegamenti](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Abilita **Traccia download**.
1. Nella casella **Scarica tipi di file** digitare le estensioni dei tipi di file da tracciare.

## Tracciamento dei collegamenti esterni {#tracking-external-links}

Puoi tenere traccia del clic dei collegamenti esterni (collegamenti di uscita) sulle pagine.

Per tenere traccia dei collegamenti esterni per il framework Adobe Analytics:

1. [Apri il framework di Adobe Analytics ed espandi la sezione **Configurazione di tracciamento dei collegamenti**](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configura le seguenti proprietà in base alle tue esigenze.

Proprietà per il tracciamento quando si fa clic su collegamenti esterni:

* **Traccia esterno**
Abilita il tracciamento dei collegamenti esterni.

* **Filtri esterni**
(Facoltativo) Definisce i filtri per la corrispondenza agli URL esterni delle destinazioni dei collegamenti. Quando le destinazioni dei collegamenti corrispondono al filtro, il collegamento viene tracciato. I filtri esterni sono utili per tenere traccia solo di alcuni collegamenti esterni sulle pagine.

  Per specificare i collegamenti esterni di cui tenere traccia, digitare tutto o parte dell&#39;URL della destinazione del collegamento. Separa più filtri con una virgola. Racchiudere i valori letterali stringa tra virgolette singole. Nessun valore (il valore predefinito di `''`, due virgolette singole) determina la registrazione di tutti i collegamenti esterni.

* **Filtri interni**
Definisce i filtri per la corrispondenza con gli URL dei collegamenti interni. Quando il collegamento è destinato a URL che corrispondono a questo filtro, il collegamento non viene tracciato. Il valore predefinito è un comando javascript che restituisce il nome host dell&#39;URL per l&#39;indirizzo della finestra corrente.

  Per specificare i collegamenti interni non tracciati, digita tutto o parte dell’URL interno della destinazione del collegamento. Separa più filtri con una virgola. Racchiudere i valori letterali stringa tra virgolette singole.

  Il valore predefinito è `'javascript:,'+window.location.hostname`

* **Lascia Stringa Di Query**
Include i parametri URL durante la valutazione delle corrispondenze con filtri interni ed esterni.

  Abilita questa opzione se desideri includere i parametri URL durante la valutazione degli URL di destinazione del collegamento rispetto ai filtri esterni e interni.

Le proprietà di tracciamento dei collegamenti esterni sono implementate come codice nel file `analytics.sitecatalyst.js` generato per una pagina. Il seguente codice di esempio viene generato per una pagina associata a un framework che ha abilitato il tracciamento dei collegamenti esterni con la seguente configurazione:

* Il filtro esterno è `'google.com'`
* Il filtro interno è il valore predefinito di `'javascript:,'+window.location.hostname`
* Le stringhe di query non sono incluse durante la valutazione della destinazione del collegamento rispetto ai filtri.

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## Invio di dati variabili con clic sui collegamenti {#sending-variable-data-with-link-clicks}

Puoi configurare l’AEM per inviare dati di eventi e variabili ad Adobe Analytics quando un utente fa clic su un collegamento. Le proprietà **Configurazione tracciamento collegamenti** consentono di specificare gli eventi Adobe Analytics e le variabili da monitorare quando si verificano i clic sui collegamenti.

Le mappature framework determinano i valori di evento e variabile. Puoi mappare le variabili di Adobe Analytics alle variabili dei componenti di contenuto che memorizzano i dati che desideri tracciare quando fai clic sui collegamenti.

Per inviare i dati delle variabili con i clic dei collegamenti:

1. [Apri il framework di Adobe Analytics ed espandi la sezione Configurazione di tracciamento collegamenti](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configura le seguenti proprietà in base alle tue esigenze.

Proprietà per l’invio di dati variabili con clic sui collegamenti:

* **Eventi traccia collegamenti**
Immetti le variabili evento Adobe Analytics da utilizzare per il conteggio dei clic sui collegamenti.

  Separa più nomi di variabili con una virgola.

  Il valore predefinito di `None` non causa il rilevamento di eventi.

* **Variabili traccia collegamenti**
Immetti le variabili Adobe Analytics da inviare ad Adobe Analytics quando fai clic sui collegamenti. Separa più nomi di variabili con una virgola.

  Il valore predefinito di `None` non causa l&#39;invio di dati di variabile.

Quando si specificano gli eventi e le variabili da inviare, la configurazione viene implementata come codice nel file `analytics.sitecatalyst.js` generato per una pagina. Il codice di esempio seguente viene generato per una pagina quando il framework tiene traccia dell&#39;evento `event10` e della proprietà `prop4`:

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## Esempio di configurazione del tracciamento dei collegamenti {#example-link-tracking-configuration}

Per esplorare il comportamento di tracciamento dei collegamenti dell’integrazione Adobe Analytics, effettua le seguenti procedure. Le procedure mostrano i risultati di [Adobe Marketing Cloud Debugger](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html?lang=it).

### Configurazione generale {#general-configuration}

Questo esempio illustra il funzionamento della mappatura nel contesto del tracciamento e del debugger:

1. Apri il framework che è stato associato a una pagina web.
1. Trascina il componente **Pagina** nell&#39;area dei mapping del framework. Il componente **Pagina** appartiene al Sidekick di componenti **Generale**.

   >[!NOTE]
   >
   >Il componente da utilizzare in uno scenario reale dipende dal componente ereditato da (se del caso).
   >
   >In caso contrario, dovresti avere esposto il tuo componente (definendo un sottonodo di analisi nel suo componente pagina).

   Configura la mappatura in base alla tabella seguente, trascinando la variabile Analytics (SiteCatalyst) dal pannello laterale sinistro:

<table>
 <tbody>
  <tr>
   <th>Variabile CQ<br /> </th>
   <th>Voce nel browser variabili<br /> </th>
   <th>Variabile Adobe Analytics</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>EVar personalizzato 1 (eVar 1)</td>
   <td>EVAR 1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>Personalizzato 1 (event1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. Trascina il componente Ricerca nell’area delle mappature del framework. Il componente Ricerca appartiene al gruppo di componenti Generale nel Sidekick. Configura la mappatura in base alla tabella seguente, trascinando la variabile Analytics (SiteCatalyst) dal pannello laterale sinistro:

<table>
 <tbody>
  <tr>
   <th>Variabile CQ<br /> </th>
   <th>Voce nel browser variabili</th>
   <th>Variabile Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>EVar personalizzato 2 (eVar 2)</td>
   <td>EVAR 2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>EVar personalizzato 3 (eVar 3)</td>
   <td>EVAR 3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>Personalizzato 2 (event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### Configurare il tracciamento dei collegamenti esterni {#configure-external-link-tracking}

1. Nel framework, espandi l&#39;area **Configurazione di tracciamento collegamenti**.
1. Deseleziona **Traccia download**.

1. Seleziona **Traccia esterno**.
1. Deseleziona **Lascia Stringa Di Query**.
1. Utilizza il seguente valore per l&#39;elenco **External Filters** per identificarlo come URL esterno:

   `'yahoo.com'`

1. Aggiungi il seguente valore al campo **Link Track Events**:

   ```
       event1,event2
   ```

1. Aggiungi il seguente valore al campo **Variabili di tracciamento collegamenti**:

   ```
       eVar1,eVar2
   ```

1. Nella pagina associata al framework, aggiungi un componente **Testo**. All&#39;interno del componente **Testo**, aggiungi un collegamento ipertestuale che punta al seguente indirizzo:

   `https://search.yahoo.com/?p=this`

1. Passa alla modalità **Anteprima** e fai clic sul collegamento.

La chiamata effettuata sarà simile alla seguente quando viene visualizzata con Adobe Marketing Cloud Debugger:

![Debugger Adobe Marketing Cloud](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>L&#39;URL non contiene la stringa di query: `?p=this`

### Includi il parametro URL {#include-the-url-parameter}

1. Nel framework, espandi l&#39;area **Configurazione di tracciamento collegamenti**.
1. Abilita **Lascia stringa di query**.
1. Ricarica l’anteprima della pagina e fai clic sul collegamento.

I dettagli delle chiamate visualizzati in Adobe Marketing Cloud Debugger sono simili a quelli del seguente esempio:

![Adobe Marketing Cloud Debugger](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>Questa volta l&#39;URL contiene la stringa di query: `?p=this`

## Tracciamento collegamenti ad hoc {#ad-hoc-link-tracking}

Il tracciamento dei collegamenti ad hoc consente agli autori di contenuto di configurare il tracciamento dei collegamenti per un componente. La configurazione del componente sostituisce la **configurazione di tracciamento dei collegamenti** del framework, pertanto nelle pagine associate al framework è possibile configurare i componenti **Testo** per il tracciamento dei collegamenti degli URL.

Il tracciamento dei collegamenti ad-hoc consente di tenere traccia dei collegamenti di download, dei collegamenti esterni e dei dati di eventi e variabili.

Per abilitare il tracciamento dei collegamenti ad-hoc è necessario:

* [Associa la pagina contenente il componente **Testo** al framework](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Configura il framework Adobe Analytics per abilitare il tracciamento dei collegamenti ad hoc](#enabling-ad-hoc-link-tracking).
* [Configurare il tracciamento dei collegamenti per un componente di testo](#configuring-link-tracking-for-a-text-component).

### Abilitazione del tracciamento dei collegamenti ad-hoc {#enabling-ad-hoc-link-tracking}

Configura il framework Adobe Analytics per abilitare il tracciamento dei collegamenti ad hoc.

1. Apri il framework Adobe Analytics ed espandi la sezione **Configurazione di tracciamento dei collegamenti**.

1. Abilita **Tracciamento collegamenti ad hoc**.

   >[!NOTE]
   >
   >Non tutti i tipi di utente hanno accesso a questa casella di controllo. Se hai bisogno di accedere, contatta l’amministratore del sito.

>[!NOTE]
>
>La configurazione dell&#39;antisamia XSS è ora in SLING nel percorso **/libs/sling/xss.config.xml** e le seguenti regole devono essere aggiunte ad hoc in modo che il collegamento funzioni:

#### Estensione regola tag di ancoraggio {#anchor-tag-rule-extension}

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

Prima di poter configurare il tracciamento dei collegamenti ad hoc per i componenti **Text**, è necessario che siano già state implementate le seguenti configurazioni:

* Il framework [Adobe Analytics è configurato per abilitare il tracciamento dei collegamenti ad hoc](#enabling-ad-hoc-link-tracking).
* La [pagina che contiene il componente **Text** è associata al framework](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

Per configurare il tracciamento dei collegamenti per un componente **Testo**, attenersi alla procedura descritta di seguito.

1. Apri la pagina in modalità di modifica e modifica il componente **Testo**.

1. Selezionare il testo da utilizzare come ipertesto e fare clic sul pulsante Collegamento ipertestuale.

   ![Icona collegamento](do-not-localize/chlimage_1.png)

1. Aggiungi l’URL di destinazione nella casella Collega a, quindi espandi l’area Tracciamento collegamenti.

   >[!NOTE]
   >
   >Il tracciamento dei collegamenti personalizzati è visibile come azione separata, accanto all&#39;azione Collega/Scollega (icona di Analytics).
   >
   >L’opzione sarà attivata solo dopo aver selezionato un collegamento valido nell’editor Rich Text.

   ![Abilitazione del tracciamento dei collegamenti](assets/aa-17.png)

1. Abilita **Custom Link Tracking** per ignorare la configurazione di tracciamento dei collegamenti del framework Adobe Analytics e abilitare il tracciamento dei collegamenti per il collegamento corrente.

1. (Facoltativo) Per tenere traccia degli eventi con il clic del collegamento, aggiungi i nomi degli eventi Adobe Analytics nel campo **Includi variabili Adobe Analytics**. Separa il nome di più eventi con virgole, ad esempio

   `event1, event22`.

1. (Facoltativo) Per tenere traccia dei dati delle variabili con il clic del collegamento, aggiungi le variabili Adobe Analytics nel campo **Includi variabili Adobe Analytics**. Utilizza uno dei seguenti formati:

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`'CONSTANT'`*

   Gli esempi seguenti illustrano ogni formato:

   * `eVar10:pagedata.title`
   * `prop1: 'Aubergine'`

   Separa più valori con una virgola.

1. Selezionare **OK**.
