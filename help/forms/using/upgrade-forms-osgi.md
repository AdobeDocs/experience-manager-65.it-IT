---
title: Aggiornamento ad AEM 6.5 Forms su OSGi
description: È possibile eseguire un aggiornamento diretto da AEM 6.1 Forms, AEM 6.2 Forms e LiveCycle ES4 SP1 ad AEM 6.3 Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin,User
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi, AEM Forms Upgrade
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 5%

---

# Aggiornamento ad AEM 6.5 Forms su OSGi {#upgrade-to-aem-forms-osgi}

Puoi eseguire un aggiornamento diretto da AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms.

Il percorso di aggiornamento diretto da **AEM 6.0 Forms, AEM 6.1 Forms** e **AEM 6.2 Forms** a AEM 6.5 Forms non è disponibile. Esegui un [aggiornamento intermedio a AEM 6.2 Forms](https://helpx.adobe.com/it/experience-manager/6-2/forms/using/upgrade.html), [aggiornamento a AEM 6.3 Forms](https://helpx.adobe.com/it/experience-manager/6-3/forms/using/upgrade.html) o [aggiornamento a AEM 6.4 Forms](/help/forms/using/upgrade.md) e quindi aggiornamento da AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms.

Per effettuare l’aggiornamento da AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms, effettua le seguenti operazioni:

1. Aggiorna l’istanza AEM esistente ad AEM 6.5. I passaggi sono elencati di seguito:

   1. Installa il service pack e le patch più recenti per AEM 6.3 Forms o AEM 6.4 Forms. Per informazioni dettagliate, vedere [AEM Sustenance Hub](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html).
   1. Prepara l’istanza di origine per l’aggiornamento. Per i passaggi dettagliati, vedi [Aggiornamento ad AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Scarica [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(solo installazioni basate su Unix/Linux)** Se si utilizza UNIX o Linux come sistema operativo sottostante, aprire la finestra del terminale, passare alla cartella contenente crx-quickstart ed eseguire il comando seguente:

      `chmod -R 755 ../crx-quickstart`

   1. Aggiorna l’istanza di AEM ad AEM 6.3. Per istruzioni dettagliate, vedere [Aggiornamento ad AEM 6.5](/help/sites-deploying/upgrade.md).

      Prima di continuare con i passaggi successivi, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano visualizzati nel file &lt;crx-repository>/error.log.

      >[!NOTE]
      >
      >Quando il server è in esecuzione, alcuni bundle AEM Forms rimangono in stato di installazione. Il numero di bundle può variare per ogni installazione. Puoi ignorare lo stato di questi bundle. I bundle sono elencati in https://&#39;[server]:[porta]&#39;/system/console/.

1. Installa il pacchetto del componente aggiuntivo AEM Forms. I passaggi sono elencati di seguito:

   1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
   1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu intestazione.
   1. Nella sezione **[!UICONTROL Filtri]**:
      1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
      1. Seleziona la versione e digita per il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Cerca download]** per filtrare i risultati.
   1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accetta termini EULA]** e selezionare **[!UICONTROL Scarica]**.
   1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it) e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
   1. Selezionare il pacchetto e fare clic su **[!UICONTROL Installa]**.

      Puoi scaricare il pacchetto anche utilizzando il collegamento diretto elencato nell&#39;articolo [Versioni di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html).

      >[!NOTE]
      >
      >Dopo l’installazione del pacchetto, viene richiesto di riavviare l’istanza di AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano più visualizzati nel file &lt;crx-repository>/error.log e che il registro sia stabile. Inoltre, alcuni pacchetti possono rimanere nello stato di installazione. Puoi ignorare lo stato di questi pacchetti.

1. Riavvia l’istanza di AEM.

   >[!NOTE]
   >
   > Si consiglia di utilizzare il comando “Ctrl + C” per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

1. Eseguire attività successive all&#39;installazione.

   * **Esegui utilità di migrazione**

     L’utility di migrazione rende compatibili con AEM 6.5 forms i moduli adattivi e le risorse di gestione della corrispondenza delle versioni precedenti. Puoi scaricare l’utility da AEM Software Distribution. Per informazioni dettagliate sulla configurazione e l&#39;utilizzo dell&#39;utilità di migrazione, vedere [utilità di migrazione](../../forms/using/migration-utility.md).

     Se si utilizza [Esempio per l&#39;integrazione del componente Bozze e invii](https://helpx.adobe.com/it/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) con il database e l&#39;aggiornamento da una versione precedente, eseguire le query SQL seguenti dopo l&#39;aggiornamento:

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(Se si esegue l&#39;aggiornamento da AEM 6.2 Forms o solo dalle versioni precedenti) Riconfigura Adobe Sign**

     Se nella versione precedente di AEM Forms hai configurato Adobe Sign, riconfigura Adobe Sign da AEM Cloud Services. Per ulteriori dettagli, consulta [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Supporto per jQuery**

     In AEM 6.5 Forms, la versione di jQuery è aggiornata alla 3.2.1 e la versione dell’interfaccia utente jQuery è aggiornata alla 1.12.1. AEM Form utilizza JQuery in modalità **noConflict**. Pertanto, se utilizzi un’altra versione di jQuery, non vengono visualizzati problemi durante l’esecuzione di un aggiornamento. Tuttavia, quando esegui l’aggiornamento a AEM 6.5 Forms:

      * Assicurati che gli eventuali componenti personalizzati siano compatibili con le versioni di jQuery supportate.
      * Rimuovi le API non supportate dai componenti personalizzati. Per l&#39;elenco delle API rimosse, consulta la [guida all&#39;aggiornamento](https://jquery.com/upgrade-guide/3.0/). Ad esempio, viene rimosso il supporto per le API load(), .unload() ed .error(). Utilizza il metodo .on() al posto delle API di cui sopra. Ad esempio, modificare $(&quot;img&quot;).load(fn) in $(&quot;img&quot;).on(&quot;load&quot;, fn).

   * **(Se si esegue l&#39;aggiornamento da AEM 6.2 Forms o solo da versioni precedenti) Riconfigura analisi e report**

     In AEM 6.4 Forms, la variabile di traffico per la sorgente e l’evento di successo per le impression non sono disponibili. Pertanto, quando esegui l’aggiornamento da AEM 6.2 Forms o versioni precedenti, AEM Forms smette di inviare dati al server Adobe Analytics e i rapporti di analisi per i moduli adattivi non sono disponibili. Inoltre, AEM 6.4 Forms introduce la variabile di traffico per la versione di analisi dei moduli e l’evento di successo per la quantità di tempo trascorso su un campo. Quindi, riconfigura le analisi e i rapporti per il tuo ambiente AEM Forms. Per i passaggi dettagliati, vedi [Configurazione di analisi e rapporti](../../forms/using/configure-analytics-forms-documents.md).

1. Verificare che il server sia stato aggiornato correttamente, che anche tutti i dati siano stati migrati correttamente e che possa funzionare normalmente.

   * **Verifica lo stato dei bundle:** Verifica che tutti i bundle siano in stato attivo.
   * **Verifica replica e replica inversa:** Pubblicare, compilare e inviare alcuni moduli migrati. Verifica anche i dati inviati.
   * **Verificare l&#39;accesso alle interfacce utente amministratore e sviluppatore:** Accedere all&#39;istanza di AEM da un account amministratore e verificare di disporre dell&#39;accesso ai seguenti URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >In AEM 6.4 Forms, la struttura dell’archivio crx è cambiata. Se esegui l’aggiornamento da Forms 6.3 a AEM 6.5 Forms, utilizza i percorsi modificati per la personalizzazione che crei nuovamente. Per l&#39;elenco completo dei percorsi modificati, vedere [Ristrutturazione dell&#39;archivio Forms in AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).
