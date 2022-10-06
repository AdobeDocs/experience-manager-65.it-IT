---
title: Archiviazione personalizzata per le bozze e i componenti di invio
seo-title: Custom storage for drafts and submissions component
description: Scopri come personalizzare l’archiviazione dei dati utente per bozze e invii.
seo-description: See how to customize the storage of user data for drafts and submissions.
uuid: ac2e80ee-a9c7-44e6-801e-fe5a840cb7f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 154255e7-468a-42e6-a33d-eee691cf854d
feature: Forms Portal
exl-id: b1300eeb-2653-4bb5-b2fd-88048c9c43b9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Archiviazione personalizzata per le bozze e i componenti di invio {#custom-storage-for-drafts-and-submissions-component}

## Panoramica {#overview}

AEM Forms consente di salvare un modulo come bozza. La funzionalità bozza ti consente di mantenere un modulo in corso di lavorazione, che puoi completare e inviare in un secondo momento da qualsiasi dispositivo.

Per impostazione predefinita, in AEM Forms i dati utente associati alla bozza e all’invio di un modulo vengono memorizzati nel `/content/forms/fp` nell’istanza Pubblica . Inoltre, i componenti del portale AEM Forms forniscono servizi dati che è possibile utilizzare per personalizzare l’implementazione dell’archiviazione dei dati utente per bozze e invii. Ad esempio, è possibile memorizzare i dati utente in un archivio dati.

## Prerequisiti  {#prerequisites}

* Abilita [componenti del portale moduli](/help/forms/using/enabling-forms-portal-components.md)
* Crea un [pagina del portale moduli](/help/forms/using/creating-form-portal-page.md)
* Abilita [portale moduli adattivi per moduli](/help/forms/using/draft-submission-component.md)
* Scopri [dettagli di implementazione dello storage personalizzato](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Servizio dati bozza {#draft-data-service}

Per personalizzare l&#39;archiviazione dei dati utente per le bozze, è necessario implementare tutti i metodi del `DraftDataService` interfaccia. Il codice di esempio seguente descrive i metodi e gli argomenti.

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null in case of creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

>[!NOTE]
>
>Il valore minimo per la lunghezza della bozza del campo ID è di 26 caratteri. Adobe consiglia di impostare la lunghezza della bozza dell&#39;ID su 26 o più caratteri.

## Servizio dati di invio {#submission-data-service}

Per personalizzare la memorizzazione dei dati utente per gli invii, è necessario implementare tutti i metodi `SubmitDataService` interfaccia. Il codice di esempio seguente descrive i metodi e gli argomenti.

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

Il portale Forms utilizza il concetto di identificatore univoco universale (UUID) per generare un ID univoco per ogni bozza e modulo inviato. Puoi anche generare un ID univoco. È possibile implementare l’interfaccia FPKeyGeneratorService, ignorarne i metodi e sviluppare una logica personalizzata per generare un ID univoco personalizzato per ogni bozza e modulo inviato. Inoltre, imposta il livello di servizio dell&#39;implementazione di generazione ID personalizzata maggiore di 0. Assicura che l’implementazione personalizzata venga utilizzata al posto dell’implementazione predefinita.

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

Puoi utilizzare l’annotazione seguente per aumentare la classificazione del servizio per l’ID personalizzato generato con il codice precedente:

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

Per utilizzare l’annotazione precedente, importa quanto segue nel progetto:

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```
