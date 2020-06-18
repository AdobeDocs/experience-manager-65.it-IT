---
title: ' Configurazione Analytics per le funzioni Community'
seo-title: ' Configurazione Analytics per le funzioni Community'
description: Configurare l'analisi per Communities
seo-description: Configurare l'analisi per Communities
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
translation-type: tm+mt
source-git-commit: df59879cfa6b0bc7eba13f679e833fabbcbe92f2
workflow-type: tm+mt
source-wordcount: '2765'
ht-degree: 3%

---


#  Configurazione Analytics per le funzioni Community {#analytics-configuration-for-communities-features}

## Panoramica {#overview}

Adobe  Analytics e  Adobe Experience Manager (AEM) sono entrambe soluzioni  Adobe Marketing Cloud.

Adobe  Analytics può essere configurato per i AEM Communities in modo che, quando un membro interagisce con le funzioni Community supportate, gli eventi vengano inviati ad Adobe  Analytics da cui vengono generati i rapporti.

Ad esempio, quando un membro di un sito community di abilitazione visualizza una risorsa video assegnata, il lettore delle risorse invia eventi a  Analytics, inclusi i dati heartbeat video. Dal sito della community, gli amministratori possono visualizzare vari rapporti sulla riproduzione del video.

Inoltre, l&#39;analisi è necessaria per:

* Nell’ambiente di pubblicazione:

   * Relazioni sulle [tendenze comunitarie](/help/communities/trends.md)
   * Possibilità per i visitatori del sito di ordinare per &quot;più visualizzati&quot;, &quot;più attivi&quot; o &quot;più graditi&quot;
   * Visualizzare i conteggi negli elenchi UGC

* Nell’ambiente di authoring:

   * Visualizzazione dei dati di partecipazione nella console [di gestione dei](/help/communities/members.md) membri (viste, post, follower, Mi piace)
   * Riepilogo delle tendenze, heartbeat video e dispositivo video per l’abilitazione dei [rapporti sulle risorse](/help/communities/reports.md)

Le funzioni Community supportate includono:

* [Risorse di abilitazione](/help/communities/resources.md)
* [Forum](/help/communities/forum.md)
* [D/R](/help/communities/working-with-qna.md)
* [Blog](/help/communities/blog-feature.md)
* [Libreria file](/help/communities/file-library.md)
* [Calendario](/help/communities/calendar.md)

In questa sezione della documentazione viene descritto come collegare una suite di rapporti Analytics  alle funzioni di Communities. I passaggi di base sono:

1. [Replicare la chiave](#replicate-the-crypto-key) di crittografia per garantire che la crittografia/decrittografia si verifichi correttamente su tutte le istanze di AEM
1. Preparare una suite di [rapporti Adobe  Analytics](#adobe-analytics-report-suite-for-video-reporting)
1. Creare un servizio [e un](#aem-analytics-cloud-service-configuration) framework [cloud AEM  Analytics](#aem-analytics-framework-configuration)

1. [Abilita  Analytics](#enable-analytics-for-a-community-site) per un sito community
1. [**Verifica **](#verify-analytics-to-aem-variable-mapping)mappatura variabile Analytics-AEM
1. Identificare l&#39;editore [principale](#primary-publisher)
1. [Pubblicare](#publish-community-site-and-analytics-cloud-service) il sito della community
1. Configurare l&#39; [importazione di dati](#obtaining-reports-from-analytics) del report da Adobe  Analytics al sito della community

## Prerequisiti {#prerequisites}

Per configurare  funzionalità di Analytics per community, è necessario collaborare con il rappresentante commerciale di riferimento per impostare un account Adobe  Analytics e una suite [di](#adobe-analytics-report-suite-for-video-reporting)rapporti. Una volta stabilite, devono essere disponibili le seguenti informazioni:

* **Nome società**

   Società associata all&#39;account Adobe  Analytics.

* **Nome utente**

   Il nome utente di accesso per l&#39;utente autorizzato a gestire l&#39;account Analytics  (deve includere i privilegi di accesso al servizio Web).

* **Password**

   La password di accesso per l’utente autorizzato.

* **Analytics Data Center**

   URL del centro dati Analytics  per l&#39;account.

* **Suite di rapporti**

   Nome della suite di rapporti Analytics  da utilizzare.

## Adobe  Analytics Report Suite for Video Reporting {#adobe-analytics-report-suite-for-video-reporting}

Utilizzando  Adobe Marketing Cloud  [Report Suite Manager](https://marketing.adobe.com/resources/help/en_US/reference/new_report_suite.html),  suite di rapporti Analytics possono essere configurate in modo che un sito community possa essere abilitato per fornire rapporti per le funzioni Community.

Effettuando l&#39;accesso a [Adobe Marketing Cloud](https://marketing.adobe.com/resources/help/en_US/analytics/getting-started/analytics-navigation.html) con Nome [società e Nome](/help/communities/analytics.md#prerequisites)utente, è possibile configurare una suite di rapporti nuova o esistente con:

* [11 Variabili](https://marketing.adobe.com/resources/help/en_US/reference/conversion_var_admin.html) di conversione (eVar)

   * **`evar1`** tramite **`evar11`** abilitato

   * Può riadattare (rinominare) le eVar esistenti o crearne di nuove da utilizzare per le funzioni Community

* [7 Eventi](https://marketing.adobe.com/resources/help/en_US/reference/success_event.html) di successo (eventi)

   * **`event1`** tramite **`event7`** abilitato

   * tipo **`Counter`**

      * not **`Counter (no subrelations)`**
   * Può riadattare (rinominare) gli eventi esistenti o crearne di nuovi da utilizzare per le funzioni Community


* [Gestione video](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_analytics_config.html)

   * Video Reporting console

      * Abilita `Video Core`
      * Seleziona Salva
   * Console di misurazione video

      * Seleziona `Use Solution Variables`
      * Seleziona Salva


Se utilizzate una **nuova suite** di rapporti, tenete presente che una nuova suite di rapporti può contenere solo 4 variabili evar e 6 eventi, mentre per le community sono richieste 11 variabili evar e 7 variabili evento.

Se si utilizza una suite **di rapporti** esistente, potrebbe essere necessario [modificare la mappatura](#modifying-analytics-variable-mapping) delle variabili prima di attivare il framework Analytics  per un sito community. Contatta il tuo rappresentante commerciale per qualsiasi dubbio sulle variabili dedicate alle Community.

>[!CAUTION]
>
>**Se si utilizza una suite di rapporti esistente che utilizza già variabili all&#39;interno di**
>
>* Da **`evar1`** a **`evar11`**
   >
   >
* Da **`event1`** a **`event7`**
>
>
**Prima della pubblicazione del sito della community,** è importante ripristinare la mappatura preesistente spostando le variabili AEM che venivano automaticamente mappate  variabili Analytics quando  Analytics era abilitato per un sito della community.
>
>Per ripristinare la mappatura preesistente e spostare le variabili AEM in altre  variabili Analytics, consulta la sezione [Modifica  mappatura](#modifying-analytics-variable-mapping)delle variabili Analytics.
>
>In caso contrario si potrebbe determinare una perdita di dati non recuperabile.

### Video Heartbeat  Analytics {#video-heartbeat-analytics}

Quando viene concessa la licenza di Video Heartbeat  Analytics, `Marketing Cloud Org Id` viene assegnato un pulsante.

Per attivare il reporting Video Heartbeat dopo la [configurazione della suite di rapporti Analytics  per il reporting](#adobe-analytics-report-suite-for-video-reporting)video:

* Creare un servizio cloud [Analytics](#aem-analytics-cloud-service-configuration)
* Abilita [Analytics per un sito community](#enable-analytics-for-a-community-site)
* Associare il sito `Marketing Cloud Org Id` alla community

L&#39; `Marketing Cloud Org Id` indicazione può essere effettuata al momento della creazione [del sito](/help/communities/sites-console.md#enablement) comunitario o successivamente, [modificando](/help/communities/sites-console.md#modifying-site-properties) le proprietà del sito comunitario. [](#aem-analytics-cloud-service-configuration)

![chlimage_1-177](assets/chlimage_1-177.png)

Quando Video Heartbeat  Analytics è abilitato, il codice JavaScript (JS) per il lettore video crea un&#39;istanza del codice della libreria heartbeat video (anche in JS) che gestisce tutte le logiche per l&#39;invio di aggiornamenti dello stato video ai server di tracciamento video  Analytics ogni 10 secondi (non configurabili) e alla fine invia un rapporto cumulativo della sessione video ai server Analytics  principali.

Se non è attivato, il codice heartbeat video non viene mai istanziato e solo l&#39;avanzamento video e il tracciamento della posizione di ripresa vengono memorizzati nell&#39;SRP per il reporting.

## Configurazione di AEM  Analytics Cloud Service {#aem-analytics-cloud-service-configuration}

Per creare una nuova integrazione Analytics , che integra Adobe  Analytics con il sito della community AEM, utilizzate l’interfaccia utente standard nell’istanza di creazione:

* Dalla navigazione globale: **[!UICONTROL Strumenti > Distribuzione > Servizi cloud]**
* Scorri verso il basso fino ad **[!UICONTROL Adobe  Analytics]**
* Seleziona **[!UICONTROL Configura ora]** o **[!UICONTROL Mostra configurazioni]**

![chlimage_1-178](assets/chlimage_1-178.png)

### Finestra di dialogo Crea configurazione {#create-configuration-dialog}

* Seleziona `[+]` l&#39;icona accanto a **[!UICONTROL Configurazioni]** disponibili per creare una nuova configurazione

Nella finestra di dialogo Crea configurazione, i valori da immettere identificano la configurazione.

![chlimage_1-179](assets/chlimage_1-179.png)

* **Titolo**

   (Obbligatorio) Un titolo di visualizzazione per la configurazione.
Ad esempio, immettete *Enablement Community  Analytics*

* **Nome**

   (Facoltativo) Se non viene specificato, per impostazione predefinita il nome verrà impostato su un nome di nodo valido derivato dal titolo.
For example, enter *communities*

* **Modello**

   Seleziona `Adobe Analytics Configuration`

* Seleziona **Crea**

   * Avvia la pagina di configurazione e apre la `Analytics Settings` finestra di dialogo

###  finestra di dialogo Impostazioni Analytics {#analytics-settings-dialog}

La creazione iniziale di una nuova configurazione  Analytics comporta la visualizzazione della configurazione e una nuova finestra di dialogo per l&#39;immissione delle  impostazioni Analytics. Questa finestra di dialogo richiede le informazioni [account](#prerequisites) preliminari ottenute dal rappresentante commerciale di riferimento.

![chlimage_1-180](assets/chlimage_1-180.png)

* **Azienda**

   Società associata all&#39;account Adobe  Analytics

* **Nome utente**

   Nome utente di accesso per l&#39;utente autorizzato a gestire l&#39;account Analytics 

* **Password**

   La password di accesso per l&#39;utente autorizzato

* **Datacenter**

   Selezionare il centro dati Analytics  che ospita la suite di rapporti

* **Non aggiungere tag di tracciamento alla pagina**

   Mantieni come predefinito (deselezionato)

* **Usa AppMeasurement**

   Mantieni come predefinito (deselezionato)

* **Non importare di notte le impression della pagina (creazione)**

   Mantieni come predefinito (deselezionato)

* **Non importare le impression pagina ogni notte (pubblicazione)** lasciare come predefinite (deselezionato)

Per salvare le impostazioni:

* Selezionate **Connect per  Analytics**

   * In caso contrario,

      * Verificare che le voci non contengano spazi iniziali
      * Provare un datacenter diverso
      * Contatta il rappresentante commerciale di riferimento

* Selezionare **OK**

![chlimage_1-181](assets/chlimage_1-181.png)

### Crea framework {#create-framework}

Dopo la configurazione corretta della connessione di base ad Adobe  Analytics, è necessario creare o modificare un framework per il sito della community. Lo scopo del framework è mappare le variabili delle funzioni Community (AEM) su  variabili Analytics (suite di rapporti).

* Selezionate `[+]` l&#39;icona accanto a **[!UICONTROL Framework]** disponibili per creare un nuovo framework

![chlimage_1-182](assets/chlimage_1-182.png)

* **Titolo**

   (Obbligatorio) Titolo visualizzato per frameworkAd esempio, immettere *Enablement Community Framework*

* **Nome**

   (Facoltativo) Se non viene specificato, per impostazione predefinita il nome verrà impostato su un nome di nodo valido derivato dal titolo.
For example, enter *communities*

* *Modello*

   Seleziona `Adobe Analytics Framework`

* Seleziona **Crea**

La creazione di  Analytics Framework apre il framework per la configurazione.

## Configurazione di AEM  Analytics Framework {#aem-analytics-framework-configuration}

Lo scopo del framework è mappare le variabili AEM su  variabili Analytics (eVar ed eventi). Le variabili Analytics  disponibili per la mappatura sono [definite nella suite](#adobe-analytics-report-suite-for-video-reporting)di rapporti.

![chlimage_1-183](assets/chlimage_1-183.png)

### Seleziona suite di rapporti {#select-report-suite}

Selezionate la suite di rapporti configurata per la generazione di rapporti video.

Se una suite di rapporti non è ancora stata creata o non è stata configurata correttamente, consulta la sezione precedente:
[Adobe  Analytics Report Suite for Video Reporting](#adobe-analytics-report-suite-for-video-reporting)

La barra laterale non è necessaria e può essere ridotta a icona in modo da non ostacolare l’accesso alle impostazioni Suite di rapporti.

#### Finestra di dialogo Suite di rapporti prima e dopo la selezione di &#39;Aggiungi elemento&#39; {#report-suites-dialog-before-and-after-selecting-add-item}

![chlimage_1-184](assets/chlimage_1-184.png)

1. Seleziona **Aggiungi elemento +**

   Vengono visualizzate due caselle a discesa.

1. Choose a `Report suite.`

   Le suite di rapporti associate all&#39;account Società sono disponibili per la selezione.

1. Selezionate **Sì** nella finestra di dialogo che si apre:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. Choose a `Run Mode`

1. Selezionate **Pubblica**

![chlimage_1-185](assets/chlimage_1-185.png)

Il servizio e il framework di Analytics Cloud ora sono completi. Le mappature verranno definite dopo la creazione di un sito community con questo servizio Analytics  abilitato.

## Abilitare  Analytics per un sito community {#enable-analytics-for-a-community-site}

### Abilita per nuovo sito community {#enable-for-new-community-site}

Per aggiungere il servizio cloud  Analytics durante [la creazione di un nuovo sito](/help/communities/sites-console.md)community:

* Nel passaggio 3, nella scheda [ANALYTICS](/help/communities/sites-console.md#analytics):
   * Selezionate la casella di controllo **Abilita  Analytics** .
   * Selezionate il framework dalla casella a discesa.

* Facoltativamente, tornate alla configurazione del framework Analytics  per regolare le mappature delle variabili.

### Abilita per sito community esistente {#enable-for-existing-community-site}

Per aggiungere il servizio cloud  Analytics a un sito [community](/help/communities/sites-console.md#modifying-site-properties)esistente:

* Andate alla console **Community > Siti** .
* Selezionate l&#39;icona Modifica sito della community.
* Selezionare le IMPOSTAZIONI.
* Nella sezione  Analytics:
   * Selezionate la casella di controllo **Abilita  Analytics** .
   * Scegliete il framework dalla casella a discesa.

* Facoltativamente, tornate alla configurazione del framework Analytics  per regolare le mappature delle variabili.

### Abilita per siti personalizzati {#enable-for-customized-sites}

Affinché il tracciamento  Analytics e l&#39;importazione funzionino correttamente per un sito community, deve essere presente un elemento pagina con gli attributi `scf-js-site-title` class e href. Nella pagina dovrebbe esistere un solo elemento di questo tipo, ad esempio in uno `sitepage.hbs` script non modificato per un sito community. Il valore di `siteUrl` viene estratto e inviato ad Adobe  Analytics come percorso *del* sito.

```xml
# present in default sitepage.hbs
# only one scf-js-site-title class should be included
# this example sets it to be hidden as it serves no visual purpose
<div
    class="navbar-brand scf-js-site-title"
    href="{{siteUrl}}.html"
    style="visibility: hidden;"
>
</div>
```

Per un sito **community** personalizzato che sovrappone lo `sitepage.hbs` script, accertatevi che l&#39;elemento sia presente. La `siteUrl`variabile viene impostata quando viene eseguito il rendering sul server prima di essere trasmessa al client.

Per un sito **AEM** generico che include componenti Community, ma non viene creato con la procedura guidata [di creazione del](/help/communities/sites-console.md)sito, è necessario aggiungere l’elemento. Il valore di href deve essere il percorso del sito. Ad esempio, se il percorso del sito è `/content/my/company/en`, utilizzate:

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

##  Analytics per le funzioni Community {#analytics-for-communities-features}

 Analytics viene utilizzato automaticamente per diverse funzioni di Communities.

La configurazione [](/help/sites-deploying/configuring-osgi.md)OSGi dell’ambiente di authoring `AEM Communities Analytics Component Configuration`fornisce un elenco dei componenti che sono stati strumentalizzati per  Analytics. La mappatura automatica delle variabili è determinata dai componenti elencati.

Se vengono creati nuovi componenti personalizzati dotati di strumenti per  Analytics, questi devono essere aggiunti a questo elenco di componenti configurati.

### Configurazione componente {#component-configuration}

![chlimage_1-185](assets/chlimage_1-186.png)

>[!NOTE]
>
>I componenti del giornale di registrazione vengono utilizzati per implementare la funzione blog.

### Mappata  Analytics alle variabili AEM {#mapped-analytics-to-aem-variables}

Una volta salvato il sito community con  abilitato Analytics e selezionato il framework di configurazione cloud, le variabili AEM saranno mappate automaticamente alle  eVar Analytics e agli eventi che iniziano rispettivamente con evar1 ed event1 e aumentano di 1.

Se utilizzate una suite di rapporti esistente che ha mappato una qualsiasi delle variabili all’interno di evar1 attraverso evar11 e event1 tramite event7, sarà necessario [ricompilare le variabili](#modifying-analytics-variable-mapping) AEM e ripristinare la mappatura originale.

Di seguito è riportato un esempio di mappature predefinite dopo aver seguito l&#39;esercitazione [introduttiva](/help/communities/getting-started-enablement.md):

![chlimage_1-187](assets/chlimage_1-187.png)

#### Mappa delle eVar inviate con ogni evento {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Tipo risorsa<br /> abilitazione<br /></strong></td>
   <td><strong>Titolo sito<br /></strong></td>
   <td><strong>Tipo di funzione<br /></strong></td>
   <td><strong>Titolo gruppo<br /></strong></td>
   <td><strong>Group<br /> Path</strong></td>
   <td><strong>Tipo UGC<br /></strong></td>
   <td><strong>Titolo UGC<br /></strong></td>
   <td><strong>Utente<br /> (membro)</strong></td>
   <td><strong>Percorso UGC<br /></strong></td>
   <td><strong>Percorso sito<br /></strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>eVar4</strong></td>
   <td><strong>eVar5</strong></td>
   <td><strong>eVar6</strong></td>
   <td><strong>eVar7</strong></td>
   <td><strong>eVar8</strong></td>
   <td><strong>eVar9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>event1<br /> Resource Play</strong></td>
   <td><em>(a)</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>i)</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>(a)</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate (Post)</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
 </tbody>
</table>

**Esempi per i valori eVar:**

* *[Tipo](https://www.iana.org/assignments/media-types)*MIME: video/mp4
* *[titolo](/help/communities/sites-console.md#step13asitetemplate)*del sito community: Geometrixx Communities
* *[nome](/help/communities/functions.md)*funzione community: Forum
* *[nome](/help/communities/creating-groups.md#creating-a-new-group)*gruppo community: Escursione
* *percorso del contenuto* del gruppo community: `/content/sites/<site name>/en/groups/hiking`
* *[UGC component resourceType](/help/communities/essentials.md)*:`social/forum/components/hbs/topic`
* *Titolo* del componente UGC: Argomenti relativi all&#39;escursione
* *login (authorizableId)*: `aaron.mcdonald@mailinator.com`
* *Percorso SRP per UGC*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
o 
*percorso del componente da seguire*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *percorso del contenuto* del sito community: `/content/sites/<site name>/en`

### Modifica  mappatura variabile Analytics {#modifying-analytics-variable-mapping}

La mappatura di  eVar ed eventi Analytics alle variabili AEM è visibile dalla configurazione del framework dopo che  Analytics è abilitato per un sito community.

Dopo aver attivato  Analytics e prima della pubblicazione del sito community, la mappatura può essere modificata nel framework trascinando l&#39;evento o l&#39;evar Analytics desiderato  dalla barra a sinistra e rilasciandolo nella riga corrispondente nella tabella di mappatura.

Per evitare mappature duplicate, assicurarsi di rimuovere dalla riga l&#39;evento o l&#39;evento Analytics  sostituito posizionando il puntatore del mouse sopra di esso e selezionando la &quot;X&quot; che appare a destra dell&#39;elemento  variabile Analytics.

Se eVar ed eventi Community sovrascrivono mappature pre-esistenti nella suite di rapporti, quindi per evitare la perdita di dati, assegna le variabili AEM per le funzionalità Community ad altre eVar o eventi Analytics  e ripristina le mappature originali.

>[!CAUTION]
>
>È importante rimappare prima che il sito della community venga [pubblicato](#publishing-the-community-site) con  Analytics abilitato, altrimenti si rischia la perdita di dati.

#### Esempio 1: Trascinamento  Analytics evar14 nella tabella di mappatura {#example-step-dragging-analytics-evar-into-mapping-table}

![chlimage_1-188](assets/chlimage_1-188.png)

#### Esempio 2: Selezione di &#39;x&#39; per rimuovere evar11 sostituito {#example-step-selecting-x-to-remove-replaced-evar}

![chlimage_1-189](assets/chlimage_1-189.png)

#### Esempio 3: AEM var eventdata.siteId riassociato a  Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![chlimage_1-190](assets/chlimage_1-190.png)

## Pubblicazione del sito della community {#publishing-the-community-site}

### Verifica  mappatura variabile Analytics-AEM {#verify-analytics-to-aem-variable-mapping}

È consigliabile verificare la mappatura delle variabili prima di pubblicare il sito community, che pubblica anche il servizio e il framework cloud Analytics .

Vedere sezioni:

* [Mappata  Analytics alle variabili AEM](#mapped-analytics-to-aem-variables)
* [Modifica  mappatura variabile Analytics](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**Se si utilizza una suite di rapporti esistente che utilizza già variabili all&#39;interno di**
>
>* Da **`evar1`** a **`evar11`**
   >
   >
* Da **`event1`** a **`event7`**
>
>
**Prima della pubblicazione del sito della community,** è importante ripristinare la mappatura preesistente e spostare le variabili AEM di Communities che venivano mappate automaticamente (quando  Analytics era abilitato per il sito della community) su altre variabili Analytics . La nuova mappatura deve essere coerente tra tutti i componenti Community.
>
>In caso contrario si potrebbe determinare una perdita di dati non recuperabile.

### Editore principale {#primary-publisher}

Se la distribuzione scelta è una farm [di](/help/communities/topologies.md#tarmk-publish-farm)pubblicazione, un&#39;istanza di pubblicazione AEM deve essere identificata come editore principale per il polling di Adobe  Analytics affinché i dati del rapporto scrivano all&#39; [SRP](/help/communities/working-with-srp.md).

Per impostazione predefinita, la configurazione `AEM Communities Publisher Configuration` OSGi identifica l’istanza di pubblicazione come editore principale, in modo che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino automaticamente come principale.

Pertanto, è necessario modificare la configurazione in tutte le istanze di pubblicazione secondarie per deselezionare la casella di controllo Editore **** principale.

Per istruzioni specifiche, consultate la sezione relativa all&#39;editore principale di [Distribuzione di Communities](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>È importante che l’editore principale sia configurato per impedire il polling da più istanze di pubblicazione.

### Replicare la chiave Crypto {#replicate-the-crypto-key}

Le credenziali Adobe  Analytics sono crittografate. Per facilitare la replica o la trasmissione di credenziali di analisi crittografate tra autori ed editori, tutte le istanze AEM devono condividere la stessa chiave di crittografia primaria.

A tale scopo, seguire le istruzioni in [Replica della chiave](/help/communities/deploy-communities.md#replicate-the-crypto-key)di crittografia.

### Pubblica sito community e  Analytics Cloud Service {#publish-community-site-and-analytics-cloud-service}

Una volta che il servizio cloud  Analytics è stato abilitato per un sito community e, se necessario, è stata modificata [la](#mapped-analytics-to-aem-variables)mappatura di  variabili Analytics su AEM, è necessario replicare la configurazione nell&#39;ambiente di pubblicazione [(ri)pubblicando nuovamente il sito](/help/communities/sites-console.md#publishing-the-site)community.

## Come ottenere rapporti da  Analytics {#obtaining-reports-from-analytics}

### Gestione report {#report-management}

La configurazione [](/help/sites-deploying/configuring-osgi.md)OSGi dell’autore e dell’editore principale, `AEM Communities Analytics Report Management`, viene utilizzata per eseguire query  Analytics.

In fase di creazione, le query sono per report in tempo reale.

Nell&#39;editore principale, le query vengono utilizzate per fornire informazioni in preparazione all&#39;importazione di dati Analytics da parte dell&#39;importatore di report.

L&#39;intervallo di query predefinito è 10 secondi.

### Importatore report {#report-importer}

Una volta pubblicato  sito community abilitato per Analytics, la configurazione [](/help/sites-deploying/configuring-osgi.md)OSGi dell&#39;editore principale può essere configurata `AEM Communities Analytics Report Importer`per impostare l&#39;intervallo di polling predefinito per le configurazioni che non sono configurate singolarmente in CRXDE.

L’intervallo di polling controlla la frequenza delle richieste ad Adobe  Analytics per il pulling e il salvataggio dei dati nell’ [SRP](/help/communities/working-with-srp.md).

Quando i dati possono essere classificati come &quot;grandi dati&quot;, sondaggi più frequenti potrebbero mettere un carico elevato sul sito della comunità.

L’intervallo **predefinito di** importazione polling è impostato su 12 ore.

![chlimage_1-191](assets/chlimage_1-191.png)

### Personalizzazione report componente {#component-report-customization}

Al momento, per personalizzare le metriche da monitorare, nell&#39;archivio vengono creati nodi che definiscono i periodi di tempo per i quali generare un rapporto su tale metrica.

L&#39;argomento forum è attualmente l&#39;unico esempio di questa personalizzazione:

* Nell&#39;editore principale, effettuate l&#39;accesso con privilegi amministrativi.
* Passare a [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Ad esempio, [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* Sotto il nodo jcr:content della directory principale della lingua (ad esempio, `/content/sites/engage/en/jcr:content),`andate al componente configurato per  report Analytics).
Esempio, **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Osservate i periodi di tempo creati:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Osservate il `total`nodo.

   * Modificando la **`interval`** proprietà si sostituisce l&#39;intervallo Importazione report.
   * Il valore è espresso in secondi ed è impostato su 4 ore (14400 secondi).

![chlimage_1-192](assets/chlimage_1-192.png)

## Gestione dei dati utente in  Analytics {#manage-user-data-in-analytics}

Adobe  Analytics fornisce API che consentono di accedere, esportare ed eliminare dati utente. Per ulteriori informazioni, vedere [Sottomettere richieste](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/gdpr_submit_access_delete.html)di accesso ed eliminazione.

## Riferimenti {#resources}

* Adobe Marketing Cloud : [Guida di  Analytics e riferimento](https://marketing.adobe.com/resources/help/en_US/reference/)
* AEM: [Integrating with Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics con fornitori esterni](/help/sites-administering/external-providers.md)

