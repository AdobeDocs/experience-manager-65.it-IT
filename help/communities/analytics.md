---
title: Configurazione di Analytics per le funzioni di Communities
seo-title: Analytics Configuration for Communities Features
description: Configurare Analytics per Communities
seo-description: Configure analytics for Communities
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
role: Admin
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
source-git-commit: 9f9f80eb4cb74b687c7fadd41d0f8ea4ee967865
workflow-type: tm+mt
source-wordcount: '2694'
ht-degree: 4%

---

# Configurazione di Analytics per le funzioni di Communities {#analytics-configuration-for-communities-features}

## Panoramica {#overview}

Adobe Analytics e Adobe Experience Manager (AEM) sono entrambe soluzioni di Adobe Marketing Cloud.

Adobe Analytics può essere configurato per AEM Communities in modo che, quando un membro interagisce con le funzioni di Communities supportate, gli eventi vengano inviati ad Adobe Analytics da cui vengono generati i rapporti.

Ad esempio, dal sito della community, gli amministratori possono visualizzare vari rapporti relativi alla riproduzione del video.

Inoltre, Analytics è necessario per:

* Nell’ambiente di pubblicazione:

   * Relazioni sulla community [tendenze](/help/communities/trends.md)
   * Consentire ai visitatori del sito di ordinare per &quot;più visualizzati&quot;, &quot;più attivi&quot;, &quot;più apprezzati&quot;
   * Visualizza i conteggi negli elenchi UGC

* Nell’ambiente di authoring:

   * Visualizzazione dei dati di partecipazione nel [console gestione membri](/help/communities/members.md) (visualizzazioni, post, segui, mi piace)
   * Riepilogo tendenze, heartbeat video e dispositivo video per risorsa di abilitazione [rapporti](/help/communities/reports.md)

Le funzioni supportate per Communities includono:

* [Forum](/help/communities/forum.md)
* [D/R](/help/communities/working-with-qna.md)
* [Blog](/help/communities/blog-feature.md)
* [Libreria file](/help/communities/file-library.md)
* [Calendario](/help/communities/calendar.md)

Questa sezione della documentazione descrive come collegare una suite di rapporti di Analytics con le funzioni di Communities. I passaggi di base sono i seguenti:

1. [Replica la chiave di crittografia](#replicate-the-crypto-key) per garantire che la crittografia/decrittografia venga eseguita correttamente in tutte le istanze AEM
1. Preparare un’Adobe Analytics [suite di rapporti](#adobe-analytics-report-suite-for-video-reporting)
1. Creare un’analisi dell’AEM [servizio cloud](#aem-analytics-cloud-service-configuration) e [framework](#aem-analytics-framework-configuration)

1. [Abilita analisi](#enable-analytics-for-a-community-site) per un sito community
1. [**Verifica**](#verify-analytics-to-aem-variable-mapping) Mappatura delle variabili da Analytics a AEM
1. Identificare [editore principale](#primary-publisher)
1. [Pubblica](#publish-community-site-and-analytics-cloud-service) il sito community
1. Configura [importazione dei dati del rapporto](#obtaining-reports-from-analytics) da Adobe Analytics al sito community

## Prerequisiti {#prerequisites}

Per configurare le funzioni di Analytics for Communities, è necessario collaborare con il rappresentante del tuo account per impostare un account Adobe Analytics e [suite di rapporti](#adobe-analytics-report-suite-for-video-reporting). Una volta stabilite, dovrebbero essere disponibili le seguenti informazioni:

* **Nome dell’azienda**

   Azienda associata all’account Adobe Analytics.

* **Nome utente**

   Il nome utente di accesso per l’utente autorizzato a gestire l’account Analytics (deve includere i privilegi di accesso al servizio Web).

* **Password**

   Password di accesso per l&#39;utente autorizzato.

* **Data center di Analytics**

   L’URL del data center di Analytics per l’account.

* **Suite per report**

   Nome della suite di rapporti di Analytics da utilizzare.

## Suite di rapporti Adobe Analytics per reporting video {#adobe-analytics-report-suite-for-video-reporting}

Utilizzo di Adobe Marketing Cloud [Report Suite Manager](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html), le suite di rapporti di Analytics possono essere configurate in modo da abilitare un sito community per fornire rapporti sulle funzioni di Communities.

Accedendo a [Adobe Experience Cloud](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) con [Nome società e nome utente](/help/communities/analytics.md#prerequisites), è possibile configurare una suite di rapporti nuova o esistente in modo che abbia:

* [11 Variabili di conversione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) (eVar)

   * **`evar1`** da a **`evar11`** abilitato

   * È possibile riutilizzare (rinominare) le eVar esistenti o crearne di nuove da utilizzare per le funzioni community

* [7 eventi di successo](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/success-events/success-event.html) (eventi)

   * **`event1`** da a **`event7`** abilitato

   * tipo **`Counter`**

      * non **`Counter (no subrelations)`**
   * Possibilità di riutilizzare (rinominare) gli eventi esistenti o crearne di nuovi da utilizzare per le funzionalità delle community


* [Gestione video](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)

   * Console di reporting video

      * Attiva `Video Core`
      * Seleziona Salva
   * Console di misurazione Core video

      * Seleziona `Use Solution Variables`
      * Seleziona Salva


Se si utilizza un **nuova suite di rapporti**, tieni presente che una nuova suite di rapporti può avere solo 4 evar e 6 variabili evento, mentre per le community sono necessarie 11 evar e 7 variabili evento.

Se utilizzi un’ **suite di rapporti esistente**, può essere necessario [modificare la mappatura delle variabili](#modifying-analytics-variable-mapping) prima di attivare il framework Analytics per un sito community.

Contatta il rappresentante del tuo account per eventuali problemi relativi alle variabili dedicate alle community.

>[!CAUTION]
>
>**Se utilizzi una suite di rapporti esistente che utilizza già variabili in**
>
>* Da **`evar1`** a **`evar11`**
>
>* Da **`event1`** a **`event7`**
>
>**Quindi, prima della pubblicazione del sito della community,** è importante ripristinare la mappatura preesistente spostando le variabili AEM mappate automaticamente sulle variabili di Analytics quando Analytics era abilitato per un sito community.
>
>Per ripristinare la mappatura preesistente e spostare le variabili AEM in altre variabili Analytics, vedi la sezione su [Modifica della mappatura delle variabili di Analytics](#modifying-analytics-variable-mapping).
>
>In caso contrario, potrebbe verificarsi una perdita di dati irreversibile.

### Video Heartbeat Analytics {#video-heartbeat-analytics}

Quando Video Heartbeat Analytics è concesso in licenza, `Marketing Cloud Org Id` è assegnato.

Per abilitare il reporting Video Heartbeat dopo [configurazione della suite di rapporti di Analytics per il reporting video](#adobe-analytics-report-suite-for-video-reporting):

* Creare un [Servizio cloud Analytics](#aem-analytics-cloud-service-configuration)
* Abilita [Analytics per un sito community](#enable-analytics-for-a-community-site)
* Associa `Marketing Cloud Org Id` con il sito community

Il `Marketing Cloud Org Id` possono essere inserite al momento del [creazione di siti community](/help/communities/sites-console.md) o in un secondo momento da [modifica](/help/communities/sites-console.md#modifying-site-properties) proprietà del sito community.

![marketing-org-id](assets/marketing-org-id.png)

Quando Video Heartbeat Analytics è abilitato, il codice JavaScript (JS) per il lettore video crea un’istanza del codice della libreria heartbeat video (anche in JS) che gestisce tutta la logica per l’invio degli aggiornamenti dello stato video ai server di tracciamento video di Analytics ogni 10 secondi (non configurabile) e alla fine l’invio di un rapporto cumulativo della sessione video ai server Analytics principali.

Se non è abilitata, non viene mai creata un&#39;istanza del codice heartbeat video e solo l&#39;avanzamento video e il tracciamento della posizione di ripresa vengono salvati in modo permanente in SRP per il reporting.

## Configurazione servizio Analytics Cloud AEM {#aem-analytics-cloud-service-configuration}

Per creare una nuova integrazione Analytics, che integri Adobe Analytics con il sito della community AEM, utilizzando l’interfaccia utente standard nell’istanza di authoring:

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud Services]**
* Scorri verso il basso fino a **[!UICONTROL Adobe Analytics]**
* Seleziona **[!UICONTROL Configura ora]** o **[!UICONTROL Mostra configurazioni]**

![cloud-config](assets/cloud-config1.png)

### Finestra di dialogo Crea configurazione {#create-configuration-dialog}

* Seleziona `[+]` icona accanto a **[!UICONTROL Configurazioni disponibili]** per creare una nuova configurazione

Nella finestra di dialogo Crea configurazione, i valori da immettere identificano la configurazione.

![create-cloud-config](assets/cloud-config2.png)

* **Titolo**

   (Obbligatorio) Titolo da visualizzare per la configurazione.
Ad esempio, immetti *Analisi community*

* **Nome**

   (Facoltativo) Se non viene specificato, per impostazione predefinita il nome verrà impostato su un nome di nodo valido derivato dal titolo.
Ad esempio, immetti *community*

* **Modello**

   Seleziona `Adobe Analytics Configuration`

* Seleziona **Crea**

   * Viene visualizzata la pagina di configurazione dei lanci `Analytics Settings` finestra di dialogo

### Finestra di dialogo Impostazioni di Analytics {#analytics-settings-dialog}

La creazione iniziale di una nuova configurazione di Analytics comporta la visualizzazione della configurazione e una nuova finestra di dialogo per l’immissione delle impostazioni di Analytics. Questa finestra richiede [informazioni sui prerequisiti per l&#39;account](#prerequisites) ottenuti dal rappresentante del conto.

![analytics-settings](assets/analytics-settings.png)

* **Azienda**

   Azienda associata all’account Adobe Analytics.

* **Nome utente**

   Il nome utente di accesso per l’utente autorizzato a gestire l’account Analytics.

* **Password**

   Password di accesso per l&#39;utente autorizzato.

* **Datacenter**

   Seleziona il data center di Analytics che ospita la suite di rapporti.

* **Non aggiungere tag di tracciamento alla pagina**

   Lascia come predefinito (deselezionato).

* **Usa AppMeasurement**

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

* Seleziona **OK**.

   ![analytics-settings](assets/analytics-settings1.png)

### Crea framework {#create-framework}

Dopo aver configurato correttamente la connessione di base ad Adobe Analytics, è necessario creare o modificare un framework per il sito community. Lo scopo del framework è quello di mappare le variabili della funzione Communities (AEM) alle variabili di Analytics (suite di rapporti).

* Seleziona `[+]` icona accanto a **[!UICONTROL Framework disponibili]** per creare un nuovo framework

   ![analytics-framework](assets/analytics-framework.png)

* **Titolo**

   (Obbligatorio) Titolo da visualizzare per il framework. Ad esempio, immettere *Quadro comunitario*.

* **Nome**

   (Facoltativo) Se non viene specificato, per impostazione predefinita il nome verrà impostato su un nome di nodo valido derivato dal titolo.
Ad esempio, immetti *community*.

* *Modello*

   Seleziona `Adobe Analytics Framework`.

* Seleziona **Crea**.

La creazione del framework di Analytics apre il framework per la configurazione.

## Configurazione framework analisi AEM {#aem-analytics-framework-configuration}

Lo scopo del framework è quello di mappare le variabili AEM alle variabili Analytics (eVar ed eventi). Le variabili di Analytics disponibili per la mappatura sono [definito nella suite di rapporti](#adobe-analytics-report-suite-for-video-reporting).

![analytics-framework](assets/analytics-framework1.png)

### Seleziona suite di rapporti {#select-report-suite}

Seleziona la suite di rapporti che è stata configurata per il reporting video.

Se una suite di rapporti non è ancora stata creata o non è configurata correttamente, vedi la sezione precedente:
[Suite di rapporti Adobe Analytics per reporting video](#adobe-analytics-report-suite-for-video-reporting)

La barra laterale non è necessaria e può essere ridotta a icona in modo da non ostacolare l’accesso alle impostazioni delle suite di rapporti.

#### Finestra di dialogo Suite di rapporti prima e dopo aver selezionato &quot;Aggiungi elemento&quot; {#report-suites-dialog-before-and-after-selecting-add-item}

![report-suite](assets/report-suite.png)

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

Il servizio cloud Analytics e il framework sono stati completati. Le mappature verranno definite dopo la creazione di un sito community con questo servizio Analytics abilitato.

## Abilitare Analytics per un sito community {#enable-analytics-for-a-community-site}

### Abilita per nuovo sito community {#enable-for-new-community-site}

Per aggiungere il servizio cloud Analytics durante [creazione di un nuovo sito community](/help/communities/sites-console.md):

* Nel passaggio 3, sotto [Scheda ANALYTICS](/help/communities/sites-console.md#analytics):
   * Seleziona la **Abilita analisi** casella di controllo.
   * Selezionare il framework dalla casella a discesa.

* Se necessario, torna alla configurazione del framework Analytics per regolare le mappature delle variabili.

### Abilita per sito community esistente {#enable-for-existing-community-site}

Per aggiungere il servizio cloud Analytics a una [sito community esistente](/help/communities/sites-console.md#modifying-site-properties):

* Accedi a **Community > Siti** console.
* Selezionare l&#39;icona Modifica sito del sito community.
* Selezionare SETTINGS.
* Nella sezione Analytics:
   * Seleziona la **Abilita analisi** casella di controllo.
   * Scegliere il framework dalla casella a discesa.

* Se necessario, torna alla configurazione del framework Analytics per regolare le mappature delle variabili.

### Abilita per siti personalizzati {#enable-for-customized-sites}

Affinché il tracciamento e l&#39;importazione di Analytics funzionino correttamente per un sito community, un elemento di pagina con `scf-js-site-title` gli attributi class e href devono essere presenti. Nella pagina deve esistere un solo elemento di questo tipo, come accade in un elemento non modificato `sitepage.hbs` script per un sito community. Il valore di `siteUrl` viene estratto e inviato ad Adobe Analytics come *percorso del sito*.

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

Per un **sito community personalizzato** che si sovrappone al `sitepage.hbs` , verificare che l&#39;elemento sia presente. Il `siteUrl` verrà impostata al momento del rendering sul server prima di servire il client.

Per un **sito AEM generico** che include i componenti di Communities, ma non viene creato con [creazione guidata sito](/help/communities/sites-console.md), è necessario aggiungere l’elemento. Il valore di href deve essere il percorso del sito. Ad esempio, se il percorso del sito è `/content/my/company/en`, quindi utilizza:

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

dell’ambiente di authoring [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration`, fornisce un elenco dei componenti instrumentati per Analytics. La mappatura automatica delle variabili è determinata dai componenti elencati.

Se vengono creati nuovi componenti personalizzati instrumentati per Analytics, questi devono essere aggiunti a questo elenco di componenti configurati.

### Configurazione componente {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>I componenti del diario vengono utilizzati per implementare la funzione blog.

### Analisi mappata alle variabili AEM {#mapped-analytics-to-aem-variables}

Una volta salvato il sito community con Analytics abilitato e il framework di configurazione cloud selezionato, le variabili AEM verranno mappate automaticamente sulle eVar e sugli eventi di Analytics che iniziano rispettivamente con evar1 ed event1 e incrementano di 1.

Se utilizzi una suite di rapporti esistente che ha mappato una qualsiasi delle variabili all’interno di evar1 fino a evar11 ed event1 fino a event7, sarà necessario: [rimappare le variabili AEM](#modifying-analytics-variable-mapping) e ripristina la mappatura originale.

Di seguito è riportato un esempio di mappature predefinite:

![map-analytics](assets/map-analytics1.png)

#### Mappa delle eVar inviate con ogni evento {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Abilitazione<br /> Risorsa<br /> Tipo</strong></td>
   <td><strong>Sito<br /> Titolo</strong></td>
   <td><strong>Funzione<br /> Tipo</strong></td>
   <td><strong>Gruppo<br /> Titolo</strong></td>
   <td><strong>Gruppo<br /> Percorso</strong></td>
   <td><strong>UGC<br /> Tipo</strong></td>
   <td><strong>UGC<br /> Titolo</strong></td>
   <td><strong>Utente<br /> (Membro)</strong></td>
   <td><strong>UGC<br /> Percorso</strong></td>
   <td><strong>Sito<br /> Percorso</strong></td>
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
   <td><strong>event1<br /> Riproduzione risorse</strong></td>
   <td><em>(a)</em></td>
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
   <td><strong>event2<br /> Visualizzazione SCFV</strong></td>
   <td><em>(a)</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate (Post)</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> Scorri verso l'alto</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> ScorriInBasso</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i) IT</em></td>
   <td><em>j)</em></td>
  </tr>
 </tbody>
</table>

**Esempi di valori eVar:**

* *[Tipo MIME](https://www.iana.org/assignments/media-types)*: video/mp4
* *[titolo del sito community](/help/communities/sites-console.md#step13asitetemplate)*: GEOMETRIXX
* *[nome funzione community](/help/communities/functions.md)*: Forum
* *[nome gruppo community](/help/communities/creating-groups.md#creating-a-new-group)*: Trekking
* *percorso del contenuto del gruppo community*: `/content/sites/<site name>/en/groups/hiking`
* *[ResourceType del componente UGC](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *Titolo componente UGC*: Argomenti trekking
* *login (authorizableId)*: `aaron.mcdonald@mailinator.com`
* *Percorso SRP a UGC*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
o 
*percorso del componente da seguire*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *percorso del contenuto del sito community*: `/content/sites/<site name>/en`

### Modifica della mappatura delle variabili di Analytics {#modifying-analytics-variable-mapping}

La mappatura di eVar ed eventi di Analytics alle variabili AEM è visibile dalla configurazione del framework dopo l’abilitazione di Analytics per un sito community.

Dopo aver abilitato Analytics e prima della pubblicazione del sito community, la mappatura può essere modificata nel framework trascinando l’evento o la variabile Analytics desiderata dalla barra a sinistra e rilasciandola nella riga pertinente nella tabella di mappatura.

Per evitare mappature duplicate, assicurati di rimuovere l’evar o l’evento Analytics sostituito dalla riga passando con il mouse sopra di esso e selezionando la &quot;X&quot; che appare a destra dell’elemento variabile Analytics.

Se le eVar e gli eventi di Communities sovrascrivono le mappature preesistenti nella suite di rapporti, per evitare perdite di dati assegna le variabili AEM per le funzioni Communities ad altre eVar o eventi di Analytics e ripristina le mappature originali.

>[!CAUTION]
>
>È importante ripetere la mappatura prima che il sito community sia [pubblicato](#publishing-the-community-site) con Analytics abilitato, altrimenti si corre il rischio di perdita di dati.

#### Esempio di passaggio 1: trascinare Analytics evar14 nella tabella di mappatura {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### Esempio di passaggio 2: selezione di &quot;x&quot; per rimuovere evar11 sostituito {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### Esempio di passaggio 3: AEM var eventdata.siteId rinominato in Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## Pubblicazione del sito community {#publishing-the-community-site}

### Verificare la mappatura delle variabili da Analytics a AEM {#verify-analytics-to-aem-variable-mapping}

È consigliabile verificare la mappatura delle variabili prima di pubblicare il sito community, che pubblica anche il servizio cloud Analytics e il framework.

Vedere le sezioni:

* [Analisi mappata alle variabili AEM](#mapped-analytics-to-aem-variables)
* [Modifica della mappatura delle variabili di Analytics](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**Se utilizzi una suite di rapporti esistente che utilizza già variabili in**
>
>* Da **`evar1`** a **`evar11`**
>
>* Da **`event1`** a **`event7`**
>
>**Quindi, prima della pubblicazione del sito della community,** è importante ripristinare la mappatura preesistente e spostare le variabili AEM delle community mappate automaticamente (quando Analytics era abilitato per il sito community) su altre variabili di Analytics. Questa nuova mappatura deve essere coerente tra tutti i componenti di Communities.
>
>In caso contrario, potrebbe verificarsi una perdita di dati irreversibile.

### Editore primario {#primary-publisher}

Quando la distribuzione scelta è un [farm di pubblicazione](/help/communities/topologies.md#tarmk-publish-farm), quindi un’istanza di pubblicazione AEM deve essere identificata come l’editore primario per il polling di Adobe Analytics per i dati del rapporto in cui scrivere [SRP](/help/communities/working-with-srp.md).

Per impostazione predefinita, il `AEM Communities Publisher Configuration` La configurazione OSGi identifica la propria istanza di pubblicazione come editore principale, in modo che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino autonomamente come principale.

Pertanto, è necessario modificare la configurazione su tutte le istanze di pubblicazione secondarie per deselezionare **Editore primario** casella di controllo.

Per istruzioni specifiche, consulta la sezione dell’editore principale di [Distribuzione delle community](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>È importante che l’editore principale sia configurato in modo da impedire il polling da più istanze di pubblicazione.

### Replica la chiave di crittografia {#replicate-the-crypto-key}

Le credenziali di Adobe Analytics sono crittografate. Per facilitare la replica o la trasmissione delle credenziali di analisi crittografate tra l’autore e gli editori, tutte le istanze AEM devono condividere la stessa chiave di crittografia primaria.

Per farlo, segui le istruzioni all’indirizzo [Replica la chiave di crittografia](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Pubblica sito community e servizio Analytics Cloud {#publish-community-site-and-analytics-cloud-service}

Dopo aver abilitato Analytics Cloud Service per un sito community e, se necessario, [la mappatura delle variabili da Analytics a AEM è stata corretta](#mapped-analytics-to-aem-variables), è necessario replicare la configurazione nell’ambiente di pubblicazione tramite [(ri)pubblicazione del sito community](/help/communities/sites-console.md#publishing-the-site).

## Ottenimento di rapporti da Analytics {#obtaining-reports-from-analytics}

### Gestione dei rapporti {#report-management}

Autore ed editore principale [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`, viene utilizzato per eseguire query in Analytics.

Per l’autore, le query sono per i rapporti in tempo reale.

Nell’editore principale, le query vengono utilizzate per fornire informazioni in preparazione all’importazione dei dati analitici di Report Importer.

L’intervallo di query predefinito è 10 secondi.

### Importazione report {#report-importer}

Dopo la pubblicazione di un sito community abilitato per Analytics, l&#39;autore principale [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`, può essere configurato per impostare l’intervallo di polling predefinito per le configurazioni che non sono configurate singolarmente in CRXDE.

L’intervallo di polling controlla la frequenza delle richieste ad Adobe Analytics per il recupero e il salvataggio dei dati [SRP](/help/communities/working-with-srp.md).

Quando i dati possono essere classificati come &quot;big data&quot;, i polling più frequenti possono comportare un carico elevato sul sito della community.

Polling predefinito **Intervallo di importazione** è impostato su 12 ore.

![report-importer](assets/report-importer.png)

### Personalizzazione dei rapporti dei componenti {#component-report-customization}

Attualmente, per personalizzare le metriche da monitorare, nell’archivio vengono creati nodi che definiscono i periodi di tempo per i quali generare un rapporto su tale metrica.

L’argomento del forum è attualmente l’unico esempio di questa personalizzazione:

* Nel server di pubblicazione principale, accedere con privilegi amministrativi.
* Accedi a [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Ad esempio: [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* Sotto il nodo jcr:content della directory principale della lingua (ad esempio `/content/sites/engage/en/jcr:content),`passa al componente configurato per la generazione di rapporti di Analytics.
Ad esempio **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Osserva i periodi di tempo creati:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Osserva `total`nodo.

   * Modifica di **`interval`** sostituisce l&#39;intervallo di Importazione report.
   * Il valore è in secondi ed è impostato su 4 ore (14400 secondi).

![component-report](assets/component-report.png)

## Gestire i dati utente in Analytics {#manage-user-data-in-analytics}

Adobe Analytics fornisce API che ti consentono di accedere, esportare ed eliminare dati utente. Per ulteriori informazioni, consulta [Inviare richieste di accesso e cancellazione](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

## Riferimenti {#resources}

* Adobe Experience Cloud: [Guida e riferimento di Analytics](https://experienceleague.adobe.com/docs/analytics.html)
* AEM: [Integrazione con Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics con provider esterni](/help/sites-administering/external-providers.md)
