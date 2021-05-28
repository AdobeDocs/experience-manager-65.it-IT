---
title: Domande frequenti su AEM
seo-title: AEM 6.4 domande frequenti
description: Usa queste domande frequenti per comprendere, configurare e risolvere i problemi e i flussi di lavoro comuni in AEM.
seo-description: Usa queste domande frequenti per comprendere, configurare e risolvere i problemi e i flussi di lavoro comuni in AEM.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---

# Domande frequenti AEM {#aem-faqs}

Scopri le risposte ad alcuni problemi AEM di risoluzione dei problemi e di configurazione.

## Sites {#sites}

### Come si configura la distribuzione senza binario? {#how-do-i-configure-binary-less-distribution}

La distribuzione senza binario è supportata per le distribuzioni su un archivio dati condiviso e coinvolge agenti che sfruttano l’esportatore del pacchetto di distribuzione basato su Vault (PID di fabbrica: Generatore di pacchetti `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`).

Con la modalità senza binario abilitata, i pacchetti di contenuto distribuiti contengono riferimenti a binari anziché ai binari effettivi.

#### Come si attiva la distribuzione senza binario? {#how-do-i-enable-binary-less-distribution}

Per abilitare la distribuzione senza binario, distribuisci con un archivio BLOB condiviso.
Controlla la proprietà `useBinaryReferences` nella configurazione OSGI con il PID di fabbrica ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* che il tuo agente sta utilizzando.

#### Come posso personalizzare i messaggi di errore durante la navigazione nella gerarchia delle pagine AEM console Sites? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

Controlla il pannello Rete (del browser Chrome) dove una configurazione personale (JS non è stata minimizzata).

Visualizza la colonna `Initiator` per determinare quale sia stato l’iniziatore di una richiesta. Fornisce i file e i numeri di riga da cui vengono effettuate le chiamate AJAX. Successivamente, puoi tenere traccia della funzione di gestione degli errori e modificare il messaggio di errore in base alle tue esigenze.

#### Come abilitare le autorizzazioni durante la creazione di una copia in lingua per gli autori di contenuti in AEM? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Per creare la funzione di copia per lingua, gli autori dei contenuti devono disporre delle autorizzazioni nel percorso `/content/projects` .

Se uno richiede che gli autori gestiscano anche i progetti, la soluzione consiste nell’aggiungere l’autore al gruppo `project-administrators` .

#### Come modificare il formato durante la creazione di una copia in lingua per un progetto? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Crea una radice linguistica e una copia della lingua all’interno della radice, prima di creare un progetto di traduzione.

Ad esempio:
Crea una directory principale della lingua in `/content/geometrixx` con nome `fr_LU` (e titolo in francese (Lussemburgo)). Successivamente, crea una copia in lingua della pagina dal pannello riferimenti e passa all&#39;opzione `Create structure only` in `Create & Translate`. Infine, crea un progetto di traduzione e quindi aggiungi la copia per lingua al lavoro di traduzione.

Per ulteriori informazioni, consulta le risorse aggiuntive seguenti:

* [Preparazione del contenuto per la traduzione](/help/sites-administering/tc-prep.md)
* [Gestione dei progetti di traduzione](/help/sites-administering/tc-manage.md)

#### Come controllare AEM funzionalità come tentativi di accesso e modifiche di ACL o autorizzazioni? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM ha introdotto la possibilità di registrare le modifiche amministrative per una migliore risoluzione dei problemi e audit. Per impostazione predefinita, le informazioni vengono registrate nel file `error.log`. Per semplificare il monitoraggio, è consigliabile reindirizzarli a un file di registro separato.
Per reindirizzare l&#39;output a un file di registro separato, vedere [Come controllare le operazioni di gestione degli utenti in AEM](/help/sites-administering/audit-user-management-operations.md).

#### Come abilitare SSL per impostazione predefinita? {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4 viene fornito con la procedura guidata SSL e offre un’interfaccia utente per configurare il supporto Jetty e Granite Jetty SSL.

Per abilitare SSL per impostazione predefinita, consulta [SSL per impostazione predefinita](/help/sites-administering/ssl-by-default.md).

#### Qual è l’architettura consigliata quando si utilizzano i Content Services di AEM da un’app mobile, idealmente React Native? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

I Content Services sono basati su modelli Sling e gli sviluppatori AEM devono fornire un pojo Sling Model per ciascun componente esportato.

Per informazioni su come utilizzare AEM servizi di contenuto da un&#39;applicazione React, consulta l&#39;esercitazione [Introduzione a AEM Content Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) .

Inoltre, se gli sviluppatori desiderano esportare una struttura di componenti possono implementare anche le interfacce `ComponentExporter` e `ContainerExporter` e utilizzare `ModelFactory` per eseguire iterazioni sui componenti secondari e restituire la rappresentazione del modello. Consulta le risorse seguenti:

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Modelli Sling](https://sling.apache.org/documentation/bundles/models.html)

#### Come disabilitare il pop-up del sondaggio AEM 6.4? {#how-to-disable-aem-survey-pop-up}

Puoi scegliere di utilizzare la raccolta di statistiche di utilizzo utilizzando l’interfaccia utente touch o la console Web. Per istruzioni dettagliate, vedere [Opting in aggregate usage statistics collection](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### Esiste una buona risorsa che evidenzia le funzioni chiave per l’aggiornamento a AEM 6.4? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Fai riferimento a [Informazioni sui motivi dell&#39;aggiornamento AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) che descrive una suddivisione di alto livello delle funzioni chiave per i clienti che considerano l&#39;aggiornamento alla versione più recente di Adobe Experience Manager.

## Assets {#assets}

### Perché il flusso di lavoro Assets si ripete durante il caricamento di file MP4 (ad esempio, utilizzando il metodo di trascinamento della selezione)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Se l’utente, il caricamento dei file di filmato non dispone delle autorizzazioni di eliminazione sotto il nodo della risorsa, i nodi di eliminazione del blocco non riescono e il caricamento si riavvia.

#### Quali sono le impostazioni predefinite per le configurazioni OOTB durante la creazione di una copia in lingua? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Quando crei una copia per lingua tramite l’interfaccia utente touch (**Riferimenti** -> **Aggiorna copia per lingua**), viene creata una nuova cartella DAM nella nuova lingua e vi si fa riferimento alle risorse.

Questa è l&#39;impostazione predefinita per le configurazioni OOTB. È possibile impostare **Traduci risorse pagina** = **Non tradurre** nelle configurazioni di traduzione.
Per AEM 6.4, **Strumenti** > **Cloud Services** > **Servizi cloud di traduzione**.

#### Come disabilitare un componente AEM che causa una crescita esponenziale per il AEM SegmentStore (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

È possibile disabilitare il Disabler del componente OSGi. Per utilizzare questo servizio, consulta [Disabler componente OSGi](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Come soluzione alternativa, puoi anche disabilitare manualmente il componente tramite l’interfaccia utente o tramite un comando `curl` (ad esempio di seguito), dopo ogni riavvio AEM.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Come personalizzare le console di amministrazione? {#how-to-customize-admin-consoles}

AEM offre diversi metodi per personalizzare le console e la funzionalità di authoring delle pagine dell’istanza di authoring. Per informazioni su come creare una console personalizzata e personalizzare una visualizzazione predefinita per una console, consulta [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md) .

#### Qual è la differenza tra i componenti basati su CoralUI 2 e CoralUI 3? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Un nuovo set di componenti Sling di Granite UI Foundation viene creato per Coral3 e si trova in [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) È disponibile un set per i componenti basati su CoralUI 2 e uno per i componenti basati su CoralUI 3. Il nuovo set non sarà solo una copia-incolla del set precedente, ma verrà anche ripulito (ad esempio, per ottimizzare, rimuovere la funzione obsoleta). Pertanto, è consigliabile che una pagina utilizzi solo un set basato su CoralUI 3 o CoralUI 2.

Per ulteriori informazioni, consulta la [Guida alla migrazione a CoralUI 3-based](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html) .

#### Come personalizzare il componente di ricerca in AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Per ulteriori informazioni sul boost/ranking della ricerca e ulteriori informazioni sull&#39;implementazione, consulta [Guida all&#39;implementazione della ricerca semplice](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

L&#39;implementazione Semplice di ricerca sono i materiali del laboratorio del Summit 2017 AEM Ricerca Demystified.

#### È possibile creare un plug-in per WordPress che consente a un cliente di accedere ad Adobe Asset Picker per selezionare le immagini? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Sì, un cliente che utilizza WordPress può utilizzare Adobe Asset Picker per selezionare le immagini dal proprio server AEM Assets da aggiungere ai post sul proprio sito WordPress.

Per ulteriori informazioni, consulta [Selettore risorse](../assets/search-assets.md#assetpicker) .
