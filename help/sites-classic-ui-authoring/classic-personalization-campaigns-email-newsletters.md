---
title: Pubblicazione di un messaggio e-mail ai provider di servizi e-mail
description: È possibile pubblicare newsletter in servizi di posta elettronica quali ExactTarget e Silverpop Engage.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: c07692f7-3618-4e8c-96d7-4db09f2d9896
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 3%

---

# Pubblicazione di un messaggio e-mail ai provider di servizi e-mail{#publishing-an-email-to-email-service-providers}

È possibile pubblicare newsletter in servizi di posta elettronica quali ExactTarget e Silverpop Engage. In questo documento viene descritto come configurare AEM per la pubblicazione di una newsletter in questi servizi di posta elettronica.

>[!NOTE]
>
>È necessario configurare il provider di servizi prima di creare e pubblicare un messaggio e-mail. Per ulteriori informazioni, vedere [Configurazione di ExactTarget](/help/sites-administering/exacttarget.md) e [Configurazione di Silverpop Engage](/help/sites-administering/silverpop.md).

Per pubblicare l’e-mail al provider di servizi e-mail, è necessario effettuare le seguenti operazioni:

1. Creare un messaggio e-mail.
1. Applica la configurazione del servizio e-mail all’e-mail.
1. Publish l’e-mail.

>[!NOTE]
>
>Se aggiorni i provider di posta elettronica, esegui un test di volo o invii una newsletter, queste operazioni non riusciranno se la newsletter non viene pubblicata prima nell’istanza di Publish o se l’istanza di Publish non è disponibile. Assicurati di pubblicare la newsletter e assicurati che l’istanza di Publish sia funzionante.

## Creazione di un messaggio e-mail {#creating-an-email}

È possibile creare un&#39;e-mail o un notiziario da pubblicare in un servizio di posta elettronica in una campagna utilizzando il modello **Geometrixx**. È inoltre possibile utilizzare il modello **Geometrixx Outdoors E-mail**. Gli esempi di e-mail/newsletter basati sul modello **Geometrixx Outdoors E-mail** sono disponibili all&#39;indirizzo `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`.

Per creare un messaggio e-mail pubblicato nel servizio e-mail configurato:

1. Vai a **Siti Web** e quindi a **Campagne**. Seleziona una campagna.
1. Fai clic su **Nuovo** per aprire la finestra **Crea pagina**.
1. Immetti il titolo, il nome e seleziona il modello **Newsletter Geometrixx** dall&#39;elenco dei modelli disponibili.
1. Fai clic su **Crea**.
1. Apri l’e-mail creata.
1. Passa alla modalità progettazione per selezionare i componenti da visualizzare nella barra laterale.
1. Passa alla modalità di modifica e inizia ad aggiungere contenuto (testo, immagini, [strumenti e-mail](#adding-exacttarget-email-tools-to-your-email), [variabili di personalizzazione](#adding-text-and-personalization-tool-to-your-e-mail) e così via) al messaggio e-mail.

### Aggiunta di strumenti e-mail ExactTarget all’e-mail {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>Questa sezione è specifica del servizio ExactTarget.

Il componente **Strumenti e-mail** per ExactTarget può aggiungere ulteriori funzionalità e-mail all&#39;e-mail/newsletter.

1. Apri un’e-mail da pubblicare su ExactTarget.
1. Aggiungi il componente **ET - Strumenti e-mail** alla pagina utilizzando la barra laterale. Apri il componente in modalità Modifica.

   ![chlimage_1](assets/chlimage_1.gif)

1. Selezionare un&#39;opzione dal menu **Opzioni**:

<table>
 <tbody>
  <tr>
   <td>Indirizzo postale (obbligatorio)</td>
   <td>Questo componente inserisce l’indirizzo postale fisico dell’organizzazione nell’e-mail.</td>
  </tr>
  <tr>
   <td>Centro profili (obbligatorio)</td>
   <td>Il centro profili è una pagina web in cui gli abbonati possono immettere e gestire le informazioni personali che si tengono su di loro.</td>
  </tr>
  <tr>
   <td>Visualizza e-mail come pagina Web</td>
   <td>Questo componente consente all’utente di visualizzare l’e-mail come pagina web.</td>
  </tr>
  <tr>
   <td>Informativa sulla privacy</td>
   <td>Questo componente inserisce il collegamento all'informativa sulla privacy nell'e-mail.<br /> </td>
  </tr>
  <tr>
   <td>Centro per annullamento sottoscrizioni</td>
   <td>Consente all’utente di annullare l’iscrizione alla mailing list.</td>
  </tr>
  <tr>
   <td>Centro sottoscrizioni</td>
   <td>Un centro abbonamenti è una pagina web in cui un utente iscritto può controllare i messaggi ricevuti dalla tua organizzazione.</td>
  </tr>
  <tr>
   <td>Traccia aperture e-mail</td>
   <td>Componente nascosto che consente di utilizzare la funzione di tracciamento ExactTarget.<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Il menu a discesa **Opzioni** è popolato solo se la configurazione ExactTarget è applicata all&#39;e-mail. Per ulteriori informazioni, vedere [Applicazione della configurazione del servizio di posta elettronica alle impostazioni di posta elettronica](#applying-e-mail-service-configuration-to-e-mail-settings).

1. Publish l’e-mail a ExactTarget.

   L’e-mail con gli strumenti e-mail è disponibile per l’utilizzo nell’account ExactTarget configurato.

>[!NOTE]
>
>* Gli URL all&#39;interno degli strumenti e-mail vengono sostituiti (nell&#39;e-mail ricevuta) dai valori effettivi solo quando un&#39;e-mail viene inviata utilizzando **Invio semplice** o **Invio guidato** ma non **Invio di test**.
>
>* Sono necessari due degli strumenti di posta elettronica: **Indirizzo postale fisico (obbligatorio)** e **Centro profili (obbligatorio)**. Quando l’e-mail viene pubblicata su ExactTarget, per impostazione predefinita questi due strumenti e-mail vengono aggiunti al fondo di ogni e-mail.
>

### Aggiunta dello strumento Testo e Personalization alla posta elettronica {#adding-text-and-personalization-tool-to-your-e-mail}

Puoi aggiungere campi personalizzati in un&#39;e-mail aggiungendo il componente **Testo e Personalization** alla pagina:

1. Aprire il messaggio di posta elettronica da pubblicare nel servizio di posta elettronica.
1. Per abilitare il campo di personalizzazione dal servizio e-mail, aggiungi la configurazione del framework durante la configurazione del servizio e-mail. Per ulteriori informazioni, vedere [configurazione di Silverpop Engage](/help/sites-administering/silverpop.md) e [configurazione di Exact Target](/help/sites-administering/exacttarget.md).
1. Aggiungi il componente **Testo e Personalization** dalla barra laterale. Questo componente fa parte del gruppo newsletter. Apri questo componente in modalità di modifica.

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. Aggiungere il campo personalizzato richiesto al testo selezionando il campo dal menu a discesa e facendo clic su **Inserisci**.
1. Fai clic su **OK** per terminare.

## Applicazione della configurazione del servizio di posta elettronica alle impostazioni di posta elettronica {#applying-e-mail-service-configuration-to-e-mail-settings}

Per applicare la configurazione del servizio di posta elettronica a una newsletter:

1. Creare una configurazione del servizio di posta elettronica.
1. Apri l’e-mail/newsletter.
1. Apri le impostazioni dell&#39;e-mail/newsletter facendo clic su **Impostazioni** o su **Proprietà pagina nella barra laterale**.
1. Fai clic su **Aggiungi servizio** nella scheda **Cloud Service**. Viene visualizzato l’elenco dei servizi. Seleziona la configurazione richiesta - **ExactTarget** o **Silverpop** - dall&#39;elenco a discesa.

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. Fai clic su **OK**.

## Pubblicazione delle e-mail nel servizio e-mail {#publishing-emails-to-email-service}

Le e-mail/newsletter possono essere pubblicate nel servizio di posta elettronica seguendo questi passaggi:

1. Apri l’e-mail.
1. Prima di pubblicare un’e-mail, assicurati di aver applicato la configurazione corretta all’e-mail.
1. Fai clic su **Pubblica**. Verrà aperta la finestra **Notiziario Publish al provider del servizio di posta elettronica**.
1. Compila il campo **Nome newsletter**. L&#39;e-mail/newsletter viene pubblicata al provider del servizio di posta elettronica con questo nome. Se non viene fornito un nome e-mail, l’e-mail viene pubblicata utilizzando il nome della pagina della newsletter in AEM.
1. Fai clic su **Pubblica**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   In caso di esito positivo, AEM conferma che puoi visualizzare l’e-mail in ExactTarget o Silverpop Engage.

   Se è presente ExactTarget, l&#39;e-mail pubblicata può essere visualizzata facendo clic su **Visualizza e-mail pubblicata**. Consente di accedere direttamente alla newsletter pubblicata in ExactTarget ([https://members.exacttarget.com/](https://members.exacttarget.com/).).

>[!NOTE]
>
>Se viene pubblicata un’e-mail/newsletter con lo stesso nome di un’e-mail/newsletter già pubblicata, l’e-mail/newsletter precedente non viene sostituita. Viene invece creata una nuova e-mail/newsletter con lo stesso nome (gli ID di due newsletter sono tuttavia diversi).
>
>Quando si pubblica l’e-mail/newsletter per il provider di servizi di posta elettronica, l’e-mail/newsletter viene pubblicata anche nell’istanza di pubblicazione dell’AEM.
>

### Aggiornamento Di Un Messaggio Di Posta Elettronica Pubblicato {#updating-a-published-e-mail}

Il pulsante **Aggiorna** nella finestra di dialogo di Publish consente di aggiornare una newsletter già pubblicata a un provider di servizi di posta elettronica. Se la newsletter non è ancora stata pubblicata e si fa clic sul pulsante **Aggiorna**, viene visualizzato un messaggio di tipo **Newsletter non pubblicata**.

Per aggiornare un messaggio e-mail pubblicato:

1. Apri l’e-mail/newsletter precedentemente pubblicata a un provider di servizi di posta elettronica che desideri ripubblicare dopo aver apportato modifiche all’e-mail/newsletter.
1. Fai clic su **Pubblica**. Viene visualizzata la finestra **Notiziario Publish al provider del servizio e-mail**. Fai clic su **Aggiorna**.

   Per verificare se l&#39;e-mail/newsletter è stata aggiornata su ExactTarget, fai clic su **Visualizza e-mail pubblicata**. In questo modo puoi passare all’e-mail pubblicata in ExactTarget.

   Per verificare se l&#39;e-mail/newsletter è stata aggiornata su Silverpop Email Service, visita il sito Silverpop Engage.
