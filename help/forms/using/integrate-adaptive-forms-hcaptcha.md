---
title: Come si utilizza hCaptcha&reg; in un Forms AEM 6.5?
description: Migliora la sicurezza dei moduli con il servizio hCaptcha&reg; senza sforzo. Guida dettagliata all’interno!
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: 6aa7a0a5-bd45-4628-abd0-312a9e6cf6fe
source-git-commit: 96e6705349fc6969ab0c40c8c770c9a0d1967619
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 19%

---

# Connetti il tuo ambiente AEM Forms con hCaptcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview">Questa funzionalità è basata sull&#39;ID attivazione/disattivazione funzionalità `FT_FORMS-12407`. Per attivare la funzionalità, seguire i passaggi indicati nell&#39;articolo [Attiva/disattiva funzionalità](/help/forms/using/enable-feature-toggle.md). </span>


Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o avere scopi dannosi.

Oltre a hCaptcha®, AEM Forms 6.5 supporta le seguenti soluzioni CAPTCHA:

* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [Tornello Cloudflare](/help/forms/using/integrate-adaptive-forms-turnstile.md)

## Integrare l’ambiente AEM Forms con hCaptcha®

Il servizio hCaptcha® protegge i moduli da bot, spam e abusi automatizzati. Pone una sfida in un widget casella di controllo e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il modulo. Questo impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o praticare attività dannose.

Supporto hCaptcha&amp;reg per Forms adattivo AEM 6.5. Puoi utilizzarlo per presentare una richiesta di verifica del widget casella di controllo all’invio del modulo.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### Prerequisiti per integrare l’ambiente AEM Forms con hCaptcha® {#prerequisite}

Per configurare hCaptcha® con AEM Forms, è necessario ottenere la chiave del sito [hCaptcha® e la chiave segreta](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) dal sito Web hCaptcha®.

### Configurare hCaptcha® {#steps-to-configure-hcaptcha}

Per integrare AEM Forms con il servizio hCaptcha®, effettua le seguenti operazioni:

1. Crea un Contenitore di configurazione nell’ambiente AEM Forms, che contiene le configurazioni cloud utilizzate per collegare l’AEM a servizi esterni. Per creare un contenitore di configurazione:
   1. Apri il tuo ambiente AEM Forms.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Nel Browser configurazioni, puoi selezionare una cartella esistente o crearne una nuova:
      * Per creare una nuova cartella e abilitare le configurazioni cloud:
         1. Nel browser configurazioni fare clic su **[!UICONTROL Crea]**.
         1. Nella finestra di dialogo Crea configurazione, specifica un nome, un titolo e seleziona **[!UICONTROL Configurazioni cloud]**.
         1. Fai clic su **[!UICONTROL Crea]**.
      * Per abilitare la configurazione cloud per una cartella esistente:
         1. Nel Browser configurazioni, selezionare la cartella e selezionare **[!UICONTROL Proprietà]**.
         1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
         1. Fai clic su **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configurare i Cloud Service:
   1. Nell&#39;istanza dell&#39;autore AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e fai clic su **[!UICONTROL hCaptcha®]**.
      ![hCaptcha® nell&#39;interfaccia utente](assets/hcaptcha-in-ui.png)
   1. Seleziona un Contenitore di configurazione, creato o aggiornato, come descritto nella sezione precedente. Seleziona **[!UICONTROL Crea]**.
      ![Configurazione hCaptcha®](assets/config-hcaptcha.png)
   1. Specifica **[!UICONTROL Titolo]**, <!--**[!UICONTROL Name]**--> **[!UICONTROL Chiave sito]** e **[!UICONTROL Chiave segreta]** per il servizio hCaptcha® [ottenuti nel prerequisito](#prerequisite).
   1. Fai clic su **[!UICONTROL Crea]**.

      ![Configura il Cloud Service per connettere il tuo ambiente AEM Forms con hCaptcha®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > Gli utenti non devono modificare [URL di convalida JavaScript lato client](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) e [URL di convalida lato server](https://docs.hcaptcha.com/#verify-the-user-response-server-side) in quanto sono già precompilati per la convalida hCaptcha®.

   Una volta configurato, il servizio hCAPTCHA è disponibile per l’utilizzo nel modulo adattivo.

## Utilizzare hCaptcha® in un Forms adattivo {#using-hCaptcha-in-aem-6.5}

1. Apri il tuo ambiente AEM Forms.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Selezionare un modulo adattivo e fare clic su **[!UICONTROL Proprietà]**.
1. Nel **[!UICONTROL Contenitore configurazione]**, seleziona la configurazione cloud per hCaptcha®.
1. Fai clic su **[!UICONTROL Salva e chiudi]**.

   Se non disponi di un contenitore di configurazione per hCaptcha, consulta la sezione [Connettere l&#39;ambiente AEM Forms con hCaptcha®](#configure-hcaptcha-steps-to-configure-hcaptcha) per scoprire come creare un contenitore di configurazione.

   ![Seleziona contenitore configurazione](/help/forms/using/assets/captcha-properties.png)

1. Seleziona un modulo adattivo e fai clic su **[!UICONTROL Modifica]** per aprire il modulo nell&#39;editor.
1. Dal browser componenti, trascina il componente **[!UICONTROL Captcha]** nel modulo adattivo.
1. Selezionare il componente **[!UICONTROL Captcha]** e fare clic su proprietà ![icona Proprietà](assets/configure-icon.svg) per aprire la finestra di dialogo delle proprietà. Specifica le seguenti proprietà:

   ![hCaptcha® v1](assets/config-hcaptcha-v1-img.png)

   * **[!UICONTROL Titolo]:** Specifica il titolo del componente Captcha.
   * **[!UICONTROL Messaggio di convalida]:** Fornisci un messaggio di convalida per la convalida Captcha all&#39;invio del modulo o a un&#39;azione dell&#39;utente.
   * **[!UICONTROL Servizio Captcha]:** Seleziona il servizio CAPTCHA per l&#39;invio del modulo, qui selezioni hCaptcha®.
   * **[!UICONTROL Impostazioni di configurazione]:** Seleziona la configurazione cloud configurata per hCaptcha®.
     >[!NOTE]
     >Puoi avere più configurazioni cloud nell’ambiente per uno scopo simile. Quindi, scegli il servizio con attenzione. Se non è elencato alcun servizio, consulta [Connettere l&#39;ambiente AEM Forms con hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) per scoprire come creare un Cloud Service che colleghi l&#39;ambiente AEM Forms al servizio hCaptcha®.

   * **[!UICONTROL Messaggio di errore]:** Fornisci il messaggio di errore da visualizzare all&#39;utente quando l&#39;invio Captcha non riesce.
   * **[!UICONTROL Dimensione captcha]:** È possibile selezionare la dimensione di visualizzazione della finestra di dialogo della richiesta di verifica hCaptcha®. Utilizza l&#39;opzione **[!UICONTROL Compact]** per visualizzare una finestra di dialogo di verifica hCaptcha® di piccole dimensioni e **[!UICONTROL Normal]** per visualizzare una finestra di dialogo di verifica hCaptcha di dimensioni relativamente grandi oppure **[!UICONTROL Invisible]** per convalidare hCaptcha® senza eseguire il rendering esplicito del widget della casella di controllo nell&#39;interfaccia utente.

1. Seleziona **[!UICONTROL Fine]**.


Ora, solo i moduli legittimi, in cui il compilatore di moduli elimina con successo la sfida posta dal servizio hCaptcha® sono consentiti per l’invio del modulo.

**hCaptcha® è un marchio registrato di Intuition Machines, Inc.**


## Domande frequenti

* **Q: posso utilizzare più di un componente Captcha in un modulo adattivo?**
* **Ans:** L&#39;utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare un componente Captcha in un frammento o in un pannello contrassegnato per il caricamento lento.

## Consulta anche {#see-also}

* [Utilizzo del CAPTCHA nei moduli adattivi](/help/forms/using/captcha-adaptive-forms.md)
* [Utilizzo di Turnstile Captcha nei moduli adattivi](/help/forms/using/integrate-adaptive-forms-turnstile.md)
