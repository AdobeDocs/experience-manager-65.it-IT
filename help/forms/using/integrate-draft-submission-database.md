---
title: Esempio per l’integrazione del componente bozze e invii con il database
seo-title: Esempio per l’integrazione del componente bozze e invii con il database
description: Implementazione di riferimento di servizi personalizzati di dati e metadati per integrare le bozze e i componenti inviati in un database.
seo-description: Implementazione di riferimento di servizi personalizzati di dati e metadati per integrare le bozze e i componenti inviati in un database.
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---


# Esempio per l’integrazione del componente bozze e invii con il database {#sample-for-integrating-drafts-submissions-component-with-database}

## Panoramica di esempio {#sample-overview}

Le bozze del portale AEM Forms e il componente di invio consentono agli utenti di salvare i moduli come bozze e di inviarli successivamente da qualsiasi dispositivo. Inoltre, gli utenti possono visualizzare i moduli inviati sul portale. Per abilitare questa funzionalità, i AEM Forms forniscono servizi per dati e metadati che consentono di memorizzare i dati compilati dall&#39;utente nel modulo, nonché i metadati del modulo associati alle bozze e ai moduli inviati. Per impostazione predefinita, questi dati sono memorizzati nell&#39;archivio CRX. Tuttavia, poiché gli utenti interagiscono con i moduli tramite l&#39;istanza di pubblicazione AEM, che in genere si trova all&#39;esterno del firewall aziendale, le organizzazioni possono voler personalizzare l&#39;archiviazione dei dati per renderla più sicura e affidabile.

L’esempio, discusso in questo documento, è un’implementazione di riferimento di servizi di dati e metadati personalizzati per integrare le bozze e i componenti inviati in un database. Il database utilizzato nell&#39;implementazione di esempio è **MySQL 5.6.24**. Tuttavia, potete integrare il componente bozze e invii con qualsiasi database di vostra scelta.

>[!NOTE]
>
>* Gli esempi e le configurazioni illustrati in questo documento sono conformi a MySQL 5.6.24 e devono essere sostituiti in modo appropriato per il sistema di database.
>* Verificate di aver installato la versione più recente del pacchetto del componente aggiuntivo AEM Forms. Per l&#39;elenco dei pacchetti disponibili, consultate l&#39;articolo sui rilasci di [AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) .
>* Il pacchetto di esempio funziona solo con le azioni di invio Moduli adattivi.


## Configurare e configurare l’esempio {#set-up-and-configure-the-sample}

Per installare e configurare l’esempio, eseguite i seguenti passaggi, su tutte le istanze di creazione e pubblicazione:

1. Scaricate il seguente pacchetto **aem-fp-db-integration-sample-pkg-6.1.2.zip** nel file system.

   Pacchetto di esempio per l&#39;integrazione del database

   [Ottieni file](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Andate a AEM Package Manager all&#39;indirizzo https://[*host*]:[*port*]/crx/packmgr/.
1. Fate clic su **[!UICONTROL Carica pacchetto]**.

1. Selezionate il pacchetto **aem-fp-db-integration-sample-pkg-6.1.2.zip** e fate clic su **[!UICONTROL OK]**.
1. Fate clic su **[!UICONTROL Installa]** accanto al pacchetto per installare il pacchetto.
1. Andate alla **[!UICONTROL pagina Configurazione]** della console Web di AEM all&#39;indirizzo https://[*host*]:[*port*]/system/console/configMgr.
1. Fare clic per aprire la configurazione **[!UICONTROL Bozza e Invio di]** Forms Portal in modalità di modifica.

1. Specificare i valori delle proprietà come descritto nella tabella seguente:

   | **Proprietà** | **Descrizione** | **Valore** |
   |---|---|---|
   | Servizio dati bozza di Forms Portal | Identificatore per il servizio dati bozza | formsportal.sampledataservice |
   | Servizio metadati bozza del portale Forms | Identificatore per il servizio di metadati bozza | formsportal.samplemetadataservice |
   | Servizio di invio dati Forms Portal | Identificatore per il servizio dati di invio | formsportal.sampledataservice |
   | Servizio di invio metadati del portale Forms | Identificatore per il servizio di invio metadati | formsportal.samplemetadataservice |
   | Servizio di firma dati in sospeso di Forms Portal | Identificatore per il servizio dati Firma in sospeso | formsportal.sampledataservice |
   | Servizio metadati firma in sospeso di Forms Portal | Identificatore per il servizio metadati Firma in sospeso | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >I servizi vengono risolti con i relativi nomi indicati come valore per la `aem.formsportal.impl.prop` chiave come segue:

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   È possibile modificare i nomi delle tabelle di dati e metadati.

   Per assegnare un nome diverso alla tabella di metadati:

   * Nella console Web Configuration (Configurazione console Web), individuare e fare clic su Forms Portal Metadata Service Sample Implementation. Potete modificare i valori dell’origine dati, i metadati o il nome della tabella di metadati aggiuntivi.

   Per specificare un nome diverso per la tabella di dati:

   * In Configurazione console Web, individuare e fare clic su Implementazione di esempio del servizio dati di Forms Portal. È possibile modificare i valori dell&#39;origine dati e il nome della tabella dati.
   >[!NOTE]
   >
   >Se si modificano i nomi delle tabelle, fornirli nella configurazione di Form Portal.

1. Lasciate invariate le altre configurazioni e fate clic su **[!UICONTROL Salva]**.

1. La connessione al database può essere eseguita tramite Apache Sling Connection Pooled Data Source.
1. Per la connessione Apache Sling, trovare e fare clic per aprire **[!UICONTROL Apache Sling Connection Conpool DataSource]** in modalità di modifica nella configurazione della console Web. Specificare i valori delle proprietà come descritto nella tabella seguente:

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Valore</strong></td>
  </tr>
  <tr>
   <td>Nome origine dati</td>
   <td><p>Nome origine dati per filtrare i driver dal pool di origini dati</p> <p><strong>Nota: </strong><em>L'implementazione di esempio utilizza FormsPortal come nome dell'origine dati.</em></p> </td>
  </tr>
  <tr>
   <td>Classe driver JDBC</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>URI connessione JDBC<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>porta</em>]/[<em>nome</em>_schema]</td>
  </tr>
  <tr>
   <td>Nome utente</td>
   <td>Un nome utente per l'autenticazione e l'esecuzione di azioni sulle tabelle del database</td>
  </tr>
  <tr>
   <td>Password</td>
   <td>Password associata al nome utente</td>
  </tr>
  <tr>
   <td>Isolamento transazione</td>
   <td>READ_COMMTED</td>
  </tr>
  <tr>
   <td>Numero massimo di connessioni attive</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>Numero massimo di connessioni inattive</td>
   <td>100</td>
  </tr>
  <tr>
   <td>Connessioni con inattività minima</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Dimensione iniziale</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Max</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>Test di credito</td>
   <td>Selezionato</td>
  </tr>
  <tr>
   <td>Test while Idle</td>
   <td>Selezionato</td>
  </tr>
  <tr>
   <td>Query convalida</td>
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
> * Il driver JDBC per MySQL non è fornito con l&#39;esempio. Assicurarsi di aver effettuato il provisioning e fornire le informazioni necessarie per configurare il pool di connessioni JDBC.
> * Indicate le istanze di creazione e pubblicazione per utilizzare lo stesso database. Il valore del campo URI della connessione JDBC deve essere lo stesso per tutte le istanze di creazione e pubblicazione.

>



1. Lasciate invariate le altre configurazioni e fate clic su **[!UICONTROL Salva]**.

1. Se nello schema del database è già presente una tabella, passare al passaggio successivo.

   In caso contrario, se nello schema del database non è già presente una tabella, eseguire le seguenti istruzioni SQL per creare tabelle separate per i dati, i metadati e i metadati aggiuntivi nello schema del database:

   >[!NOTE]
   >
   >Non sono necessari database diversi per le istanze di creazione e pubblicazione. Usate lo stesso database per tutte le istanze di creazione e pubblicazione.

   **Istruzione SQL per la tabella di dati**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Istruzione SQL per la tabella di metadati**

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

   **Istruzione SQL per i metadati aggiuntivi**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
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

1. Se nello schema del database sono già presenti tabelle (dati, metadati e altri metadati), eseguire le seguenti query di modifica della tabella:

   **Istruzione SQL per la modifica della tabella di dati**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Istruzione SQL per la modifica della tabella di metadati**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >La query di aggiunta metadati ALTER TABLE non riesce se è già stata eseguita e la colonna marcata per Deletion è presente nella tabella.

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

   **Istruzione SQL per la modifica della tabella aggiuntiva metadati**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

L&#39;implementazione di esempio è ora configurata, che consente di elencare le bozze e gli invii durante la memorizzazione di tutti i dati e metadati in un database. Vediamo ora in che modo i servizi di dati e metadati sono configurati nell’esempio.

## Installare il file mysql-Connector-java-5.1.39-bin.jar {#install-mysql-connector-java-bin-jar-file}

Per installare il file mysql-Connector-java-5.1.39-bin.jar, eseguite i seguenti passaggi in tutte le istanze di creazione e pubblicazione:

1. Individuate `https://'[server]:[port]'/system/console/depfinder` e cercate il pacchetto com.mysql.jdbc.
1. Nella colonna Esportato da, verificate che il pacchetto sia esportato da un pacchetto qualsiasi.

   Continuate se il pacchetto non viene esportato da alcun bundle.

1. Andate a `https://'[server]:[port]'/system/console/bundles` e fate clic su **[!UICONTROL Installa/Aggiorna]**.
1. Fate clic su **[!UICONTROL Scegli file]** e individuate il file mysql-Connector-java-5.1.39-bin.jar. Inoltre, selezionate le caselle di controllo **[!UICONTROL Avvia pacchetto]** e **[!UICONTROL Aggiorna pacchetti]** .
1. Fate clic su **[!UICONTROL Installa o Aggiorna]**. Al termine, riavviare il server.
1. (Solo ** Windows) Disattivare il firewall di sistema del sistema operativo in uso.

## Codice di esempio per i dati del portale dei moduli e il servizio di metadati {#sample-code-for-forms-portal-data-and-metadata-service}

Il file ZIP seguente contiene `FormsPortalSampleDataServiceImpl` e `FormsPortalSampleMetadataServiceImpl` (classi di implementazione) per le interfacce di servizi di dati e metadati. Contiene inoltre tutte le classi necessarie per la compilazione delle suddette classi di implementazione.

[Ottieni file](assets/sample_package.zip)

## Verificare la lunghezza del nome del file  {#verify-length-of-the-file-name}

L&#39;implementazione del database di Forms Portal utilizza una tabella di metadati aggiuntiva. La tabella presenta una chiave primaria composita basata sulle colonne Key e id della tabella. MySQL consente chiavi primarie fino a un massimo di 255 caratteri. È possibile utilizzare il seguente script di convalida sul lato client per verificare la lunghezza del nome file associato al widget del file. La convalida viene eseguita quando un file viene allegato. Lo script fornito nella procedura seguente visualizza un messaggio, quando il nome del file è maggiore di 150 (inclusa l&#39;estensione). È possibile modificare lo script per verificarne la presenza di un numero diverso di caratteri.

Per creare [una libreria](/help/sites-developing/clientlibs.md) client e utilizzare lo script, effettuate le seguenti operazioni:

1. Accedete a CRXDE e andate a /etc/clientlibs/
1. Create un nodo di tipo **cq:ClientLibraryFolder** e fornite il nome del nodo. Esempio, `validation`.

   Fate clic su **[!UICONTROL Salva tutto]**.

1. Fare clic con il pulsante destro del mouse sul nodo, scegliere **[!UICONTROL Crea nuovo file]** e creare un file con estensione .txt. Ad esempio, `js.txt`aggiungete il codice seguente al file .txt appena creato e fate clic su **[!UICONTROL Salva tutto]**.

   ```javascript
   #base=util
    util.js
   ```

   Nel codice riportato sopra, `util` è il nome della cartella e `util.js` il nome del file nella `util` cartella. La `util` cartella e `util.js` il file vengono creati nei passaggi successivi.

1. Fate clic con il pulsante destro del mouse sul `cq:ClientLibraryFolder` nodo creato al punto 2, selezionate Crea > Crea cartella. Create una cartella denominata `util`. Fate clic su **[!UICONTROL Salva tutto]**. Fate clic con il pulsante destro del mouse sulla `util` cartella e scegliete Crea > Crea file. Create un file denominato `util.js`. Fate clic su **[!UICONTROL Salva tutto]**.

1. Aggiungi il codice seguente al file util.js e fai clic su **[!UICONTROL Salva tutto]**. Lunghezza di convalida del codice per il nome del file.

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
   >Lo script è per il componente widget allegato out (OOTB) fornito con il prodotto. Se avete personalizzato il widget degli allegati OOTB, modificate lo script precedente in modo da includere le rispettive modifiche.

1. Aggiungete la seguente proprietà alla cartella creata nel passaggio 2 e fate clic su **[!UICONTROL Salva tutto]**.

   * **[!UICONTROL Nome:]** category

   * **[!UICONTROL Tipo:]** Stringa

   * **[!UICONTROL Valore:]** fp.validation

   * **[!UICONTROL opzione multipla:]** Abilitato

1. Spostarsi `/libs/fd/af/runtime/clientlibs/guideRuntime`e aggiungere il `fp.validation` valore alla proprietà embed.

1. Andate a /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA e aggiungete il `fp.validation` valore alla proprietà embed.

   >[!NOTE]
   >
   >Se si utilizzano librerie client personalizzate invece delle librerie client guideRuntime e guideRuntimeWithXfa, utilizzare il nome della categoria per incorporare la libreria client creata in questa procedura nelle librerie personalizzate caricate in fase di esecuzione.

1. Fate clic su **[!UICONTROL Salva tutto.]** Ora, quando il nome del file è più grande di 150 (inclusa l&#39;estensione) caratteri, viene visualizzato un messaggio.

