---
title: Uso del CAPTCHA nei moduli adattivi
seo-title: Uso del CAPTCHA nei moduli adattivi
description: Scoprite come configurare AEM servizio CAPTCHA o Google reCAPTCHA nei moduli adattivi.
seo-description: Scoprite come configurare AEM servizio CAPTCHA o Google reCAPTCHA nei moduli adattivi.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---


# Uso del CAPTCHA nei moduli adattivi{#using-captcha-in-adaptive-forms}

CAPTCHA (Test di Turing Pubblico Completamente Automatizzato per dire Computer e Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra gli umani e i programmi o robot automatizzati. Rappresenta una sfida e valuta la risposta degli utenti per determinare se si tratta di un essere umano o un bot che interagisce con il sito. Impedisce all&#39;utente di procedere in caso di esito negativo del test e contribuisce a rendere sicure le transazioni online, impedendo ai bot di inviare spam o scopi dannosi.

 AEM Forms supporta il CAPTCHA nei moduli adattivi. Potete utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA.

>[!NOTE]
>
>*  AEM Forms supporta solo reCaptcha v2. Qualsiasi altra versione non è supportata.
>* CAPTCHA nei moduli adattivi non è supportato in modalità offline nell&#39;app  AEM Forms.

>



## Configurare il servizio ReCAPTCHA da Google {#google-recaptcha}

Gli autori dei moduli possono utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA nei moduli adattivi. Offre funzionalità CAPTCHA avanzate per proteggere il sito. Per ulteriori informazioni sul funzionamento di reCAPTCHA, consultate [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

Per implementare il servizio reCAPTCHA in  AEM Forms:

1. Ottenete una coppia [di chiavi API](https://www.google.com/recaptcha/admin) reCAPTCHA da Google. Include una chiave del sito e un segreto.
1. Creare un contenitore di configurazione per i servizi cloud.

   1. Go to **[!UICONTROL Tools > General > Configuration Browser]**.
      * See the [Configuration Browser](/help/sites-administering/configurations.md) documentation for more information.
   1. Effettuate le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud o saltate questo passaggio per creare e configurare un&#39;altra cartella per le configurazioni del servizio cloud.

      1. Nel browser di configurazione, selezionate la cartella **[!UICONTROL globale]** e toccate **[!UICONTROL Proprietà]**.

      1. Nella finestra di dialogo Proprietà configurazione, abilita Configurazioni **[!UICONTROL Cloud]**.
      1. Toccate **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.
   1. Nel browser di configurazione, toccate **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione, specificate un titolo per la cartella e abilitate **[!UICONTROL Cloud Configurations]**.
   1. Toccate **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.


1. Configurare il servizio cloud per reCAPTCHA.

   1. Nell’istanza di AEM authoring, andate a ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Toccate **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Selezionate il contenitore di configurazione creato nel passaggio precedente e toccate **[!UICONTROL Crea]**.
   1. Specificate Nome, Chiave del sito e Chiave segreta per il servizio reCAPTCHA e toccate **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.
   1. Nella finestra di dialogo Modifica componente, specificate il sito e le chiavi segrete ottenute al punto 1. Toccate **Salva impostazioni** , quindi toccate **OK** per completare la configurazione.

   Una volta configurato, il servizio reCAPTCHA è disponibile per l&#39;uso nei moduli adattivi. Per ulteriori informazioni, vedere [Uso di CAPTCHA nei moduli](#using-captcha)adattivi.

## Uso del CAPTCHA nei moduli adattivi {#using-captcha}

Per utilizzare CAPTCHA nei moduli adattivi:

1. Aprire un modulo adattivo in modalità di modifica.

   >[!NOTE]
   >
   >Verificare che il contenitore di configurazione selezionato al momento della creazione del modulo adattivo contenga il servizio cloud reCAPTCHA. È inoltre possibile modificare le proprietà del modulo adattivo per modificare il contenitore di configurazione associato al modulo.

1. Dal Browser componenti, trascinate il componente **Captcha** nel modulo adattivo.

   >[!NOTE]
   >
   >L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, non è consigliabile utilizzare CAPTCHA in un pannello contrassegnato per il caricamento pigro o in un frammento.

   >[!NOTE]
   >
   >Captcha è sensibile al tempo e scade tra circa un minuto. Pertanto, si consiglia di posizionare il componente Captcha subito prima del pulsante Invia nel modulo adattivo.

1. Selezionate il componente Captcha aggiunto e toccate ![cmppr](assets/cmppr.png) per modificarne le proprietà.
1. Specificate un titolo per il widget CAPTCHA. The default value is **Captcha**. Selezionate **Nascondi titolo** se non desiderate che il titolo venga visualizzato.
1. Dal menu a discesa del servizio **** Captcha, selezionate **reCaptcha** per abilitare il servizio reCAPTCHA se lo avete configurato come descritto nel servizio [ReCAPTCHA di Google](#google-recaptcha). Selezionate una configurazione dal menu a discesa Impostazioni. Selezionate inoltre la dimensione **Normale** o **Compatta** per il widget reCAPTCHA.

   >[!NOTE]
   >
   >Non selezionate **[!UICONTROL Predefinito]** dal menu a discesa del servizio Captcha perché il servizio AEM CAPTCHA predefinito è obsoleto.

1. Salvare le proprietà.

Il servizio reCAPTCHA è attivato nel modulo adattivo. È possibile visualizzare l&#39;anteprima del modulo e vedere il funzionamento di CAPTCHA.
