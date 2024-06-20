---
title: Aggiornamento a Forms AEM 6.5 su OSGi
description: È possibile eseguire un aggiornamento diretto da Forms AEM 6.1, Forms AEM 6.2 e Forms LiveCycle ES4 SP1 a AEM 6.3.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin,User
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, OSGI
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 1%

---

# Aggiornamento a Forms AEM 6.5 su OSGi {#upgrade-to-aem-forms-osgi}

È possibile eseguire un aggiornamento diretto dal Forms AEM 6.3 o dal Forms AEM 6.4 al Forms AEM 6.5.

Percorso di aggiornamento diretto da **Forms AEM 6.0, AEM 6.1 Forms**, e **AEM 6.2 Forms** al Forms AEM 6.5 non è disponibile. Eseguire un&#39;operazione intermedia [aggiornamento al Forms AEM 6.2](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [aggiornamento al Forms AEM 6.3](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html), o [aggiornamento al Forms AEM 6.4](/help/forms/using/upgrade.md) e quindi passare dal Forms AEM 6.3 o dal Forms AEM 6.4 al Forms AEM 6.5.

Per effettuare l’aggiornamento da Forms AEM 6.3 o Forms AEM 6.4 a Forms AEM 6.5, procedere come segue:

1. Aggiorna l’istanza AEM esistente a AEM 6.5. I passaggi sono elencati di seguito:

   1. Installare il service pack e le patch più recenti per Forms AEM 6.3 o AEM 6.4 Forms. Per ulteriori informazioni, consulta [Centro per il sostegno dell’AEM](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html).
   1. Prepara l’istanza di origine per l’aggiornamento. Per i passaggi dettagliati, consulta [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Scarica il file [QuickStart per AEM 6.5](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(solo installazioni basate su Unix/Linux)** Se si utilizza UNIX o Linux come sistema operativo sottostante, aprire la finestra del terminale, passare alla cartella contenente crx-quickstart ed eseguire il comando seguente:

      `chmod -R 755 ../crx-quickstart`

   1. Aggiorna l’istanza AEM all’AEM 6.3. Per istruzioni dettagliate, consulta [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).

      Prima di continuare con i passaggi successivi, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano più visualizzati nel &lt;crx-repository>file /error.log.

      >[!NOTE]
      >
      >Quando il server è in esecuzione, alcuni bundle AEM Forms rimangono in stato di installazione. Il numero di bundle può variare per ogni installazione. Puoi ignorare lo stato di questi bundle. I bundle sono elencati in https://&#39;[server]:[porta]&#39;/system/console/.

1. Installa il pacchetto del componente aggiuntivo AEM Forms. I passaggi sono elencati di seguito:

   1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
   1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu di intestazione.
   1. In **[!UICONTROL Filtri]** sezione:
      1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
      1. Seleziona la versione e digita per il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Cerca download]** per filtrare i risultati.
   1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, quindi selezionare **[!UICONTROL Accetta termini EULA]**, e seleziona **[!UICONTROL Scarica]**.
   1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
   1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

      Puoi scaricare il pacchetto anche utilizzando il collegamento diretto elencato in [Versioni di AEM Forms](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) articolo.

      >[!NOTE]
      >
      >Dopo l’installazione del pacchetto, viene richiesto di riavviare l’istanza AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano più visualizzati nel &lt;crx-repository>/error.log e il registro è stabile. Inoltre, alcuni pacchetti possono rimanere nello stato di installazione. Puoi ignorare lo stato di questi pacchetti.

1. Riavvia l’istanza AEM.

   >[!NOTE]
   >
   Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

1. Eseguire attività successive all&#39;installazione.

   * **Esegui utilità di migrazione**

     L’utility di migrazione rende compatibili con i moduli AEM 6.5 i moduli adattivi e le risorse di gestione della corrispondenza delle versioni precedenti. Puoi scaricare l’utility da AEM Software Distribution. Per informazioni dettagliate sulla configurazione e l’utilizzo dell’utility di migrazione, consulta [utilità di migrazione](../../forms/using/migration-utility.md).

     Se sta usando [Esempio per integrare il componente Bozze e invii](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) con il database e l’aggiornamento da una versione precedente, esegui le seguenti query SQL dopo aver eseguito l’aggiornamento:

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

   * **(Se si esegue l’aggiornamento da AEM 6.2 Forms o solo dalle versioni precedenti) Riconfigura Adobe Sign**

     Se hai configurato Adobe Sign nella versione precedente di AEM Forms, riconfigura Adobe Sign da AEM Cloud Services. Per ulteriori dettagli, consulta [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Supporto per jQuery**

     In Forms con AEM 6.5, la versione di jQuery è stata aggiornata alla 3.2.1 e la versione dell’interfaccia utente jQuery alla 1.12.1. Il modulo AEM utilizza la query in **noConflict** modalità. Pertanto, se utilizzi un’altra versione di jQuery, non vengono visualizzati problemi durante l’esecuzione di un aggiornamento. Tuttavia, quando si esegue l’aggiornamento al Forms AEM 6.5:

      * Assicurati che gli eventuali componenti personalizzati siano compatibili con le versioni di jQuery supportate.
      * Rimuovi le API non supportate dai componenti personalizzati. Consulta [guida all’aggiornamento](https://jquery.com/upgrade-guide/3.0/) per l’elenco delle API rimosse. Ad esempio, viene rimosso il supporto per le API load(), .unload() ed .error(). Utilizza il metodo .on() al posto delle API di cui sopra. Ad esempio, modificare $(&quot;img&quot;).load(fn) in $(&quot;img&quot;).on(&quot;load&quot;, fn).

   * **(Se si esegue l’aggiornamento da AEM 6.2 Forms o solo dalle versioni precedenti) Riconfigura analisi e rapporti**

     In AEM 6.4 Forms, la variabile di traffico per la sorgente e l’evento di successo per l’impression non sono disponibili. Pertanto, quando esegui l’aggiornamento da AEM 6.2 Forms o versioni precedenti, AEM Forms smette di inviare dati al server Adobe Analytics e i rapporti di analisi per i moduli adattivi non sono disponibili. Inoltre, AEM 6.4 Forms introduce una variabile di traffico per la versione di form analytics e un evento di successo per la quantità di tempo trascorso su un campo. Quindi, riconfigura le analisi e i rapporti per il tuo ambiente AEM Forms. Per i passaggi dettagliati, consulta [Configurazione di analisi e rapporti](../../forms/using/configure-analytics-forms-documents.md).

1. Verificare che il server sia stato aggiornato correttamente, che anche tutti i dati siano stati migrati correttamente e che possa funzionare normalmente.

   * **Verifica lo stato dei bundle:** Assicurati che tutti i bundle siano in stato attivo.
   * **Verifica replica e replica inversa:** Publish, compila e invia alcuni moduli migrati. Verifica anche i dati inviati.
   * **Verificare l&#39;accesso alle interfacce utente amministratore e sviluppatore:** Accedi all’istanza AEM da un account amministratore e verifica di avere accesso ai seguenti URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   In AEM 6.4 Forms, la struttura dell’archivio crx è cambiata. Se si esegue l’aggiornamento da Forms 6.3 a Forms AEM 6.5, utilizzare i percorsi modificati per la personalizzazione che si creano di nuovo. Per l&#39;elenco completo dei percorsi modificati, vedere [Ristrutturazione dell’archivio Forms nell’AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).
