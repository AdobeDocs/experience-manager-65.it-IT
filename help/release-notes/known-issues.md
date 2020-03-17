---
title: Problemi noti
description: Note specifiche per i problemi noti di Adobe Experience Manager 6.5
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 86dbd52d44a78401aa50cce299850469c51b691c

---


# Problemi noti {#known-issues}

Questa pagina contiene un elenco dei problemi noti di Adobe Experience Manager 6.5 che è stato rilasciato nell’aprile 2019.

[Contatta l’assistenza](https://helpx.adobe.com/support/experience-manager.html) per ulteriori informazioni sui problemi noti.

## Platform {#platform}

* Viene segnalato un problema di eliminazione del CRX-Quickstart e del relativo contenuto.

   Per ciascuna di queste azioni, assicurarsi che la proprietà &quot;*htmllibmanager.fileSystemOutputCacheLocation*&quot; non sia mai una stringa vuota:

   1. Chiamata di &quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;.
   2. Aggiornamento ad AEM 6.5.
   3. Esecuzione di una &quot;migrazione pigra dei contenuti&quot; su AEM 6.5.
   È disponibile un articolo della [Knowledge Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) con ulteriori dettagli e la soluzione a questo problema.

* Se utilizzate JDK 11 con l’istanza AEM 6.5, alcune pagine potrebbero essere visualizzate come vuote dopo la distribuzione di alcuni pacchetti. Nel file di registro viene visualizzato il seguente messaggio di errore:

   ```
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Per risolvere questo errore:

1. Arrestate l’istanza AEM. Vai a `<aem_server_path_on_server>crx-quickstart\conf` e apri il `sling.properties` file. Adobe consiglia di eseguire una copia di backup del file.

2. Cerca `org.osgi.framework.bootdelegation=`. Aggiungere `jdk.internal.reflect,jdk.internal.reflect.*` proprietà per visualizzare il risultato come:

   ```
   org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
   ```

3. Salvate il file e riavviate l&#39;istanza di AEM.

## Assets {#assets}

* **Ricerca:** La ricerca non restituisce alcun risultato se la stringa di ricerca contiene spazi iniziali ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Schema metadati cartelle**: dopo aver aggiunto un pulsante di selezione, i campi ID e Valore non vengono visualizzati come previsto e l’opzione Elimina non funziona correttamente. (CQ-4261144)
* Quando si rinomina una risorsa, non è possibile utilizzare spazi vuoti nel nome della risorsa. (CQ-4266403)

## Forms {#forms}

* Quando AEM Forms è installato su sistema operativo Linux, la firma digitale con modulo di sicurezza hardware non funziona. (CQ-4266721)
* (Solo AEM Forms su WebSphere) L’opzione **Forms Workflow**> **Task Search** (Flusso di lavoro per moduli > Ricerca attività) non produce alcun risultato se si cerca un **amministratore** utilizzando il **nome utente** come criterio di ricerca. (CQ-4266457)

* AEM Forms non riesce a convertire i file .tif e .tiff con compressione JPEG in documenti PDF. (CQ-4265972)
* Le opzioni di AEM Forms **Scanner risorse** e **Migrazione da lettere a comunicazioni interattive** non funzionano nella pagina **Migrazione AEM Forms**. (CQ-4266572)

* (Solo per JBoss 7) Quando si esegue l’aggiornamento da una versione precedente ad AEM 6.5 Forms e la versione precedente conteneva processi (.lca) che creavano e utilizzavano una copia del processo di rendering predefinito per l’invio o per il rendering, HTML5 Forms con tali processi (.lca) non riusciva a eseguire le azioni richieste. (CQ-4243928)
* In un modulo adattivo, quando un servizio di modello di dati modulo viene richiamato dall’editor di regole per l’aggiornamento dinamico dei valori del componente di scelta dell’immagine, i valori del componente di scelta dell’immagine non vengono aggiornati. (CQ-4254754)
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Assicurati che tali Redistributable Runtime Package siano installati prima di avviare l’installazione. (CQ-4265668)

* Quando un modulo adattivo è configurato per aggiornare dinamicamente i valori di un componente e l’istanza di pubblicazione che ospita il modulo è accessibile attraverso il dispatcher, la funzionalità di aggiornamento dinamico dei valori di un campo smette di funzionare. Per risolvere il problema, nell’istanza di pubblicazione apri CRXDE, pass a /libs/fd/af/runtime/clientlibs/guideChartReducer e crea la proprietà elencata di seguito.

   * Nome: allowProxy
   * Tipo: booleano
   * Valore: true
   * Protetto: false
   * Obbligatorio: false
   * Varie: false
   * Creazione automatica: false

La proprietà consente alle librerie client all’interno della cartella runtime di accedere ai proxy. (CQ-4268679)

