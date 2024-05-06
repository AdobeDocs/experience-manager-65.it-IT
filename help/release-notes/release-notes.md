---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: Trova informazioni sulla versione, novità, procedure guidate di installazione e un elenco dettagliato delle modifiche per [!DNL Adobe Experience Manager] 6.5
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 14b52e7763c4d83a4dcce593f155cb1bb8f56b97
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | Giovedì 23 maggio 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Cosa è incluso in [!DNL Experience Manager] 6.5.21.0 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] La versione 6.5.21.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti, correzioni di bug e miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la disponibilità iniziale della versione 6.5 di aprile 2019. [Installa questo Service Pack](#install) il [!DNL Experience Manager] 6.5

<!-- UPDATE FOR EACH NEW RELEASE -->

## Funzioni principali e miglioramenti

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Alcune delle funzioni e dei miglioramenti principali di questa versione includono:

* Una credenziale nuova e più semplice da utilizzare per l’autenticazione da server a server, che sostituisce la credenziale esistente dell’account di servizio (JWT). (NPR-41994) PRINCIPALE

### [!DNL Forms]

* A

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Problemi risolti in Service Pack 21 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### Accessibilità {#sites-accessibility-6521}

* Il **[!UICONTROL Ricerche salvate]** l’etichetta non è persistente. Il segnaposto viene utilizzato come unica etichetta visiva per un campo di testo. (SITES-3050)

#### Interfaccia utente amministratore{#sites-adminui-6521}

* Quando fai clic su **[!UICONTROL Sites]** > **[!UICONTROL Componenti core]** > **[!UICONTROL Proprietà]** > **[!UICONTROL Autorizzazioni]** scheda > **[!UICONTROL Autorizzazione effettiva]**, il **Autorizzazioni effettive** non si apre in. (SITES-17378)

#### Interfaccia classica{#sites-classicui-6521}

* M

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* È stata corretta la doppia inclusione degli elementi modulo. (SITES-21109) BLOCCANTE
* Durante la creazione di un frammento di contenuto, a volte il pulsante Chiudi non risponde e l’intera pagina viene bloccata e richiede un aggiornamento per chiuderlo. Per quanto riguarda il problema di creazione della versione, il sistema sta creando una nuova versione di un frammento di contenuto. Ciò si verifica anche quando l’utente non ha apportato alcuna modifica, semplicemente interagendo con l’editor Rich Text o un campo di testo. (SITES-21187) PRINCIPALE


#### [!DNL Content Fragments] - API GRAPHQL {#sites-graphql-api-6521}

* Durante l’aggiornamento di Adobe Experience Manager da 6.5.19.0 a 6.5.20.0, il percorso `/libs/cq/graphql/sites/graphiql` Eliminazione in corso. (SITES-20098) CRITICO




#### [!DNL Content Fragments] - Editor query di GraphQL{#sites-graphql-query-editor-6521}

* Me

#### [!DNL Content Fragments] - API REST{#sites-restapi-6521}

* Me

#### Back-end core{#sites-core-backend-6521}

* Me

#### Componenti core{#sites-core-components-6521}

* I

#### Integrazione di Campaign{#sites-campaign-integration-6521}

* A

#### Frammenti di esperienza{#sites-experiencefragments-6521}

* Rollout di frammenti esperienza da `masters/language` a `country/language` non aggiorna i riferimenti incrociati. (SITES-20559) BLOCCANTE
* Modelli non solo specificati in `cq:allowedTemplates`, ma modelli che hanno `allowedPaths` configurati a livello di modello, vengono visualizzati come opzioni durante la creazione di un nuovo frammento di esperienza. (SITES-20855) PRINCIPALE

#### Componenti di base (legacy){#sites-foundation-components-legacy-6521}

* M

#### Lanci{#sites-launches-6521}

* Il `sourceRootResource` configurato nella configurazione Launch in CRXDE Liti, fa riferimento a contenuti che non esistono più, causando un malfunzionamento quando si tenta di eliminare i lanci. L’eliminazione si avvia anche se la pagina viene eliminata o se il percorso non è lo stesso. (SITES-20750)

#### MSM - Live Copy{#sites-msm-live-copies-6521}

* Ha sovrapposto il componente Pagina per aggiungere schede nelle proprietà della pagina. Una di queste è la configurazione della pagina e dispone di una proprietà per aggiungere un URL del frammento di esperienza. Il collegamento configurato nelle proprietà della pagina per il frammento di esperienza non cambia per nessuna copia per lingua creata per quella pagina. Il collegamento configurato deve cambiare con l’URL della copia per lingua. (SITES-19580) PRINCIPALE

#### Editor pagina{#sites-pageeditor-6521}

* La modalità di modifica applica uno sfondo grigio in modo incoerente, non conforme agli standard di contrasto del colore WCAG (Web Content Accessibility Guidelines). (SITES-20060)

### [!DNL Assets]{#assets-6521}

* U

#### [!DNL Dynamic Media]{#assets-dm-6521}

* A decorrere dal 1° maggio 2024, Adobe Dynamic Medie cesserà il supporto per i seguenti elementi:
   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 e 1.1
   * Le seguenti crittografie deboli in TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

### [!DNL Forms]{#forms-6521}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.21.0 Forms add-on package release is scheduled for Thursday, May 30, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* 
  <!-- THIS BUG WAS ALREADY REPORTED IN 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


#### [!DNL Forms Designer] {#forms-designer-6521}

* Me


### Foundation {#foundation-6521}

#### Apache Felix {#felix-6521}

* Problema di aggiornamento con AEM 6.5 Service Pack 19 (SP19) in cui manca il percorso radice di contesto dell’Application Server per le richieste non autorizzate ad Apache Felix in seguito all’installazione di SP19. Aggiornamento ad Apache Felix Web Management Console 4.9.8. (NPR-41933)

* U

#### Campaign{#campaign-6521}

* AEM 6.5 Service Pack 15 genera registri di errore continui con voci significative. Sono stati segnalati i seguenti problemi:

   * Errore 404 INFO per risorsa mancante nel percorso `/libs/granite/ui/content/shell/start.html`
   * Voce del registro errori per un’eccezione SlingException non rilevata a causa di `NullPointerException` a `CampaignsDataSourceServlet.java:147`

  I registri di errore non devono essere compilati con voci di errore frequenti e voluminose e l’istanza AEM deve funzionare senza problemi relativi a risorse o eccezioni mancanti. (CQ-4357064)

#### Communities {#communities-6521}

* U

#### Distribuzione dei contenuti{#foundation-content-distribution-6521}

* M

#### Granite{#granite-6521}

* **Elimina** o **Modifica** non è possibile selezionare le autorizzazioni senza **Sfoglia** nel browser di configurazione. (GRANITE-51002)

#### Integrazioni{#integrations-6521}

* Riguardo `cq-target-integration`, è necessario rimuovere l’utilizzo non di prova di Google Guava. (CQ-4357101)
* Sostituzione delle credenziali dell’account di servizio (JSON Web Token o JWT) con le credenziali server-to-server OAuth2 (note anche come entità servizio).(NPR-41994) PRINCIPALE
* La richiesta Crea pubblico non riesce con la configurazione IMS (Identity Management System). (NPR-41888) PRINCIPALE
* Quando un cliente tenta di visualizzare la pagina Payload, il contenuto non viene visualizzato correttamente a causa di un URL non corretto; viene visualizzato un errore 404. L’errore è causato dalla mancanza di un simbolo di punto interrogativo nell’URL prima dei parametri di query. Questo problema richiede che il cliente inserisca manualmente il simbolo del punto interrogativo per visualizzare correttamente la pagina Payload. (NPR-41957)
* Rimuovi il codice e la dipendenza di Adobe Search&amp;Promote da AEM 6.5 che ha raggiunto [fine del ciclo di vita di settembre 2022 come da avviso](https://experienceleague.adobe.com/en/docs/discontinued/using/search-promote). (NPR-41855)


#### Localizzazione{#localization-6521}

* Nell’editor modelli, la stringa di testo *`No video available.`* non è localizzato. (SITES-13190)
* La stringa dopo l&#39;attivazione o la disattivazione di un utente non è localizzata in **Strumenti** > **Sicurezza** > **Utenti** > *any_user_name* > **Attiva** > **OK**, e seleziona *any_user_name* > **Disattiva** > **OK**. (NPR-41737)

#### Platform{#foundation-platform-6521}

* Il `Unclosed resource resolver` si verifica un errore per `com.day.cq.mailer.impl.DefaultMailService`. Il `MessageGatewayService` La classe, predefinita, veniva utilizzata senza un risolutore risorse. Il problema si è verificato in qualsiasi pagina con un pulsante di invio del modulo che invia un’e-mail utilizzando questa classe. (NPR-41853)

#### Sling{#foundation-sling-6521}

* M

#### Traduzione{#foundation-translation-6521}

* Un problema con lo stato di traduzione predefinito dell’AEM 6.5.19 che non viene aggiornato come previsto per un lancio. Dopo aver importato un file tradotto in un processo di traduzione associato a un avvio AEM, era previsto che lo stato cambiasse in `Approved`. Lo stato è cambiato in `Ready for Review`, che non è il comportamento previsto. (NPR-41756) PRINCIPALE
* Quando crei più configurazioni e accedi alle configurazioni dei Cloud Service di traduzione, non tutti gli elementi vengono visualizzati nell’interfaccia utente. Vengono visualizzati solo i primi 40 elementi/cartella, il caricamento lento viene attivato ma non viene aggiunto altro contenuto. (NPR-41829)
* I caratteri illeggibili si verificano in caso di giapponese nella pagina Autorizzazioni dell’interfaccia utente touch. (NPR-41794)

#### Interfaccia utente{#foundation-ui-6521}

* In Strumenti > Protezione > Utenti > &lt;user_name> > Profili, nella **Modifica impostazioni utente** , facendo clic su Annulla, la finestra di dialogo non viene chiusa. (NPR-41793) PRINCIPALE
* Granite `pathfield` componente in `/libs/granite/ui/components/coral/foundation/form/pathfield` non riesce ad abilitare **[!UICONTROL Seleziona]** quando viene selezionata una risorsa. Quando viene visualizzato il campo percorso e l’utente seleziona la casella di controllo della risorsa, la **[!UICONTROL Seleziona]** non è attivato; non cambia da grigio a blu. (NPR-41970)
* Esiste un problema con il campo di riferimento del Modello di Frammento di contenuto (CFM) all’interno dell’AEM. Nonostante il campo di riferimento CFM sia impostato come obbligatorio, in alcuni scenari il sistema consente agli utenti di fare clic su Salva per salvare i contenuti con valori non CFM. Il pulsante Salva dovrebbe essere oscurato (non disponibile). (NPR-41894)
* Le finestre di dialogo standard dell&#39;interfaccia utente di Coral che utilizzano `successresponse` L&#39;azione deve attivare una Risposta di successo dopo l&#39;azione. Tuttavia, in AEM 6.5 Service Pack 19, l’azione di ricaricamento non viene richiamata e non viene visualizzato alcun messaggio. (NPR-41797)
* I collegamenti per le notifiche AEM non funzionano in AEM 6.5 Service Pack 18. Durante l’aggiornamento a Service Pack 18, i collegamenti Notifiche AEM non funzionano quando si selezionano i messaggi tramite il pulsante Notifiche. (NPR-41792)

#### WCM{#wcm-6521}

* M

#### Flusso di lavoro{#foundation-workflow-6521}

* In AEM 6.5.18, errori ripetuti nella rimozione della cache dei metadati utente durante l’eliminazione. (NPR-41762)

## Installa [!DNL Experience Manager] 6.5.21.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0 richiede [!DNL Experience Manager] 6.5. Cfr. [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) per istruzioni dettagliate. <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del Service Pack è disponibile su Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip).
* In una distribuzione con MongoDB e più istanze, installa [!DNL Experience Manager] 6.5.21.0 in una delle istanze di authoring che utilizzano Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> L’Adobe non consiglia di rimuovere o disinstallare il [!DNL Experience Manager] pacchetto 6.5.21.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup del `crx-repository` nel caso in cui sia necessario riportarlo indietro. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installare il Service Pack in [!DNL Experience Manager] 6,5{#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia di riavviare se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup del file [!DNL Experience Manager] dell&#39;istanza.

1. Scarica il Service Sack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l’istanza dopo l’installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l’istanza. Consulta [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Talvolta si apre una finestra di dialogo sull’interfaccia utente di Gestione pacchetti durante l’installazione del Service Pack. L’Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di avere la certezza che l’installazione sia andata a buon fine. In genere, questo problema si verifica in [!DNL Safari] ma può verificarsi in modo intermittente su qualsiasi browser.

**Installazione automatica**

Esistono due metodi diversi che è possibile utilizzare per installare automaticamente [!DNL Experience Manager] 6.5.21.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserisci la confezione in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza il [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzare `cmd=install&recursive=true` affinché i pacchetti nidificati vengano installati.

>[!NOTE]
>
>L&#39;Experience Manager 6.5.21.0 non supporta l&#39;installazione Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalidare l’installazione**

Per informazioni sulle piattaforme certificate per l’utilizzo di questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. Pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa della versione aggiornata `Adobe Experience Manager (6.5.21.0)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (usa la console web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.18 o successiva (utilizzare la console Web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installa Service Pack per [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Per istruzioni sull&#39;installazione del Service Pack in Experience Manager Forms, vedere [Istruzioni di installazione di Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funzione Forms adattivo, disponibile in [QuickStart per AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html), è progettata esclusivamente a scopo di esplorazione e valutazione. Per l’utilizzo in produzione, è essenziale ottenere una licenza valida per AEM Forms, in quanto la funzionalità Adaptive Forms richiede una licenza appropriata.

### Installare il pacchetto di indice GraphQL per frammenti di contenuto Experience Manager{#install-aem-graphql-index-add-on-package}

I clienti che utilizzano GraphQL devono installare [Frammento di contenuto di Experience Manager con pacchetto indice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

In questo modo puoi aggiungere la definizione dell’indice richiesta in base alle funzioni effettivamente utilizzate.

Se non si installa questo pacchetto, è possibile che le query GraphQL risultino lente o non riuscite.

>[!NOTE]
>
>Installare il pacchetto una sola volta per istanza; non è necessario reinstallarlo con ogni Service Pack.

### UberJar{#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.21.0 è disponibile nel [Archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Per utilizzare UberJar in un progetto Maven, vedi [come usare UberJar](/help/sites-developing/ht-projects-maven.md) e includere la seguente dipendenza nel POM del progetto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.21</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell’archivio centrale Maven invece che nell’archivio Maven pubblico di Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Quindi, non c&#39;è `classifier`, con `apis` come valore, per `dependency` tag.


## Funzioni obsolete e rimosse{#removed-deprecated-features}

Consulta [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md/).

## Problemi noti{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


* **Correlato a Oak**
Da Service Pack 13 e versioni successive è stato avviato il seguente log degli errori che influisce sulla cache di persistenza:

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  Oppure

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Per risolvere l&#39;eccezione, eseguire le operazioni seguenti:

   1. Elimina le due cartelle seguenti da `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Installa il Service Pack o riavvia Experience Manager as a Cloud Service.
Nuove cartelle di `cache` e `diff-cache` vengono create automaticamente e non si verifica più un&#39;eccezione relativa a `mvstore` nel `error.log`.

* Aggiorna le query GraphQL che potrebbero aver utilizzato un nome API personalizzato per il modello di contenuto in modo da utilizzare il nome predefinito del modello di contenuto.

* Una query GraphQL può utilizzare `damAssetLucene` indice invece di `fragments` indice. Questa azione potrebbe causare l’errore o richiedere molto tempo per l’esecuzione delle query GraphQL.

  Per risolvere il problema: `damAssetLucene` deve essere configurato per includere le seguenti due proprietà in `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Dopo aver modificato la definizione dell’indice, è necessaria una reindicizzazione (`reindex` = `true`).

  Dopo questi passaggi, le query GraphQL dovrebbero funzionare più rapidamente.

* Quando si tenta di spostare, eliminare o pubblicare frammenti di contenuto, siti o pagine, si verifica un problema quando si recuperano i riferimenti ai frammenti di contenuto, poiché la query in background non riesce. In altre parole, la funzionalità non funziona.
Per garantire il corretto funzionamento, è necessario aggiungere le seguenti proprietà al nodo di definizione dell’indice `/oak:index/damAssetLucene` (non è richiesta alcuna reindicizzazione):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se aggiorni il tuo [!DNL Experience Manager] dalla versione 6.5.0 alla versione 6.5.4 al Service Pack più recente su Java™ 11, vedi `RRD4JReporter` eccezioni in `error.log` file. Per interrompere le eccezioni, riavvia l’istanza di [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Gli utenti possono rinominare una cartella in una gerarchia in [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] fino alla ripubblicazione della cartella principale.

* Durante l&#39;installazione di [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando l’integrazione di Adobe Target è configurata in [!DNL Experience Manager] se utilizzi l’API di Target Standard (autenticazione IMS), e successivamente esporti frammenti di esperienza in Target, verranno creati tipi di offerta errati. Invece del tipo &quot;Frammento di esperienza&quot;/sorgente &quot;Adobe Experience Manager&quot;, Target crea diverse offerte con il tipo &quot;HTML&quot;/sorgente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nessuna finestra di manutenzione trovata in granite/operations/maintenance.
   * La convalida lato server di Moduli adattivi non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nessuna finestra di manutenzione trovata in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Medie non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : timeout in attesa del completamento della modifica del registro, annullamento della registrazione.

* A partire da AEM 6.5.15, il motore JavaScript Rhino fornito da ```org.apache.servicemix.bundles.rhino``` Il bundle ha un nuovo comportamento di posizionamento. Script che utilizzano la modalità rigorosa (```use strict;```) devono dichiarare correttamente le loro variabili, altrimenti non vengono eseguite, generando invece un errore di runtime.

* L’installazione di contenuti predefiniti relativi ai tag tramite un pacchetto di aggiornamento ufficiale (inclusi Service Pack, Security Service Pack, Extended Feature Pack, Cumulative Feature Pack, patch e simili) reimposta la proprietà Languages (lingue) di `/content/cq:tags` per impostazione predefinita. Pertanto, è necessario aggiungerlo dalle proprietà prima dell’installazione.

### Problemi noti per AEM Sites {#known-issues-aem-sites-6521}

* SITES-17934 - Frammenti di contenuto - Anteprima non riuscita a causa della protezione DoS per una struttura ad albero di frammenti di grandi dimensioni. Consulta la [Articolo KB sulle opzioni di configurazione predefinite di GraphQL Query Executor](https://experienceleague.adobe.com/it/docs/experience-cloud-kcs/kbarticles/ka-23945)

### Problemi noti per AEM Forms {#known-issues-aem-forms-6521}

* M

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in questo [!DNL Experience Manager] 6.5 Service Pack:

* [Elenco dei bundle OSGi inclusi nell’Experience Manager 6.5.21.0](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi nell&#39;Experience Manager 6.5.21.0](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti Web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedervi, contatta il tuo account manager Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta l’Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina prodotto](https://business.adobe.com/it/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Iscriviti agli aggiornamenti dei prodotti con priorità Adobe](https://www.adobe.com/subscription/priority-product-update.html)
