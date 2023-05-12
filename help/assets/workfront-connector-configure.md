---
title: Configurare [!DNL Workfront for Experience Manager enhanced connector]
description: Configurare [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 1%

---

# Configurare [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | Questo articolo |

Un utente con accesso amministratore in [!DNL Adobe Experience Manager] configura il connettore avanzato dopo l’installazione. Per istruzioni sull&#39;installazione, vedi [Installare il connettore](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* L&#39;Adobe richiede la distribuzione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
>
>* Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono tale connettore ridondante; in questo caso, potrebbe essere richiesto ai clienti di effettuare la transizione dall’utilizzo di questo connettore.
>
>* Adobe supporta le versioni di connettore avanzate 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per controllare la versione del connettore avanzato, passa alla `digital.hoodoo` gruppo disponibile nel riquadro a sinistra in [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it).
>
>* Vedi [Esame di certificazione dei partner per Workfront per il connettore avanzato Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedi [Guida all’esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Configurazione delle sottoscrizioni di eventi {#event-subscriptions}

Gli abbonamenti agli eventi vengono utilizzati per notificare AEM eventi che si verificano in [!DNL Adobe Workfront]. Ce ne sono tre [!DNL Workfront for Experience Manager enhanced connector] funzionalità che richiedono l’abbonamento a un evento per poter funzionare, sono le seguenti:

* Creazione automatica di cartelle collegate al progetto.
* Sincronizzazione delle modifiche apportate ai valori dei moduli personalizzati del documento Workfront con AEM metadati delle risorse.
* Pubblicazione automatica delle risorse in Brand Portal al termine del progetto.

Per utilizzare queste funzioni, abilita gli abbonamenti agli eventi.

* Modifica [!UICONTROL Strumenti Workfront] Configurazione dei Cloud Services creata al passaggio 5 e seleziona la [!UICONTROL Sottoscrizioni evento] scheda .
* Seleziona la [!UICONTROL Integrazione personalizzata Workfront] creato nella sezione 6.
* Fai clic su [!UICONTROL Abilita sottoscrizioni di eventi Workfront].

   ![Abbonamento evento](/help/assets/assets/event-subs.png)

## Configurare le cartelle collegate {#linked-folders}

Per abbonarti agli eventi, segui questi passaggi:

1. Passa a **[!UICONTROL Sottoscrizioni evento]** in servizi cloud.
1. Seleziona l’integrazione personalizzata creata in [!DNL Workfront].
1. Fai clic su **[!UICONTROL Abilita sottoscrizioni di eventi Workfront]**.

### Configurazione della struttura delle cartelle collegate {#linked-folder-structure}

1. Passa alla scheda Cartelle collegate al progetto nei servizi cloud.
1. Percorso padre della cartella collegata: Seleziona una cartella nel DAM in cui desideri creare le cartelle collegate. Se lasciato vuoto, verrà impostato automaticamente su /content/dam. Assicurati che lo schema metadati Workfront Tools e lo schema metadati della cartella collegata Workfront siano stati applicati alla cartella selezionata.
1. Struttura della cartella collegata: Immetti valori separati da virgole. Ogni valore deve essere `DE:<some-project-custom-form-field>`, Portfolio, programma, anno, nome o alcuni &quot;Valore stringa letterale&quot; (quest’ultimo con virgolette). È attualmente impostato su Portfolio,Programma,Anno,DE:Tipo di progetto,Nome.
1. Crea il titolo della cartella collegata in Workfront utilizzando la casella di controllo dei nomi della struttura della cartella se il titolo della cartella in Workfront deve includere tutte le cartelle nella struttura. In caso contrario, sarà il titolo dell’ultima cartella.
1. I campi multipli delle sottocartelle consentono di specificare un elenco di cartelle da creare come cartella figlia della cartella collegata.
1. Stato del progetto: Seleziona lo stato in cui deve essere impostato il progetto per creare la cartella collegata.
1. Crea una cartella collegata nei progetti con portfolio: Elenco di Portfoli a cui il progetto deve appartenere per creare la cartella collegata. Lascia vuoto questo elenco per creare la cartella collegata per tutto il portfolio di progetti.
1. Crea una cartella collegata in progetti con campo modulo personalizzato: Campo modulo personalizzato e il valore corrispondente che il progetto deve avere per creare la cartella collegata. Questa configurazione verrà ignorata se lasciata vuota. Seleziona `CUSTOM FORMS: Create DAM Linked Folder` per il campo e l&#39;input `Yes` per il valore.
1. Fai clic su Abilita creazione automatica di cartelle collegate. Tornando alla scheda Sottoscrizioni evento, viene visualizzato un evento di creazione.

![configurazione della cartella collegata](/help/assets/assets/wf-linked-folder-config.png)

## Mappatura schema metadati {#metadata-schema-mapping}

### Configurare la mappatura dei metadati delle cartelle {#folder-metadata-mapping}

La mappatura dei metadati tra progetti Workfront e cartelle AEM è definita all’interno AEM schemi metadati cartelle. Gli schemi di metadati delle cartelle devono essere creati e configurati come di consueto in AEM. Strumenti di Workfront aggiunge un menu a discesa di completamento automatico alla scheda Configurazione impostazioni di ciascun campo modulo schema metadati della cartella. Questo menu a discesa di completamento automatico consente di specificare a quale campo Workfront deve essere mappata ciascuna proprietà AEM cartella.

Per configurare le mappature, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati cartelle]**.
1. Selezionare il modulo schema metadati della cartella da modificare e fare clic su Modifica.
1. Selezionare il campo del modulo schema metadati della cartella da modificare e selezionare la scheda Impostazioni nel pannello di destra.
1. In [!UICONTROL Mappato da campo Workfront] selezionare il nome del campo Workfront da mappare alla proprietà della cartella AEM selezionata. Le opzioni disponibili sono:

   * Campi modulo personalizzati del progetto
   * Campi Panoramica del progetto (ID, Nome, Descrizione, Numero di riferimento, Data di completamento pianificata, Proprietario del progetto, Sponsor del progetto, Portfolio o programma)

![configurazione mappatura metadati](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configurare la mappatura dei metadati delle risorse {#asset-metadata-mapping}

La mappatura dei metadati tra documenti Adobe Workfront e risorse è definita all’interno AEM schemi di metadati. Gli schemi di metadati devono essere creati e configurati come di consueto in AEM. Strumenti di Workfront aggiunge opzioni di configurazione alla scheda Configurazione impostazioni di ciascun campo modulo schema metadati. Queste opzioni consentono di specificare a quale campo Workfront deve essere mappata ciascuna proprietà AEM.

Per configurare le mappature, effettua le seguenti operazioni:

1. Passa a **Strumenti** > **Risorse** > **Schemi metadati**.
1. Seleziona il modulo schema metadati da modificare e fai clic su **Modifica** oppure crea un nuovo schema di metadati da zero.
1. Selezionare il campo modulo schema metadati da modificare e selezionare **Impostazioni** nel pannello di destra.
1. In [!DNL Workfront] Campo modulo personalizzato seleziona il nome del [!DNL Workfront] campo da mappare alla proprietà AEM selezionata. Le opzioni disponibili sono:

   * Campi modulo personalizzati del documento
   * Campi modulo personalizzati del progetto
   * Genera campi modulo personalizzati
   * Campi modulo personalizzati dell’attività
   * Campi Panoramica progetto (ID, Nome, Descrizione o Numero di riferimento)

1. Nel caso in cui [!DNL Workfront] campo selezionato in [!UICONTROL Campo modulo personalizzato Workfront] è un campo Workfront User type-ahead e sarà necessario specificare quale campo Workfront User si desidera mappare. A questo scopo, selezionare Ottieni valore dal campo oggetto di riferimento Workfront, quindi specificare il nome del [!UICONTROL Campo modulo personalizzato utente Workfront] da cui recuperare il valore da mappare.

   ![configurazione mappatura metadati](/help/assets/assets/wf-metadata-mapping-config1.png)

## Proprietà mappa {#map-property}

Questo passaggio del flusso di lavoro consente a un utente di mappare una proprietà su un [!DNL Workfront] modulo personalizzato su un progetto, un&#39;attività, un problema o un documento. La [!DNL Workfront] l&#39;artefatto che questo passaggio influisce viene cercato utilizzando un percorso relativo dal payload. Le proprietà da mappare sono controllate dalla configurazione della finestra di dialogo dei passaggi.

**Tipo**: Questo campo consente di selezionare il tipo di oggetto Workfront a cui mappare le proprietà.

**Proprietà ID**: Questo campo consente di specificare il percorso dell’ID dell’oggetto Workfront a cui le proprietà devono essere mappate. Il percorso specificato in questo campo deve essere relativo al payload del flusso di lavoro.

**Assegnazioni proprietà**: Questo multicampo consente di specificare le mappature tra le proprietà AEM e i campi Workfront. Ogni elemento nel campo multiplo specifica una mappatura. Ogni mappatura deve avere il formato `<workfront-field>=<aem-mapped-property>`.

* La `workfront-field` può

   * Un campo modulo personalizzato identificato dal prefisso `DE:`.
   * Campo modificabile identificato dal relativo nome. I nomi dei campi si trovano in [[!DNL Workfront] API explorer](https://experience.workfront.com/s/api-explorer).

* La `aem-mapped-property` può essere:

   * Valore letterale. Queste devono essere racchiuse tra virgolette.
   * Una proprietà AEM. Questo riferimento deve essere relativo al payload del flusso di lavoro.
   * Un valore denominato. Queste devono essere circondate da parentesi.
   * Una concatenazione dei 3 elementi di cui sopra. Specifica tramite `{+}`.
   * Una modifica dei 3 elementi di cui sopra circondando il valore con `{replace(<value>,"old-char","new-char")}`.

* Alcuni esempi sono:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Configurazione per mappare la proprietà](/help/assets/assets/wf-map-property-config.png)

## Imposta stato {#set-status}

Nell’editor del flusso di lavoro, modifica le proprietà di **[!UICONTROL Workfront - Imposta stato]** in **[!UICONTROL Argomenti]** scheda .

![Modifica flusso di lavoro per impostare lo stato](/help/assets/assets/wf-set-status.png)

## Sincronizzazione dei commenti {#comments-sync}

1. In [!DNL Experience Manager], accesso **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione strumenti Workfront]**, seleziona la configurazione e seleziona **[!UICONTROL Proprietà]**.

   ![sincronizzazione commenti](/help/assets/assets/comments-sync1.png)

1. Seleziona **[!UICONTROL Sottoscrizioni evento]** scheda , fai clic su **[!UICONTROL Abilita sincronizzazione commenti]** su **[!UICONTROL Invia commenti effettuati in Workfront a AEM]** opzione .

   ![Sincronizzazione abilitata](/help/assets/assets/wf-comment-sync-enabled.png)

Per verificare la sincronizzazione dei commenti da Workfront a AEM, effettua le seguenti operazioni:

1. Passa a un documento collegato in Workfront e aggiungi un commento nella scheda Aggiornamenti .

   ![lascia un commento in Workfront](/help/assets/assets/comments-sync2.png)

1. Passa allo stesso documento collegato in AEM, seleziona il documento e apri il [!UICONTROL Timeline] nella navigazione a sinistra e seleziona [!UICONTROL Commenti]. Nella barra laterale sinistra vengono visualizzati i commenti sincronizzati da [!DNL Workfront].

## Versioni delle risorse {#asset-versions}

Per mantenere la cronologia delle versioni delle risorse in AEM, configura il controllo delle versioni delle risorse in AEM.

1. Ad Experience Manager, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione strumenti Workfront]**, e apri la **[!UICONTROL Avanzate]** scheda .

1. Opzione Seleziona **[!UICONTROL Archiviare risorse con lo stesso nome delle versioni della risorsa esistente]**. Quando questa opzione è selezionata, consente di memorizzare le risorse caricate con lo stesso nome e nella stessa posizione della versione della risorsa esistente. Se questa opzione è deselezionata, verrà creata una nuova risorsa con un nome diverso (ad esempio `asset-name.pdf` e `asset-name-1.pdf`).

1. Opzione Seleziona **[!UICONTROL Aggiornare i metadati delle risorse durante la creazione di una nuova versione]**. Quando questa opzione è selezionata, i metadati della risorsa vengono aggiornati ogni volta che viene creata una nuova versione della risorsa. Se questa opzione è deselezionata, la risorsa conserva i metadati che aveva prima di creare la nuova versione.

![configurare il controllo delle versioni delle risorse](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Il controllo delle versioni non è supportato nelle cartelle collegate. Durante la creazione di un [!DNL Workfront] i commenti e le annotazioni sulla versione precedente della risorsa vengono rimossi con un documento all’interno di una cartella collegata.

## Allegare moduli personalizzati {#attach-custom-forms}

Questo passaggio del flusso di lavoro consente agli utenti di allegare un modulo personalizzato a un [!DNL Workfront] artefatto. Questo passaggio del flusso di lavoro può essere aggiunto a qualsiasi modello di flusso di lavoro. La [!DNL Workfront] l&#39;artefatto che questo passaggio interessa sarà cercato utilizzando un percorso relativo dal payload.

Nell’editor del flusso di lavoro in Experience Manager, modifica le proprietà di [!UICONTROL Workfront - Allega modulo personalizzato] passaggio del flusso di lavoro.

![moduli personalizzati](/help/assets/assets/wf-custom-forms.png).

## Pubblicare automaticamente le risorse {#auto-publish-assets}

1. Ad Experience Manager, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione strumenti Workfront]**, e apri la **[!UICONTROL Avanzate]** scheda .

1. Seleziona **[!UICONTROL Pubblica automaticamente le risorse quando vengono inviate da Workfront]**. Questa opzione consente la pubblicazione automatica delle risorse quando vengono inviate da Workfront a AEM. Questa funzione può essere abilitata a determinate condizioni specificando un campo modulo personalizzato Workfront e il valore su cui deve essere impostata. Ogni volta che un documento viene inviato a AEM, se soddisfa la condizione, la risorsa verrà pubblicata automaticamente.

1. Seleziona **[!UICONTROL Pubblica tutte le risorse di progetto in Brand Portal al termine del progetto]**. Questa opzione consente la pubblicazione automatica delle risorse in [!DNL Brand Portal] quando lo stato del progetto Workfront a cui appartengono viene modificato in `Complete`.

![configura pubblicazione automatica](/help/assets/assets/wf-auto-publish-config.png)

## Aggiornamenti dei moduli personalizzati di Workfront {#subscribe-workfront-doc-custom-form-updates}

Per abbonarti alle modifiche in [!DNL Workfront] moduli personalizzati del documento, seleziona l’opzione relativa nel **[!UICONTROL Avanzate]** scheda . Quando ti abboni a questi aggiornamenti, aggiorna la tua mappatura [!DNL Experience Manager] campi di metadati quando il campo corrispondente in [!DNL Workfront] il modulo personalizzato del documento viene modificato.

![Configurazione degli aggiornamenti dei moduli personalizzati per i documenti Workfront in [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
