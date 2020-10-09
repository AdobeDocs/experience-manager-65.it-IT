---
title: AEM domande frequenti
seo-title: AEM 6.4 domande frequenti
description: Utilizzate queste domande frequenti per comprendere, configurare e risolvere i flussi di lavoro o i problemi più comuni in AEM.
seo-description: Utilizzate queste domande frequenti per comprendere, configurare e risolvere i flussi di lavoro o i problemi più comuni in AEM.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---


# AEM domande frequenti {#aem-faqs}

Scopri le risposte ad alcuni AEM problemi di risoluzione dei problemi e configurazione.

## Sites {#sites}

### Come si configura la distribuzione senza binario? {#how-do-i-configure-binary-less-distribution}

La distribuzione senza binario è supportata per le distribuzioni su un archivio dati condiviso e coinvolge gli agenti che sfruttano l&#39;esportatore di pacchetti di distribuzione basato su Vault (PID di fabbrica: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`).

Se la modalità binaria è attivata, i pacchetti di contenuto distribuiti contengono riferimenti a file binari anziché ai file binari effettivi.

#### Come si abilita la distribuzione senza binario? {#how-do-i-enable-binary-less-distribution}

Per abilitare la distribuzione binaria, distribuisci con uno store BLOB condiviso.
Controllate la `useBinaryReferences` proprietà nella configurazione OSGI con il PID di fabbrica ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* che il vostro agente sta utilizzando.

#### Come è possibile personalizzare i messaggi di errore durante la navigazione nella gerarchia delle pagine AEM console Siti? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

Controllare il pannello Rete (del browser Chrome) dove una configurazione personale (JS non è stata ridotta).

Visualizzate la `Initiator` colonna per determinare l’iniziatore di una richiesta. Fornisce i file e i numeri di riga da cui vengono effettuate le chiamate AJAX. Successivamente, è possibile tracciare la funzione di gestione degli errori e modificare il messaggio di errore in base alle proprie esigenze.

#### Come abilitare le autorizzazioni durante la creazione di una copia della lingua per gli autori di contenuti in AEM? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Per creare la funzione di copia per lingua, gli autori dei contenuti devono disporre delle autorizzazioni sul `/content/projects` posto.

Se uno richiede che gli autori gestiscano anche i progetti, la soluzione consiste nell’aggiungere l’autore al `project-administrators` gruppo.

#### Come modificare il formato durante la creazione di una copia della lingua per un progetto? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Prima di creare un progetto di traduzione, create una copia radice della lingua e della lingua all’interno della directory principale.

Ad esempio, create un livello principale della lingua `/content/geometrixx` con nome `fr_LU` (e titolo come francese (Lussemburgo)). Successivamente, create una copia della lingua della pagina dal pannello Riferimenti e selezionate l’opzione `Create structure only` in `Create & Translate`. Infine, create un progetto di traduzione e aggiungete la copia per lingua al processo di traduzione.

Per informazioni dettagliate, consultate le risorse aggiuntive riportate di seguito:

* [Preparazione del contenuto per la traduzione](/help/sites-administering/tc-prep.md)
* [Gestione dei progetti di traduzione](/help/sites-administering/tc-manage.md)

#### Come controllare AEM funzionalità come tentativi di accesso e modifiche di ACL o autorizzazioni? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM ha introdotto la possibilità di registrare le modifiche amministrative per migliorare la risoluzione dei problemi e il controllo. Per impostazione predefinita, le informazioni vengono registrate nel `error.log` file. Per semplificare il monitoraggio, si consiglia di reindirizzarli a un file di registro separato.
Per reindirizzare l&#39;output a un file di registro separato, vedere [Come controllare le operazioni di gestione degli utenti in AEM](/help/sites-administering/audit-user-management-operations.md).

#### Come abilitare SSL per impostazione predefinita? {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4 viene fornito con la procedura guidata SSL e offre un&#39;interfaccia utente per configurare il supporto SSL Jetty e Granite Jetty.

Per abilitare SSL per impostazione predefinita, vedi [SSL per impostazione predefinita](/help/sites-administering/ssl-by-default.md).

#### Qual è l&#39;architettura consigliata quando si utilizzano i Content Services di AEM da un&#39;app mobile, React Native (Reazione nativa) idealmente? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Content Services si basa sui modelli Sling e gli sviluppatori AEM devono fornire un pojo Sling Model per ciascun componente esportato.

Per informazioni su come utilizzare AEM servizi di contenuto da un&#39;applicazione React, vedere Esercitazione [Primi passi con AEM Content Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) .

Inoltre, se gli sviluppatori desiderano esportare una struttura di componenti, possono implementare le `ComponentExporter` interfacce e le `ContainerExporter` interfacce e utilizzare `ModelFactory` per iterare i componenti secondari e restituire la rappresentazione del modello. Consulta le risorse seguenti:

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Modelli Sling](https://sling.apache.org/documentation/bundles/models.html)

#### Come disattivare AEM sondaggio popup 6.4? {#how-to-disable-aem-survey-pop-up}

È possibile scegliere di utilizzare la raccolta delle statistiche di utilizzo utilizzando l&#39;interfaccia utente touch o la console Web. Per istruzioni dettagliate, vedere [Scelta nella raccolta](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)delle statistiche di utilizzo aggregate.

#### Esiste una buona risorsa che evidenzia le caratteristiche chiave per l&#39;aggiornamento a AEM 6.4? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Fare riferimento a [Informazioni sui motivi dell&#39;aggiornamento AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) che descrive la suddivisione ad alto livello delle funzioni chiave per i clienti che stanno pensando di effettuare l&#39;aggiornamento all&#39;ultima versione di Adobe Experience Manager.

## Assets {#assets}

### Perché il flusso di lavoro Risorse si ripete durante il caricamento di file MP4 (ad esempio, tramite trascinamento)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Se l’utente carica i file del filmato non dispone delle autorizzazioni di eliminazione nel nodo della risorsa, i nodi dei blocchi eliminati non riescono e il caricamento viene riavviato.

#### Qual è il numero massimo di risorse digitali utilizzabili con AEM 6.4 alla volta? {#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Adobe Experience Manager (AEM) 6.5 attualmente consente di caricare fino a 2 GB di risorse alla volta.

Per ulteriori informazioni sul numero massimo di risorse utilizzabili con AEM 6.5, consulta la guida [al ridimensionamento delle](/help/assets/assets-sizing-guide.md)risorse.

#### Quali sono le impostazioni predefinite per le configurazioni OOOTB durante la creazione di una copia lingua? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Durante la creazione di copie della lingua nell’interfaccia classica, le risorse non vengono spostate sotto la nuova gerarchia di lingue ma utilizzate dal master della lingua.

Quando create una copia per lingua tramite l’interfaccia utente touch (**Riferimenti** -> **Aggiorna copia** lingua), viene creata una nuova cartella DAM con la nuova lingua e viene fatto riferimento alle risorse disponibili.

Questa è l&#39;impostazione predefinita per le configurazioni OOTB. Potete impostare **Traduci risorse** pagina = **Non tradurre** nelle configurazioni di traduzione.
Per AEM 6.4, **Strumenti** > **Cloud Services** > Servizi **** di Translation Cloud.

#### Come disattivare un componente AEM che causa una crescita esponenziale per il AEM SegmentStore (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

È possibile disattivare il Disabler dei componenti OSGi. Per utilizzare questo servizio, vedere Disabler [di componenti](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html)OSGi.

Per risolvere il problema, potete anche disattivare manualmente il componente tramite l’interfaccia utente o tramite un `curl` comando (ad esempio di seguito), dopo ogni AEM riavvio.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Come configurare Asset Insights con AEM 6.5 instance? {#how-to-configure-asset-insights-with-aem-instance}

Per impostare e configurare approfondimenti risorse per  Experience Manager distribuito tramite  Attivazione Adobe (DTM), consulta come [configurare approfondimenti risorse con  AEM Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

#### Come personalizzare le console di amministrazione? {#how-to-customize-admin-consoles}

AEM offre diversi metodi per personalizzare le console e la funzionalità di authoring delle pagine dell’istanza di authoring. Per informazioni su come creare una console personalizzata e personalizzare una visualizzazione predefinita per una console, consultate [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md).

#### Qual è la differenza tra i componenti basati su CoralUI 2 e CoralUI 3? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Per Coral3 viene creato un nuovo set di componenti Sling di Granite UI Foundation ed è ubicato in [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) È disponibile un set per i componenti basati su CoralUI 2 e uno per i componenti basati su CoralUI 3. Il nuovo set non sarà solo una copia-incolla del set precedente, ma verrà anche ripulito (ad esempio, snellimento, rimozione della funzione obsoleta). È quindi consigliabile che una pagina utilizzi solo il set basato su CoralUI 3 o CoralUI 2 basato su CoralUI.

Per ulteriori informazioni, consulta la Guida alla [migrazione alla CoralUI basata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)su 3.

#### Come personalizzare il componente di ricerca in  AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Per ulteriori informazioni su come migliorare/classificare la ricerca e ulteriori informazioni sull’implementazione, consulta la guida [all’implementazione della ricerca](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)semplice.

L&#39;implementazione semplice della ricerca sono i materiali del laboratorio Summit 2017 AEM Search Demystified.

#### Qual è la differenza tra  AEM Assets e AEM MediaLibrary? {#what-is-the-difference-between-aem-assets-and-aem-medialibrary}

 AEM Assets è un&#39;applicazione della piattaforma AEM che consente ai nostri clienti di gestire le proprie risorse digitali (immagini, video, documenti e clip audio) in un archivio basato su Web, mentre AEM Media Library è una parte designata dell&#39;archivio AEM contenuti WCM in cui vengono memorizzate immagini e altre risorse condivise.

Per ulteriori informazioni, consulta [AEM Assets e AEM MediaLibrary](/help/assets/medialibrary.md) .

#### È possibile creare un plug-in per WordPress che consenta a un cliente di accedere  Adobe Asset Picker per selezionare le immagini? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Sì, un cliente che utilizza WordPress può utilizzare  Adobe Asset Picker per selezionare le immagini dal proprio server AEM Assets  da aggiungere ai post sul suo sito WordPress.

Per ulteriori informazioni, consultate Selettore [](../assets/search-assets.md#assetpicker) risorse.

#### È possibile estendere i facet di ricerca in  AEM Assets per aggiungere ulteriori predicati? {#is-it-possible-to-extend-the-search-facets-in-aem-assets-to-add-additional-predicates}

Una distribuzione aziendale di Adobe Experience Manager (AEM) Assets consente di archiviare molte risorse. È possibile aggiungere predicati al modulo predefinito o utilizzare un modulo personalizzato che includa facet di propria scelta.

Per ulteriori informazioni, consulta Facet di [ricerca](/help/assets/search-facets.md) .
