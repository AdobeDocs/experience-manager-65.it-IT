---
title: Utilizzo del CAPTCHA nei moduli adattivi
seo-title: Using CAPTCHA in adaptive forms
description: Scopri come configurare il servizio AEM CAPTCHA o Google reCAPTCHA in moduli adattivi.
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in adaptive forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Adaptive Forms
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '1972'
ht-degree: 0%

---

# Utilizzo del CAPTCHA nei moduli adattivi{#using-captcha-in-adaptive-forms}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o scopi dannosi.

AEM Forms supporta il CAPTCHA nei moduli adattivi. Puoi utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA.

>[!NOTE]
>
>* AEM Forms supporta reCAPTCHA v2 ed enterprise. Qualsiasi altra versione non è supportata.
>* Il CAPTCHA nei moduli adattivi non è supportato in modalità offline nell’app AEM Forms.

## Configurare il servizio reCAPTCHA di Google per Adaptive Forms {#google-reCAPTCHA}

Gli utenti di AEM Forms possono utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA nei moduli adattivi. Offre funzionalità CAPTCHA avanzate per proteggere il sito. Per ulteriori informazioni sul funzionamento di reCAPTCHA, consulta [Google reCAPTCHA](https://developers.google.com/recaptcha/). Il servizio reCAPTCHA, che include reCAPTCHA v2 e reCAPTCHA Enterprise, è integrato in AEM Forms. In base alle tue esigenze puoi configurare il servizio reCAPTCHA per abilitare:

* [reCAPTCHA Enterprise in AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 in AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)

![reCAPTCHA](/help/forms/using/assets/recaptcha_new.png)

### Configurare reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Creare un [Progetto reCAPTCHA Enterprise](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) abilitato con [API di reCAPTCHA Enterprise](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. [Ottenere](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) l’ID del progetto.
1. Creare un [Chiave API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) e un [chiave del sito per i siti web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Crea un contenitore di configurazione per i servizi cloud.

   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**. Consulta la [Browser configurazioni](/help/sites-administering/configurations.md) per ulteriori informazioni.
   1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud oppure ignora questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.
      1. Nel browser configurazioni, seleziona la **[!UICONTROL globale]** cartella e tocca **[!UICONTROL Proprietà]**.
      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

   1. Nel browser configurazioni, tocca **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione, specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
   1. Tocca **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.
1. Configura il servizio cloud per reCAPTCHA Enterprise.

   1. Nell’istanza Autore dell’Experience Manager, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. Tocca **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Seleziona il contenitore di configurazione creato nel passaggio precedente e tocca **[!UICONTROL Crea]**.
   1. Seleziona la versione come Enterprise reCAPTCHA e specifica Nome; ID progetto, Chiave sito e Chiave API (ottenuta nei passaggi 2 e 3) per il servizio Enterprise reCAPTCHA.
   1. Seleziona il tipo di chiave; il tipo di chiave deve essere lo stesso della chiave del sito configurata nel progetto cloud Google, ad esempio, **Casella di selezione chiave sito** o **Chiave del sito basata su punteggio**.
   1. Specifica un punteggio di soglia compreso tra 0 e 1 ([Fai clic per ulteriori informazioni sul punteggio](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores)). I punteggi superiori o uguali ai punteggi di soglia identificano l’interazione umana, altrimenti considerata interazione da bot.

      > Nota:
      >
      > * Gli autori dei moduli possono specificare un punteggio nell’intervallo idoneo per l’invio ininterrotto di moduli.

   1. Tocca **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.

   1. Nella finestra di dialogo Modifica componente, specifica il nome, l’ID progetto, la chiave del sito e la chiave API (ottenuta nei passaggi 2 e 3), seleziona il tipo di chiave e immetti il punteggio di soglia. Tocca **[!UICONTROL Salva impostazioni]** e quindi tocca **[!UICONTROL OK]** per completare la configurazione.

Una volta abilitato, il servizio reCAPTCHA Enterprise è disponibile per l’utilizzo in moduli adattivi. Consulta [utilizzo del CAPTCHA nei moduli adattivi](#using-reCAPTCHA).

![reCAPTCHA Enterprise](/help/forms/using/assets/recaptcha1-enterprise.png)


### Configurare Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Ottenere [coppia di chiavi API reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Include un **chiave del sito** e un **chiave segreta**.
1. Crea un contenitore di configurazione per i servizi cloud.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**. Consulta la [Browser configurazioni](/help/sites-administering/configurations.md) per ulteriori informazioni.
   1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud oppure ignora questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

      1. Nel browser configurazioni, seleziona la **[!UICONTROL globale]** cartella e tocca **[!UICONTROL Proprietà]**.

      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

   1. Nel browser configurazioni, tocca **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione, specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
   1. Tocca **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

1. Configura il servizio cloud per reCAPTCHA v2.

   1. Nell’istanza di authoring dell’AEM, vai a ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Tocca **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Seleziona il contenitore di configurazione creato nel passaggio precedente e tocca **[!UICONTROL Crea]**.
   1. Seleziona la versione come reCAPTCHA v2, specifica Nome, Chiave sito e Chiave segreta per il servizio reCAPTCHA (ottenuti nel passaggio 1) e tocca **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.
   1. Nella finestra di dialogo Modifica componente, specifica il sito e le chiavi segrete ottenuti nel passaggio 1. Tocca **[!UICONTROL Salva impostazioni]** e quindi tocca **OK** per completare la configurazione.

   Una volta configurato, il servizio reCAPTCHA è disponibile per l’utilizzo nei moduli adattivi. Per ulteriori informazioni, consulta [utilizzo del CAPTCHA nei moduli adattivi](#using-captcha).

![reCAPTCHA v2](/help/forms/using/assets/recaptcha-v2.png)


## Utilizzare reCAPTCHA nei moduli adattivi {#using-reCAPTCHA}

Per utilizzare reCAPTCHA nei moduli adattivi:

1. Apri un modulo adattivo in modalità di modifica.

   >[!NOTE]
   >
   >Assicurati che il contenitore di configurazione selezionato durante la creazione del modulo adattivo contenga il servizio cloud reCAPTCHA. Puoi anche modificare le proprietà dei moduli adattivi per cambiare il contenitore di configurazione associato al modulo.

1. Dal browser Componenti, trascina **Captcha** nel modulo adattivo.

   >[!NOTE]
   >
   >L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il CAPTCHA in un pannello contrassegnato per il caricamento lento o in un frammento.

   >[!NOTE]
   >
   >Il Captcha è sensibile al tempo e scade tra circa un minuto. Pertanto, si consiglia di inserire il componente Captcha subito prima del pulsante Invia nel modulo adattivo.

1. Seleziona il componente Captcha aggiunto e tocca ![cmppr](assets/cmppr.png) per modificarne le proprietà.
1. Specificate un titolo per il widget CAPTCHA. Il valore predefinito è **Captcha**. Seleziona **Nascondi titolo** se non desideri che il titolo venga visualizzato.
1. Dalla sezione **Servizio Captcha** a discesa, seleziona **reCAPTCHA** per abilitare il servizio reCAPTCHA se è stato configurato come descritto in [Servizio reCAPTCHA di Google](#google-reCAPTCHA).
1. Seleziona una configurazione dal menu a discesa Impostazioni.
1. **Se la configurazione selezionata dispone della versione reCAPTCHA Enterprise**:
   1. Puoi selezionare la configurazione cloud reCAPTCHA con **tipo di chiave** as **casella di controllo**. In tasto casella di controllo, digita il messaggio di errore personalizzato come messaggio in linea se la convalida captcha non riesce. È possibile selezionare le dimensioni come **[!UICONTROL Normale]** e **[!UICONTROL Compatto]**.
   1. Puoi selezionare la configurazione cloud reCAPTCHA con **tipo di chiave** as **basato su punteggio**. In chiave basata su punteggio, il messaggio di errore personalizzato viene visualizzato come messaggio a comparsa se la convalida captcha non riesce.
   1. Quando selezioni un **[!UICONTROL Riferimento binding]** i dati inviati sono dati associati, altrimenti si tratta di dati non associati. Di seguito sono riportati alcuni esempi XML di dati non associati e dati associati (con riferimento di associazione come SSN) rispettivamente, quando un modulo viene inviato.

      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data>
                  <captcha16820607953761>
                      <captchaType>reCAPTCHAEnterprise</captchaType>
                      <captchaScore>0.9</captchaScore>
                  </captcha16820607953761>
              </data>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>371237912</SSN>
                      <FirstName>Sarah </FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608034928</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data/>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>
                          <captchaType>reCAPTCHAEnterprise</captchaType>
                          <captchaScore>0.9</captchaScore>
                      </SSN>
                      <FirstName>Sarah</FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608035111</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


   **Se la configurazione selezionata dispone della versione reCAPTCHA v2**:
   1. Seleziona la dimensione come **[!UICONTROL Normale]** o **[!UICONTROL Compatto]** per il widget reCAPTCHA. È inoltre possibile selezionare **[!UICONTROL Invisibile]** per mostrare la richiesta CAPTCHA solo nel caso di attività sospetta. Il **protetto da reCAPTCHA** nei moduli protetti viene visualizzato il contrassegno riportato di seguito.

      ![Google protetto da badge reCAPTCHA](/help/forms/using/assets/google-recaptcha-v2.png)


   Il servizio reCAPTCHA è abilitato nel modulo adattivo. Puoi visualizzare l’anteprima del modulo e vedere il CAPTCHA che funziona.

1. Salva le proprietà.

>[!NOTE]
> 
> Non selezionare **[!UICONTROL Predefinito]** dall’elenco a discesa del servizio Captcha poiché il servizio AEM CAPTCHA predefinito è obsoleto.

### Mostrare o nascondere il componente CAPTCHA in base alle regole {#show-hide-captcha}

Puoi scegliere di mostrare o nascondere il componente CAPTCHA in base alle regole applicate a un componente in un modulo adattivo. Tocca il componente, seleziona ![modifica regole](assets/edit-rules-icon.svg), e tocca **[!UICONTROL Crea]** per creare una regola. Per ulteriori informazioni sulla creazione delle regole, consulta [Editor regole](rule-editor.md).

Ad esempio, il componente CAPTCHA deve essere visualizzato in un modulo adattivo solo se il campo Valore valuta nel modulo ha un valore superiore a 25000.

Tocca il **[!UICONTROL Valore valuta]** nel modulo e creare le regole seguenti:

![Mostra o nascondi regole](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> * Se selezioni reCAPTCHA v2 configuration with size as **[!UICONTROL Invisibile]** o le chiavi basate su punteggio Enterprise reCAPTCHA, l’opzione mostra/nascondi non è applicabile.

### Convalida CAPTCHA {#validate-captcha}

È possibile convalidare il CAPTCHA in un modulo adattivo quando si invia il modulo oppure basare la convalida CAPTCHA sulle azioni e condizioni dell’utente.

#### Convalida CAPTCHA all’invio del modulo {#validation-form-submission}

Per convalidare automaticamente un CAPTCHA quando si invia un modulo adattivo:

1. Tocca il componente CAPTCHA e seleziona ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. In **[!UICONTROL Convalida CAPTCHA]** sezione, seleziona **[!UICONTROL Convalida CAPTCHA all’invio del modulo]**.
1. Tocca ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

#### Convalida CAPTCHA per azioni e condizioni dell’utente {#validate-captcha-user-action}

Per convalidare un CAPTCHA in base a condizioni e azioni dell’utente:

1. Tocca il componente CAPTCHA e seleziona ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. In **[!UICONTROL Convalida CAPTCHA]** sezione, seleziona **[!UICONTROL Convalida CAPTCHA per azione dell’utente]**.
1. Tocca ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

   >[!NOTE]
   >
   >
   > Se selezioni reCAPTCHA v2 configuration with size as **[!UICONTROL Invisibile]** o le chiavi basate su punteggio Enterprise reCAPTCHA, non è possibile applicare un Captcha valido su un’azione utente.

[!DNL Experience Manager Forms] fornisce `ValidateCAPTCHA` API per convalidare CAPTCHA utilizzando condizioni predefinite. Puoi richiamare l’API utilizzando un’azione di invio personalizzata o definendo regole sui componenti in un modulo adattivo.

Di seguito è riportato un esempio di `ValidateCAPTCHA` API per convalidare CAPTCHA utilizzando condizioni predefinite:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
        GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

L&#39;esempio indica che `ValidateCAPTCHA` L’API convalida il CAPTCHA nel modulo solo se il numero di cifre nella casella numerica specificata dall’utente durante la compilazione del modulo è maggiore di 5.

**Opzione 1: utilizzo [!DNL Experience Manager Forms] API ValidateCAPTCHA per convalidare CAPTCHA tramite un’azione di invio personalizzata**

Per utilizzare il `ValidateCAPTCHA` API per convalidare CAPTCHA tramite un’azione di invio personalizzata:

1. Aggiungi lo script che include `ValidateCAPTCHA` API per personalizzare l’azione di invio. Per ulteriori informazioni sulle azioni di invio personalizzate, consulta [Creare un’azione di invio personalizzata per Adaptive Forms](custom-submit-action-form.md).
1. Selezionare il nome dell&#39;azione di invio personalizzata dalla **[!UICONTROL Azione di invio]** elenco a discesa in **[!UICONTROL Invio]** proprietà di un modulo adattivo.
1. Tocca **[!UICONTROL Invia]**. Il CAPTCHA viene convalidato in base alle condizioni definite in `ValidateCAPTCHA` API dell’azione di invio personalizzata.

**Opzione 2: utilizzo [!DNL Experience Manager Forms] API ValidateCAPTCHA per convalidare CAPTCHA su un’azione utente prima di inviare il modulo**

Puoi anche richiamare `ValidateCAPTCHA` tramite l’applicazione di regole su un componente in un modulo adattivo.

Ad esempio, puoi aggiungere un’ **[!UICONTROL Convalida CAPTCHA]** in un modulo adattivo e crea una regola per richiamare un servizio facendo clic su un pulsante.

Nella figura seguente viene illustrato come richiamare un servizio facendo clic su un **[!UICONTROL Convalida CAPTCHA]** pulsante:

![Convalida CAPTCHA](assets/captcha-validation1.gif)

Puoi richiamare il servlet personalizzato che include `ValidateCAPTCHA` tramite l’editor di regole e abilita o disabilita il pulsante di invio del modulo adattivo in base al risultato della convalida.

Allo stesso modo, puoi utilizzare l’editor di regole per includere un metodo personalizzato per convalidare il CAPTCHA in un modulo adattivo.

### Aggiungere servizi CAPTCHA personalizzati {#add-custom-captcha-service}

[!DNL Experience Manager Forms] fornisce reCAPTCHA come servizio CAPTCHA. Tuttavia, puoi aggiungere un servizio personalizzato da visualizzare nel **[!UICONTROL Servizio CAPTCHA]** elenco a discesa.

Di seguito è riportato un esempio di implementazione dell’interfaccia per aggiungere un servizio CAPTCHA aggiuntivo al modulo adattivo:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` Fa riferimento al percorso della risorsa del componente CAPTCHA nell’archivio Sling. Utilizzare questa proprietà per includere dettagli specifici del componente CAPTCHA. Ad esempio: `captchaPropertyNodePath` include informazioni sulla configurazione cloud reCAPTCHA configurata sul componente CAPTCHA. Le informazioni sulla configurazione cloud forniscono **[!UICONTROL Chiave sito]** e **[!UICONTROL Chiave segreta]** impostazioni per l’implementazione del servizio reCAPTCHA.

`userResponseToken` Si riferisce al `g_reCAPTCHA_response` che viene generato dopo la risoluzione di un CAPTCHA in un modulo.
