---
title: Esempio per l'integrazione del componente bozze e invii con il database
seo-title: Sample for integrating drafts & submissions component with database
description: Implementazione di riferimento di servizi di dati e metadati personalizzati per integrare le bozze e il componente di invio con un database.
seo-description: Reference implementation of customized data and metadata services to integrate drafts and submissions component with a database.
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 1%

---

# Esempio per l&#39;integrazione del componente bozze e invii con il database {#sample-for-integrating-drafts-submissions-component-with-database}

## Panoramica di esempio {#sample-overview}

Il componente bozze e invii del portale AEM Forms consente agli utenti di salvare i moduli come bozze e di inviarli successivamente da qualsiasi dispositivo. Inoltre, gli utenti possono visualizzare i moduli inviati sul portale. Per abilitare questa funzionalità, AEM Forms fornisce servizi per dati e metadati per memorizzare i dati compilati da un utente nel modulo e i metadati del modulo associati alle bozze e ai moduli inviati. Per impostazione predefinita, questi dati vengono memorizzati nell’archivio CRX. Tuttavia, poiché gli utenti interagiscono con i moduli tramite AEM’istanza di pubblicazione, generalmente all’esterno del firewall aziendale, le organizzazioni possono voler personalizzare l’archiviazione dati per renderla più sicura e affidabile.

L&#39;esempio, discusso in questo documento, è un&#39;implementazione di riferimento di servizi di dati e metadati personalizzati per integrare le bozze e i componenti di invio con un database. Il database utilizzato nell&#39;implementazione di esempio è **MySQL 5.6.24**. Tuttavia, è possibile integrare le bozze e il componente di invio con qualsiasi database desiderato.

>[!NOTE]
>
>* Gli esempi e le configurazioni illustrati in questo documento sono in base a MySQL 5.6.24 e devono essere sostituiti in modo appropriato per il sistema di database.
>* Assicurati di aver installato la versione più recente del pacchetto aggiuntivo di AEM Forms. Per l’elenco dei pacchetti disponibili, consulta [Versioni di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) articolo.
>* Il pacchetto di esempio funziona solo con le azioni di invio di Forms adattivo.


## Imposta e configura l’esempio {#set-up-and-configure-the-sample}

Esegui i seguenti passaggi, su tutte le istanze di authoring e pubblicazione, per installare e configurare l’esempio :

1. Scarica quanto segue **aem-fp-db-integration-sample-pkg-6.1.2.zip** creare un pacchetto nel file system.

   Pacchetto di esempio per l&#39;integrazione del database

[Ottieni file](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Vai AEM gestore dei pacchetti all&#39;indirizzo https://[*host*]:[*porta*]/crx/packmgr/.
1. Fai clic su **[!UICONTROL Carica pacchetto]**.

1. Sfoglia per selezionare il **aem-fp-db-integration-sample-pkg-6.1.2.zip** pacchetto e fai clic su **[!UICONTROL OK]**.
1. Fai clic su **[!UICONTROL Installa]** accanto al pacchetto per installare il pacchetto.
1. Vai a **[!UICONTROL Configurazione della console Web AEM]**
pagina https://[*host*]:[*porta*]/system/console/configMgr.
1. Fai clic per aprire **[!UICONTROL Configurazione bozza e invio del portale Forms]** in modalità di modifica.

1. Specifica i valori delle proprietà come descritto nella tabella seguente:

   | **Proprietà** | **Descrizione** | **Valore** |
   |---|---|---|
   | Servizio dati bozza di Forms Portal | Identificatore del servizio dati bozza | formsportal.sampledataservice |
   | Servizio metadati bozza del portale Forms | Identificatore per il servizio di metadati bozza | formsportal.samplemetadataservice |
   | Servizio di invio dati di Forms Portal | Identificatore per il servizio di invio dati | formsportal.sampledataservice |
   | Servizio di invio metadati del portale Forms | Identificatore per il servizio di invio metadati | formsportal.samplemetadataservice |
   | Servizio dati di firma in sospeso del portale Forms | Identificatore del servizio dati Firma in sospeso | formsportal.sampledataservice |
   | Servizio metadati di firma in sospeso del portale Forms | Identificatore del servizio metadati Firma in sospeso | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >I servizi vengono risolti con i loro nomi indicati come valore per il `aem.formsportal.impl.prop` come segue:

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   È possibile modificare i nomi delle tabelle di dati e metadati.

   Per assegnare un nome diverso alla tabella di metadati:

   * Nella Configurazione della console Web, trova e fai clic su Implementazione di esempio del servizio metadati del portale Forms. Puoi modificare i valori dell’origine dati, i metadati o il nome della tabella di metadati aggiuntivi.

   Per assegnare un nome diverso alla tabella di dati:

   * Nella Configurazione della console Web, trova e fai clic su Implementazione di esempio del servizio dati del portale Forms. È possibile modificare i valori dell’origine dati e il nome della tabella dati.
   >[!NOTE]
   >
   >Se si modificano i nomi delle tabelle, fornirli nella configurazione del Portale moduli.

1. Lascia le altre configurazioni così come sono e fai clic su **[!UICONTROL Salva]**.

1. La connessione al database può essere eseguita tramite l’origine dati in pool di connessione Apache Sling.
1. Per la connessione Apache Sling, trova e fai clic per aprire **[!UICONTROL Origine dati in pool di connessione Apache Sling]** in modalità di modifica nella configurazione della console Web. Specifica i valori delle proprietà come descritto nella tabella seguente:

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Valore</strong></td>
  </tr>
  <tr>
   <td>Nome origine dati</td>
   <td><p>Un nome di origine dati per filtrare i driver dal pool di origini dati</p> <p><strong>Nota: </strong><em>L’implementazione di esempio utilizza FormsPortal come nome dell’origine dati.</em></p> </td>
  </tr>
  <tr>
   <td>Classe del driver JDBC</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>URI di connessione JDBC<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>porta</em>]/[<em>nome_schema</em>]</td>
  </tr>
  <tr>
   <td>Nome utente</td>
   <td>Nome utente per l'autenticazione e l'esecuzione di azioni sulle tabelle del database</td>
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
   <td>Connessioni di inattività minima</td>
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
   <td>Test su credito</td>
   <td>Selezionato</td>
  </tr>
  <tr>
   <td>Test durante l'inattività</td>
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
>* Il driver JDBC per MySQL non viene fornito con l&#39;esempio. Assicurati di aver effettuato il provisioning e di fornire le informazioni necessarie per configurare il pool di connessioni JDBC.
>* Posiziona il puntatore sull’istanza di creazione e pubblicazione per utilizzare lo stesso database. Il valore del campo URI di connessione JDBC deve essere lo stesso per tutte le istanze di authoring e pubblicazione.


1. Lascia le altre configurazioni così come sono e fai clic su **[!UICONTROL Salva]**.

1. Se nello schema di database è già presente una tabella, passare al passaggio successivo.

   In caso contrario, se nello schema di database non è già presente una tabella, eseguire le istruzioni SQL seguenti per creare tabelle separate per i dati, i metadati e i metadati aggiuntivi nello schema di database:

   >[!NOTE]
   >
   >Non sono necessari database diversi per le istanze di authoring e pubblicazione. Utilizza lo stesso database su tutte le istanze di authoring e pubblicazione.

   **Istruzione SQL per tabella dati**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Istruzione SQL per tabella metadati**

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

   **Istruzione SQL per metadati aggiuntivi**

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

1. Se nello schema di database sono già presenti tabelle (dati, metadati e metadati aggiuntivi), eseguire le seguenti query di modifica della tabella:

   **Istruzione SQL per la modifica della tabella dati**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Istruzione SQL per la modifica della tabella metadati**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >Se la query di aggiunta dei metadati ALTER TABLE è già stata eseguita e la colonna markedforDeletion è presente nella tabella.

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

   **Istruzione SQL per la modifica della tabella aggiuntiva dei metadati**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

L&#39;implementazione di esempio è ora configurata e può essere utilizzata per elencare le bozze e gli invii durante la memorizzazione di tutti i dati e metadati in un database. Vediamo ora in che modo i servizi dati e metadati sono configurati nell’esempio.

## Installa il file mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-bin-jar-file}

Esegui i seguenti passaggi, su tutte le istanze di authoring e pubblicazione, per installare il file mysql-connector-java-5.1.39-bin.jar:

1. Passa a `https://'[server]:[port]'/system/console/depfinder` e cerca il pacchetto com.mysql.jdbc.
1. Nella colonna Esportato da , controlla se il pacchetto viene esportato da un bundle.

   Procedi se il pacchetto non viene esportato da alcun bundle.

1. Passa a `https://'[server]:[port]'/system/console/bundles` e fai clic su **[!UICONTROL Installazione/aggiornamento]**.
1. Fai clic su **[!UICONTROL Scegli file]** e cerca di selezionare il file mysql-connector-java-5.1.39-bin.jar . Inoltre, seleziona **[!UICONTROL Avvia bundle]** e **[!UICONTROL Aggiorna pacchetti]** caselle di controllo.
1. Fai clic su **[!UICONTROL Installa o aggiorna]**. Una volta completato, riavvia il server.
1. (*Solo Windows*) Disattivare il firewall di sistema per il sistema operativo in uso.

## Codice di esempio per il servizio dati e metadati del portale moduli {#sample-code-for-forms-portal-data-and-metadata-service}

Il seguente file ZIP contiene `FormsPortalSampleDataServiceImpl` e `FormsPortalSampleMetadataServiceImpl` (classi di implementazione) per le interfacce del servizio dati e metadati. Inoltre, contiene tutte le classi necessarie per la compilazione delle suddette classi di implementazione.

[Ottieni file](assets/sample_package.zip)

## Verificare la lunghezza del nome file  {#verify-length-of-the-file-name}

L’implementazione del database di Forms Portal utilizza una tabella di metadati aggiuntiva. La tabella dispone di una chiave primaria composita basata sulle colonne Chiave e ID della tabella. MySQL consente le chiavi primarie fino alla lunghezza di 255 caratteri. È possibile utilizzare il seguente script di convalida lato client per verificare la lunghezza del nome file allegato al widget file. La convalida viene eseguita quando un file viene allegato. Lo script fornito nella procedura seguente visualizza un messaggio, quando il nome del file è maggiore di 150 (inclusa l’estensione). È possibile modificare lo script per verificarne la presenza in un numero diverso di caratteri.

Esegui i seguenti passaggi per creare [una libreria client](/help/sites-developing/clientlibs.md) e utilizza lo script:

1. Accedi a CRXDE e naviga su /etc/clientlibs/
1. Crea un nodo di tipo **cq:ClientLibraryFolder** e fornire il nome del nodo. Esempio: `validation`.

   Fai clic su **[!UICONTROL Salva tutto]**.

1. Fai clic con il pulsante destro del mouse sul nodo e fai clic su **[!UICONTROL crea nuovo file]** e crea un file con estensione .txt. Ad esempio: `js.txt`Aggiungi il codice seguente al file .txt appena creato e fai clic su **[!UICONTROL Salva tutto]**.

   ```javascript
   #base=util
    util.js
   ```

   Nel codice di cui sopra, `util` è il nome della cartella e `util.js` nome del file nel `util` cartella. La `util` cartella e `util.js` vengono creati nei passaggi successivi.

1. Fai clic con il pulsante destro del mouse sul pulsante `cq:ClientLibraryFolder` creato al passaggio 2, selezionare Crea > Crea cartella. Crea una cartella denominata `util`. Fai clic su **[!UICONTROL Salva tutto]**. Fai clic con il pulsante destro del mouse sul pulsante `util` selezionare Crea > Crea file. Crea un file denominato `util.js`. Fai clic su **[!UICONTROL Salva tutto]**.

1. Aggiungi il codice seguente al file util.js e fai clic su **[!UICONTROL Salva tutto]**. Lunghezza di convalida del codice del nome del file.

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
   >Lo script è per il componente widget allegato pronto all’uso (OOTB). Se hai personalizzato il widget allegato OOTB, modifica lo script precedente per incorporare le relative modifiche.

1. Aggiungi la seguente proprietà alla cartella creata nel passaggio 2 e fai clic su **[!UICONTROL Salva tutto]**.

   * **[!UICONTROL Nome:]** categorie

   * **[!UICONTROL Tipo:]** Stringa

   * **[!UICONTROL Valore:]** fp.validation

   * **[!UICONTROL opzione multipla:]** Abilitato

1. Passa a `/libs/fd/af/runtime/clientlibs/guideRuntime`e aggiunge `fp.validation` alla proprietà embed .

1. Passa a /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA e aggiungi il `fp.validation` da incorporare.

   >[!NOTE]
   >
   >Se utilizzi librerie client personalizzate invece delle librerie client guideRuntime e guideRuntimeWithXfa, utilizza il nome della categoria per incorporare la libreria client creata in questa procedura nelle librerie personalizzate caricate in fase di esecuzione.

1. Fai clic su **[!UICONTROL Salva tutto.]** Ora, quando il nome del file è più grande di 150 caratteri (inclusa l’estensione), viene visualizzato un messaggio.
