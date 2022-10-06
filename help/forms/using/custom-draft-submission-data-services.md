---
title: Personalizzazione dei servizi di dati Bozza e Invio
seo-title: Customizing Draft and Submission data services
description: Per impostazione predefinita, AEM Forms memorizza i moduli adattivi bozza e inviati in un nodo predefinito sull’istanza Pubblica. Tuttavia, puoi configurare la bozza e l’invio di servizi dati di AEM Forms per personalizzare l’archiviazione dei moduli adattivi bozza e inviati.
seo-description: AEM Forms, by default, stores draft and submitted adaptive forms in a default node on the Publish instance. However, you can configure the draft and submission data services of AEM Forms to customize the storage of draft and submitted adaptive forms.
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Personalizzazione dei servizi di dati Bozza e Invio {#customizing-draft-and-submission-data-services}

## Panoramica {#overview}

AEM Forms consente agli utenti di salvare un modulo adattivo come bozza. La funzionalità bozza consente agli utenti di mantenere un modulo in corso di lavorazione. Un utente può quindi completare e inviare il modulo in qualsiasi momento da qualsiasi dispositivo.

Per impostazione predefinita, AEM Forms memorizza i dati utente associati alla bozza e all’invio nell’istanza Pubblica in `/content/forms/fp` nodo.

Tuttavia, i componenti del portale AEM Forms forniscono servizi dati che consentono di personalizzare l’implementazione dell’archiviazione dei dati utente per bozze e invii. Ad esempio, puoi archiviare i dati in un archivio dati attualmente implementato nella tua organizzazione.

Per personalizzare la memorizzazione dei dati utente, è necessario implementare il [Dati bozza](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) e [Dati di invio](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p) servizi.

## Prerequisiti {#prerequisites}

* Abilita [Componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md)
* Crea un [pagina del portale moduli](/help/forms/using/creating-form-portal-page.md)
* Abilita [portale moduli adattivi per moduli](/help/forms/using/draft-submission-component.md)
* Scopri [dettagli di implementazione dello storage personalizzato](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Servizio dati bozza {#draft-data-service}

Per personalizzare l&#39;archiviazione dei dati di bozza dell&#39;utente, è necessario fornire l&#39;implementazione di tutti i metodi del `DraftAFDataService` interfaccia.

Una descrizione dei metodi e dei relativi argomenti è fornita nel seguente codice di esempio dell’interfaccia:

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

## Servizio dati di invio {#submission-data-service}

Per personalizzare l’archiviazione dei dati di invio degli utenti, è necessario fornire l’implementazione di tutti i metodi del `SubmittedAFDataService` interfaccia.

Una descrizione dei metodi e dei relativi argomenti è fornita nel seguente codice di esempio dell’interfaccia:

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
