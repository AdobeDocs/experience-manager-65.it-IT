---
title: Problemi noti
description: Note specifiche per i problemi noti di Adobe Experience Manager 6.5
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 3d607217e3d66998a8463db3f527a626beaca769

---


# Problemi noti {#known-issues}

Questa pagina contiene un elenco dei problemi noti di Adobe Experience Manager 6.5 che è stato rilasciato nell’aprile 2019.

[Contatta l’assistenza](https://helpx.adobe.com/support/experience-manager.html) per ulteriori informazioni sui problemi noti.

## Platform {#platform}

Viene segnalato un problema di eliminazione del CRX-Quickstart e del relativo contenuto.

Per ciascuna di queste azioni, assicurarsi che la proprietà &quot;*htmllibmanager.fileSystemOutputCacheLocation*&quot; non sia mai una stringa vuota:

1. Chiamata di &quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;.
2. Aggiornamento ad AEM 6.5.
3. Esecuzione di una &quot;migrazione pigra dei contenuti&quot; su AEM 6.5.

È disponibile un articolo della [Knowledge Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) con ulteriori dettagli e la soluzione a questo problema.

## Assets {#assets}

* **Ricerca:** La ricerca non restituisce alcun risultato se la stringa di ricerca contiene spazi iniziali ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Schema metadati cartelle**: dopo aver aggiunto un pulsante di selezione, i campi ID e Valore non vengono visualizzati come previsto e l’opzione Elimina non funziona correttamente. (CQ-4261144)
* Quando si rinomina una risorsa, non è possibile utilizzare spazi vuoti nel nome della risorsa. (CQ-4266403)

## Forms {#forms}

* Quando AEM Forms è installato su sistema operativo Linux, la firma digitale con modulo di sicurezza hardware non funziona. (CQ-4266721)
* (AEM Forms on WebSphere only) The **Forms Workflow **> **Task Search** option does not return any result if you search for an **Administrator** with **Username** as the search criteria. (CQ-4266457)

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

