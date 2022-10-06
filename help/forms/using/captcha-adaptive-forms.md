---
title: Uso del CAPTCHA nei moduli adattivi
seo-title: Using CAPTCHA in adaptive forms
description: Scopri come configurare AEM servizio CAPTCHA o Google reCAPTCHA nei moduli adattivi.
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in adaptive forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Adaptive Forms
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 0%

---

# Uso del CAPTCHA nei moduli adattivi{#using-captcha-in-adaptive-forms}

CAPTCHA (Test di Turing Pubblico Completamente Automatizzato per dire Computer e Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra umani e programmi automatizzati o bot. Rappresenta una sfida e valuta la risposta dell&#39;utente per determinare se si tratta di un essere umano o un bot che interagisce con il sito. Impedisce all&#39;utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o scopi dannosi.

AEM Forms supporta il CAPTCHA nei moduli adattivi. Puoi utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA.

>[!NOTE]
>
>* AEM Forms supporta solo reCaptcha v2. Qualsiasi altra versione non è supportata.
>* Il CAPTCHA nei moduli adattivi non è supportato in modalità offline nell’app AEM Forms.
>


## Configurare il servizio ReCAPTCHA da Google {#google-recaptcha}

Gli autori di moduli possono utilizzare il servizio reCAPTCHA di Google per implementare il CAPTCHA nei moduli adattivi. Offre funzionalità CAPTCHA avanzate per proteggere il tuo sito. Per ulteriori informazioni sul funzionamento di reCAPTCHA, consulta [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

Per implementare il servizio reCAPTCHA in AEM Forms:

1. Recuperare [Coppia di chiavi API reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Include una chiave del sito e un segreto.
1. Crea un contenitore di configurazione per i servizi cloud.

   1. Vai a **[!UICONTROL Strumenti > Generale > Browser di configurazione]**.
      * Consulta la sezione [Browser di configurazione](/help/sites-administering/configurations.md) documentazione per ulteriori informazioni.
   1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud o salta questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

      1. Nel browser di configurazione, seleziona la **[!UICONTROL globale]** tocca e fai clic su **[!UICONTROL Proprietà]**.

      1. Nella finestra di dialogo Proprietà configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.
   1. Nel browser di configurazione, tocca **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione , specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
   1. Tocca **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.


1. Configura il servizio cloud per reCAPTCHA.

   1. Nell’istanza di authoring di AEM, vai a ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Tocca **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni . Seleziona il contenitore di configurazione creato nel passaggio precedente e tocca **[!UICONTROL Crea]**.
   1. Specifica nome, chiave del sito e chiave segreta per il servizio reCAPTCHA e tocca **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.
   1. Nella finestra di dialogo Modifica componente , specifica il sito e le chiavi segrete ottenute nel passaggio 1. Tocca **Salva impostazioni** quindi tocca **OK** per completare la configurazione.

   Una volta configurato il servizio reCAPTCHA, è disponibile per l’uso nei moduli adattivi. Per ulteriori informazioni, consulta [Uso del CAPTCHA nei moduli adattivi](#using-captcha).

## Utilizzare il CAPTCHA nei moduli adattivi {#using-captcha}

Per utilizzare il CAPTCHA nei moduli adattivi:

1. Apri un modulo adattivo in modalità di modifica.

   >[!NOTE]
   >
   >Assicurati che il contenitore di configurazione selezionato durante la creazione del modulo adattivo contenga il servizio cloud reCAPTCHA. È inoltre possibile modificare le proprietà del modulo adattivo per modificare il contenitore di configurazione associato al modulo.

1. Dal browser Componenti, trascina la **Captcha** nel modulo adattivo.

   >[!NOTE]
   >
   >L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il CAPTCHA in un pannello contrassegnato per il caricamento lento o in un frammento.

   >[!NOTE]
   >
   >Captcha è sensibile al tempo e scade tra circa un minuto. Pertanto, si consiglia di posizionare il componente Captcha immediatamente prima del pulsante Invia nel modulo adattivo.

1. Seleziona il componente Captcha aggiunto e tocca ![cmppr](assets/cmppr.png) per modificarne le proprietà.
1. Specifica un titolo per il widget CAPTCHA. Il valore predefinito è **Captcha**. Seleziona **Nascondi titolo** se non si desidera che il titolo venga visualizzato.
1. Da **Servizio Captcha** a discesa, seleziona **reCaptcha** per abilitare il servizio reCAPTCHA se lo hai configurato come descritto in [Servizio ReCAPTCHA di Google](#google-recaptcha). Seleziona una configurazione dal menu a discesa Impostazioni . Inoltre, seleziona la dimensione come **Normale** o **Compatto** per il widget reCAPTCHA.

   >[!NOTE]
   >
   >Non selezionare **[!UICONTROL Predefinito]** dal menu a discesa del servizio Captcha , poiché il servizio AEM CAPTCHA predefinito è obsoleto.

1. Salva le proprietà.

Il servizio reCAPTCHA è abilitato nel modulo adattivo. Puoi visualizzare l’anteprima del modulo e vedere come funziona il CAPTCHA.

### Mostra o nasconde il componente CAPTCHA in base alle regole {#show-hide-captcha}

Puoi selezionare di mostrare o nascondere il componente CAPTCHA in base alle regole applicate a un componente in un modulo adattivo. Tocca il componente, seleziona ![modifica regole](assets/edit-rules-icon.svg), e tocca **[!UICONTROL Crea]** per creare una regola. Per ulteriori informazioni sulla creazione delle regole, consulta [Editor regole](rule-editor.md).

Ad esempio, il componente CAPTCHA deve essere visualizzato in un Modulo adattivo solo se il campo Valore valuta del modulo ha un valore superiore a 25000.

Tocca **[!UICONTROL Valore valuta]** nel modulo e creare le regole seguenti:

![Mostrare o nascondere le regole](assets/rules-show-hide-captcha.png)

### Convalida CAPTCHA {#validate-captcha}

È possibile convalidare il CAPTCHA in un modulo adattivo sia quando si invia il modulo sia basando la convalida CAPTCHA sulle azioni e condizioni dell’utente.

#### Convalida CAPTCHA durante l’invio del modulo {#validation-form-submission}

Per convalidare automaticamente un CAPTCHA quando si invia un modulo adattivo:

1. Tocca il componente CAPTCHA e seleziona ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. In **[!UICONTROL Convalida CAPTCHA]** sezione , seleziona **[!UICONTROL Convalida CAPTCHA all’invio del modulo]**.
1. Tocca ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

#### Convalida CAPTCHA sulle azioni e condizioni dell’utente {#validate-captcha-user-action}

Per convalidare un CAPTCHA in base a condizioni e azioni dell’utente:

1. Tocca il componente CAPTCHA e seleziona ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. In **[!UICONTROL Convalida CAPTCHA]** sezione , seleziona **[!UICONTROL Convalida CAPTCHA in un’azione dell’utente]**.
1. Tocca ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

[!DNL Experience Manager Forms] fornisce `ValidateCAPTCHA` API per convalidare CAPTCHA utilizzando condizioni predefinite. Puoi richiamare l’API utilizzando un’azione di invio personalizzata o definendo le regole sui componenti in un modulo adattivo.

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

L’esempio indica che il `ValidateCAPTCHA` L’API convalida il CAPTCHA nel modulo solo se il numero di cifre nella casella numerica specificata dall’utente durante la compilazione del modulo è maggiore di 5.

**Opzione 1: Utilizzo [!DNL Experience Manager Forms] API ValidateCAPTCHA per convalidare CAPTCHA utilizzando un’azione di invio personalizzata**

Esegui i seguenti passaggi per utilizzare il `ValidateCAPTCHA` API per convalidare CAPTCHA utilizzando un’azione di invio personalizzata:

1. Aggiungi lo script che include `ValidateCAPTCHA` API per l’azione di invio personalizzata. Per ulteriori informazioni sulle azioni di invio personalizzate, consulta [Creare un’azione di invio personalizzata per Adaptive Forms](custom-submit-action-form.md).
1. Seleziona il nome dell’azione di invio personalizzata dal menu **[!UICONTROL Invia azione]** elenco a discesa in **[!UICONTROL Invio]** proprietà di un modulo adattivo.
1. Tocca **[!UICONTROL Invia]**. Il CAPTCHA viene convalidato in base alle condizioni definite in `ValidateCAPTCHA` API dell’azione di invio personalizzata.

**Opzione 2: Utilizzo [!DNL Experience Manager Forms] API ValidateCAPTCHA per convalidare il CAPTCHA in un’azione dell’utente prima di inviare il modulo**

Puoi anche richiamare `ValidateCAPTCHA` Applicando regole su un componente in un modulo adattivo.

Ad esempio, aggiungi un **[!UICONTROL Convalida CAPTCHA]** in un modulo adattivo e crea una regola per richiamare un servizio facendo clic su un pulsante.

La figura seguente illustra come richiamare un servizio al clic di un **[!UICONTROL Convalida CAPTCHA]** pulsante:

![Convalida CAPTCHA](assets/captcha-validation1.gif)

Puoi richiamare il servlet personalizzato che include `ValidateCAPTCHA` API utilizzando l’editor di regole e abilitare o disabilitare il pulsante di invio del modulo adattivo in base al risultato della convalida.

Allo stesso modo, puoi utilizzare l’editor di regole per includere un metodo personalizzato per convalidare il CAPTCHA in un modulo adattivo.

### Aggiungi servizi CAPTCHA personalizzati {#add-custom-captcha-service}

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

`captchaPropertyNodePath` si riferisce al percorso della risorsa del componente CAPTCHA nell’archivio Sling. Utilizzare questa proprietà per includere dettagli specifici del componente CAPTCHA. Ad esempio: `captchaPropertyNodePath` include informazioni per la configurazione cloud reCAPTCHA configurata sul componente CAPTCHA. Le informazioni sulla configurazione cloud forniscono **[!UICONTROL Chiave del sito]** e **[!UICONTROL Chiave segreta]** impostazioni per l&#39;implementazione del servizio reCAPTCHA.

`userResponseToken` si riferisce al `g_recaptcha_response` che viene generato dopo la risoluzione di un CAPTCHA in un modulo.
