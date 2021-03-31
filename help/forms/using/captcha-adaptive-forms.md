---
title: Uso del CAPTCHA nei moduli adattivi
seo-title: Uso del CAPTCHA nei moduli adattivi
description: Scopri come configurare AEM servizio CAPTCHA o Google reCAPTCHA nei moduli adattivi.
seo-description: Scopri come configurare AEM servizio CAPTCHA o Google reCAPTCHA nei moduli adattivi.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Moduli adattivi
translation-type: tm+mt
source-git-commit: 7a3f54d90769708344e6751756b2a12ac6c962d7
workflow-type: tm+mt
source-wordcount: '1291'
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

1. Ottenere [la coppia di chiavi API reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Include una chiave del sito e un segreto.
1. Crea un contenitore di configurazione per i servizi cloud.

   1. Vai a **[!UICONTROL Strumenti > Generale > Browser di configurazione]**.
      * Per ulteriori informazioni, consulta la documentazione [Browser configurazioni](/help/sites-administering/configurations.md) .
   1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud o salta questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

      1. Nel Browser configurazioni, seleziona la cartella **[!UICONTROL global]** e tocca **[!UICONTROL Properties]**.

      1. Nella finestra di dialogo Proprietà configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.
   1. Nel Browser configurazioni, tocca **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione , specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
   1. Tocca **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.


1. Configura il servizio cloud per reCAPTCHA.

   1. Sull&#39;istanza di authoring di AEM, vai a ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Tocca **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni . Seleziona il contenitore di configurazione creato nel passaggio precedente e tocca **[!UICONTROL Crea]**.
   1. Specifica nome, chiave del sito e chiave segreta per il servizio reCAPTCHA e tocca **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.
   1. Nella finestra di dialogo Modifica componente , specifica il sito e le chiavi segrete ottenute nel passaggio 1. Tocca **Salva impostazioni**, quindi tocca **OK** per completare la configurazione.

   Una volta configurato il servizio reCAPTCHA, è disponibile per l’uso nei moduli adattivi. Per ulteriori informazioni, consulta [Uso del CAPTCHA nei moduli adattivi](#using-captcha).

## Utilizzare il CAPTCHA nei moduli adattivi {#using-captcha}

Per utilizzare il CAPTCHA nei moduli adattivi:

1. Apri un modulo adattivo in modalità di modifica.

   >[!NOTE]
   >
   >Assicurati che il contenitore di configurazione selezionato durante la creazione del modulo adattivo contenga il servizio cloud reCAPTCHA. È inoltre possibile modificare le proprietà del modulo adattivo per modificare il contenitore di configurazione associato al modulo.

1. Dal browser Componenti, trascina il componente **Captcha** nel modulo adattivo.

   >[!NOTE]
   >
   >L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il CAPTCHA in un pannello contrassegnato per il caricamento lento o in un frammento.

   >[!NOTE]
   >
   >Captcha è sensibile al tempo e scade tra circa un minuto. Pertanto, si consiglia di posizionare il componente Captcha immediatamente prima del pulsante Invia nel modulo adattivo.

1. Seleziona il componente Captcha aggiunto e tocca ![cmppr](assets/cmppr.png) per modificarne le proprietà.
1. Specifica un titolo per il widget CAPTCHA. Il valore predefinito è **Captcha**. Selezionare **Nascondi titolo** se non si desidera che il titolo venga visualizzato.
1. Dal menu a discesa **Servizio Captcha** , seleziona **reCaptcha** per abilitare il servizio reCAPTCHA se lo hai configurato come descritto in [Servizio ReCAPTCHA di Google](#google-recaptcha). Seleziona una configurazione dal menu a discesa Impostazioni . Inoltre, seleziona la dimensione come **Normale** o **Compatta** per il widget reCAPTCHA.

   >[!NOTE]
   >
   >Non selezionare **[!UICONTROL Predefinito]** dal menu a discesa del servizio Captcha perché il servizio AEM CAPTCHA predefinito è obsoleto.

1. Salva le proprietà.

Il servizio reCAPTCHA è abilitato nel modulo adattivo. Puoi visualizzare l’anteprima del modulo e vedere come funziona il CAPTCHA.

### Mostra o nasconde il componente CAPTCHA in base alle regole {#show-hide-captcha}

Puoi selezionare di mostrare o nascondere il componente CAPTCHA in base alle regole applicate a un componente in un modulo adattivo. Tocca il componente, seleziona ![modifica regole](assets/edit-rules-icon.svg) e tocca **[!UICONTROL Crea]** per creare una regola. Per ulteriori informazioni sulla creazione delle regole, consulta [Editor regole](rule-editor.md).

Ad esempio, il componente CAPTCHA deve essere visualizzato in un Modulo adattivo solo se il campo Valore valuta del modulo ha un valore superiore a 25000.

Toccare il campo **[!UICONTROL Valore valuta]** nel modulo e creare le regole seguenti:

![Mostrare o nascondere le regole](assets/rules-show-hide-captcha.png)

### Convalida CAPTCHA {#validate-captcha}

È possibile convalidare il CAPTCHA in un modulo adattivo sia quando si invia il modulo sia basando la convalida CAPTCHA sulle azioni e condizioni dell’utente.

#### Convalida CAPTCHA all’invio del modulo {#validation-form-submission}

Per convalidare automaticamente un CAPTCHA quando si invia un modulo adattivo:

1. Tocca il componente CAPTCHA e seleziona ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. Nella sezione **[!UICONTROL Convalida CAPTCHA]**, selezionare **[!UICONTROL Convalida CAPTCHA all’invio del modulo]**.
1. Tocca ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

#### Convalida CAPTCHA sulle azioni e condizioni dell’utente {#validate-captcha-user-action}

Per convalidare un CAPTCHA in base a condizioni e azioni dell’utente:

1. Tocca il componente CAPTCHA e seleziona ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. Nella sezione **[!UICONTROL Convalida CAPTCHA]**, seleziona **[!UICONTROL Convalida CAPTCHA per un&#39;azione utente]**.
1. Tocca ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

[!DNL Experience Manager Forms] fornisce  `ValidateCAPTCHA` API per convalidare CAPTCHA utilizzando condizioni predefinite. Puoi richiamare l’API utilizzando un’azione di invio personalizzata o definendo le regole sui componenti in un modulo adattivo.

Di seguito è riportato un esempio di API `ValidateCAPTCHA` per convalidare CAPTCHA utilizzando condizioni predefinite:

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

L’esempio indica che l’API `ValidateCAPTCHA` convalida il CAPTCHA nel modulo solo se il numero di cifre nella casella numerica specificata dall’utente durante la compilazione del modulo è maggiore di 5.

**Opzione 1: Utilizza l’API  [!DNL Experience Manager Forms] ValidateCAPTCHA per convalidare i CAPTCHA utilizzando un’azione di invio personalizzata**

Esegui i seguenti passaggi per utilizzare l’API `ValidateCAPTCHA` per convalidare CAPTCHA utilizzando un’azione di invio personalizzata:

1. Aggiungi lo script che include l’ `ValidateCAPTCHA` API all’azione di invio personalizzata. Per ulteriori informazioni sulle azioni di invio personalizzate, consulta [Creare un’azione di invio personalizzata per Forms adattivo](custom-submit-action-form.md).
1. Selezionare il nome dell&#39;azione di invio personalizzata dall&#39;elenco a discesa **[!UICONTROL Invia azione]** nelle proprietà **[!UICONTROL Invio]** di un modulo adattivo.
1. Tocca **[!UICONTROL Invia]**. Il CAPTCHA viene convalidato in base alle condizioni definite in `ValidateCAPTCHA` API dell’azione di invio personalizzata.

**Opzione 2: Utilizza l’API  [!DNL Experience Manager Forms] ValidateCAPTCHA per convalidare il CAPTCHA in un’azione dell’utente prima di inviare il modulo**

Puoi anche richiamare l’ API `ValidateCAPTCHA` applicando regole su un componente in un modulo adattivo.

Ad esempio, è possibile aggiungere un pulsante **[!UICONTROL Convalida CAPTCHA]** in un modulo adattivo e creare una regola per richiamare un servizio facendo clic su un pulsante.

La figura seguente illustra come richiamare un servizio facendo clic su un pulsante **[!UICONTROL Convalida CAPTCHA]** :

![Convalida CAPTCHA](assets/captcha-validation1.gif)

Puoi richiamare il servlet personalizzato che include l’API `ValidateCAPTCHA` utilizzando l’editor di regole e abilitare o disabilitare il pulsante di invio del modulo adattivo in base al risultato della convalida.

Allo stesso modo, puoi utilizzare l’editor di regole per includere un metodo personalizzato per convalidare il CAPTCHA in un modulo adattivo.

### Aggiungi servizi CAPTCHA personalizzati {#add-custom-captcha-service}

[!DNL Experience Manager Forms] fornisce reCAPTCHA come servizio CAPTCHA. Tuttavia, puoi aggiungere un servizio personalizzato da visualizzare nell&#39;elenco a discesa **[!UICONTROL Servizio CAPTCHA]** .

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

`captchaPropertyNodePath` si riferisce al percorso della risorsa del componente CAPTCHA nell’archivio Sling. Utilizzare questa proprietà per includere dettagli specifici del componente CAPTCHA. Ad esempio, `captchaPropertyNodePath` include informazioni per la configurazione cloud reCAPTCHA configurata sul componente CAPTCHA. Le informazioni sulla configurazione cloud forniscono le impostazioni **[!UICONTROL Chiave del sito]** e **[!UICONTROL Chiave segreta]** per l&#39;implementazione del servizio reCAPTCHA.

`userResponseToken` si riferisce al  `g_recaptcha_response` che viene generato dopo la risoluzione di un CAPTCHA in un modulo.
