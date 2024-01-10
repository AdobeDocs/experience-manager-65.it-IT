---
title: Configura [!DNL Workfront for Experience Manager enhanced connector]
description: Configura [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
source-git-commit: 2cf980f643e1896ecd581fec44f963d7eb44766d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# Configurare [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | Questo articolo |

Un utente con accesso amministratore in [!DNL Adobe Experience Manager] configura il connettore avanzato dopo averlo installato. Per istruzioni sull&#39;installazione, vedere [Installare il connettore](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* L’Adobe richiede l’implementazione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
>
>* Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono questo connettore ridondante; in tal caso, i clienti potrebbero dover passare dall’utilizzo di questo connettore.
>
>* Adobe supporta le versioni migliorate del connettore 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione del connettore avanzato, passare alla `digital.hoodoo` gruppo disponibile nel riquadro a sinistra in [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* Consulta [Connettore avanzato per la certificazione dei partner per Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedere [Guida all’esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Configurare le sottoscrizioni di eventi {#event-subscriptions}

Gli abbonamenti agli eventi vengono utilizzati per notificare all’AEM gli eventi che si verificano in [!DNL Adobe Workfront]. Sono tre [!DNL Workfront for Experience Manager enhanced connector] funzionalità che richiedono abbonamenti agli eventi per funzionare, sono:

* Creazione automatica di cartelle collegate al progetto.
* Sincronizzazione delle modifiche nei valori del modulo personalizzato del documento Workfront con i metadati delle risorse AEM.
* Pubblicazione automatica delle risorse in Brand Portal al completamento del progetto.

Per utilizzare queste funzioni, abilita sottoscrizioni eventi.

* Modifica [!UICONTROL Strumenti Workfront] configurazione dei Cloud Service creata al passaggio 5 e selezionare [!UICONTROL Abbonamenti eventi] scheda.
* Seleziona la [!UICONTROL Integrazione personalizzata Workfront] creato nella sezione 6.
* Clic [!UICONTROL Abilita sottoscrizioni eventi Workfront].

  ![Abbonamento evento](/help/assets/assets/event-subs.png)

## Configurare le cartelle collegate {#linked-folders}

Per iscriverti agli eventi, segui questi passaggi:

1. Accedi a **[!UICONTROL Abbonamenti eventi]** nei servizi cloud.
1. Seleziona l’integrazione personalizzata creata in [!DNL Workfront].
1. Clic **[!UICONTROL Abilita sottoscrizioni eventi Workfront]**.

### Configurazione della struttura delle cartelle collegate {#linked-folder-structure}

1. Vai alla scheda Cartelle collegate al progetto nei servizi cloud.
1. Percorso principale della cartella collegata: seleziona una cartella in DAM in cui desideri creare le cartelle collegate. Se lasciato vuoto, per impostazione predefinita viene impostato su /content/dam. Verificare che lo schema metadati Strumenti di Workfront e lo schema metadati cartelle collegate a Workfront siano stati applicati alla cartella selezionata.
1. Struttura delle cartelle collegate: immetti valori separati da virgole. Ogni valore deve essere `DE:<some-project-custom-form-field>`, Portfolio, Programma, Anno, Nome o un &quot;valore stringa letterale&quot; (quest&#39;ultimo con virgolette). Attualmente è impostato su Portfolio,Programma,Anno,DE:Tipo di progetto,Nome.
1. Configurare le autorizzazioni: Aggiungi `jcr:all permissions` autorizzazioni a `/conf/workfront-tools/settings/cloudconfigs` per `wf-workfront-users` gruppo.
1. Se il titolo della cartella in Workfront deve includere tutte le cartelle della struttura, seleziona la casella di controllo Crea titolo della cartella collegata in Workfront utilizzando i nomi della struttura di cartelle. In caso contrario, si tratta del titolo dell&#39;ultima cartella.
1. Sottocartelle con più campi consente di specificare un elenco di cartelle da creare come cartella secondaria della cartella collegata.
1. Stato progetto: seleziona lo stato del progetto per creare la cartella collegata.
1. Creazione di una cartella collegata in progetti con portfolio: elenco di Portfoli a cui il progetto deve appartenere per creare la cartella collegata. Lascia vuoto questo elenco per creare la cartella collegata per tutto il portfolio di progetti.
1. Creare una cartella collegata nei progetti con campo modulo personalizzato: campo modulo personalizzato e il valore corrispondente che il progetto deve avere per creare la cartella collegata. Questa configurazione viene ignorata se viene lasciata vuota. Seleziona `CUSTOM FORMS: Create DAM Linked Folder` per il campo e l’input `Yes` per il valore.
1. Fai clic su Abilita creazione automatica di cartelle collegate. Se torni alla scheda Sottoscrizioni evento, vedrai che ora è presente un evento di creazione.

![configurazione cartella collegata](/help/assets/assets/wf-linked-folder-config.png)

## Mappatura schema metadati {#metadata-schema-mapping}

### Configurare la mappatura dei metadati delle cartelle {#folder-metadata-mapping}

La mappatura dei metadati tra i progetti Workfront e le cartelle AEM è definita negli schemi di metadati delle cartelle AEM. Gli schemi di metadati delle cartelle devono essere creati e configurati come di consueto in AEM. Strumenti di Workfront aggiunge un elenco a discesa di completamento automatico alla scheda Configurazione impostazioni di ogni campo modulo schema metadati cartelle. Questo menu a discesa di completamento automatico consente di specificare a quale campo Workfront deve essere mappata ogni proprietà della cartella AEM.

Per configurare le mappature, effettua le seguenti operazioni:

1. Aggiungi `jcr:read` autorizzazioni a `/conf/global/settings/dam/adminui-extension/foldermetadataschema` per `wf-workfront-users` gruppo.
1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati cartelle]**.
1. Seleziona il modulo schema metadati cartelle da modificare e fai clic su Modifica.
1. Seleziona il campo modulo schema metadati cartelle da modificare e seleziona la scheda Impostazioni nel pannello di destra.
1. In entrata [!UICONTROL Mappato dal campo Workfront] , selezionare il nome del campo Workfront che si desidera mappare alla proprietà della cartella AEM selezionata. Le opzioni disponibili sono:

   * Campi modulo personalizzati del progetto
   * Campi Panoramica progetto (ID, Nome, Descrizione, Numero di riferimento, Data di completamento pianificata, Proprietario progetto, Sponsor progetto, Portfolio o Programma)

![configurazione mappatura metadati](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configurare la mappatura dei metadati delle risorse {#asset-metadata-mapping}

La mappatura dei metadati tra i documenti di Adobe Workfront e le risorse è definita negli schemi di metadati AEM. Gli schemi di metadati devono essere creati e configurati come di consueto in AEM. Strumenti di Workfront aggiunge opzioni di configurazione alla scheda Configurazione impostazioni di ciascun campo modulo schema metadati. Queste opzioni ti consentono di specificare a quale campo Workfront deve essere mappata ogni proprietà AEM.

Per configurare le mappature, effettua le seguenti operazioni:

1. Accedi a **Strumenti** > **Risorse** > **Schemi metadati**.
1. Seleziona il modulo schema metadati da modificare e fai clic su **Modifica** oppure crea uno schema di metadati da zero.
1. Seleziona il campo del modulo schema metadati da modificare e seleziona **Impostazioni** nel pannello di destra.
1. In entrata [!DNL Workfront] Campo modulo personalizzato seleziona il nome del [!DNL Workfront] che desideri mappare sulla proprietà AEM selezionata. Le opzioni disponibili sono:

   * Documenta campi modulo personalizzati
   * Campi modulo personalizzati del progetto
   * Campi modulo personalizzati problema
   * Campi modulo personalizzato attività
   * Campi Panoramica progetto (ID, Nome, Descrizione o Numero di riferimento)

1. Nel caso in cui [!DNL Workfront] campo selezionato in [!UICONTROL Campo modulo personalizzato Workfront] è un campo di completamento automatico di tipo utente di Workfront, sarà necessario specificare quale campo utente di Workfront si desidera mappare. A tale scopo, selezionare Ottieni valore dal campo oggetto di riferimento Workfront e quindi specificare il nome dell&#39; [!UICONTROL Campo modulo personalizzato utente Workfront] da cui recuperare il valore da mappare.

   ![configurazione mappatura metadati](/help/assets/assets/wf-metadata-mapping-config1.png)

## Proprietà mappa {#map-property}

Questo passaggio di flusso di lavoro consente a un utente di mappare una proprietà su un [!DNL Workfront] modulo personalizzato per un progetto, un’attività, un problema o un documento. Il [!DNL Workfront] artefatto che questo passaggio influisce viene cercato utilizzando un percorso relativo dal payload. Le proprietà da mappare sono controllate dalla configurazione della finestra di dialogo dei passaggi.

**Tipo**: questo campo consente di selezionare il tipo di oggetto Workfront a cui mappare le proprietà.

**ID, proprietà**: questo campo consente di specificare il percorso dell’ID dell’oggetto Workfront a cui mappare le proprietà. Il percorso specificato in questo campo deve essere relativo al payload del flusso di lavoro.

**Assegnazioni proprietà**: questo campo multiplo consente di specificare le mappature tra le proprietà AEM e i campi Workfront. Ogni elemento nel campo multiplo specifica una mappatura. Ogni mappatura deve avere il formato `<workfront-field>=<aem-mapped-property>`.

* Il `workfront-field` può essere

   * Campo modulo personalizzato identificato dal prefisso `DE:`.
   * Campo modificabile identificato dal relativo nome. I nomi dei campi si trovano in [[!DNL Workfront] API Explorer](https://experience.workfront.com/s/api-explorer).

* Il `aem-mapped-property` può essere:

   * Un valore letterale. Queste devono essere racchiuse tra virgolette.
   * Una proprietà AEM. Questo riferimento deve essere relativo al payload del flusso di lavoro.
   * Un valore denominato. Queste devono essere racchiuse tra parentesi.
   * Una concatenazione dei 3 elementi sopra indicati. Specificalo utilizzando `{+}`.
   * Una modifica dei 3 elementi precedenti racchiudendo il valore con `{replace(<value>,"old-char","new-char")}`.

* Alcuni esempi sono:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Configurazione per mappare la proprietà](/help/assets/assets/wf-map-property-config.png)

## Imposta stato {#set-status}

Nell’editor del flusso di lavoro, modifica le proprietà di **[!UICONTROL Workfront - Imposta stato]** nel **[!UICONTROL Argomenti]** scheda.

![Modifica flusso di lavoro per impostare lo stato](/help/assets/assets/wf-set-status.png)

## Sincronizzazione commenti {#comments-sync}

1. In entrata [!DNL Experience Manager], accesso **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione strumenti Workfront]**, seleziona la configurazione e seleziona **[!UICONTROL Proprietà]**.

   ![commenti sincronizzati](/help/assets/assets/comments-sync1.png)

1. Seleziona **[!UICONTROL Abbonamenti eventi]** , fare clic su **[!UICONTROL Abilita sincronizzazione commenti]** il **[!UICONTROL Inviare commenti aggiunti in Workfront all’AEM]** opzione.

   ![Sincronizzazione abilitata](/help/assets/assets/wf-comment-sync-enabled.png)

Per verificare la sincronizzazione dei commenti da Workfront all’AEM, effettua le seguenti operazioni:

1. Passa a un documento collegato in Workfront e aggiungi un commento nella scheda Aggiornamenti.

   ![lascia un commento in Workfront](/help/assets/assets/comments-sync2.png)

1. Passare allo stesso documento collegato in AEM, selezionare il documento e aprire [!UICONTROL Timeline] nella barra di navigazione a sinistra, quindi seleziona [!UICONTROL Commenti]. Nella barra laterale a sinistra vengono visualizzati i commenti sincronizzati da [!DNL Workfront].

## Versioni risorsa {#asset-versions}

Per mantenere la cronologia delle versioni delle risorse in AEM, configura il controllo delle versioni delle risorse in AEM.

1. Ad Experience Manager, l’accesso **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione strumenti Workfront]** e aprire **[!UICONTROL Avanzate]** scheda.

1. Seleziona opzione **[!UICONTROL Memorizza le risorse con lo stesso nome delle versioni della risorsa esistente]**. Se selezionata, questa opzione consente di memorizzare le risorse caricate con lo stesso nome e nella stessa posizione della versione della risorsa esistente. Se questa opzione non è selezionata, verrà creata una nuova risorsa con un nome diverso (ad esempio, `asset-name.pdf` e `asset-name-1.pdf`).

1. Seleziona opzione **[!UICONTROL Aggiornare i metadati delle risorse durante la creazione di una versione]**. Se selezionata, questa opzione aggiorna i metadati della risorsa ogni volta che ne viene creata una nuova versione. Se questa opzione è deselezionata, la risorsa manterrà i metadati che aveva prima di creare la nuova versione.

![configurare il controllo delle versioni delle risorse](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Il controllo delle versioni non è supportato nelle cartelle collegate. Durante la creazione di un’ [!DNL Workfront] bozza con un documento all’interno di una cartella collegata, i commenti e le annotazioni sulla versione precedente della risorsa vengono rimossi.

## Allegare moduli personalizzati {#attach-custom-forms}

Questo passaggio di flusso di lavoro consente agli utenti di allegare un modulo personalizzato a un [!DNL Workfront] artefatto. Questo passaggio di flusso di lavoro può essere aggiunto a qualsiasi modello di flusso di lavoro. Il [!DNL Workfront] artefatto che questo passaggio influisce verrà cercato utilizzando un percorso relativo dal payload.

Nell’editor del flusso di lavoro di Experience Manager, modifica le proprietà della [!UICONTROL Workfront - Allega modulo personalizzato] passaggio di workflow.

![moduli personalizzati](/help/assets/assets/wf-custom-forms.png).

## Pubblicazione automatica delle risorse {#auto-publish-assets}

1. Ad Experience Manager, l’accesso **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione strumenti Workfront]** e aprire **[!UICONTROL Avanzate]** scheda.

1. Seleziona **[!UICONTROL Pubblica automaticamente le risorse quando inviate da Workfront]**. Questa opzione consente la pubblicazione automatica delle risorse quando vengono inviate da Workfront all’AEM. Questa funzione può essere abilitata in modo condizionale specificando un campo modulo personalizzato Workfront e il valore su cui deve essere impostata. Ogni volta che un documento viene inviato al AEM, se soddisfa la condizione, la risorsa verrà pubblicata automaticamente.

1. Seleziona **[!UICONTROL Pubblica tutte le risorse del progetto in Brand Portal al completamento del progetto]**. Questa opzione consente la pubblicazione automatica delle risorse in [!DNL Brand Portal] quando lo stato del progetto Workfront a cui appartengono viene modificato in `Complete`.

![configurare la pubblicazione automatica](/help/assets/assets/wf-auto-publish-config.png)

## Aggiornamenti dei moduli personalizzati per documenti di Workfront {#subscribe-workfront-doc-custom-form-updates}

Per sottoscrivere le modifiche in [!DNL Workfront] documenti moduli personalizzati, seleziona l’opzione pertinente nella sezione **[!UICONTROL Avanzate]** scheda. Quando si sottoscrivono questi aggiornamenti, vengono aggiornati i [!DNL Experience Manager] campi di metadati quando il campo corrispondente in [!DNL Workfront] il modulo personalizzato del documento è stato modificato.

![configurazione degli aggiornamenti del modulo personalizzato del documento Workfront in [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
