---
title: Problemi noti
description: Note specifiche per i problemi noti di Adobe Experience Manager 6.5
exl-id: 736037cf-af8c-4ce2-969e-c100a939a038
source-git-commit: e0f024c2e1dc9fc7908382d406844575b4b38363
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 43%

---

# Problemi noti {#known-issues}

Questa pagina contiene un elenco dei problemi noti di Adobe Experience Manager 6.5 che è stato rilasciato nell’aprile 2019.

[Contatta l’assistenza](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it) per ulteriori informazioni sui problemi noti.

## Platform {#platform}

* Viene segnalato un problema in cui il CRX-Quickstart e il relativo contenuto vengono eliminati.

   Per ciascuna di queste azioni, assicurati che la proprietà `htmllibmanager.fileSystemOutputCacheLocation` non è una stringa vuota:

   1. Chiamata `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Aggiornamento a AEM 6.5.
   3. Esecuzione della &quot;migrazione pigra dei contenuti&quot; in AEM 6.5.

   A [Knowledge Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) questo articolo è disponibile con ulteriori dettagli e la soluzione a questo problema.

* Se utilizzi JDK 11 con AEM istanza 6.5, alcune pagine potrebbero essere visualizzate come vuote dopo la distribuzione di alcuni pacchetti. Nel file di registro viene visualizzato il seguente messaggio di errore:

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Per risolvere questo errore:

1. Interrompi l&#39;istanza AEM. Vai a `<aem_server_path_on_server>crx-quickstart\conf` e aprire `sling.properties` file. L&#39;Adobe consiglia di eseguire un backup del file.

1. Cerca `org.osgi.framework.bootdelegation=`. Aggiungi `jdk.internal.reflect,jdk.internal.reflect.*` proprietà per visualizzare il risultato come.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Salva il file e riavvia l&#39;istanza AEM.

## Assets {#assets}

* **Ricerca:** La ricerca non restituisce alcun risultato se la stringa di ricerca contiene spazi iniziali ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Schema metadati cartelle**: dopo aver aggiunto un pulsante di selezione, i campi ID e Valore non vengono visualizzati come previsto e l’opzione Elimina non funziona correttamente. (CQ-4261144)
* Quando si rinomina una risorsa, non è possibile utilizzare spazi vuoti nel nome della risorsa. (CQ-4266403)

## Forms {#forms}

* Quando AEM Forms è installato sul sistema operativo Linux, la firma digitale con modulo di sicurezza hardware non funziona. (CQ-4266721)
* (Solo AEM Forms su WebSphere) L’opzione **Forms Workflow**> **Task Search** (Flusso di lavoro per moduli > Ricerca attività) non produce alcun risultato se si cerca un **amministratore** utilizzando il **nome utente** come criterio di ricerca. (CQ-4266457)

* AEM Forms non riesce a convertire i file TIF e TIFF con compressione JPEG in documenti PDF. (CQ-4265972)
* Le opzioni di AEM Forms **Scanner risorse** e **Migrazione da lettere a comunicazioni interattive** non funzionano nella pagina **Migrazione AEM Forms**. (CQ-4266572)

* (Solo JBoss 7) Quando si esegue l’aggiornamento da una versione precedente a AEM 6.5 Forms e la versione precedente presentava processi (.lca) che creavano e utilizzavano una copia del processo di rendering predefinito o di invio, HTML5 Forms che utilizza tali processi (.lca) non riesce a eseguire le azioni richieste. (CQ-4243928)
* In un modulo adattivo, quando un servizio di modello di dati modulo viene richiamato dall’editor di regole per l’aggiornamento dinamico dei valori del componente di scelta dell’immagine, i valori del componente di scelta dell’immagine non vengono aggiornati. (CQ-4254754)
* Il programma di installazione di AEM Forms Designer richiede la versione a 32 bit di [Pacchetto runtime ridistribuibile di Visual C++ 2012](https://support.microsoft.com/it-it/help/2977003/the-latest-supported-visual-c-downloads) e [Pacchetti runtime ridistribuibili di Visual C++ 2013](https://support.microsoft.com/it-it/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Assicurati che tali Redistributable Runtime Package siano installati prima di avviare l’installazione. (CQ-4265668)

* PDF Generator non supporta l&#39;autenticazione basata su smart card.  Quando un amministratore abilita Criteri di gruppo `Interactive Logon: Require Smart card` su un server Windows, tutti gli utenti esistenti di PDF Generator vengono invalidati.

* Quando un modulo adattivo è configurato per aggiornare dinamicamente i valori di un componente e l’istanza di pubblicazione che ospita il modulo è accessibile attraverso il dispatcher, la funzionalità di aggiornamento dinamico dei valori di un campo smette di funzionare. Per risolvere il problema, nell&#39;istanza di pubblicazione, apri CRXDE, accedi a `/libs/fd/af/runtime/clientlibs/guideChartReducer`, e crea la proprietà elencata di seguito.

   * Nome: allowProxy
   * Tipo: booleano
   * Valore: true
   * Protetto: false
   * Obbligatorio: false
   * Varie: false
   * Creazione automatica: False

   La proprietà consente alle librerie client all’interno della cartella runtime di accedere ai proxy. (CQ-4268679)

* Quando AEM Forms viene avviato, la `SAX Security Manager could not be setup` viene visualizzato un avviso.
* Quando si apre un PDF protetto con AEM Forms Document Security su un Apple iOS o iPadOS con Adobe Acrobat Reader versione 20.10.00.
* Quando si invia un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file a 0 byte dall’altro lato. Apple iOS 15.1 fornisce una correzione al problema.
