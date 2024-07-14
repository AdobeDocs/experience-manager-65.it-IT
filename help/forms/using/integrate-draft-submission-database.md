---
title: Esempio per integrare il componente Bozze e invii con il database
description: Implementazione di riferimento di servizi personalizzati per dati e metadati al fine di integrare il componente Bozze e richieste con un database.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# Esempio per integrare il componente Bozze e invii con il database {#sample-for-integrating-drafts-submissions-component-with-database}

## Panoramica di esempio {#sample-overview}

Il componente Bozze e invii del portale AEM Forms consente agli utenti di salvare i moduli come bozze e inviarli successivamente da qualsiasi dispositivo. Gli utenti possono inoltre visualizzare i moduli inviati nel portale. Per abilitare questa funzionalità, AEM Forms fornisce servizi di dati e metadati per memorizzare i dati compilati da un utente nel modulo e i metadati del modulo associati alle bozze e ai moduli inviati. Per impostazione predefinita, questi dati vengono memorizzati nell’archivio di CRX. Tuttavia, poiché gli utenti interagiscono con i moduli tramite l’istanza di pubblicazione dell’AEM, che in genere si trova al di fuori del firewall aziendale, le organizzazioni potrebbero voler personalizzare l’archiviazione dei dati per renderla più sicura e affidabile.

L’esempio, discusso in questo documento, è un’implementazione di riferimento di servizi di dati e metadati personalizzati per integrare bozze e componenti di invio con un database. Il database utilizzato nell&#39;implementazione di esempio è **MySQL 5.6.24**. Tuttavia, è possibile integrare il componente Bozze e invii con qualsiasi database desiderato.

>[!NOTE]
>
>* Gli esempi e le configurazioni illustrate in questo documento sono conformi a MySQL 5.6.24 e devono essere sostituiti in modo appropriato per il sistema di database.
>* Verifica di aver installato la versione più recente del pacchetto del componente aggiuntivo AEM Forms. Per un elenco dei pacchetti disponibili, consulta l&#39;articolo [Versioni di AEM Forms](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).
>* Il pacchetto di esempio funziona solo con azioni di invio Adaptive Forms.

## Impostare e configurare l’esempio {#set-up-and-configure-the-sample}

Per installare e configurare l’esempio in tutte le istanze di authoring e pubblicazione, effettua le seguenti operazioni:

1. Scarica il seguente pacchetto **aem-fp-db-integration-sample-pkg-6.1.2.zip** nel file system.

   Pacchetto di esempio per l’integrazione del database

[Ottieni file](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Vai a Gestione pacchetti AEM all&#39;indirizzo https://[*host*]:[*porta*]/crx/packmgr/.
1. Fare clic su **[!UICONTROL Carica pacchetto]**.

1. Individua il pacchetto **aem-fp-db-integration-sample-pkg-6.1.2.zip** e fai clic su **[!UICONTROL OK]**.
1. Fai clic su **[!UICONTROL Installa]** accanto al pacchetto per installarlo.
1. Vai a **[!UICONTROL Configurazione console Web AEM]**
pagina all&#39;indirizzo https://[*host*]:[*porta*]/system/console/configMgr.
1. Fare clic per aprire **[!UICONTROL Configurazione bozza e invio portale Forms]** in modalità di modifica.

1. Specificare i valori per le proprietà come descritto nella tabella seguente:

   | **Proprietà** | **Descrizione** | **Valore** |
   |---|---|---|
   | Servizio dati bozza portale Forms | Identificatore per bozza di servizio dati | formsportal.sampledataservice |
   | Servizio metadati bozza portale Forms | Identificatore per bozza servizio metadati | formsportal.samplemetadataservice |
   | Servizio di invio dati per Forms Portal | Identificatore per il servizio dati di invio | formsportal.sampledataservice |
   | Servizio metadati invio portale Forms | Identificatore per il servizio di invio metadati | formsportal.samplemetadataservice |
   | Servizio dati di firma in sospeso di Forms Portal | Identificatore per il servizio dati di firma in sospeso | formsportal.sampledataservice |
   | Servizio metadati firma in sospeso di Forms Portal | Identificatore per il servizio metadati di firma in sospeso | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >I servizi vengono risolti dai nomi indicati come valore per la chiave `aem.formsportal.impl.prop` nel modo seguente:

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   È possibile modificare i nomi delle tabelle di dati e metadati.

   Per specificare un nome diverso per la tabella dei metadati:

   * Nella configurazione della console Web, trovare e fare clic su Implementazione di esempio del servizio metadati di Forms Portal. È possibile modificare i valori dell&#39;origine dati, dei metadati o del nome di tabelle di metadati aggiuntive.

   Per specificare un nome diverso per la tabella dati:

   * Nella configurazione della console Web, trovare e fare clic su Implementazione di esempio del servizio dati di Forms Portal. È possibile modificare i valori dell&#39;origine dati e del nome della tabella dati.

   >[!NOTE]
   >
   >Se si modificano i nomi delle tabelle, specificarli nella configurazione del portale moduli.

1. Lascia invariate le altre configurazioni e fai clic su **[!UICONTROL Salva]**.

1. La connessione al database può essere effettuata tramite Apache Sling Connection Pooled Data Source.
1. Per la connessione Apache Sling, individua e fai clic per aprire **[!UICONTROL Origine dati in pool di connessione Apache Sling]** in modalità di modifica nella configurazione della console Web. Specificare i valori per le proprietà come descritto nella tabella seguente:

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Valore</strong></td>
  </tr>
  <tr>
   <td>Nome origine dati</td>
   <td><p>Nome di origine dati per filtrare i driver dal pool di origini dati</p> <p><strong>Nota: </strong><em>L'implementazione di esempio utilizza FormsPortal come nome dell'origine dati.</em></p> </td>
  </tr>
  <tr>
   <td>Classe driver JDBC</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>URI connessione JDBC <br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>porta</em>]/[<em>nome_schema</em>]</td>
  </tr>
  <tr>
   <td>Nome utente</td>
   <td>Un nome utente per autenticare ed eseguire azioni sulle tabelle del database</td>
  </tr>
  <tr>
   <td>Password</td>
   <td>Password associata al nome utente</td>
  </tr>
  <tr>
   <td>Isolamento transazione</td>
   <td>READ_COMMIT</td>
  </tr>
  <tr>
   <td>Numero massimo connessioni attive</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>Numero massimo di connessioni inattive</td>
   <td>100</td>
  </tr>
  <tr>
   <td>Connessioni inattive minime</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Dimensione iniziale</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Attesa massima</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>Test su prestito</td>
   <td>Selezionato</td>
  </tr>
  <tr>
   <td>Test durante inattività</td>
   <td>Selezionato</td>
  </tr>
  <tr>
   <td>Query di convalida</td>
   <td>I valori di esempio sono SELECT 1(mysql), select 1 from dual(oracle), SELECT 1(MS Sql Server) (validationQuery)</td>
  </tr>
  <tr>
   <td>Timeout query di convalida</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Il driver JDBC per MySQL non viene fornito con l&#39;esempio. Verificare di aver eseguito il provisioning e fornire le informazioni necessarie per configurare il connection pool JDBC.
>* Indirizza le istanze di authoring e pubblicazione per utilizzare lo stesso database. Il valore del campo URI connessione JDBC deve essere lo stesso per tutte le istanze di authoring e pubblicazione.

1. Lascia invariate le altre configurazioni e fai clic su **[!UICONTROL Salva]**.

1. Se nello schema del database è già presente una tabella, andare al passaggio successivo.

   In caso contrario, se nello schema del database non è già presente una tabella, eseguire le istruzioni SQL seguenti per creare tabelle separate per dati, metadati e metadati aggiuntivi nello schema del database:

   >[!NOTE]
   >
   >Non sono necessari database diversi per le istanze di authoring e pubblicazione. Utilizza lo stesso database su tutte le istanze di authoring e pubblicazione.

   **Istruzione SQL per la tabella dati**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Istruzione SQL per la tabella dei metadati**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Istruzione SQL per additionalmetadatatable**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT 'additionalmetadatatable_fk' FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Istruzione SQL per la tabella dei commenti**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. Se nello schema del database sono già presenti le tabelle (dati, metadati e metadati aggiuntivi), eseguire le query di modifica seguenti:

   **Istruzione SQL per la modifica della tabella dati**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Istruzione SQL per la modifica della tabella dei metadati**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >La query di aggiunta dei metadati ALTER TABLE ha esito negativo se è già stata eseguita e la colonna markedforDeletion è presente nella tabella.

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Istruzione SQL per la modifica della tabella additionalmetadatatable**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

L’implementazione di esempio è ora configurata e può essere utilizzata per elencare le bozze e gli invii durante la memorizzazione di tutti i dati e i metadati in un database. Vediamo ora come sono configurati i servizi dati e metadati nell’esempio.

## Installare il file mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-bin-jar-file}

Per installare il file mysql-connector-java-5.1.39-bin.jar, effettua le seguenti operazioni su tutte le istanze di authoring e pubblicazione:

1. Passare a `https://'[server]:[port]'/system/console/depfinder` e cercare il pacchetto com.mysql.jdbc.
1. Nella colonna Esportato da, controlla se il pacchetto viene esportato da un bundle.

   Procedi se il pacchetto non viene esportato da alcun bundle.

1. Passare a `https://'[server]:[port]'/system/console/bundles` e fare clic su **[!UICONTROL Installa/Aggiorna]**.
1. Fare clic su **[!UICONTROL Scegli file]** e selezionare il file mysql-connector-java-5.1.39-bin.jar. Selezionare inoltre le caselle di controllo **[!UICONTROL Avvia bundle]** e **[!UICONTROL Aggiorna pacchetti]**.
1. Fare clic su **[!UICONTROL Installa o Aggiorna]**. Al termine, riavviare il server.
1. (*Solo Windows*) Disattivare il firewall di sistema per il sistema operativo.

>[!NOTE]
>
> Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

## Codice di esempio per il servizio metadati e i dati del portale Forms {#sample-code-for-forms-portal-data-and-metadata-service}

Il seguente file zip contiene `FormsPortalSampleDataServiceImpl` e `FormsPortalSampleMetadataServiceImpl` (classi di implementazione) per le interfacce del servizio dati e metadati. Inoltre, contiene tutte le classi richieste per la compilazione delle classi di implementazione sopra menzionate.

[Ottieni file](assets/sample_package.zip)

## Verifica la lunghezza del nome del file  {#verify-length-of-the-file-name}

L’implementazione del database di Forms Portal utilizza una tabella di metadati aggiuntiva. La tabella dispone di una chiave primaria composita basata sulle colonne Chiave e ID della tabella. MySQL consente chiavi primarie fino a una lunghezza di 255 caratteri. Puoi utilizzare il seguente script di convalida lato client per verificare la lunghezza del nome file associato al widget file. La convalida viene eseguita quando un file viene allegato. Lo script fornito nella procedura seguente visualizza un messaggio quando il nome del file è maggiore di 150 (inclusa l’estensione). È possibile modificare lo script per verificare la presenza di un numero diverso di caratteri.

Per creare [una libreria client](/help/sites-developing/clientlibs.md) e utilizzare lo script, effettuare le seguenti operazioni:

1. Accedi a CRXDE e passa a /etc/clientlibs/
1. Creare un nodo di tipo **cq:ClientLibraryFolder** e fornire il nome del nodo. Esempio: `validation`.

   Fare clic su **[!UICONTROL Salva tutto]**.

1. Fare clic con il pulsante destro del mouse sul nodo, scegliere **[!UICONTROL crea nuovo file]** e creare un file con estensione .txt. Ad esempio, `js.txt`Aggiungi il codice seguente al file .txt appena creato e fai clic su **[!UICONTROL Salva tutto]**.

   ```javascript
   #base=util
    util.js
   ```

   Nel codice precedente, `util` è il nome della cartella e `util.js` il nome del file nella cartella `util`. La cartella `util` e il file `util.js` vengono creati nei passaggi seguenti.

1. Fare clic con il pulsante destro del mouse sul nodo `cq:ClientLibraryFolder` creato nel passaggio 2, selezionare Crea > Crea cartella. Creare una cartella denominata `util`. Fare clic su **[!UICONTROL Salva tutto]**. Fare clic con il pulsante destro del mouse sulla cartella `util`, selezionare Crea > Crea file. Creare un file denominato `util.js`. Fare clic su **[!UICONTROL Salva tutto]**.

1. Aggiungi il codice seguente al file util.js e fai clic su **[!UICONTROL Salva tutto]**. Lunghezza di convalida del codice del nome file.

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >Lo script è per il componente widget di allegati predefinito. Se avete personalizzato il widget di allegati predefinito, modificate lo script precedente per incorporare le rispettive modifiche.

1. Aggiungi la seguente proprietà alla cartella creata al passaggio 2 e fai clic su **[!UICONTROL Salva tutto]**.

   * **[!UICONTROL Nome:]** categorie

   * **[!UICONTROL Tipo:]** Stringa

   * **[!UICONTROL Valore:]** fp.validation

   * **[!UICONTROL opzione multipla:]** abilitata

1. Passa a `/libs/fd/af/runtime/clientlibs/guideRuntime` e aggiungi il valore `fp.validation` alla proprietà di incorporamento.

1. Passa a /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA e aggiungi il valore `fp.validation` alla proprietà di incorporamento.

   >[!NOTE]
   >
   >Se utilizzi librerie client personalizzate invece delle librerie client guideRuntime e guideRuntimeWithXfa, utilizza il nome della categoria per incorporare la libreria client creata in questa procedura nelle librerie personalizzate caricate in fase di esecuzione.

1. Fare clic su **[!UICONTROL Salva tutto.]** Ora, quando il nome del file supera i 150 caratteri (inclusa l&#39;estensione) viene visualizzato un messaggio.
