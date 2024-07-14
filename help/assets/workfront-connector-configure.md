---
title: Configura [!DNL Workfront for Experience Manager enhanced connector]
description: Configura [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
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
>* Adobe richiede la distribuzione e la configurazione di [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se distribuita e configurata senza un partner certificato o [!DNL Adobe Professional Services], non è supportata da Adobe.
>
>* Adobe potrebbe rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono ridondante questo connettore; in tal caso, i clienti potrebbero dover passare dall&#39;utilizzo di questo connettore.
>
>* Adobe supporta le versioni migliorate del connettore 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione avanzata del connettore, passa al gruppo `digital.hoodoo` disponibile nel riquadro a sinistra in [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* Consulta [Esame di certificazione partner per il connettore avanzato Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedere [Guida all&#39;esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Configurare le sottoscrizioni di eventi {#event-subscriptions}

Gli abbonamenti agli eventi vengono utilizzati per notificare all&#39;AEM gli eventi che si verificano in [!DNL Adobe Workfront]. Sono disponibili tre funzionalità [!DNL Workfront for Experience Manager enhanced connector] che richiedono abbonamenti agli eventi per funzionare:

* Creazione automatica di cartelle collegate al progetto.
* Sincronizzazione delle modifiche nei valori del modulo personalizzato del documento Workfront con i metadati delle risorse AEM.
* Pubblicazione automatica delle risorse in Brand Portal al completamento del progetto.

Per utilizzare queste funzioni, abilita sottoscrizioni eventi.

* Modifica la configurazione di [!UICONTROL Strumenti di Workfront] Cloud Service creata nel passaggio 5 e seleziona la scheda [!UICONTROL Sottoscrizioni eventi].
* Seleziona la [!UICONTROL Integrazione personalizzata Workfront] creata nella sezione 6.
* Fare clic su [!UICONTROL Abilita sottoscrizioni eventi Workfront].

  ![Sottoscrizione evento](/help/assets/assets/event-subs.png)

## Configurare le cartelle collegate {#linked-folders}

Per iscriverti agli eventi, segui questi passaggi:

1. Passa alla scheda **[!UICONTROL Iscrizioni eventi]** nei servizi cloud.
1. Selezionare l&#39;integrazione personalizzata creata in [!DNL Workfront].
1. Fare clic su **[!UICONTROL Abilita sottoscrizioni eventi Workfront]**.

### Configurazione della struttura delle cartelle collegate {#linked-folder-structure}

1. Vai alla scheda Cartelle collegate al progetto nei servizi cloud.
1. Percorso principale della cartella collegata: seleziona una cartella in DAM in cui desideri creare le cartelle collegate. Se lasciato vuoto, per impostazione predefinita viene impostato su /content/dam. Verificare che lo schema metadati Strumenti di Workfront e lo schema metadati cartelle collegate a Workfront siano stati applicati alla cartella selezionata.
1. Struttura delle cartelle collegate: immetti valori separati da virgole. Ogni valore deve essere `DE:<some-project-custom-form-field>`, Portfolio, Programma, Anno, Nome o un valore di tipo &quot;Stringa letterale&quot; (quest&#39;ultimo con virgolette). Attualmente è impostato su Portfolio,Programma,Anno,DE:Tipo di progetto,Nome.
1. Configura autorizzazioni: aggiungi le autorizzazioni `jcr:all permissions` a `/conf/workfront-tools/settings/cloudconfigs` per il gruppo `wf-workfront-users`.
1. Se il titolo della cartella in Workfront deve includere tutte le cartelle della struttura, seleziona la casella di controllo Crea titolo della cartella collegata in Workfront utilizzando i nomi della struttura di cartelle. In caso contrario, si tratta del titolo dell&#39;ultima cartella.
1. Sottocartelle con più campi consente di specificare un elenco di cartelle da creare come cartella secondaria della cartella collegata.
1. Stato progetto: seleziona lo stato del progetto per creare la cartella collegata.
1. Creazione di una cartella collegata in progetti con portfolio: elenco di Portfoli a cui il progetto deve appartenere per creare la cartella collegata. Lascia vuoto questo elenco per creare la cartella collegata per tutto il portfolio di progetti.
1. Creare una cartella collegata nei progetti con campo modulo personalizzato: campo modulo personalizzato e il valore corrispondente che il progetto deve avere per creare la cartella collegata. Questa configurazione viene ignorata se viene lasciata vuota. Selezionare `CUSTOM FORMS: Create DAM Linked Folder` per il campo e immettere `Yes` per il valore.
1. Fai clic su Abilita creazione automatica di cartelle collegate. Se torni alla scheda Sottoscrizioni evento, vedrai che ora è presente un evento di creazione.

![configurazione cartella collegata](/help/assets/assets/wf-linked-folder-config.png)

## Mappatura schema metadati {#metadata-schema-mapping}

### Configurare la mappatura dei metadati delle cartelle {#folder-metadata-mapping}

La mappatura dei metadati tra i progetti Workfront e le cartelle AEM è definita negli schemi di metadati delle cartelle AEM. Gli schemi di metadati delle cartelle devono essere creati e configurati come di consueto in AEM. Strumenti di Workfront aggiunge un elenco a discesa di completamento automatico alla scheda Configurazione impostazioni di ogni campo modulo schema metadati cartelle. Questo menu a discesa di completamento automatico consente di specificare a quale campo Workfront deve essere mappata ogni proprietà della cartella AEM.

Per configurare le mappature, effettua le seguenti operazioni:

1. Aggiungere le autorizzazioni `jcr:read` a `/conf/global/settings/dam/adminui-extension/foldermetadataschema` per il gruppo `wf-workfront-users`.
1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Cartella schemi metadati]**.
1. Seleziona il modulo schema metadati cartelle da modificare e fai clic su Modifica.
1. Seleziona il campo modulo schema metadati cartelle da modificare e seleziona la scheda Impostazioni nel pannello di destra.
1. Nel campo [!UICONTROL Mappato dal campo Workfront], selezionare il nome del campo Workfront che si desidera mappare alla proprietà della cartella AEM selezionata. Le opzioni disponibili sono:

   * Campi modulo personalizzati del progetto
   * Campi Panoramica progetto (ID, Nome, Descrizione, Numero di riferimento, Data di completamento pianificata, Proprietario progetto, Sponsor progetto, Portfolio o Programma)

![configurazione mappatura metadati](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configurare la mappatura dei metadati delle risorse {#asset-metadata-mapping}

La mappatura dei metadati tra i documenti di Adobe Workfront e Assets è definita negli schemi di metadati AEM. Gli schemi di metadati devono essere creati e configurati come di consueto in AEM. Strumenti di Workfront aggiunge opzioni di configurazione alla scheda Configurazione impostazioni di ciascun campo modulo schema metadati. Queste opzioni ti consentono di specificare a quale campo Workfront deve essere mappata ogni proprietà AEM.

Per configurare le mappature, effettua le seguenti operazioni:

1. Passa a **Strumenti** > **Assets** > **Schemi metadati**.
1. Seleziona il modulo schema metadati da modificare e fai clic su **Modifica** oppure crea uno schema metadati da zero.
1. Seleziona il campo del modulo schema metadati che desideri modificare e fai clic sulla scheda **Impostazioni** nel pannello di destra.
1. In Campo modulo personalizzato [!DNL Workfront] selezionare il nome del campo [!DNL Workfront] che si desidera mappare alla proprietà AEM selezionata. Le opzioni disponibili sono:

   * Documenta campi modulo personalizzati
   * Campi modulo personalizzati del progetto
   * Campi modulo personalizzati problema
   * Campi modulo personalizzato attività
   * Campi Panoramica progetto (ID, Nome, Descrizione o Numero di riferimento)

1. Nel caso in cui il campo [!DNL Workfront] selezionato nel [!UICONTROL campo modulo personalizzato Workfront] sia un campo di tipo Utente Workfront, sarà necessario specificare quale campo Utente Workfront si desidera mappare. Per eseguire questa operazione, selezionare Ottieni valore dal campo oggetto di riferimento di Workfront, quindi specificare il nome del [!UICONTROL Campo modulo personalizzato utente Workfront] dal quale recuperare il valore da mappare.

   ![configurazione mappatura metadati](/help/assets/assets/wf-metadata-mapping-config1.png)

## Proprietà mappa {#map-property}

Questo passaggio del flusso di lavoro consente a un utente di mappare una proprietà su un modulo personalizzato [!DNL Workfront] in un progetto, un&#39;attività, un problema o un documento. L&#39;artefatto [!DNL Workfront] interessato da questo passaggio viene cercato utilizzando un percorso relativo dal payload. Le proprietà da mappare sono controllate dalla configurazione della finestra di dialogo dei passaggi.

**Tipo**: questo campo consente di selezionare il tipo di oggetto Workfront a cui mappare le proprietà.

**Proprietà ID**: questo campo consente di specificare il percorso dell&#39;ID dell&#39;oggetto Workfront a cui mappare le proprietà. Il percorso specificato in questo campo deve essere relativo al payload del flusso di lavoro.

**Assegnazioni proprietà**: questo campo multiplo consente di specificare le mappature tra le proprietà AEM e i campi Workfront. Ogni elemento nel campo multiplo specifica una mappatura. Ogni mappatura deve avere il formato `<workfront-field>=<aem-mapped-property>`.

* `workfront-field` può essere

   * Campo modulo personalizzato identificato dal prefisso `DE:`.
   * Campo modificabile identificato dal relativo nome. I nomi dei campi sono stati trovati in [[!DNL Workfront] API explorer](https://experience.workfront.com/s/api-explorer).

* `aem-mapped-property` può essere:

   * Un valore letterale. Queste devono essere racchiuse tra virgolette.
   * Una proprietà AEM. Questo riferimento deve essere relativo al payload del flusso di lavoro.
   * Un valore denominato. Queste devono essere racchiuse tra parentesi.
   * Una concatenazione dei 3 elementi sopra indicati. Specificarlo utilizzando `{+}`.
   * Una modifica dei 3 elementi precedenti racchiudendo il valore con `{replace(<value>,"old-char","new-char")}`.

* Alcuni esempi sono:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Configurazione per mappare la proprietà](/help/assets/assets/wf-map-property-config.png)

## Imposta stato {#set-status}

Nell&#39;editor del flusso di lavoro, modificare le proprietà di **[!UICONTROL Workfront - Imposta stato]** nella scheda **[!UICONTROL Argomenti]**.

![Modifica flusso di lavoro per impostare lo stato](/help/assets/assets/wf-set-status.png)

## Sincronizzazione commenti {#comments-sync}

1. In [!DNL Experience Manager], accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione strumenti di Workfront]**, selezionare la configurazione e selezionare **[!UICONTROL Proprietà]**.

   ![commenti sincronizzati](/help/assets/assets/comments-sync1.png)

1. Seleziona la scheda **[!UICONTROL Sottoscrizioni eventi]**, fai clic su **[!UICONTROL Abilita sincronizzazione commenti]** in **[!UICONTROL Invia commenti aggiunti in Workfront all&#39;opzione AEM]**.

   ![Sincronizzazione abilitata](/help/assets/assets/wf-comment-sync-enabled.png)

Per verificare la sincronizzazione dei commenti da Workfront all’AEM, effettua le seguenti operazioni:

1. Passa a un documento collegato in Workfront e aggiungi un commento nella scheda Aggiornamenti.

   ![lascia un commento in Workfront](/help/assets/assets/comments-sync2.png)

1. Passare allo stesso documento collegato in AEM, selezionare il documento e aprire l&#39;opzione [!UICONTROL Timeline] nel menu di navigazione a sinistra, quindi selezionare [!UICONTROL Commenti]. Nella barra laterale a sinistra vengono visualizzati i commenti sincronizzati da [!DNL Workfront].

## Versioni risorsa {#asset-versions}

Per mantenere la cronologia delle versioni delle risorse in AEM, configura il controllo delle versioni delle risorse in AEM.

1. In Experience Manager, accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione strumenti Workfront]** e aprire la scheda **[!UICONTROL Avanzate]**.

1. Selezionare l&#39;opzione **[!UICONTROL Memorizza risorse con lo stesso nome delle versioni della risorsa esistente]**. Se selezionata, questa opzione consente di memorizzare le risorse caricate con lo stesso nome e nella stessa posizione della versione della risorsa esistente. Se questa opzione non è selezionata, verrà creata una nuova risorsa con un nome diverso (ad esempio, `asset-name.pdf` e `asset-name-1.pdf`).

1. Selezionare l&#39;opzione **[!UICONTROL Aggiorna metadati risorsa durante la creazione di una versione]**. Se selezionata, questa opzione aggiorna i metadati della risorsa ogni volta che ne viene creata una nuova versione. Se questa opzione è deselezionata, la risorsa manterrà i metadati che aveva prima di creare la nuova versione.

![configurare il controllo delle versioni delle risorse](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Il controllo delle versioni non è supportato nelle cartelle collegate. Durante la creazione di una bozza [!DNL Workfront] con un documento all&#39;interno di una cartella collegata, i commenti e le annotazioni della versione precedente della risorsa vengono rimossi.

## Allegare moduli personalizzati {#attach-custom-forms}

Questo passaggio del flusso di lavoro consente agli utenti di allegare un modulo personalizzato a un artefatto [!DNL Workfront]. Questo passaggio di flusso di lavoro può essere aggiunto a qualsiasi modello di flusso di lavoro. L&#39;artefatto [!DNL Workfront] interessato da questo passaggio verrà cercato utilizzando un percorso relativo dal payload.

Nell&#39;editor del flusso di lavoro di Experience Manager, modificare le proprietà del passaggio del flusso di lavoro [!UICONTROL Workfront - Allega modulo personalizzato].

![moduli personalizzati](/help/assets/assets/wf-custom-forms.png).

## Pubblicazione automatica delle risorse {#auto-publish-assets}

1. In Experience Manager, accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione strumenti Workfront]** e aprire la scheda **[!UICONTROL Avanzate]**.

1. Seleziona **[!UICONTROL Pubblica automaticamente le risorse se inviate da Workfront]**. Questa opzione consente la pubblicazione automatica delle risorse quando vengono inviate da Workfront all’AEM. Questa funzione può essere abilitata in modo condizionale specificando un campo modulo personalizzato Workfront e il valore su cui deve essere impostata. Ogni volta che un documento viene inviato al AEM, se soddisfa la condizione, la risorsa verrà pubblicata automaticamente.

1. Seleziona **[!UICONTROL Publish tutte le risorse del progetto in Brand Portal al completamento del progetto]**. Questa opzione consente la pubblicazione automatica delle risorse in [!DNL Brand Portal] quando lo stato del progetto Workfront a cui appartengono viene modificato in `Complete`.

![configura pubblicazione automatica](/help/assets/assets/wf-auto-publish-config.png)

## Aggiornamenti dei moduli personalizzati per documenti di Workfront {#subscribe-workfront-doc-custom-form-updates}

Per sottoscrivere le modifiche nei moduli personalizzati del documento [!DNL Workfront], selezionare l&#39;opzione appropriata nella scheda **[!UICONTROL Avanzate]**. Quando si sottoscrivono questi aggiornamenti, i campi di metadati [!DNL Experience Manager] mappati vengono aggiornati quando viene modificato il campo corrispondente nel modulo personalizzato del documento [!DNL Workfront].

![configurazione aggiornamenti modulo personalizzato documento Workfront in [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
