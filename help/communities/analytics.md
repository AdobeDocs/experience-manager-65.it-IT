---
title: Configurazione di Analytics per le funzioni Community
seo-title: Configurazione di Analytics per le funzioni Community
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
source-git-commit: ef57d53fc780bd222abbe994fc71e133ce8a77fc
workflow-type: tm+mt
source-wordcount: '2756'
ht-degree: 4%

---


# Configurazione di Analytics per le funzioni Community {#analytics-configuration-for-communities-features}

## Panoramica {#overview}

 Adobe Analytics e Adobe Experience Manager (AEM) sono entrambe soluzioni di Adobe Marketing Cloud.

 Adobe Analytics può essere configurato per  AEM Communities in modo che, quando un membro interagisce con le funzioni Community supportate, gli eventi vengano inviati  Adobe Analytics da cui vengono generati i rapporti.

Ad esempio, quando un membro di un sito community di abilitazione visualizza una risorsa video assegnata, il lettore delle risorse invia eventi ad Analytics, inclusi i dati heartbeat video. Dal sito della community, gli amministratori possono visualizzare vari rapporti sulla riproduzione del video.

Inoltre, l&#39;analisi è necessaria per:

* Nell’ambiente di pubblicazione:

   * Generazione di rapporti sulla community [trend](/help/communities/trends.md)
   * Possibilità per i visitatori del sito di ordinare per &quot;più visualizzati&quot;, &quot;più attivi&quot; o &quot;più graditi&quot;
   * Visualizzare i conteggi negli elenchi UGC

* Nell’ambiente di authoring:

   * Visualizzazione dei dati di partecipazione nella [console di gestione membri](/help/communities/members.md) (viste, post, segue, mi piace)
   * Riepilogo delle tendenze, heartbeat video e dispositivo video per le risorse di abilitazione [report](/help/communities/reports.md)

Le funzioni Community supportate includono:

* [Risorse di abilitazione](/help/communities/resources.md)
* [Forum](/help/communities/forum.md)
* [D/R](/help/communities/working-with-qna.md)
* [Blog](/help/communities/blog-feature.md)
* [Libreria file](/help/communities/file-library.md)
* [Calendario](/help/communities/calendar.md)

Questa sezione della documentazione descrive come collegare una suite di rapporti di Analytics alle funzioni di Communities. I passaggi di base sono:

1. [Replicare la ](#replicate-the-crypto-key) chiave di crittografia per garantire che la crittografia/decrittografia si verifichi correttamente su tutte le istanze AEM
1. Preparare una  Adobe Analytics [suite di rapporti](#adobe-analytics-report-suite-for-video-reporting)
1. Creare un servizio AEM di Analytics [cloud](#aem-analytics-cloud-service-configuration) e [framework](#aem-analytics-framework-configuration)

1. [Abilita ](#enable-analytics-for-a-community-site) analisi per un sito community
1. [****](#verify-analytics-to-aem-variable-mapping) VerifyAnalytics per AEM mappatura variabile
1. Identificare [editore principale](#primary-publisher)
1. [](#publish-community-site-and-analytics-cloud-service) Pubblicare il sito della community
1. Configura [importazione di dati del report](#obtaining-reports-from-analytics) da  Adobe Analytics al sito della community

## Prerequisiti {#prerequisites}

Per configurare le funzioni di Analytics for Communities, è necessario collaborare con il rappresentante commerciale di riferimento per impostare un account Adobe Analytics  e [suite di rapporti](#adobe-analytics-report-suite-for-video-reporting). Una volta stabilite, devono essere disponibili le seguenti informazioni:

* **Nome società**

   Società associata all&#39;account Adobe Analytics .

* **Nome utente**

   Nome utente di accesso per l&#39;utente autorizzato a gestire l&#39;account Analytics
(devono includere i privilegi di accesso al servizio Web).

* **Password**

   La password di accesso per l’utente autorizzato.

* **Centro dati di Analytics**

   L&#39;URL del centro dati di Analytics per l&#39;account.

* **Suite di rapporti**

   Nome della suite di rapporti di Analytics da utilizzare.

##  Adobe Analytics Report Suite for Video Reporting {#adobe-analytics-report-suite-for-video-reporting}

Utilizzando il [Report Suite Manager](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html) di Adobe Marketing Cloud, le suite di rapporti di Analytics possono essere configurate in modo che un sito community possa essere abilitato per fornire rapporti per le funzioni Community.

Effettuando l&#39;accesso a [Adobe Experience Cloud](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/home.html) con [Nome società e Nome utente](/help/communities/analytics.md#prerequisites), è possibile configurare una suite di rapporti nuova o esistente in modo che abbia:

* [11 Variabili](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html)  di conversione (eVar)

   * **`evar1`** tramite  **`evar11`** abilitato

   * Può riadattare (rinominare) le eVar esistenti o crearne di nuove da utilizzare per le funzioni Community

* [7 Eventi](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/success-events/success-event.html)  di successo (eventi)

   * **`event1`** tramite  **`event7`** abilitato

   * tipo **`Counter`**

      * not **`Counter (no subrelations)`**
   * Può riadattare (rinominare) gli eventi esistenti o crearne di nuovi da utilizzare per le funzioni Community


* [Gestione video](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)

   * Video Reporting console

      * Abilita `Video Core`
      * Seleziona Salva
   * Console di misurazione video

      * Seleziona `Use Solution Variables`
      * Seleziona Salva


Se utilizzate una **nuova suite di rapporti**, tenete presente che una nuova suite di rapporti può contenere solo 4 variabili evar e 6 variabili evento, mentre per le community sono necessarie 11 variabili evar e 7 variabili evento.

Se si utilizza una **suite di rapporti esistente**, potrebbe essere necessario modificare la mappatura della variabile](#modifying-analytics-variable-mapping) prima di attivare il framework Analytics per un sito community.[

Contatta il tuo rappresentante commerciale per qualsiasi dubbio sulle variabili dedicate alle Community.

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
**Quindi, prima della pubblicazione del sito community,** è importante ripristinare la mappatura preesistente spostando le variabili AEM che venivano automaticamente mappate sulle variabili Analytics quando Analytics era abilitato per un sito community.
>
>Per ripristinare la mappatura preesistente e spostare AEM variabili in altre variabili Analytics, consulta la sezione su [Modifica della mappatura delle variabili Analytics](#modifying-analytics-variable-mapping).
>
>In caso contrario si potrebbe determinare una perdita di dati non recuperabile.

### Video Heartbeat Analytics {#video-heartbeat-analytics}

Quando viene concessa la licenza di Video Heartbeat Analytics, viene assegnato un `Marketing Cloud Org Id`.

Per abilitare la generazione di report Video Heartbeat dopo [la configurazione della suite di rapporti Analytics per la generazione di report video](#adobe-analytics-report-suite-for-video-reporting):

* Creare un [servizio cloud di Analytics](#aem-analytics-cloud-service-configuration)
* Abilita [Analytics per un sito community](#enable-analytics-for-a-community-site)
* Associare il `Marketing Cloud Org Id` al sito della community

La `Marketing Cloud Org Id` può essere inserita al momento della [creazione del sito community](/help/communities/sites-console.md#enablement) o successivamente mediante la [modifica](/help/communities/sites-console.md#modifying-site-properties) delle proprietà del sito community. [](#aem-analytics-cloud-service-configuration)

![marketing-org-id](assets/marketing-org-id.png)

Quando Video Heartbeat Analytics è abilitato, il codice JavaScript (JS) per il lettore video crea un&#39;istanza del codice libreria heartbeat video (anche in JS) che gestisce tutte le logiche per l&#39;invio di aggiornamenti dello stato video ai server di tracciamento video di Analytics ogni 10 secondi (non configurabile) e alla fine invia un rapporto cumulativo della sessione video ai server Analytics principali.

Se non è attivato, il codice heartbeat video non viene mai istanziato e solo l&#39;avanzamento video e il tracciamento della posizione di ripresa vengono memorizzati nell&#39;SRP per il reporting.

## AEM  configurazione del servizio Analytics Cloud {#aem-analytics-cloud-service-configuration}

Per creare una nuova integrazione di Analytics, che integra  Adobe Analytics con il sito della community AEM, utilizzando l&#39;interfaccia utente standard nell&#39;istanza di creazione:

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud Services]**
* Scorri verso il basso fino a **[!UICONTROL Adobe Analytics]**
* Selezionare **[!UICONTROL Configura ora]** o **[!UICONTROL Mostra configurazioni]**

![cloud-config](assets/cloud-config1.png)

### Finestra di dialogo Crea configurazione {#create-configuration-dialog}

* Seleziona l&#39;icona `[+]` accanto a **[!UICONTROL Configurazioni disponibili]** per creare una nuova configurazione

Nella finestra di dialogo Crea configurazione, i valori da immettere identificano la configurazione.

![create-cloud-config](assets/cloud-config2.png)

* **Titolo**

   (Obbligatorio) Un titolo di visualizzazione per la configurazione.
Ad esempio, immettete *Enablement Community Analytics*

* **Nome**

   (Facoltativo) Se non viene specificato, per impostazione predefinita il nome verrà impostato su un nome di nodo valido derivato dal titolo.
Ad esempio, immettere *community*

* **Modello**

   Seleziona `Adobe Analytics Configuration`

* Seleziona **Crea**

   * Avvia la pagina di configurazione e apre la finestra di dialogo `Analytics Settings`

### Finestra di dialogo Impostazioni analisi {#analytics-settings-dialog}

La creazione iniziale di una nuova configurazione di Analytics determina la visualizzazione della configurazione e una nuova finestra di dialogo per l&#39;immissione delle impostazioni di Analytics. Questa finestra di dialogo richiede le [informazioni preliminari sull&#39;account](#prerequisites) ottenute dal rappresentante dell&#39;account.

![analytics-settings](assets/analytics-settings.png)

* **Azienda**

   Società associata all&#39;account Adobe Analytics .

* **Nome utente**

   Il nome utente di accesso per l&#39;utente autorizzato a gestire l&#39;account Analytics.

* **Password**

   La password di accesso per l’utente autorizzato.

* **Datacenter**

   Selezionate il centro dati di Analytics in cui è distribuita la suite di rapporti.

* **Non aggiungere tag di tracciamento alla pagina**

   Mantieni come predefinito (deselezionato).

* **Usa AppMeasurement**

   Mantieni come predefinito (deselezionato).

* **Non importare di notte le impression della pagina (creazione)**

   Mantieni come predefinito (deselezionato).

* **Non importare di notte le impression della pagina (pubblicazione)**

   Mantieni come predefinito (deselezionato).

Per salvare le impostazioni:

* Seleziona **Connetti ad Analytics**

   * In caso contrario,

      * Verificare che le voci non contengano spazi iniziali.
      * Prova a utilizzare un datacenter diverso.

* Selezionare **OK**.

   ![analytics-enablement-settings](assets/analytics-settings1.png)

### Crea framework {#create-framework}

Dopo aver configurato correttamente la connessione di base a  Adobe Analytics, è necessario creare o modificare un framework per il sito community. Lo scopo del framework è mappare le variabili delle funzioni (AEM) di Communities alle variabili di Analytics (suite di rapporti).

* Selezionate l&#39;icona `[+]` accanto a **[!UICONTROL Framework disponibili]** per creare un nuovo framework

   ![analytics-framework](assets/analytics-framework.png)

* **Titolo**

   (Obbligatorio) Titolo visualizzato per il framework
Ad esempio, immettere *Enablement Community Framework*.

* **Nome**

   (Facoltativo) Se non viene specificato, per impostazione predefinita il nome verrà impostato su un nome di nodo valido derivato dal titolo.
Ad esempio, immettere *community*.

* *Modello*

   Seleziona `Adobe Analytics Framework`.

* Seleziona **Crea**.

La creazione di Analytics Framework consente di aprire il framework per la configurazione.

## Configurazione AEM framework Analytics {#aem-analytics-framework-configuration}

Lo scopo del framework è quello di mappare AEM variabili alle variabili di Analytics (eVar ed eventi). Le variabili Analytics disponibili per la mappatura sono [definite nella suite di rapporti](#adobe-analytics-report-suite-for-video-reporting).

![analytics-enablement-framework](assets/analytics-framework1.png)

### Seleziona suite di rapporti {#select-report-suite}

Selezionate la suite di rapporti impostata per il reporting video.

Se una suite di rapporti non è ancora stata creata o non è stata configurata correttamente, consulta la sezione precedente:
[ Adobe Analytics Report Suite for Video Reporting](#adobe-analytics-report-suite-for-video-reporting)

La barra laterale non è necessaria e può essere ridotta a icona in modo da non ostacolare l’accesso alle impostazioni Suite di rapporti.

#### Finestra di dialogo Suite di rapporti prima e dopo la selezione di &#39;Aggiungi elemento&#39; {#report-suites-dialog-before-and-after-selecting-add-item}

![suite di rapporti](assets/report-suite.png)

1. Selezionare **Aggiungi elemento +**.

   Vengono visualizzate due caselle a discesa.

1. Scegliere `Report suite.`

   Le suite di rapporti associate all&#39;account Società sono disponibili per la selezione.

1. Selezionare **Sì** nella finestra di dialogo che si apre:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. Scegliete un elemento `Run Mode`.

1. Selezionate **Pubblica**.

![analytics-framework2](assets/analytics-framework2.png)

Il servizio e il framework di Analytics Cloud ora sono completi. Le mappature verranno definite dopo la creazione di un sito community con il servizio Analytics abilitato.

## Abilita Analytics per un sito community {#enable-analytics-for-a-community-site}

### Abilita per il nuovo sito community {#enable-for-new-community-site}

Per aggiungere il servizio cloud di Analytics durante la [creazione di un nuovo sito community](/help/communities/sites-console.md):

* Nel passaggio 3, nella scheda [ANALYTICS](/help/communities/sites-console.md#analytics):
   * Selezionare la casella di controllo **Abilita Analytics**.
   * Selezionate il framework dalla casella a discesa.

* Facoltativamente, tornate alla configurazione del framework Analytics per regolare le mappature delle variabili.

### Abilita per sito community esistente {#enable-for-existing-community-site}

Per aggiungere il servizio cloud di Analytics a un [sito community esistente](/help/communities/sites-console.md#modifying-site-properties):

* Andate alla console **Community > Siti**.
* Selezionate l&#39;icona Modifica sito della community.
* Selezionare le IMPOSTAZIONI.
* Nella sezione Analisi:
   * Selezionare la casella di controllo **Abilita Analytics**.
   * Scegliete il framework dalla casella a discesa.

* Facoltativamente, tornate alla configurazione del framework Analytics per regolare le mappature delle variabili.

### Abilita per siti personalizzati {#enable-for-customized-sites}

Affinché il monitoraggio e l&#39;importazione di Analytics funzioni correttamente per un sito community, è necessario che sia presente un elemento di pagina con gli attributi `scf-js-site-title` class e href. Nella pagina dovrebbe esistere un solo elemento di questo tipo, ad esempio in uno script `sitepage.hbs` non modificato per un sito community. Il valore di `siteUrl` viene estratto e inviato a  Adobe Analytics come percorso *del sito*.

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

Per un **sito community personalizzato** che sovrappone lo script `sitepage.hbs`, accertatevi che l&#39;elemento sia presente. La variabile `siteUrl` verrà impostata quando viene eseguito il rendering sul server prima di distribuirla al client.

Per un **sito AEM generico** che include componenti Community, ma non viene creato con la [procedura guidata di creazione del sito](/help/communities/sites-console.md), è necessario aggiungere l&#39;elemento. Il valore di href deve essere il percorso del sito. Ad esempio, se il percorso del sito è `/content/my/company/en`, utilizza:

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Funzioni di Analytics per community {#analytics-for-communities-features}

Analytics viene utilizzato automaticamente per diverse funzioni Community.

La [configurazione OSGi dell&#39;ambiente di authoring](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration` fornisce un elenco dei componenti che sono stati strumentalizzati per Analytics. La mappatura automatica delle variabili è determinata dai componenti elencati.

Se vengono creati nuovi componenti personalizzati dotati di strumenti per Analytics, questi devono essere aggiunti a questo elenco di componenti configurati.

### Configurazione componente {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>I componenti del giornale di registrazione vengono utilizzati per implementare la funzione blog.

### Analisi mappata su AEM variabili {#mapped-analytics-to-aem-variables}

Una volta salvato il sito community con Analytics abilitato e selezionato il framework di configurazione cloud, le variabili AEM verranno mappate automaticamente sulle eVar e sugli eventi di Analytics a partire rispettivamente da evar1 ed event1 e con un incremento di 1.

Se utilizzate una suite di rapporti esistente che ha mappato una qualsiasi delle variabili all&#39;interno di evar1 attraverso evar11 e event1 tramite event7, sarà necessario [modificare le variabili AEM](#modifying-analytics-variable-mapping) e ripristinare la mappatura originale.

Di seguito è riportato un esempio di mappature predefinite dopo aver seguito l&#39; [esercitazione introduttiva](/help/communities/getting-started-enablement.md):

![map-analytics](assets/map-analytics1.png)

#### Mappa delle eVar inviate con ogni evento {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Tipo di abilitazione<br /> Resource<br /></strong></td>
   <td><strong>Titolo del sito<br /></strong></td>
   <td><strong>Tipo funzione<br /></strong></td>
   <td><strong>Titolo gruppo<br /></strong></td>
   <td><strong>Percorso gruppo<br /></strong></td>
   <td><strong>Tipo UGC<br /></strong></td>
   <td><strong>Titolo UGC<br /></strong></td>
   <td><strong>Utente<br /> (membro)</strong></td>
   <td><strong>Percorso UGC<br /></strong></td>
   <td><strong>Percorso Site<br /></strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong> eVar1</strong></td>
   <td><strong> eVar 2</strong></td>
   <td><strong> eVar 3</strong></td>
   <td><strong> eVar 4</strong></td>
   <td><strong> eVar 5</strong></td>
   <td><strong> eVar 6</strong></td>
   <td><strong> eVar 7</strong></td>
   <td><strong> eVar 8</strong></td>
   <td><strong> eVar 9</strong></td>
   <td><strong> eVar10</strong></td>
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
   <td><em>i)</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>a)</em></td>
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
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>d)</em></td>
   <td><em>e)</em></td>
   <td><em>f)</em></td>
   <td><em>g)</em></td>
   <td><em>h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
 </tbody>
</table>

**Esempi per  valori eVar:**

* *[Tipo](https://www.iana.org/assignments/media-types)* MIME: video/mp4
* *[titolo](/help/communities/sites-console.md#step13asitetemplate)* del sito community: Geometrixx
* *[nome](/help/communities/functions.md)* funzione community: Forum
* *[nome](/help/communities/creating-groups.md#creating-a-new-group)* gruppo community: Escursione
* *percorso del contenuto* del gruppo community:  `/content/sites/<site name>/en/groups/hiking`
* *[UGC component resourceType](/help/communities/essentials.md)*:  `social/forum/components/hbs/topic`
* *Titolo* del componente UGC: Argomenti relativi all&#39;escursione
* *login (authorizableId)*:  `aaron.mcdonald@mailinator.com`
* *Percorso SRP per UGC*:  `/content/usergenerated/asi/.../forum/jmtz-topic3`
o 
*percorso del componente da seguire*:  `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *percorso del contenuto* del sito community:  `/content/sites/<site name>/en`

### Modifica mappatura variabili di Analytics {#modifying-analytics-variable-mapping}

La mappatura di eVar ed eventi di Analytics su variabili AEM è visibile dalla configurazione del framework dopo che Analytics è abilitato per un sito community.

Dopo l&#39;abilitazione di Analytics e prima della pubblicazione del sito community, la mappatura può essere modificata nel framework trascinando l&#39;evento o l&#39;evento Analytics desiderato dalla barra a sinistra e rilasciandolo nella riga corrispondente nella tabella di mappatura.

Per evitare mappature duplicate, accertatevi di rimuovere la variabile evar o l&#39;evento Analytics sostituito dalla riga posizionando il puntatore del mouse sopra di essa e selezionando la &quot;X&quot; che appare a destra dell&#39;elemento della variabile Analytics.

Se eVar ed eventi Community sovrascrivono mappature pre-esistenti nella suite di rapporti, quindi per evitare la perdita di dati, assegna le variabili AEM per le funzionalità Community ad altre eVar o eventi di Analytics e ripristina le mappature originali.

>[!CAUTION]
>
>È importante rimappare prima che il sito della community sia [pubblicato](#publishing-the-community-site) con Analytics abilitato, altrimenti esiste il rischio di perdita di dati.

#### Esempio 1: Trascinamento di Analytics evar14 nella tabella di mappatura {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### Esempio 2: Selezione di &#39;x&#39; per rimuovere evar11 sostituito {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### Esempio 3: AEM var eventdata.siteId è stato ricollegato ad Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## Pubblicazione del sito community {#publishing-the-community-site}

### Verifica analisi per AEM mappatura variabile {#verify-analytics-to-aem-variable-mapping}

È consigliabile verificare la mappatura delle variabili prima di pubblicare il sito community, che pubblica anche il servizio e il framework cloud di Analytics.

Vedere sezioni:

* [Analisi mappata su variabili AEM](#mapped-analytics-to-aem-variables)
* [Modifica della mappatura delle variabili di Analytics](#modifying-analytics-variable-mapping)

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
**Prima della pubblicazione del sito della community,** è importante ripristinare la mappatura preesistente e spostare le variabili Community AEM che sono state mappate automaticamente (quando Analytics era abilitato per il sito della community) ad altre variabili Analytics. La nuova mappatura deve essere coerente tra tutti i componenti Community.
>
>In caso contrario si potrebbe determinare una perdita di dati non recuperabile.

### Editore principale {#primary-publisher}

Se la distribuzione scelta è una [farm di pubblicazione](/help/communities/topologies.md#tarmk-publish-farm), un&#39;istanza di pubblicazione AEM deve essere identificata come editore principale per il polling  Adobe Analytics per i dati del report da scrivere in [SRP](/help/communities/working-with-srp.md).

Per impostazione predefinita, la configurazione `AEM Communities Publisher Configuration` OSGi identifica l’istanza di pubblicazione come editore principale, in modo che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino automaticamente come principale.

Pertanto, è necessario modificare la configurazione in tutte le istanze di pubblicazione secondarie per deselezionare la casella di controllo **Principale Editore**.

Per istruzioni specifiche, vedere la sezione relativa all&#39;editore principale di [Implementazione di Communities](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>È importante che l’editore principale sia configurato in modo da impedire il polling da più istanze di pubblicazione.

### Replicare la chiave di crittografia {#replicate-the-crypto-key}

Le credenziali Adobe Analytics  sono crittografate. Per facilitare la replica o la trasmissione di credenziali di analisi crittografate tra autori e editori, tutte AEM istanze devono condividere la stessa chiave di crittografia primaria.

A tal fine, seguire le istruzioni riportate in [Replicare la chiave di crittografia](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Pubblica sito community e  servizio Analytics Cloud {#publish-community-site-and-analytics-cloud-service}

Una volta che il servizio cloud di Analytics è stato abilitato per un sito community e, se necessario, la [mappatura di Analytics AEM variabili è stata modificata](#mapped-analytics-to-aem-variables), è necessario replicare la configurazione nell&#39;ambiente di pubblicazione [(ri)pubblicando il sito community](/help/communities/sites-console.md#publishing-the-site).

## Come ottenere report da Analytics {#obtaining-reports-from-analytics}

### Gestione report {#report-management}

La configurazione [OSGi dell&#39;autore e dell&#39;editore principale ](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`, viene utilizzata per eseguire query in Analytics.

In fase di creazione, le query sono per report in tempo reale.

Nell&#39;editore principale, le query vengono utilizzate per fornire informazioni in preparazione all&#39;importazione di dati Analytics da parte dell&#39;importatore di report.

L&#39;intervallo di query predefinito è 10 secondi.

### Importatore report {#report-importer}

Dopo la pubblicazione di un sito community abilitato per Analytics, la configurazione [OSGi dell&#39;editore principale](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer` può essere configurata per impostare l&#39;intervallo di polling predefinito per le configurazioni che non sono configurate singolarmente in CRXDE.

L&#39;intervallo di polling controlla la frequenza delle richieste inviate a  Adobe Analytics per estrarre e salvare i dati in [SRP](/help/communities/working-with-srp.md).

Quando i dati possono essere classificati come &quot;grandi dati&quot;, sondaggi più frequenti potrebbero mettere un carico elevato sul sito della comunità.

Il polling predefinito **Intervallo di importazione** è impostato su 12 ore.

![importatore di report](assets/report-importer.png)

### Personalizzazione report componente {#component-report-customization}

Al momento, per personalizzare le metriche da monitorare, nell&#39;archivio vengono creati nodi che definiscono i periodi di tempo per i quali generare un rapporto su tale metrica.

L&#39;argomento forum è attualmente l&#39;unico esempio di questa personalizzazione:

* Nell&#39;editore principale, effettuate l&#39;accesso con privilegi amministrativi.
* Passare a [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Ad esempio, [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* Sotto il nodo jcr:content della directory principale della lingua (ad esempio `/content/sites/engage/en/jcr:content),`andate al componente configurato per il reporting di Analytics.
Esempio, **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Osservate i periodi di tempo creati:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Osservate il nodo `total`.

   * La modifica della proprietà **`interval`** ha la priorità sull&#39;intervallo di importazione dei report.
   * Il valore è espresso in secondi ed è impostato su 4 ore (14400 secondi).

![report componente](assets/component-report.png)

## Gestione dei dati utente in Analytics {#manage-user-data-in-analytics}

 Adobe Analytics fornisce API che consentono di accedere, esportare ed eliminare dati utente. Per ulteriori informazioni, vedere [Invia richieste di accesso ed eliminazione](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html).

## Riferimenti {#resources}

* Adobe Experience Cloud: [Guida e riferimento di Analytics](https://docs.adobe.com/content/help/en/analytics/landing/home.html)
* AEM: [Integrazione con  Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics con provider esterni](/help/sites-administering/external-providers.md)
