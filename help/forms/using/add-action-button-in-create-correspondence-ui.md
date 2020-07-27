---
title: Aggiunta di azioni/pulsanti personalizzati nell’interfaccia utente Crea corrispondenza
seo-title: Aggiunta di azioni/pulsanti personalizzati nell’interfaccia utente Crea corrispondenza
description: Scoprite come aggiungere azione/pulsante personalizzato nell’interfaccia utente Crea corrispondenza
seo-description: Scoprite come aggiungere azione/pulsante personalizzato nell’interfaccia utente Crea corrispondenza
uuid: 1b2b00bb-93ef-4bfe-9fc5-25c45e4cb4b1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 046e3314-b436-47ed-98be-43d85f576789
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 1%

---


# Aggiunta di azioni/pulsanti personalizzati nell’interfaccia utente Crea corrispondenza {#add-custom-action-button-in-create-correspondence-ui}

## Panoramica {#overview}

La soluzione Correspondence Management consente di aggiungere azioni personalizzate all&#39;interfaccia utente Crea corrispondenza.

Lo scenario illustrato in questo documento illustra come creare un pulsante nell’interfaccia utente Crea corrispondenza per condividere una lettera come PDF di revisione allegato a un messaggio e-mail.

### Prerequisiti {#prerequisites}

Per completare questo scenario, è necessario quanto segue:

* Conoscenza di CRX e JavaScript
* LiveCycle Server

## Scenario: Creare il pulsante nell&#39;interfaccia utente Crea corrispondenza per inviare una lettera da rivedere {#scenario-create-the-button-in-the-create-correspondence-user-interface-to-send-a-letter-for-review}

L’aggiunta di un pulsante con un’azione (in questo caso, invia lettera per la revisione) all’interfaccia utente Crea corrispondenza include:

1. Aggiunta del pulsante all&#39;interfaccia utente Crea corrispondenza
1. Aggiunta della gestione delle azioni al pulsante
1. Aggiunta del processo LiveCycle per abilitare la gestione delle azioni

### Aggiungere il pulsante all’interfaccia utente Crea corrispondenza {#add-the-button-to-the-create-correspondence-user-interface}

1. Accedete a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedete come amministratore.
1. Nella cartella delle app, crea una cartella denominata `defaultApp` con percorso/struttura simile alla cartella defaultApp (che si trova nella cartella di configurazione). Per creare la cartella, effettuate le seguenti operazioni:

   1. Fai clic con il pulsante destro del mouse sulla cartella **defaultApp** nel percorso seguente e seleziona Nodo **** sovrapposizione:

      /libs/fd/cm/config/defaultApp/

      ![Sovrapposizione, nodo](assets/1_defaultapp.png)

   1. Verificate che la finestra di dialogo Nodo sovrapposizione contenga i seguenti valori:

      **Percorso:** /libs/fd/cm/config/defaultApp/

      **Posizione overlay:** /apps/

      **Corrispondenza tipi di nodo:** Selezionato

      ![Sovrapposizione, nodo](assets/2_defaultappoverlaynode.png)

   1. Fai clic su **OK**.
   1. Fate clic su **Salva tutto**.

1. Eseguite una copia del file acmExtensionsConfig.xml (esiste nel ramo /libs) sotto il ramo /apps.

   1. Vai a &quot;/libs/fd/cm/config/defaultApp/acmExtensionsConfig.xml&quot;

   1. Fate clic con il pulsante destro del mouse sul file acmExtensionsConfig.xml e selezionate **Copia**.

      ![Copia acmExtensionsConfig.xml](assets/3_acmextensionsconfig_xml_copy.png)

   1. Fate clic con il pulsante destro del mouse sulla cartella **defaultApp** in &quot;/apps/fd/cm/config/defaultApp/&quot;, quindi selezionate **Incolla**.
   1. Fate clic su **Salva tutto**.

1. Fate doppio clic sulla copia di acmExtentionsConfig.xml appena creata nella cartella delle app. Il file viene aperto per la modifica.
1. Individuate il codice seguente:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <extensionsConfig>
       <modelExtensions>
           <modelExtension type="LetterInstance">
     <customAction name="Preview" label="loc.letterInstance.preview.label" tooltip="loc.letterInstance.preview.tooltip" styleName="previewButton"/>
               <customAction name="Submit" label="loc.letterInstance.submit.label" tooltip="loc.letterInstance.submit.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="SaveAsDraft" label="loc.letterInstance.saveAsDraft.label" tooltip="loc.letterInstance.saveAsDraft.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="Close" label="loc.letterInstance.close.label" tooltip="loc.letterInstance.close.tooltip" styleName="closeButton"/>
           </modelExtension>
       </modelExtensions>
   </extensionsConfig>
   ```

1. Per inviare un messaggio e-mail, è possibile utilizzare LiveCycle Forms Workflow. Aggiungi un tag customAction sotto il tag modelExtension in acmExtensionsConfig.xml come segue:

   ```xml
    <customAction name="Letter Review" label="Letter Review" tooltip="Letter Review" styleName="" permissionName="forms-users" actionHandler="CM.domain.CCRCustomActionHandler">
         <serviceName>Forms Workflow -> SendLetterForReview/SendLetterForReviewProcess</serviceName>
       </customAction>
   ```

   ![tag customAction](assets/5_acmextensionsconfig_xml.png)

   Il tag modelExtension dispone di un set di tag secondari customAction che configurano l’azione, le autorizzazioni e l’aspetto del pulsante di azione. Di seguito è riportato l&#39;elenco dei tag di configurazione customAction:

   | **Nome** | **Descrizione** |
   |---|---|
   | name | Nome alfanumerico dell’azione da eseguire. Il valore di questo tag è obbligatorio, deve essere univoco (all&#39;interno del tag modelExtension) e deve iniziare con un alfabeto. |
   | label | Etichetta da visualizzare sul pulsante dell&#39;azione |
   | tooltip | Testo descrittivo del pulsante, visualizzato quando l&#39;utente passa il mouse sul pulsante. |
   | styleName | Nome dello stile personalizzato applicato al pulsante di azione. |
   | permissionsName | L&#39;azione corrispondente viene visualizzata solo se l&#39;utente dispone dell&#39;autorizzazione specificata da permissionsName. Quando si specifica permissionsName come `forms-users`, tutti gli utenti possono accedere a questa opzione. |
   | actionHandler | Nome completo della classe ActionHandler che viene chiamata quando l&#39;utente fa clic sul pulsante. |

   Oltre ai parametri indicati sopra, possono essere associate configurazioni aggiuntive a customAction. Queste configurazioni aggiuntive sono rese disponibili al gestore tramite l&#39;oggetto CustomAction.

   | **Nome** | **Descrizione** |
   |---|---|
   | serviceName | Se un oggetto customAction contiene un tag secondario con nome serviceName, quando si fa clic sul pulsante o collegamento corrispondente viene chiamato un processo con il nome rappresentato dal tag serviceName. Assicurarsi che il processo abbia la stessa firma del PostProcess Lettera. Aggiungi il prefisso &quot;Forms Workflow ->&quot; nel nome del servizio. |
   | Parametri contenenti il prefisso cm_ nel nome del tag | Se un oggetto customAction contiene tag secondari che iniziano con nome cm_, nel processo di post (che si tratti di Letter Post Process o del processo speciale rappresentato dal tag serviceName) questi parametri sono disponibili nel codice XML di input all&#39;interno del tag corrispondente, con la rimozione del prefisso cm_. |
   | actionName | Ogni volta che un processo di pubblicazione è dovuto a un clic, l’XML inviato contiene un tag speciale con nome sotto il tag con il nome dell’azione dell’utente. |

1. Fate clic su **Salva tutto**.

#### Creare una cartella delle impostazioni internazionali con il file delle proprietà nel ramo /apps {#create-a-locale-folder-with-properties-file-in-the-apps-branch}

Il file ACMExtensionMessages.properties include etichette e messaggi di descrizione dei vari campi nell&#39;interfaccia utente Crea corrispondenza. Affinché le azioni/i pulsanti personalizzati funzionino, create una copia di questo file nel ramo /apps.

1. Fate clic con il pulsante destro del mouse sulla cartella delle **impostazioni** internazionali nel percorso seguente e selezionate Nodo **** sovrapposizione:

   /libs/fd/cm/config/defaultApp/locale

1. Verificate che la finestra di dialogo Nodo sovrapposizione contenga i seguenti valori:

   **Percorso:** /libs/fd/cm/config/defaultApp/locale

   **Posizione overlay:** /apps/

   **Corrispondenza tipi di nodo:** Selezionato

1. Fai clic su **OK**.
1. Fate clic su **Salva tutto**.
1. Fare clic con il pulsante destro del mouse sul file seguente e selezionare **Copia**:

   `/libs/fd/cm/config/defaultApp/locale/ACMExtensionsMessages.properties`

1. Fare clic con il pulsante destro del mouse sulla cartella **locale** nel percorso seguente e selezionare **Incolla**:

   `/apps/fd/cm/config/defaultApp/locale/`

   Il file ACMExtensionMessages.properties viene copiato nella cartella locale.

1. Per localizzare le etichette dell&#39;azione/pulsante personalizzato appena aggiunto, create il file ACMExtensionMessages.properties per le impostazioni internazionali pertinenti in `/apps/fd/cm/config/defaultApp/locale/`.

   Ad esempio, per localizzare l&#39;azione/il pulsante personalizzato creato in questo articolo, create un file denominato ACMExtensionMessages_fr.properties con la voce seguente:

   `loc.letterInstance.letterreview.label=Revue De Lettre`

   In modo simile, in questo file è possibile aggiungere più proprietà, ad esempio per la descrizione comandi e lo stile.

1. Fate clic su **Salva tutto**.

#### Riavviate il bundle Adobe Asset Composer Building Block {#restart-the-adobe-asset-composer-building-block-bundle}

Dopo aver apportato ogni modifica sul lato server, riavviate il bundle Adobe Asset Composer Building Block. In questo scenario, i file acmExtensionsConfig.xml e ACMExtensionMessages.properties sul lato server vengono modificati, pertanto il bundle Adobe Asset Composer Building Block richiede un riavvio.

>[!NOTE]
>
>Potrebbe essere necessario cancellare la cache del browser.

1. Passa a `https://[host]:'port'/system/console/bundles`. Se necessario, effettuate l’accesso come amministratore.

1. Individuate il bundle Adobe Asset Composer Building Block. Riavviate il bundle: fate clic su Interrompi e quindi su Avvia.

   ![Blocco predefinito di Adobe Asset Composer](assets/6_assetcomposerbuildingblockbundle.png)

Dopo aver riavviato il bundle Adobe Asset Composer Building Block, il pulsante personalizzato viene visualizzato nell’interfaccia utente Crea corrispondenza. Potete aprire una lettera nell&#39;interfaccia utente Crea corrispondenza per visualizzare l&#39;anteprima del pulsante personalizzato.

### Aggiungere la gestione delle azioni al pulsante {#add-action-handling-to-the-button}

Per impostazione predefinita, l’interfaccia utente Crea corrispondenza ha implementato ActionHandler nel file cm.domain.js nel percorso seguente:

/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccr/js/cm.domain.js

Per la gestione delle azioni personalizzate, create una sovrapposizione del file cm.domain.js nel ramo /apps di CRX.

La gestione dell&#39;azione o del pulsante quando si fa clic su action/button include logica per:

* L’azione appena aggiunta diventa visibile/invisibile: eseguito ignorando la funzione actionVisible().
* Attivare/disattivare l’azione aggiunta: eseguito ignorando la funzione actionEnabled().
* Gestione effettiva dell&#39;azione quando l&#39;utente fa clic sul pulsante: viene eseguito ignorando l&#39;implementazione della funzione handleAction().

1. Passa a `https://'[server]:[port]'/[ContextPath]/crx/de`. Se necessario, effettuate l’accesso come amministratore.

1. Nella cartella delle app, create una cartella denominata `js` nel ramo /apps di CRX con una struttura simile alla seguente:

   `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   Per creare la cartella, effettuate le seguenti operazioni:

   1. Fate clic con il pulsante destro del mouse sulla cartella **js** nel percorso seguente e selezionate Nodo **** sovrapposizione:

      `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   1. Verificate che la finestra di dialogo Nodo sovrapposizione contenga i seguenti valori:

      **Percorso:** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js

      **Posizione overlay:** /apps/

      **Corrispondenza tipi di nodo:** Selezionato

   1. Fai clic su **OK**.
   1. Fate clic su **Salva tutto**.

1. Nella cartella js, create un file denominato ccrcustomization.js con il codice per la gestione dell&#39;azione del pulsante utilizzando la procedura seguente:

   1. Fate clic con il pulsante destro del mouse sulla cartella **js** nel percorso seguente e selezionate **Crea > Crea file**:

      `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

      Denominate il file come ccrcustomization.js.

   1. Fate doppio clic sul file ccrcustomization.js per aprirlo in CRX.
   1. Nel file, incollate il codice seguente e fate clic su **Salva tutto**:

      ```javascript
      /* for adding and handling custom actions in Extensible Toolbar.
        * One instance of handler will be created for each action.
        * CM.domain.CCRCustomActionHandler is actionHandler class.
        */
      var CCRCustomActionHandler;
          CCRCustomActionHandler = CM.domain.CCRCustomActionHandler = new Class({
              className: 'CCRCustomActionHandler',
              extend: CCRDefaultActionHandler,
              construct : function(action,model){
              }
          });
          /**
           * Called when user user click an action
           * @param extraParams additional arguments that may be passed to handler (For future use)
           */
          CCRCustomActionHandler.prototype.handleAction = function(extraParams){
              if (this.action.name == CCRCustomActionHandler.SEND_FOR_REVIEW) {
                  var sendForReview = function(){
                      var serviceName = this.action.actionConfig["serviceName"];
                      var inputParams = {};
                      inputParams["dataXML"] = this.model.iccData.data;
                      inputParams["letterId"] = this.letterVO.id;
                      inputParams["letterName"] = this.letterVO.name;
                      inputParams["mailId"] = $('#email').val();
                      /*function to invoke the LivecyleService */
                      ServiceDelegate.callJSONService(this,"lc.icc.renderlib.serviceInvoker.json","invokeProcess",[serviceName,inputParams],this.onProcessInvokeComplete,this.onProcessInvokeFail);
                      $('#ccraction').modal("hide");
                  }
                  if($('#ccraction').length == 0){
                      /*For first click adding popup & setting letterName.*/
                      $("body").append(popUp);
                      $("input[id*='letterName']").val(this.letterVO.name);
                      $(document).on('click',"#submitLetter",$.proxy( sendForReview, this ));
                  }
                  $('#ccraction').modal("show");
              }
          };
          /**
           * Should the action be enabled in toolbar
           * @param extraParams additional arguements that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
         CCRCustomActionHandler.prototype.actionEnabled = function(extraParams){
                  /*can be customized as per user requirement*/
                  return true;
          };
          /**
           * Should the action be visible in toolbar
           * @param extraParams additional arguments that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
          CCRCustomActionHandler.prototype.actionVisible = function(extraParams){
              /*Check can be enabled for Non-Preview Mode.*/
              return true;
          };
          /*SuccessHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeComplete = function(response) {
              ErrorHandler.showSuccess("Letter Sent for Review");
          };
          /*FaultHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeFail = function(event) {
              ErrorHandler.showError(event.message);
          };
          CCRCustomActionHandler.SEND_FOR_REVIEW  = "Letter Review";
      /*For PopUp*/
          var popUp = '<div class="modal fade" id="ccraction" tabindex="-1" role="dialog" aria-hidden="true">'+
          '<div class="modal-dialog modal-sm">'+
              '<div class="modal-content">' +
                  '<div class="modal-header">'+
                      '<button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</code></button>'+
                      '<h4 class="modal-title"> Send Review </h4>'+
                  '</div>'+
                  '<div class="modal-body">'+
                      '<form>'+
                          '<div class="form-group">'+
                              '<label class="control-label">Email Id</label>'+
                              '<input type="text" class="form-control" id="email">'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<label  class="control-label">Letter Name</label>'+
                              '<input id="letterName" type="text" class="form-control" readonly>'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<input id="letterData" type="text" class="form-control hide" readonly>'+
                          '</div>'+
                      '</form>'+
                  '</div>'+
                  '<div class="modal-footer">'+
                     '<button type="button" class="btn btn-default" data-dismiss="modal"> Cancel </button>'+
                     '<button type="button" class="btn btn-primary" id="submitLetter"> Submit </button>'+
                  '</div>'+
              '</div>'+
          '</div>'+
      '</div>';
      ```

### Aggiunta del processo LiveCycle per abilitare la <span class="acrolinxCursorMarker"></code>gestione delle azioni {#add-the-livecycle-process-to-enable-action-span-class-acrolinxcursormarker-span-handling}

In questo scenario, abilita i seguenti componenti, che fanno parte del file components.zip allegato:

* Jar del componente DSC (DSCSample.jar)
* Invia lettera per il processo di revisione LCA (SendLetterForReview.lca)

Scaricate e decomprimete il file components.zip per ottenere i file DSCSample.jar e SendLetterForReview.lca. Utilizzate questi file come specificato nelle procedure seguenti.
components.zip

#### Configurare il server LiveCycle per eseguire il processo LCA {#configure-the-livecycle-server-to-run-the-lca-process}

>[!NOTE]
>
>Questo passaggio è richiesto solo se si è in una configurazione OSGI e l&#39;integrazione LC è necessaria per il tipo di personalizzazione che si sta implementando.

Il processo LCA viene eseguito sul server LiveCycle e richiede l&#39;indirizzo del server e le credenziali di accesso.

1. Accedete a `https://'[server]:[port]'/system/console/configMgr` e accedete come amministratore.
1. Individuare la configurazione Adobe LiveCycle Client SDK e fare clic su **Modifica** (icona di modifica). Viene visualizzato il pannello Configurazioni.

1. Immettete i seguenti dettagli e fate clic su **Salva**:

   * **Url** server: URL del server LC il cui servizio Send For Review viene utilizzato dal codice del gestore di azioni.
   * **Nome utente**: Nome utente amministratore del server LC
   * **Password**: Password del nome utente amministratore

   ![Configurazione Adobe LiveCycle Client SDK](assets/3_clientsdkconfiguration.png)

#### Installare LiveCycle Archive (LCA) {#install-livecycle-archive-lca}

Processo di LiveCycle richiesto per abilitare il processo del servizio e-mail.

>[!NOTE]
>
>Per visualizzare le operazioni eseguite da questo processo o per creare un processo simile, è necessario disporre di Workbench.

1. Accedete come amministratore a Livecycle Server adminui in `https:/[lc server]/:[lc port]/adminui`.

1. Vai a **Home > Servizi > Applicazioni e servizi > Gestione** applicazione.

1. Se l&#39;applicazione SendLetterForReview è già presente, ignora i passaggi rimanenti di questa procedura, altrimenti continua con i passaggi successivi.

   ![Applicazione SendLetterForReview nell&#39;interfaccia utente](assets/12_applicationmanagementlc.png)

1. Fai clic su **Importa**.

1. Fare clic su **Scegli file** e selezionare InviaLetteraPerRivedi.lca.

   ![Selezionare il file SendLetterForReview.lca](assets/14_sendletterforreview_lca.png)

1. Fate clic su **Anteprima**.

1. Selezionate **Distribuisci risorse in fase di esecuzione al termine** dell&#39;importazione.

1. Fai clic su **Importa**.

#### Aggiunta di ServiceName all&#39;elenco  Inserire nell&#39;elenco Consentiti Servizio {#adding-servicename-to-the-allowlist-service-list}

Ricorda nel server AEM i servizi LiveCycle a cui vuoi accedere.

1. Accedete come amministratore a `https:/[host]:'port'/system/console/configMgr`.

1. Individua e fai clic su Configurazione **SDK client** Adobe LiveCycle. Viene visualizzato il pannello Configurazione Adobe LiveCycle Client SDK.
1. Nell’elenco Nome servizio, fare clic sull’icona + e aggiungere un serviceName **SendLetterForReview/SendLetterForReviewProcess**.

1. Fai clic su **Salva**.

#### Configurare il servizio e-mail {#configure-the-email-service}

In questo scenario, affinché Gestione corrispondenza possa inviare un messaggio e-mail, configurare il servizio e-mail nel server LiveCycle.

1. Effettuate l&#39;accesso con le credenziali di amministratore a Livecycle Server adminui in `https:/[lc server]:[lc port]/adminui`.

1. Vai a **Home > Servizi > Applicazioni e servizi > Gestione** dei servizi.

1. Individua e fai clic su **EmailService**.

1. Nell&#39;host **** SMTP, configurare il servizio e-mail.

1. Fai clic su **Salva**.

#### Configurare il servizio DSC {#configure-the-dsc-service}

Per utilizzare l&#39;API di gestione della corrispondenza, scaricate il file DSCSample.jar (allegato in questo documento come parte di components.zip) e caricatelo nel server di LiveCycle. Dopo il caricamento del file DSCSample.jar nel server LiveCycle, il server AEM utilizza il file DSCSample.jar per accedere all&#39;API renderingLetter.

Per ulteriori informazioni, vedere [Collegamento di AEM Forms con Adobe LiveCycle](/help/forms/using/aem-livecycle-connector.md).

1. Aggiorna l’URL del server AEM in cmsa.properties in DSCSample.jar, che si trova nel seguente percorso:

   DSCSample.jar\com\adobe\livecycle\cmsa.properties

1. Immettete i seguenti parametri nel file di configurazione:

   * **crx.serverUrl**=https:/host:port/[percorso]contestuale/URL[AEM]
   * **crx.username**= nome utente AEM
   * **crx.password**= password AEM
   * **crx.appRoot**=/content/apps/cm

   >[!NOTE]
   >
   >Ogni volta che si apportano modifiche sul lato server, riavviare il server LiveCycle. Per informazioni sulla creazione di un componente LiveCycle personalizzato, vedere [Estensione del software LiveCycle ES tramite lo sviluppo](https://www.adobe.com/devnet/livecycle/articles/dsc_development.html)DSC personalizzato.

   Il file DSCSample.jar utilizza l&#39;API renderingLetter. Per ulteriori informazioni sull&#39;API renderLetter, vedi [Interfaccia LetterRenderService](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/ddg/api/LetterRenderService.html).

#### Importa DSC in LiveCycle {#import-dsc-to-livecyle}

Il file DSCSample.jar utilizza l&#39;API renderingLetter per eseguire il rendering della lettera come byte PDF dai dati XML che C fornisce come input. Per ulteriori informazioni su renderingLetter e altre API, consultate Servizio [di rendering](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/ddg/api/LetterRenderService.html)Lettera.

1. Avviare Workbench ed effettuare l&#39;accesso.
1. Selezionare **Finestra > Mostra viste > Componenti**. La visualizzazione Componenti viene aggiunta a Workbench ES2.

1. Fare clic con il pulsante destro del mouse su **Componenti** e selezionare **Installa componente**.

1. Selezionate il file **DSCSample.jar** nel browser del file e fate clic su **Apri**.
1. Fare clic con il pulsante destro del mouse su **RenderWrapper** e selezionare **Avvia componente**. Se il componente viene avviato, accanto al nome del componente viene visualizzata una freccia verde.

## Invia lettera per revisione {#send-letter-for-review}

Dopo aver configurato l’azione e il pulsante per l’invio della lettera per la revisione:

1. Cancellate la cache del browser.

1. Nell’interfaccia utente Crea corrispondenza, fate clic su **Lettera revisione** e specificate l’ID e-mail del revisore.

1. Fate clic su **Invia**.

![sendreview](assets/sendreview.png)

Il revisore riceve un&#39;e-mail dal sistema con la lettera come allegato PDF.
