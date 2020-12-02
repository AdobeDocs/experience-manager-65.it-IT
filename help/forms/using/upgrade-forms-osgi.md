---
title: Aggiornamento a AEM 6.5 Forms
seo-title: Aggiornamento a AEM 6.5 Forms
description: È possibile eseguire un aggiornamento diretto da Forms 6.1, Forms 6.2 e da Forms ES4 SP1 a AEM 6.3.
seo-description: È possibile eseguire un aggiornamento diretto da Forms 6.1, Forms 6.2 e da Forms ES4 SP1 a AEM 6.3.
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


# Aggiornamento a AEM 6.5 Forms su OSGi {#upgrade-to-aem-forms-osgi}

Potete eseguire un aggiornamento diretto da AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms.

Il percorso di aggiornamento diretto da **AEM 6.0 Forms, AEM 6.1 Forms** e **AEM 6.2 Forms** a AEM 6.5 Forms non è disponibile. Eseguire un [aggiornamento intermedio a AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [aggiornamento a AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html) o [aggiornamento a AEM 6.4 Forms](/help/forms/using/upgrade.md), quindi effettuare l&#39;aggiornamento da AEM 6.3 Forms, o AEM 6.4 Forms a AEM 6.5.

Per effettuare l’aggiornamento da AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms, effettuate le seguenti operazioni:

1. Aggiornare l&#39;istanza AEM esistente a AEM 6.5. I passaggi sono elencati di seguito:

   1. Installate il service pack e le patch più recenti per AEM 6.3 Forms o AEM 6.4 Forms. Per informazioni dettagliate, vedere [AEM SustMaintenance Hub](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html).
   1. Preparare l’istanza di origine per l’aggiornamento. Per i passaggi dettagliati, vedere [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Scaricate la [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Solo installazioni basate su Unix/Linux)** Se utilizzate UNIX o Linux come sistema operativo sottostante, aprite la finestra del terminale, individuate la cartella contenente crx-quickstart ed eseguite il comando seguente:

      `chmod -R 755 ../crx-quickstart`

   1. Aggiorna l&#39;istanza AEM a AEM 6.3. Per istruzioni dettagliate, vedere [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).

      Prima di continuare con i passaggi successivi, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano visualizzati nel file &lt;crx-repository>/error.log.

      >[!NOTE]
      >
      >Una volta che il server è in esecuzione, alcuni  bundle AEM Forms rimangono nello stato di installazione. Il numero di pacchetti può variare per ogni installazione. Potete ignorare lo stato di questi bundle. I bundle sono elencati in https://&#39;[server]:[porta]&#39;/system/console/.

1. Installate  pacchetto del componente aggiuntivo AEM Forms. I passaggi sono elencati di seguito:

   1. Aprire [Distribuzione software](https://experience.adobe.com/downloads). È necessario un Adobe ID  per accedere a Distribuzione software.
   1. Toccate **[!UICONTROL Adobe Experience Manager]** disponibile nel menu di intestazione.
   1. Nella sezione **[!UICONTROL Filtri]**:
      1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
      1. Selezionate la versione e digitate il tipo di pacchetto. Potete anche utilizzare l&#39;opzione **[!UICONTROL Download di ricerca]** per filtrare i risultati.
   1. Toccate il nome del pacchetto applicabile al sistema operativo in uso, selezionate **[!UICONTROL Accetta termini EULA]**, quindi toccate **[!UICONTROL Scarica]**.
   1. Aprite [Gestione pacchetti](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
   1. Selezionate il pacchetto e fate clic su **[!UICONTROL Installa]**.

      Potete anche scaricare il pacchetto utilizzando il collegamento diretto elencato nell&#39;articolo [ rilasci di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html).

      >[!NOTE]
      >
      >Dopo l&#39;installazione del pacchetto, viene richiesto di riavviare l&#39;istanza AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms , attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano visualizzati nel file  &lt;crx-repository>/error.log e il registro sia stabile. Inoltre, alcuni pacchetti possono rimanere nello stato di installazione. Potete ignorare lo stato di questi pacchetti in tutta sicurezza.

1. Riavviate l&#39;istanza AEM.

1. Eseguire attività post-installazione.

   * **Esegui utility di migrazione**

      L&#39;utility di migrazione rende compatibili i moduli adattivi e le risorse per la gestione della corrispondenza delle versioni precedenti con i moduli AEM 6.5. È possibile scaricare l&#39;utility da AEM Distribuzione software. Per informazioni dettagliate su come configurare e utilizzare l&#39;utility di migrazione, consultate [utility di migrazione](../../forms/using/migration-utility.md).

      Se si utilizza [Esempio per integrare il componente Bozze e invii](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) con il database e per eseguire l&#39;aggiornamento da una versione precedente, eseguire le query SQL seguenti dopo aver eseguito l&#39;aggiornamento:

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

   * **(solo se si esegue l&#39;aggiornamento da AEM 6.2 Forms o versioni precedenti) Riconfigurare  Adobe Sign**

      Se  Adobe Sign è stato configurato nella versione precedente di  AEM Forms, riconfigurate  Adobe Sign dai servizi AEM Cloud. Per ulteriori dettagli, vedere [Integrare  Adobe Sign con  AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Supporto per jQuery**

      Nell&#39;Forms AEM 6.5, la versione di jQuery viene aggiornata alla 3.2.1 e la versione dell&#39;interfaccia utente jQuery alla 1.12.1. AEM Form utilizza JQuery in modalità **noConflict**. Pertanto, se utilizzate qualsiasi altra versione di jQuery, durante l&#39;esecuzione di un aggiornamento non vengono visualizzati problemi. Tuttavia, quando effettuate l’aggiornamento a Forms AEM 6.5:

      * Verificate che gli eventuali componenti personalizzati siano compatibili con le versioni jQuery supportate.
      * Rimuovere le API non supportate dai componenti personalizzati. Consulta [guida all&#39;aggiornamento](https://jquery.com/upgrade-guide/3.0/) per l&#39;elenco delle API rimosse. Ad esempio, il supporto per le API load(), .unload() e .error() viene rimosso. Utilizzate il metodo .on() al posto delle API citate sopra. Ad esempio, modificate $(&quot;img&quot;).load(fn) in $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(solo se si esegue l&#39;aggiornamento da AEM 6.2 Forms o versioni precedenti) Riconfigurare analisi e report**

      Nell&#39;Forms AEM 6.4, la variabile di traffico per l&#39;origine e l&#39;evento di successo per l&#39;impressione non sono disponibili. Pertanto, quando si esegue l&#39;aggiornamento da AEM 6.2 Forms o versioni precedenti,  AEM Forms interrompe l&#39;invio di dati  server Adobe Analytics e i report di analisi per i moduli adattivi non sono disponibili. Inoltre, AEM 6.4 Forms introduce la variabile del traffico per la versione dell&#39;analisi dei moduli e l&#39;evento di successo per il tempo trascorso su un campo. Quindi, riconfigurate analisi e report per il vostro ambiente AEM Forms . Per i passaggi dettagliati, vedere [Configurazione di analisi e report](../../forms/using/configure-analytics-forms-documents.md).


1. Verificare che il server sia aggiornato correttamente, che tutti i dati siano migrati correttamente e che possa funzionare normalmente.

   * **Verificare lo stato dei bundle:** Verificare che tutti i bundle siano nello stato attivo.
   * **Verificare la replica e la replica inversa:** pubblicare, compilare e inviare alcuni moduli migrati. Verificare anche i dati inviati.
   * **Verifica l&#39;accesso alle interfacce utente di amministrazione e sviluppatore:** Accedi a AEM&#39;istanza da un account amministratore e verifica di avere accesso ai seguenti URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   In Forms AEM 6.4, la struttura del repository crx è cambiata. Se esegui l’aggiornamento da Forms 6.3 a Forms AEM 6.5, usa i percorsi modificati per la personalizzazione creati di nuovo. Per l&#39;elenco completo dei percorsi modificati, vedere [Ristrutturazione repository Forms in AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).

