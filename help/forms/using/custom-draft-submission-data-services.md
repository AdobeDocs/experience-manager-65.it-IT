---
title: Personalizzazione dei servizi di dati Bozza e Invio
seo-title: Personalizzazione dei servizi di dati Bozza e Invio
description: ' AEM Forms, per impostazione predefinita, memorizza i moduli adattivi bozza e inviati in un nodo predefinito nell''istanza Pubblica. Tuttavia, è possibile configurare i servizi dati bozza e invio di  AEM Forms per personalizzare l''archiviazione dei moduli adattivi bozza e inviati.'
seo-description: ' AEM Forms, per impostazione predefinita, memorizza i moduli adattivi bozza e inviati in un nodo predefinito nell''istanza Pubblica. Tuttavia, è possibile configurare i servizi dati bozza e invio di  AEM Forms per personalizzare l''archiviazione dei moduli adattivi bozza e inviati.'
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Personalizzazione dei servizi di dati Bozza e Invio {#customizing-draft-and-submission-data-services}

## Panoramica {#overview}

 AEM Forms consente agli utenti di salvare un modulo adattivo come bozza. La funzionalità bozza offre agli utenti la possibilità di mantenere un modulo in corso di elaborazione. Un utente può quindi completare e inviare il modulo in qualsiasi momento da qualsiasi dispositivo.

Per impostazione predefinita,  AEM Forms memorizza i dati utente associati alla bozza e all&#39;invio nell&#39;istanza Pubblica nel nodo `/content/forms/fp`.

Tuttavia,  componenti del portale AEM Forms offre servizi di dati che consentono di personalizzare l&#39;implementazione dell&#39;archiviazione dei dati utente per bozze e invii. Ad esempio, puoi archiviare i dati in un archivio dati attualmente implementato nell&#39;organizzazione.

Per personalizzare la memorizzazione dei dati utente, è necessario implementare i servizi [Draft Data](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) e [Invia dati](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p).

## Prerequisiti {#prerequisites}

* Abilita [componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md)
* Creare una pagina del portale dei moduli [](/help/forms/using/creating-form-portal-page.md)
* Abilitare i [moduli adattivi per il portale dei moduli](/help/forms/using/draft-submission-component.md)
* Informazioni [sull&#39;implementazione di storage personalizzato](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Servizio dati bozza {#draft-data-service}

Per personalizzare l&#39;archiviazione dei dati delle bozze degli utenti, è necessario fornire l&#39;implementazione per tutti i metodi dell&#39;interfaccia `DraftAFDataService`.

Una descrizione dei metodi e dei relativi argomenti è fornita nel seguente esempio di codice dell&#39;interfaccia:

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") in case of update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## Servizio dati invio {#submission-data-service}

Per personalizzare la memorizzazione dei dati di invio degli utenti, è necessario fornire l&#39;implementazione per tutti i metodi dell&#39;interfaccia `SubmittedAFDataService`.

Una descrizione dei metodi e dei relativi argomenti è fornita nel seguente esempio di codice dell&#39;interfaccia:

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```

