---
title: 'Utilizzare i metadati in una notifica e-mail '
seo-title: Use metadata in an email notification
description: Utilizzare i metadati per compilare le informazioni in una notifica e-mail del flusso di lavoro dei moduli
seo-description: Use metadata to populate information in a forms workflow email notification
uuid: 9075b64e-1934-44d5-8b16-aa6e95e93da9
topic-tags: publish
discoiquuid: d48b5137-c866-43cd-925b-7a6a8eac8c0b
docset: aem65
exl-id: 18cfc4be-676d-4f08-afc1-4f11bb48dab6
source-git-commit: 9cf4a68a2b3312fe53282e2fd4ec81988f2fd453
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 1%

---

# Utilizzare i metadati in una notifica e-mail {#use-metadata-in-an-email-notification}

È possibile utilizzare il passaggio Assegna attività per creare e assegnare attività a un utente o a un gruppo. Quando un’attività viene assegnata a un utente o a un gruppo, viene inviata una notifica e-mail all’utente definito o a ciascun membro del gruppo definito. Una tipica [notifica e-mail](../../forms/using/use-custom-email-template-assign-task-step.md) contiene il collegamento dell&#39;attività assegnata e le informazioni relative all&#39;attività.

Puoi utilizzare i metadati in un modello e-mail per popolare dinamicamente le informazioni in una notifica e-mail. Ad esempio, il valore del titolo, della descrizione, della data di scadenza, della priorità, del flusso di lavoro e dell’ultima data nella seguente notifica e-mail viene selezionato dinamicamente in fase di esecuzione (quando viene generata una notifica e-mail).

![Modello e-mail predefinito](assets/default_email_template_metadata_new.png)

I metadati vengono memorizzati in coppie chiave-valore. Puoi specificare la chiave nel modello e-mail e la chiave viene sostituita con un valore in fase di esecuzione (quando viene generata una notifica e-mail). Ad esempio, nell&#39;esempio di codice seguente, &quot;$ {workitem_title}&quot; è una chiave. Viene sostituito con il valore &quot;Loan-Request&quot; in fase di runtime.

```html
subject=Task Assigned - ${workitem_title}

message=<html><body>\n\
 <table style="width: 480px; font-family: Helvetica, Arial, sans-serif; border: 0; padding: 0; vertical-align: top; text-align: left; word-wrap: break-word; margin: 16px auto; color:#323232; background-color:#FFFCF9; border-collapse: collapse;">\n\
  <tbody>\n\
   <tr>\n\
    <td style="height: 100px; width: 480px; background-color: #FFE0CB; border-top: 5pt solid black; font-family: Helvetica, Arial, sans-serif; font-weight: bold; font-size: 15px; line-height: 20px; padding: 12px; color: #707070;">\n\
      Sample Company\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="font-family: Helvetica, Arial, sans-serif; height: auto; background-color: #FFFCF9; padding: 32px 16px 20px 16px; ">\n\
     <pre style="font-size: 13px; font-family: Helvetica, Arial, sans-serif;  font-weight: normal; color: #323232;"> Hello ${workitem_assignee},\n\
 The following task has been assigned to you:</pre>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="width: 480px;">\n\
     <table style="height: auto; width: 480px; background-color:#FFFBF9; font-family: Helvetica, Arial, sans-serif; border-collapse: collapse;">\n\
      <tbody>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> TITLE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_title}</p>\n\
        </td>\n\
       </tr>\n\
                            <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DESCRIPTION</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_description}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DUE DATE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_due_date}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> PRIORITY</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_priority}</p>\n\
        </td>\n\
       </tr>\n\
       <tr>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> WORKFLOW</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_workflow}</p>\n\
        </td>\n\
       </tr>\n\
      </tbody>\n\
     </table>\n\
    </td>\n\
   </tr>\n\
   <tr style = "text-align: center; vertical-align: middle;">\n\
    <td style="padding:48px 0 72px 0;"> \n\
     <a href="${workitem_url}" target="_blank" style="background-color: #1EBBBB; font-size: 18px; line-height: 25px; font-weight: bold; color: #FFFFFF; text-decoration: none; padding: 15px 15px 15px 15px;">Open Task</a>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="border-top: solid 1px #EDEAE7; padding: 16px;">\n\
     <p><span style="font-size: 12px; font-weight: normal; font-style: italic; color: #919191;">This is an automatically generated email. Please do not reply to this email.</code></p>\n\
    </td>\n\
   </tr>\n\
  </tbody>\n\
 </table>\n\
</body>\n\
</html>\n\
```

## Utilizzo dei metadati generati dal sistema in una notifica e-mail {#using-system-generated-metadata-in-an-email-notification}

Un&#39;applicazione AEM Forms fornisce diverse variabili di metadati (coppie chiave-valore) pronte all&#39;uso. Puoi utilizzare queste variabili in un modello e-mail. Il valore della variabile si basa sull’applicazione forms associata. Nella tabella seguente sono elencate tutte le variabili di metadati disponibili:

<table>
 <tbody> 
  <tr> 
   <td>Chiave</td> 
   <td>Descrizione</td> 
  </tr> 
  <tr> 
   <td>titolo_elemento_lavoro</td> 
   <td>Titolo dell’applicazione dei moduli associata.</td> 
  </tr> 
  <tr> 
   <td>workitem_url</td> 
   <td>URL per accedere all’applicazione forms associata.</td> 
  </tr> 
  <tr> 
   <td>descrizione_elemento_lavoro</td> 
   <td>Descrizione dell’applicazione dei moduli associata.</td> 
  </tr> 
  <tr> 
   <td>elemento di lavoro_priorità</td> 
   <td>Priorità specificata per l’applicazione dei moduli associata.</td> 
  </tr> 
  <tr> 
   <td>data_scadenza_elemento_lavoro</td> 
   <td>Ultima data di intervento sull’applicazione dei moduli associata.</td> 
  </tr> 
  <tr> 
   <td>workflow</td> 
   <td>Nome del flusso di lavoro associato all’applicazione dei moduli.</td> 
  </tr> 
  <tr> 
   <td>workitem_assign_timestamp</td> 
   <td>Data e ora in cui l’elemento del flusso di lavoro è stato assegnato all’assegnatario attuale.</td> 
  </tr> 
  <tr> 
   <td>workitem_assignee</td> 
   <td>Nome del presente assegnatario.</td> 
  </tr> 
  <tr> 
   <td>host_prefix</td> 
   <td>URL del server autore. Ad esempio, https://10.41.42.66:4502<br /> </td> 
  </tr> 
  <tr> 
   <td>publish_prefix</td> 
   <td>URL del server di pubblicazione. Ad esempio, https://10.41.42.66:4503</td> 
  </tr> 
 </tbody> 
</table>

## Utilizzo di metadati personalizzati in una notifica e-mail {#using-custom-metadata-in-an-email-notification}

Puoi anche utilizzare metadati personalizzati in una notifica e-mail. I metadati personalizzati contengono informazioni oltre ai metadati generati dal sistema. Ad esempio, i dettagli dei criteri recuperati da un database. Puoi utilizzare un bundle ECMAScript o OSGi per aggiungere metadati personalizzati in crx-repository:

### Utilizzare ECMAScript per aggiungere metadati personalizzati  {#use-ecmascript-to-add-custom-metadata}

[](https://en.wikipedia.org/wiki/ECMAScript) ECMAScripta un linguaggio di script. Viene utilizzato per applicazioni di script lato client e server. Esegui i seguenti passaggi per utilizzare ECMAScript per aggiungere metadati personalizzati per un modello e-mail:

1. Accedi a CRX DE con un account amministrativo. L&#39;URL è https://&#39;[server]:[port]&#39;/crx/de/index.jsp

1. Passa a /apps/fd/dashboard/scripts/metadataScripts. Crea un file con estensione .ecma. Ad esempio, usermetadata.ecma

   Se il percorso indicato sopra non esiste, crealo.

1. Aggiungi il codice al file .ecma che ha la logica per generare metadati personalizzati in coppie chiave-valore. Ad esempio, il seguente codice ECMAScript genera metadati personalizzati per una polizza assicurativa:

   ```javascript
   function getUserMetaData()  {
       //Commented lines below provide an overview on how to set user metadata in map and return it.
       var HashMap = Packages.java.util.HashMap;
       var valuesMap = new HashMap();
       valuesMap.put("policyNumber", "2017568972695");
       valuesMap.put("policyHolder", "Adobe Systems");
   
       return valuesMap;
   }
   ```

1. Fai clic su Salva tutto. Ora, lo script è disponibile per la selezione AEM modello di flusso di lavoro.

   ![assigntask-metadata](assets/assigntask-metadata.png)

1. (Facoltativo) Specifica il titolo dello script:

   Se non si specifica il titolo, nel campo Metadati personalizzati viene visualizzato il percorso completo del file ECMAScript. Per specificare un titolo significativo per lo script, effettua le seguenti operazioni:

   1. Espandi il nodo dello script, fai clic con il pulsante destro del mouse sul nodo **[!UICONTROL jcr:content]** e fai clic su **[!UICONTROL Mixins]**.
   1. Digita mix:title nella finestra di dialogo Modifica mixini e fai clic su **+**.
   1. Aggiungi una proprietà con i seguenti valori.

      | Nome | jcr:title |
      |---|---|
      | Tipo | Stringa |
      | Valore | Specifica il titolo dello script. Ad esempio, metadati personalizzati per il titolare della polizza. Il valore specificato viene visualizzato nel passaggio dell&#39;attività di assegnazione. |

### Utilizza un bundle OSGi e un&#39;interfaccia Java per aggiungere metadati personalizzati {#use-an-osgi-bundle-and-java-interface-to-add-custom-metadata}

Puoi utilizzare l’interfaccia Java WorkitemUserMetadataService per aggiungere metadati personalizzati per i modelli e-mail. Puoi creare un bundle OSGi che utilizza l&#39;interfaccia Java WorkitemUserMetadataService e distribuirlo al server AEM Forms. Rende i metadati disponibili per la selezione nel passaggio Assegna attività .

Per creare un bundle OSGi con l&#39;interfaccia Java, aggiungi i file [AEM Forms Client SDK](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) jar e [granite jar](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) come dipendenze esterne al progetto di bundle OSGi. Puoi utilizzare qualsiasi Java IDE per creare un bundle OSGi. La procedura seguente fornisce i passaggi per utilizzare Eclipse per creare un bundle OSGi:

1. Apri Eclipse IDE. Passa a File > Nuovo progetto.

1. Nella schermata Seleziona una procedura guidata, seleziona Progetto Maven e fai clic su Avanti.

1. Nel nuovo progetto Maven, mantenere le impostazioni predefinite e fare clic su Avanti. Selezionare un archetipo e fare clic su Avanti. Ad esempio, maven-archetype-quickstart. Specificare ID gruppo, ID articolo, versione e pacchetto per il progetto e fare clic su Fine. Il progetto viene creato.

1. Apri il file pom.xml per la modifica e sostituisci tutti i contenuti del file con quanto segue:

1. Aggiungi il codice sorgente che utilizza l’interfaccia Java WorkitemUserMetadataService per aggiungere metadati personalizzati per i modelli e-mail. Di seguito è riportato un codice di esempio:

   ```java
   package com.aem.impl;
   
   import com.adobe.fd.workspace.service.external.WorkitemUserMetadataService;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Properties;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.osgi.framework.Constants;
   
   import java.util.HashMap;
   import java.util.Map;
   
   @Component
   @Service
   @Properties({
           @Property(name = Constants.SERVICE_DESCRIPTION, value = "A sample implementation of a user metadata service."),
           @Property(name = WorkitemUserMetadataService.SERVICE_PROPERTY_LABEL, value = "Default User Metadata Service")})
   
   public class WorkitemUserMetadataServiceImpl
     implements WorkitemUserMetadataService
   {
     public WorkitemUserMetadataServiceImpl() {}
   
     public Map<String, String> getUserMetadataMap()
     {
       HashMap<String, String> metadataMap = null;
       metadataMap = new HashMap();
       metadataMap.put("test_metadata", "tested-interface implementation");
       return metadataMap;
     }
   }
   ```

1. Apri un prompt dei comandi e passa alla directory contenente il progetto di bundle OSGi. Utilizza il seguente comando per creare il bundle OSGi:

   `mvn clean install`

1. Carica il bundle su un server AEM Forms. Puoi utilizzare AEM Gestione pacchetti per importare il bundle nel server AEM Forms.

Dopo l’importazione del bundle, puoi selezionare i metadati nel passaggio Assegna attività e utilizzarli come modello di e-mail.
