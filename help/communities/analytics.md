---
title: Configurazione di Analytics per le funzioni di Communities
description: Scopri come configurare Adobe Analytics per AEM Communities in modo che, quando un membro interagisce con le funzioni di Communities supportate, gli eventi vengano inviati ad Adobe Analytics.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2658'
ht-degree: 1%

---

# Configurazione di Analytics per le funzioni di Communities {#analytics-configuration-for-communities-features}

## Panoramica {#overview}

Adobe Analytics e Adobe Experience Manager (AEM) sono entrambe soluzioni di Adobe Experience Cloud.

Adobe Analytics può essere configurato per AEM Communities in modo che, quando un membro interagisce con le funzioni di Communities supportate, gli eventi vengano inviati ad Adobe Analytics da cui vengono generati i rapporti.

Ad esempio, dal sito della community, gli amministratori possono visualizzare vari rapporti relativi alla riproduzione del video.

Inoltre, Analytics è necessario per:

* Nell’ambiente Publish:

   * Generazione di rapporti sulle [tendenze](/help/communities/trends.md) della community
   * Consentire ai visitatori del sito di ordinare per &quot;più visualizzati&quot;, &quot;più attivi&quot;, &quot;più apprezzati&quot;
   * Visualizza conteggi in elenchi UGC (User-Generated Content)

* Nell’ambiente di authoring:

   * Visualizzazione dei dati di partecipazione nella [console di gestione membri](/help/communities/members.md) (visualizzazioni, post, operazioni seguenti, Mi piace)
   * Riepilogo tendenze, heartbeat video e dispositivo video per la risorsa di abilitazione [rapporti](/help/communities/reports.md)

Le funzioni supportate per Communities includono:

* [Forum](/help/communities/forum.md)
* [D/R](/help/communities/working-with-qna.md)
* [Blog](/help/communities/blog-feature.md)
* [Libreria file](/help/communities/file-library.md)
* [Calendario](/help/communities/calendar.md)

Questa sezione della documentazione descrive come collegare una suite di rapporti di Analytics con le funzioni di Communities. I passaggi di base sono i seguenti:

1. [Replica la chiave di crittografia](#replicate-the-crypto-key) per verificare che la crittografia/decrittografia venga eseguita correttamente in tutte le istanze AEM
1. Prepara una [suite di rapporti](#adobe-analytics-report-suite-for-video-reporting) di Adobe Analytics
1. Crea un [servizio cloud](#aem-analytics-cloud-service-configuration) e un [framework](#aem-analytics-framework-configuration) di analisi AEM

1. [Abilitare Analytics](#enable-analytics-for-a-community-site) per un sito community
1. [**Verifica**](#verify-analytics-to-aem-variable-mapping) mappatura variabile da Analytics a AEM
1. Identifica [editore primario](#primary-publisher)
1. [Publish](#publish-community-site-and-analytics-cloud-service) il sito della community
1. Configura [l&#39;importazione dei dati del report](#obtaining-reports-from-analytics) da Adobe Analytics al sito community

## Prerequisiti {#prerequisites}

Per configurare le funzionalità di Analytics for Communities, è necessario collaborare con il rappresentante del tuo account per impostare un account Adobe Analytics e [una suite di rapporti](#adobe-analytics-report-suite-for-video-reporting). Una volta stabilite, dovrebbero essere disponibili le seguenti informazioni:

* **Nome società**

  Azienda associata all’account Adobe Analytics.

* **Nome utente**

  Nome utente di accesso per l’utente autorizzato a gestire l’account Analytics
(deve includere i privilegi di accesso al servizio Web).

* **Password**

  Password di accesso per l&#39;utente autorizzato.

* **Centro dati di Analytics**

  L’URL del data center di Analytics per l’account.

* **Suite di rapporti**

  Nome della suite di rapporti di Analytics da utilizzare.

## Suite di rapporti Adobe Analytics per reporting video {#adobe-analytics-report-suite-for-video-reporting}

Utilizzando la [Gestione suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/new-report-suite.html?lang=it) di Adobe Experience Cloud, è possibile configurare le suite di rapporti di Analytics in modo che un sito community possa essere abilitato per fornire rapporti per le funzioni di Communities.

Effettuando l&#39;accesso a [Adobe Experience Cloud](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=it) con [Nome società e Nome utente](/help/communities/analytics.md#prerequisites), è possibile configurare una suite di rapporti nuova o esistente con:

* [11 Variabili di conversione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/conversion-var-admin.html?lang=it) (eVars)

   * Da **`evar1`** a **`evar11`** abilitato

   * Possibilità di riutilizzare (rinominare) le eVar esistenti o crearne di da utilizzare per le funzioni community

* [7 eventi di successo](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/success-events/success-event.html?lang=it) (eventi)

   * Da **`event1`** a **`event7`** abilitato

   * tipo **`Counter`**

      * non **`Counter (no subrelations)`**

   * È possibile riutilizzare (rinominare) gli eventi esistenti o crearne di nuovi da utilizzare per le funzioni di Communities

* [Gestione video](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=it)

   * Console di reporting video

      * Abilita `Video Core`
      * Seleziona Salva

   * Console di misurazione Core video

      * Seleziona `Use Solution Variables`
      * Seleziona Salva

Se utilizzi una **nuova suite di rapporti**, una nuova suite di rapporti può contenere solo 4 eVar e 6 variabili evento, mentre per le community sono necessarie 11 e 7 variabili evento.

Se utilizzi una **suite di rapporti esistente**, potrebbe essere necessario [modificare la mappatura delle variabili](#modifying-analytics-variable-mapping) prima di attivare il framework Analytics per un sito community.

Contatta il rappresentante del tuo account per eventuali problemi relativi alle variabili dedicate alle community.

>[!CAUTION]
>
>**Se si utilizza una suite di rapporti esistente che utilizza già variabili in**
>
>* Da **`evar1`** a **`evar11`**
>
>* Da **`event1`** a **`event7`**
>
>**Quindi, prima della pubblicazione del sito della community,** è importante ripristinare la mappatura preesistente spostando le variabili AEM mappate automaticamente alle variabili di Analytics quando Analytics era abilitato per un sito della community.
>
>Per ripristinare la mappatura preesistente e spostare le variabili AEM in altre variabili Analytics, vedere la sezione relativa alla [modifica della mappatura delle variabili Analytics](#modifying-analytics-variable-mapping).
>
>In caso contrario, potrebbe verificarsi una perdita di dati irreversibile.

### Video Heartbeat Analytics {#video-heartbeat-analytics}

Quando Video Heartbeat Analytics è concesso in licenza, viene assegnato `Marketing Cloud Org Id`.

Per abilitare il reporting Video Heartbeat dopo [la configurazione della suite di rapporti Analytics per il reporting video](#adobe-analytics-report-suite-for-video-reporting):

* Crea un servizio [Analytics Cloud](#aem-analytics-cloud-service-configuration)
* Abilita [Analytics per un sito community](#enable-analytics-for-a-community-site)
* Associa `Marketing Cloud Org Id` al sito community

`Marketing Cloud Org Id` può essere immesso al momento della [creazione del sito community](/help/communities/sites-console.md) o successiva [modifica](/help/communities/sites-console.md#modifying-site-properties) le proprietà del sito community.

![marketing-org-id](assets/marketing-org-id.png)

Quando Video Heartbeat Analytics è abilitato, il codice JavaScript (JS) del lettore video crea un’istanza del codice libreria heartbeat video (anche in JS). Il codice gestisce tutte le logiche per l’invio degli aggiornamenti dello stato video ai server di tracciamento video di Analytics ogni 10 secondi (non configurabile). Alla fine invia un rapporto cumulativo della sessione video ai server principali di Analytics.

Se non è abilitata, non viene mai creata un&#39;istanza del codice heartbeat video e solo l&#39;avanzamento video e il tracciamento della posizione di ripresa vengono salvati in modo permanente in SRP per il reporting.

## Configurazione servizio Analytics Cloud AEM {#aem-analytics-cloud-service-configuration}

Per creare un’integrazione Analytics, che integri Adobe Analytics con il sito della community AEM, utilizzando l’interfaccia utente standard nell’istanza di authoring:

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud Service]**
* Scorri verso il basso fino a **[!UICONTROL Adobe Analytics]**
* Seleziona **[!UICONTROL Configura ora]** o **[!UICONTROL Mostra configurazioni]**

![cloud-config](assets/cloud-config1.png)

### Finestra di dialogo Crea configurazione {#create-configuration-dialog}

* Seleziona l&#39;icona `[+]` accanto a **[!UICONTROL Configurazioni disponibili]** per creare una configurazione.

Nella finestra di dialogo Crea configurazione, i valori da immettere identificano la configurazione.

![create-cloud-config](assets/cloud-config2.png)

* **Titolo**

  (Obbligatorio) Titolo da visualizzare per la configurazione.
Ad esempio, immetti *Analytics community*

* **Nome**

  (Facoltativo) Se non viene specificato, per impostazione predefinita il nome corrisponde a un nome di nodo valido derivato dal titolo.
Ad esempio, immettere *community*

* **Modello**

  Seleziona `Adobe Analytics Configuration`

* Seleziona **Crea**

   * Avvia la pagina di configurazione e apre la finestra di dialogo `Analytics Settings`

### Finestra di dialogo Impostazioni di Analytics {#analytics-settings-dialog}

La creazione iniziale di una nuova configurazione di Analytics comporta la visualizzazione della configurazione e una nuova finestra di dialogo per l’immissione delle impostazioni di Analytics. Questa finestra di dialogo richiede le [informazioni sui prerequisiti](#prerequisites) ottenute dal rappresentante dell&#39;account.

![impostazioni-analisi](assets/analytics-settings.png)

* **Società**

  Azienda associata all’account Adobe Analytics.

* **Nome utente**

  Il nome utente di accesso per l’utente autorizzato a gestire l’account Analytics.

* **Password**

  Password di accesso per l&#39;utente autorizzato.

* **Centro dati**

  Seleziona il data center di Analytics che ospita la suite di rapporti.

* **Non aggiungere tag di tracciamento alla pagina**

  Lascia come predefinito (deselezionato).

* **Utilizza AppMeasurement**

  Lascia come predefinito (deselezionato).

* **Non importare di notte le impression della pagina (creazione)**

  Lascia come predefinito (deselezionato).

* **Non importare di notte le impression della pagina (pubblicazione)**

  Lascia come predefinito (deselezionato).

Per salvare le impostazioni:

* Seleziona **Connetti ad Analytics**

   * In caso contrario,

      * Verificare che le voci non contengano spazi iniziali.
      * Prova con un altro centro dati.

* Selezionare **OK**.

  ![impostazioni-analisi](assets/analytics-settings1.png)

### Crea framework {#create-framework}

Dopo aver configurato correttamente la connessione di base ad Adobe Analytics, è necessario creare o modificare un framework per il sito community. Lo scopo del framework è quello di mappare le variabili della funzione Communities (AEM) alle variabili di Analytics (suite di rapporti).

* Seleziona l&#39;icona `[+]` accanto a **[!UICONTROL framework disponibili]** per creare un framework.

  ![analytics-framework](assets/analytics-framework.png)

* **Titolo**

  (Obbligatorio) Titolo da visualizzare per il framework
Ad esempio, immettere *Framework community*.

* **Nome**

  (Facoltativo) Se non viene specificato, per impostazione predefinita il nome corrisponde a un nome di nodo valido derivato dal titolo.
Ad esempio, immettere *community*.

* *Modello*

  Selezionare `Adobe Analytics Framework`.

* Seleziona **Crea**.

La creazione del framework di Analytics apre il framework per la configurazione.

## Configurazione framework analisi AEM {#aem-analytics-framework-configuration}

Lo scopo del framework è quello di mappare le variabili AEM alle variabili Analytics (eVar ed eventi). Le variabili di Analytics disponibili per la mappatura sono [definite nella suite di rapporti](#adobe-analytics-report-suite-for-video-reporting).

![analytics-framework](assets/analytics-framework1.png)

### Seleziona suite di rapporti {#select-report-suite}

Seleziona la suite di rapporti che è stata configurata per il reporting video.

Se una suite di rapporti non è ancora stata creata o non è configurata correttamente, vedi la sezione precedente:
[Suite di rapporti Adobe Analytics per reporting video](#adobe-analytics-report-suite-for-video-reporting)

Il Sidekick non è necessario e può essere ridotto a icona in modo da non ostacolare l’accesso alle impostazioni delle suite di rapporti.

#### Finestra di dialogo Suite di rapporti prima e dopo aver selezionato &quot;Aggiungi elemento&quot; {#report-suites-dialog-before-and-after-selecting-add-item}

![suite di rapporti](assets/report-suite.png)

1. Seleziona **Aggiungi elemento +**.

   Vengono visualizzate due caselle a discesa.

1. Scegli un `Report suite.`

   Le suite di rapporti associate all’account aziendale sono disponibili per la selezione.

1. Seleziona **Sì** nella finestra di dialogo visualizzata:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. Scegli un `Run Mode`.

1. Seleziona **Pubblica**.

![analytics-framework2](assets/analytics-framework2.png)

Il servizio cloud Analytics e il framework sono stati completati. Le mappature vengono definite dopo la creazione di un sito community con questo servizio Analytics abilitato.

## Abilitare Analytics per un sito community {#enable-analytics-for-a-community-site}

### Abilita per nuovo sito community {#enable-for-new-community-site}

Per aggiungere il servizio Analytics Cloud durante la [creazione di un sito community](/help/communities/sites-console.md):

* Nel passaggio 3, nella [scheda ANALYTICS](/help/communities/sites-console.md#analytics):
   * Selezionare la casella di controllo **Abilita analisi**.
   * Selezionare il framework dalla casella a discesa.

* Se necessario, torna alla configurazione del framework Analytics per regolare le mappature delle variabili.

### Abilita per sito community esistente {#enable-for-existing-community-site}

Per aggiungere il servizio Analytics Cloud a un [sito community esistente](/help/communities/sites-console.md#modifying-site-properties):

* Passa alla console **Community > Sites**.
* Selezionare l&#39;icona Modifica sito del sito community.
* Selezionare SETTINGS.
* Nella sezione Analytics:
   * Selezionare la casella di controllo **Abilita analisi**.
   * Scegliere il framework dalla casella a discesa.

* Se necessario, torna alla configurazione del framework Analytics per regolare le mappature delle variabili.

### Abilita per siti personalizzati {#enable-for-customized-sites}

Affinché il tracciamento e l&#39;importazione di Analytics funzionino correttamente per un sito community, è necessario che sia presente un elemento pagina con la classe `scf-js-site-title` e gli attributi href. Nella pagina deve essere presente un solo elemento di questo tipo, come nel caso di uno script `sitepage.hbs` non modificato per un sito community. Il valore di `siteUrl` viene estratto e inviato ad Adobe Analytics come *percorso sito*.

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

Per un **sito community personalizzato** che si sovrappone allo script `sitepage.hbs`, verificare che l&#39;elemento sia presente. La variabile `siteUrl` viene impostata quando viene riprodotta sul server prima di essere trasmessa al client.

Per un **sito AEM generico** che include componenti di Communities ma non è stato creato con la [procedura guidata per la creazione del sito](/help/communities/sites-console.md), è necessario aggiungere l&#39;elemento. Il valore di href deve essere il percorso del sito. Ad esempio, se il percorso del sito è `/content/my/company/en`, utilizzare:

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Funzioni di Analytics per Communities {#analytics-for-communities-features}

Analytics viene utilizzato automaticamente per diverse funzioni di Communities.

La [configurazione OSGi](/help/sites-deploying/configuring-osgi.md) dell&#39;ambiente di authoring, `AEM Communities Analytics Component Configuration`, fornisce un elenco dei componenti instrumentati per Analytics. La mappatura automatica delle variabili è determinata dai componenti elencati.

Se vengono creati nuovi componenti personalizzati instrumentati per Analytics, questi devono essere aggiunti a questo elenco di componenti configurati.

### Configurazione componente {#component-configuration}

![configurazione-componente1](assets/component-configuration1.png)

>[!NOTE]
>
>I componenti del diario vengono utilizzati per implementare la funzione blog.

### Analisi mappata alle variabili AEM {#mapped-analytics-to-aem-variables}

Dopo il salvataggio del sito community, con Analytics abilitato e il framework di configurazione cloud selezionato, le variabili AEM vengono mappate automaticamente sulle eVar e sugli eventi di Analytics. Inizia rispettivamente con evar1 ed event1 e viene incrementato di 1.

Se si utilizza una suite di rapporti esistente che ha mappato una qualsiasi delle variabili all&#39;interno di evar1 fino a evar11 ed event1 fino a event7, diventa necessario [rimappare le variabili AEM](#modifying-analytics-variable-mapping) e ripristinare la mappatura originale.

Di seguito è riportato un esempio di mappature predefinite:

![map-analytics](assets/map-analytics1.png)

#### Mappa delle eVar inviate con ogni evento {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Tipo di risorsa <br /> di attivazione<br /></strong></td>
   <td><strong>Titolo sito<br /></strong></td>
   <td><strong>Tipo di funzione <br /></strong></td>
   <td><strong>Titolo gruppo<br /></strong></td>
   <td><strong>Percorso gruppo <br /></strong></td>
   <td><strong>Tipo UGC<br /></strong></td>
   <td><strong>Titolo UGC<br /></strong></td>
   <td><strong>Utente <br /> (membro)</strong></td>
   <td><strong>Percorso UGC<br /></strong></td>
   <td><strong>Percorso <br /> sito</strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>EVAR 1</strong></td>
   <td><strong>EVAR 2</strong></td>
   <td><strong>EVAR 3</strong></td>
   <td><strong>EVAR 4</strong></td>
   <td><strong>EVAR 5</strong></td>
   <td><strong>EVAR 6</strong></td>
   <td><strong>EVAR 7</strong></td>
   <td><strong>EVAR 8</strong></td>
   <td><strong>EVAR 9</strong></td>
   <td><strong>eVar 10</strong></td>
  </tr>
  <tr>
   <td><strong>event1<br /> Riproduzione risorse</strong></td>
   <td><em>a) IT</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>i) IT</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>a) IT</em></td>
   <td><em>b) IT</em></td>
   <td><em>c) IT</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate (Post)</strong></td>
   <td><em>-</em></td>
   <td><em>b) IT</em></td>
   <td><em>c) IT</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>b) IT</em></td>
   <td><em>c) IT</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>b) IT</em></td>
   <td><em>c) IT</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>b) IT</em></td>
   <td><em>c) IT</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>b) IT</em></td>
   <td><em>c) IT</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
 </tbody>
</table>

**Esempi per valori eVar:**

* *[Tipo MIME](https://www.iana.org/assignments/media-types/media-types.xhtml)*: video/mp4
* *[titolo del sito community](/help/communities/sites-console.md#step13asitetemplate)*: Geometrixx
* *[nome funzione community](/help/communities/functions.md)*: forum
* *[nome gruppo community](/help/communities/creating-groups.md#creating-a-new-group)*: trekking
* *percorso del contenuto del gruppo community*: `/content/sites/<site name>/en/groups/hiking`
* *[Tipo risorsa componente UGC](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *Titolo componente UGC*: argomenti trekking
* *accesso (authorizableId)*: `aaron.mcdonald@mailinator.com`
* *Percorso SRP per UGC*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
o *percorso del componente da seguire*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *percorso del contenuto del sito community*: `/content/sites/<site name>/en`

### Modifica della mappatura delle variabili di Analytics {#modifying-analytics-variable-mapping}

La mappatura di eVar ed eventi di Analytics alle variabili AEM è visibile dalla configurazione del framework dopo l’abilitazione di Analytics per un sito community.

Dopo l&#39;abilitazione di Analytics e prima della pubblicazione del sito community, la mappatura può essere modificata nel framework. Trascina la eVar o l’evento di Analytics desiderato dalla barra a sinistra e rilascialo nella riga pertinente nella tabella di mappatura.

Per evitare mappature duplicate, assicurati di rimuovere l’evar o l’evento Analytics sostituito dalla riga passando con il mouse sopra di esso e selezionando la &quot;X&quot; che appare a destra dell’elemento variabile Analytics.

Se le eVar e gli eventi di Communities sovrascrivono le mappature preesistenti nella suite di rapporti, per evitare perdite di dati assegna le variabili AEM per le funzioni Communities ad altre eVar o eventi di Analytics e ripristina le mappature originali.

>[!CAUTION]
>
>È importante ripetere la mappatura prima che il sito community sia [pubblicato](#publishing-the-community-site) con Analytics abilitato, altrimenti si potrebbe verificare una perdita di dati.

#### Esempio di passaggio 1: trascinare Analytics evar14 nella tabella di mappatura {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### Esempio di passaggio 2: selezione di &quot;x&quot; per rimuovere evar11 sostituito {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### Esempio di passaggio 3: AEM var eventdata.siteId rinominato in Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## Pubblicazione del sito community {#publishing-the-community-site}

### Verificare la mappatura delle variabili da Analytics a AEM {#verify-analytics-to-aem-variable-mapping}

È consigliabile verificare la mappatura delle variabili prima di pubblicare il sito community, che pubblica anche il servizio e il framework di Analytics Cloud.

Vedere le sezioni:

* [Analisi mappata alle variabili AEM](#mapped-analytics-to-aem-variables)
* [Modifica della mappatura delle variabili di Analytics](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**Se si utilizza una suite di rapporti esistente che utilizza già variabili in**
>
>* Da **`evar1`** a **`evar11`**
>
>* Da **`event1`** a **`event7`**
>
>**Quindi, prima della pubblicazione del sito della community,** ripristina la mappatura preesistente. Sposta le variabili AEM delle community mappate automaticamente (quando Analytics era abilitato per il sito community) su altre variabili di Analytics. Questa mappatura deve essere coerente tra tutti i componenti di Communities.
>
>In caso contrario, potrebbe verificarsi una perdita di dati irreversibile.

### Editore primario {#primary-publisher}

Se la distribuzione scelta è una [farm di pubblicazione](/help/communities/topologies.md#tarmk-publish-farm), è necessario identificare un&#39;istanza di pubblicazione AEM come editore principale per il polling di Adobe Analytics per i dati del report da scrivere in [SRP](/help/communities/working-with-srp.md).

Per impostazione predefinita, la configurazione OSGi `AEM Communities Publisher Configuration` identifica la propria istanza di pubblicazione come editore principale, in modo che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino autonomamente come principale.

È pertanto necessario modificare la configurazione in tutte le istanze di pubblicazione secondarie per deselezionare la casella di controllo **Editore primario**.

Per istruzioni specifiche, vedere la sezione relativa all&#39;editore principale di [Distribuzione delle community](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>È importante che l’editore principale sia configurato in modo da impedire il polling da più istanze di pubblicazione.

### Replica la chiave di crittografia {#replicate-the-crypto-key}

Le credenziali di Adobe Analytics sono crittografate. Per facilitare la replica o la trasmissione delle credenziali di analisi crittografate tra l’autore e gli editori, tutte le istanze AEM devono condividere la stessa chiave di crittografia primaria.

A tale scopo, seguire le istruzioni in [Replica la chiave di crittografia](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Sito della community Publish e servizio Analytics Cloud {#publish-community-site-and-analytics-cloud-service}

Dopo che il servizio Analytics Cloud è stato abilitato per un sito community e, se necessario, la [mappatura delle variabili da Analytics a AEM è stata regolata](#mapped-analytics-to-aem-variables), replicare la configurazione nell&#39;ambiente di pubblicazione [(ri)pubblicando il sito community](/help/communities/sites-console.md#publishing-the-site).

## Ottenimento di rapporti da Analytics {#obtaining-reports-from-analytics}

### Gestione dei rapporti {#report-management}

La [configurazione OSGi](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`, dell&#39;autore e dell&#39;editore primario viene utilizzata per eseguire query in Analytics.

Per l’autore, le query sono per i rapporti in tempo reale.

Nell’editore principale, le query vengono utilizzate per fornire informazioni in preparazione all’importazione dei dati analitici di Report Importer.

L’intervallo di query predefinito è 10 secondi.

### Importazione report {#report-importer}

Dopo la pubblicazione di un sito community abilitato per Analytics, è possibile configurare la [configurazione OSGi](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`, dell&#39;editore primario per impostare l&#39;intervallo di polling predefinito per le configurazioni non configurate singolarmente in CRXDE.

L&#39;intervallo di polling controlla la frequenza delle richieste ad Adobe Analytics per i dati da estrarre e salvare in [SRP](/help/communities/working-with-srp.md).

Quando i dati possono essere classificati come &quot;big data&quot;, i polling più frequenti possono comportare un carico elevato sul sito della community.

Il polling predefinito **Intervallo di importazione** è impostato su 12 ore.

![report-importer](assets/report-importer.png)

### Personalizzazione dei rapporti dei componenti {#component-report-customization}

Attualmente, per personalizzare le metriche da monitorare, nell’archivio vengono creati nodi che definiscono i periodi di tempo per i quali generare un rapporto su tale metrica.

L’argomento del forum è attualmente l’unico esempio di questa personalizzazione:

* Nel server di pubblicazione principale, accedere con privilegi amministrativi.
* Passa a [CRXDE Liti](/help/sites-developing/developing-with-crxde-lite.md). Ad esempio, [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* Nel nodo `jcr:content` della directory principale della lingua (ad esempio, `/content/sites/engage/en/jcr:content`), passa al componente configurato per la generazione di rapporti di Analytics.
Ad esempio **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Osserva i periodi di tempo creati:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Osserva il nodo `total`.

   * La modifica della proprietà **`interval`** sovrascrive l&#39;intervallo di Importazione report.
   * Il valore è in secondi ed è impostato su quattro ore (14400 secondi).

![component-report](assets/component-report.png)

## Gestire i dati utente in Analytics {#manage-user-data-in-analytics}

Adobe Analytics fornisce API che ti consentono di accedere, esportare ed eliminare dati utente. Per ulteriori informazioni, vedere [Invia richieste di accesso ed eliminazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=it).

## Riferimenti {#resources}

* Adobe Experience Cloud: [Guida e riferimento di Analytics](https://experienceleague.adobe.com/docs/analytics.html?lang=it)
* AEM: [Integrazione con Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics con provider esterni](/help/sites-administering/external-providers.md)
