---
title: Aggiornamento ad AEM 6.5 Forms
seo-title: Aggiornamento ad AEM 6.5 Forms
description: È possibile eseguire un aggiornamento diretto da AEM 6.1 Forms, AEM 6.2 Forms e LiveCycle ES4 SP1 a AEM 6.3 Forms.
seo-description: È possibile eseguire un aggiornamento diretto da AEM 6.1 Forms, AEM 6.2 Forms e LiveCycle ES4 SP1 a AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# Aggiornamento ad AEM 6.5 Forms su OSGi {#upgrade-to-aem-forms-osgi}

È possibile eseguire un aggiornamento diretto da AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms.

Il percorso di aggiornamento diretto dai moduli **AEM 6.0, AEM 6.1 Forms** e **AEM 6.2 Forms** a AEM 6.5 Forms non è disponibile. Effettuate un [aggiornamento intermedio a AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [eseguite l&#39;aggiornamento ad AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)o [aggiornate ad AEM 6.4 Forms](/help/forms/using/upgrade.md) , quindi eseguite l&#39;aggiornamento da AEM 6.3 Forms o AEM 6.4 a AEM 6.5 Forms.

Per effettuare l’aggiornamento da AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms, effettuate le seguenti operazioni:

1. Aggiorna l’istanza AEM esistente a AEM 6.5. I passaggi sono elencati di seguito:

   1. Installa il service pack e le patch più recenti per AEM 6.3 Forms o AEM 6.4 Forms. Per informazioni dettagliate, consultate [AEM SustMaintenance Hub](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html).
   1. Preparare l’istanza di origine per l’aggiornamento. Per i passaggi dettagliati, consultate [Aggiornamento ad AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Scaricate la Guida rapida [di](/help/sites-deploying/deploy.md#getting%20the%20software)AEM 6.5.
   1. **(Solo installazioni basate su Unix/Linux)** Se utilizzate UNIX o Linux come sistema operativo sottostante, aprite la finestra del terminale, individuate la cartella contenente crx-quickstart ed eseguite il comando seguente:

      `chmod -R 755 ../crx-quickstart`

   1. Aggiorna l’istanza di AEM a AEM 6.3. Per istruzioni dettagliate, consultate [Aggiornamento ad AEM 6.5](/help/sites-deploying/upgrade.md).

      Prima di continuare con i passaggi successivi, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano visualizzati nel file &lt;crx-repository>/error.log.

      >[!NOTE]
      >
      >Una volta che il server è in esecuzione, alcuni bundle di AEM Forms rimangono nello stato di installazione. Il numero di pacchetti può variare per ogni installazione. Potete ignorare lo stato di questi bundle. I bundle sono elencati in https://&#39;[server]:[port]&#39;/system/console/.

1. Installare il pacchetto del componente aggiuntivo AEM Forms. I passaggi sono elencati di seguito:

   1. Apri distribuzione [](https://experience.adobe.com/downloads)software. È necessario un Adobe ID  per accedere a Distribuzione software.
   1. Toccate **[!UICONTROL Adobe Experience Manager]** disponibile nel menu dell&#39;intestazione.
   1. Nella sezione **[!UICONTROL Filtri]** :
      1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]** .
      1. Selezionate la versione e digitate il tipo di pacchetto. Potete anche utilizzare l&#39;opzione Download **[!UICONTROL di]** ricerca per filtrare i risultati.
   1. Toccate il nome del pacchetto applicabile al sistema operativo in uso, selezionate **[!UICONTROL Accetta termini]** EULA e toccate **[!UICONTROL Scarica]**.
   1. Aprite [Package Manager](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
   1. Select the package and click **[!UICONTROL Install]**.

      Potete anche scaricare il pacchetto utilizzando il collegamento diretto elencato nell&#39;articolo delle release [](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) AEM Forms.

      >[!NOTE]
      >
      >Dopo l&#39;installazione del pacchetto, viene richiesto di riavviare l&#39;istanza di AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano visualizzati nel file &lt;crx-repository>/error.log e il registro sia stabile. Inoltre, alcuni pacchetti possono rimanere nello stato di installazione. Potete ignorare lo stato di questi pacchetti in tutta sicurezza.

1. Riavviate l’istanza di AEM.

1. Eseguire attività post-installazione.

   * **Esegui utility di migrazione**

      L’utility di migrazione rende compatibili i moduli adattivi e le risorse per la gestione della corrispondenza delle versioni precedenti con i moduli AEM 6.5. Potete scaricare l&#39;utility da Distribuzione software AEM. Per informazioni dettagliate su come configurare e utilizzare l’utility di migrazione, consultate Utility [di](../../forms/using/migration-utility.md)migrazione.

      Se si utilizza [Sample per integrare il componente](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) bozze e invii con il database e per eseguire l&#39;aggiornamento da una versione precedente, eseguire le query SQL seguenti dopo l&#39;esecuzione dell&#39;aggiornamento:

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

   * **(solo se si esegue l&#39;aggiornamento da AEM 6.2 Forms o versioni precedenti) Riconfigurare Adobe Sign**

      Se Adobe Sign è stato configurato nella versione precedente dei AEM Forms, riconfigurare Adobe Sign dai AEM cloud services. Per ulteriori dettagli, vedere [Integrazione di Adobe Sign con i AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Supporto per jQuery**

      In AEM 6.5 Forms, la versione di jQuery viene aggiornata alla 3.2.1 e la versione dell&#39;interfaccia utente jQuery alla 1.12.1. AEM Form utilizza JQuery in modalità **noConflict** . Pertanto, se utilizzate qualsiasi altra versione di jQuery, durante l&#39;esecuzione di un aggiornamento non vengono visualizzati problemi. Tuttavia, quando si esegue l&#39;aggiornamento ad AEM 6.5 Forms:

      * Verificate che gli eventuali componenti personalizzati siano compatibili con le versioni jQuery supportate.
      * Rimuovere le API non supportate dai componenti personalizzati. Consulta la guida [all&#39;](https://jquery.com/upgrade-guide/3.0/) aggiornamento per l&#39;elenco delle API rimosse. Ad esempio, il supporto per le API load(), .unload() e .error() viene rimosso. Utilizzate il metodo .on() al posto delle API citate sopra. Ad esempio, modificate $(&quot;img&quot;).load(fn) in $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(solo se si esegue l&#39;aggiornamento da AEM 6.2 Forms o versioni precedenti) Riconfigurare analisi e report**

      In AEM 6.4 Forms, la variabile di traffico per l’origine e l’evento di successo per l’impressione non sono disponibili. Pertanto, quando si esegue l&#39;aggiornamento da AEM 6.2 Forms o versioni precedenti, i AEM Forms smettono di inviare dati al server Adobe  Analytics e i report di analisi per i moduli adattivi non sono disponibili. Inoltre, AEM 6.4 Forms introduce la variabile del traffico per la versione dell&#39;analisi dei moduli e l&#39;evento di successo per il tempo trascorso su un campo. Quindi, riconfigurate analisi e report per l&#39;ambiente AEM Forms. Per informazioni dettagliate, consultate [Configurazione di analisi e rapporti](../../forms/using/configure-analytics-forms-documents.md).


1. Verificare che il server sia aggiornato correttamente, che tutti i dati siano migrati correttamente e che possa funzionare normalmente.

   * **Verificare lo stato dei bundle:** Verificate che tutti i bundle siano nello stato attivo.
   * **Verifica replica e replica inversa:** Pubblicare, compilare e inviare alcuni moduli migrati. Verificare anche i dati inviati.
   * **Verificare l&#39;accesso alle interfacce utente amministratore e sviluppatore:** Accedi all’istanza AEM da un account amministratore e verifica di avere accesso ai seguenti URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   In AEM 6.4 Forms, la struttura del repository crx è cambiata. Se esegui l’aggiornamento da 6.3 Forms a AEM 6.5 Forms, usa i percorsi modificati per la personalizzazione creati di nuovo. Per l&#39;elenco completo dei percorsi modificati, consultate Ristrutturazione archivio [moduli in AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).

