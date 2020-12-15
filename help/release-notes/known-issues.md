---
title: Problemi noti
description: Note specifiche per i problemi noti di Adobe Experience Manager 6.5
translation-type: tm+mt
source-git-commit: f72101dadaa8d5d12f2f9a636548b18386b79b0a
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 46%

---


# Problemi noti {#known-issues}

Questa pagina contiene un elenco dei problemi noti di Adobe Experience Manager 6.5 che è stato rilasciato nell’aprile 2019.

[Contatta l’assistenza](https://helpx.adobe.com/it/support/experience-manager.html) per ulteriori informazioni sui problemi noti.

## Platform {#platform}

* Viene segnalato un problema di eliminazione del CRX-Quickstart e del relativo contenuto.

   Per ciascuna di queste azioni, assicurarsi che la proprietà `htmllibmanager.fileSystemOutputCacheLocation` non sia una stringa vuota:

   1. Chiamata di `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Aggiornamento alla AEM 6.5.
   3. Esecuzione della &quot;migrazione pigra dei contenuti&quot; in AEM 6.5.

   È disponibile un articolo [Knowledge Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) con ulteriori dettagli e la soluzione alternativa per questo problema.

* Se utilizzate JDK 11 con AEM 6.5, alcune pagine potrebbero essere visualizzate come vuote dopo la distribuzione di alcuni pacchetti. Nel file di registro viene visualizzato il seguente messaggio di errore:

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Per risolvere questo errore:

1. Arrestate l&#39;istanza AEM. Vai a `<aem_server_path_on_server>crx-quickstart\conf` e apri il file `sling.properties`.  Adobe consiglia di eseguire un backup del file.

1. Cerca `org.osgi.framework.bootdelegation=`. Aggiungete le proprietà `jdk.internal.reflect,jdk.internal.reflect.*` per visualizzare il risultato come.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Salvate il file e riavviate l&#39;istanza AEM.

## Assets {#assets}

* **Ricerca:** La ricerca non restituisce alcun risultato se la stringa di ricerca contiene spazi iniziali ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Schema metadati cartelle**: dopo aver aggiunto un pulsante di selezione, i campi ID e Valore non vengono visualizzati come previsto e l’opzione Elimina non funziona correttamente. (CQ-4261144)
* Quando si rinomina una risorsa, non è possibile utilizzare spazi vuoti nel nome della risorsa. (CQ-4266403)

## Forms {#forms}

* Se  AEM Forms è installato nel sistema operativo Linux, la firma digitale con il modulo di sicurezza hardware non funziona. (CQ-4266721)
* (Solo AEM Forms su WebSphere) L’opzione **Forms Workflow**> **Task Search** (Flusso di lavoro per moduli > Ricerca attività) non produce alcun risultato se si cerca un **amministratore** utilizzando il **nome utente** come criterio di ricerca. (CQ-4266457)

*  AEM Forms non riesce a convertire i file TIF e TIFF con compressione JPEG in documenti PDF. (CQ-4265972)
* Le opzioni di AEM Forms **Scanner risorse** e **Migrazione da lettere a comunicazioni interattive** non funzionano nella pagina **Migrazione AEM Forms**. (CQ-4266572)

* (Solo per JBoss 7) Quando si esegue l’aggiornamento da una versione precedente a AEM 6.5 Forms e la versione precedente conteneva processi (.lca) che creavano e utilizzavano una copia del processo di rendering predefinito, HTML5 Forms con tali processi (.lca) non riesce a eseguire le azioni richieste. (CQ-4243928)
* In un modulo adattivo, quando un servizio di modello di dati modulo viene richiamato dall’editor di regole per l’aggiornamento dinamico dei valori del componente di scelta dell’immagine, i valori del componente di scelta dell’immagine non vengono aggiornati. (CQ-4254754)
*  programma di installazione di AEM Forms Designer richiede la versione a 32 bit di [pacchetti runtime redistribuibili di Visual C++ 2012](https://support.microsoft.com/it-it/help/2977003/the-latest-supported-visual-c-downloads) e di [pacchetti runtime redistribuibili di Visual C++ 2013](https://support.microsoft.com/it-it/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Assicurati che tali Redistributable Runtime Package siano installati prima di avviare l’installazione. (CQ-4265668)

* PDF Generator non supporta l&#39;autenticazione basata su smart card.  Quando un amministratore abilita i Criteri di gruppo `Interactive Logon: Require Smart card` su un server Windows, tutti gli utenti di PDF Generator esistenti vengono invalidati.

* Quando un modulo adattivo è configurato per aggiornare dinamicamente i valori di un componente e l’istanza di pubblicazione che ospita il modulo è accessibile attraverso il dispatcher, la funzionalità di aggiornamento dinamico dei valori di un campo smette di funzionare. Per risolvere il problema, nell’istanza di pubblicazione aprite CRXDE, andate a `/libs/fd/af/runtime/clientlibs/guideChartReducer` e create la proprietà elencata di seguito.

   * Nome: allowProxy
   * Tipo: booleano
   * Valore: true
   * Protetto: false
   * Obbligatorio: false
   * Varie: false
   * Creazione automatica: False

   La proprietà consente alle librerie client all’interno della cartella runtime di accedere ai proxy. (CQ-4268679)

* Quando  AEM Forms viene avviato, viene visualizzato l&#39;avviso `SAX Security Manager could not be setup`.
* Quando si apre un PDF protetto con  AEM Forms Document Security su un Apple iOS o iPadOS in esecuzione  Adobe Acrobat Reader versione 20.10.00.
