---
title: Aggiornamento ad AEM 6.5 Forms
seo-title: Aggiornamento ad AEM 6.5 Forms
description: È possibile eseguire un aggiornamento diretto da Forms 6.1, Forms 6.2 AEM e LiveCycle ES4 SP1 a Forms 6.3.
seo-description: È possibile eseguire un aggiornamento diretto da Forms 6.1, Forms 6.2 AEM e LiveCycle ES4 SP1 a Forms 6.3.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 6%

---

# Aggiornamento a AEM 6.5 Forms su OSGi {#upgrade-to-aem-forms-osgi}

Puoi eseguire un aggiornamento diretto da Forms 6.3 o Forms AEM 6.4 a Forms 6.5 AEM.

Il percorso di aggiornamento diretto da **AEM 6.0 Forms, AEM 6.1 Forms** e **AEM 6.2 Forms** a AEM 6.5 Forms non è disponibile. Esegui un [aggiornamento intermedio a AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [aggiornamento a AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html) o [aggiornamento a AEM 6.4 Forms](/help/forms/using/upgrade.md) e quindi esegui l&#39;aggiornamento da AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5.

Effettua le seguenti operazioni per eseguire l’aggiornamento da Forms 6.3 o Forms AEM 6.4 a Forms 6.5 AEM:

1. Aggiorna l&#39;istanza AEM esistente a AEM 6.5. I passaggi sono elencati di seguito:

   1. Installa il service pack e le patch più recenti per Forms 6.3 o AEM 6.4 Forms. Per informazioni dettagliate, consulta [AEM SustMaintenance Hub](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it).
   1. Prepara l&#39;istanza sorgente per l&#39;aggiornamento. Per passaggi dettagliati, consulta [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Scarica la [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Solo installazioni basate su Unix/Linux)** Se utilizzi UNIX o Linux come sistema operativo sottostante, apri la finestra del terminale, accedi alla cartella contenente crx-quickstart ed esegui il seguente comando:

      `chmod -R 755 ../crx-quickstart`

   1. Aggiorna l&#39;istanza AEM a AEM 6.3. Per istruzioni dettagliate, consulta [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).

      Prima di continuare con i passaggi successivi, attendi che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED smettano di essere visualizzati nel file &lt;crx-repository>/error.log .

      >[!NOTE]
      >
      >Quando il server è in esecuzione, alcuni bundle AEM Forms rimangono nello stato di installazione. Il numero di bundle può variare per ogni installazione. Puoi tranquillamente ignorare lo stato di questi bundle. I bundle sono elencati in https://&#39;[server]:[port]&#39;/system/console/.

1. Installa il pacchetto aggiuntivo di AEM Forms. I passaggi sono elencati di seguito:

   1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
   1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
   1. Nella sezione **[!UICONTROL Filtri]** :
      1. Seleziona **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
      1. Seleziona la versione e digita il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Download di ricerca]** per filtrare i risultati.
   1. Tocca il nome del pacchetto applicabile al tuo sistema operativo, seleziona **[!UICONTROL Accetta termini EULA]** e tocca **[!UICONTROL Scarica]**.
   1. Apri [Gestione pacchetti](https://docs.adobe.com/content/help/it/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
   1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

      Puoi anche scaricare il pacchetto utilizzando il collegamento diretto elencato nell&#39;articolo [Versioni di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) .

      >[!NOTE]
      >
      >Una volta installato il pacchetto, viene richiesto di riavviare l&#39;istanza AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED smettano di apparire nel file  &lt;crx-repository>/error.log e il registro sia stabile. Inoltre, alcuni pacchetti possono rimanere nello stato di installazione. Puoi ignorare lo stato di questi pacchetti in tutta sicurezza.

1. Riavvia l&#39;istanza AEM.

1. Eseguire attività post-installazione.

   * **Esegui utility di migrazione**

      L’utility di migrazione rende compatibili le risorse di gestione della corrispondenza e dei moduli adattivi delle versioni precedenti con AEM 6.5 forms. È possibile scaricare l&#39;utility da Distribuzione software AEM. Per informazioni dettagliate su come configurare e utilizzare l&#39;utility di migrazione, consulta [utility di migrazione](../../forms/using/migration-utility.md).

      Se utilizzi [Esempio per integrare il componente per bozze e invii](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) con il database e per l&#39;aggiornamento da una versione precedente, esegui le seguenti query SQL dopo l&#39;esecuzione dell&#39;aggiornamento:

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

   * **(Solo per l’aggiornamento da AEM 6.2 Forms o versioni precedenti) Riconfigura Adobe Sign**

      Se Adobe Sign era stato configurato nella versione precedente di AEM Forms, riconfigura Adobe Sign dai servizi AEM Cloud. Per ulteriori dettagli, consulta [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Supporto per jQuery**

      In Forms 6.5, la versione di jQuery viene aggiornata alla versione 3.2.1 e l&#39;interfaccia utente jQuery viene aggiornata alla versione 1.12.1. AEM Form utilizza JQuery in modalità **noConflict**. Quindi, se utilizzi qualsiasi altra versione di jQuery, non vengono visualizzati problemi durante l’esecuzione di un aggiornamento. Tuttavia, quando esegui l’aggiornamento a Forms 6.5 AEM:

      * Assicurati che gli eventuali componenti personalizzati siano compatibili con le versioni jQuery supportate.
      * Rimuovi le API non supportate dai componenti personalizzati. Consulta [guida all&#39;aggiornamento](https://jquery.com/upgrade-guide/3.0/) per l&#39;elenco delle API rimosse. Ad esempio, il supporto per le API load(), .unload() e .error() viene rimosso. Utilizza il metodo .on() al posto delle API di cui sopra. Ad esempio, cambia $(&quot;img&quot;).load(fn) in $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(Solo per l’aggiornamento da Forms 6.2 o versioni precedenti) Riconfigura analisi e rapporti**

      In Forms 6.4 AEM, la variabile di traffico per la sorgente e l’evento di successo per l’impression non sono disponibili. Pertanto, quando esegui l’aggiornamento da AEM 6.2 Forms o versioni precedenti, AEM Forms smette di inviare dati al server Adobe Analytics e i rapporti di analisi per i moduli adattivi non sono disponibili. Inoltre, AEM 6.4 Forms introduce una variabile di traffico per la versione di analisi dei moduli e un evento di successo per la quantità di tempo trascorso su un campo. Quindi, riconfigura analisi e rapporti per il tuo ambiente AEM Forms. Per passaggi dettagliati, consulta [Configurazione di analisi e rapporti](../../forms/using/configure-analytics-forms-documents.md).


1. Verificare che il server sia stato aggiornato correttamente, che anche tutti i dati siano migrati correttamente e che possa funzionare normalmente.

   * **Verifica lo stato dei bundle:** Assicurati che tutti i bundle siano in stato attivo.
   * **Verificare la replica e la replica inversa:** pubblicare, compilare e inviare alcuni moduli migrati. Verifica anche i dati inviati.
   * **Verifica l&#39;accesso alle interfacce utente amministratore e sviluppatore:** accedi a AEM&#39;istanza da un account amministratore e verifica di avere accesso ai seguenti URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   In Forms 6.4 AEM, la struttura di crx-repository è cambiata. Se esegui l’aggiornamento da Forms 6.3 a Forms 6.5, utilizza i percorsi modificati per la personalizzazione che crei nuovamente. Per l&#39;elenco completo dei percorsi modificati, vedere [Ristrutturazione dell&#39;archivio Forms in AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).
