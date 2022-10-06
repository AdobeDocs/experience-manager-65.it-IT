---
title: Pubblicazione di un’e-mail ai provider di servizi e-mail
seo-title: Publishing an Email to Email Service Providers
description: È possibile pubblicare le newsletter su servizi e-mail come ExactTarget e Silverpop Engage.
seo-description: You can publish newsletters to e-mail services such as ExactTarget and Silverpop Engage.
uuid: 1a7adcfe-8e52-49f4-9a00-99ac99881225
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b9618913-5433-4baf-9ff6-490a26860505
exl-id: c07692f7-3618-4e8c-96d7-4db09f2d9896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 67%

---

# Pubblicazione di un’e-mail ai provider di servizi e-mail{#publishing-an-email-to-email-service-providers}

È possibile pubblicare le newsletter su servizi e-mail come ExactTarget e Silverpop Engage. Questo documento descrive come configurare AEM affinché pubblichi una newsletter per questi servizi di posta elettronica.

>[!NOTE]
>
>È necessario configurare il provider prima di poter creare e modificare un messaggio e-mail. Vedi [Configurazione di ExactTarget](/help/sites-administering/exacttarget.md) e [Configurazione di Silverpop Engage](/help/sites-administering/silverpop.md) per ulteriori informazioni.

Per pubblicare l&#39;e-mail su provider di servizi e-mail, è necessario eseguire i seguenti passaggi:

1. Crea un messaggio e-mail.
1. Applica la configurazione del servizio e-mail all&#39;e-mail.
1. Modifica il messaggio e-mail.

>[!NOTE]
>
>Se devi aggiornare i provider e-mail, eseguire un invio di prova o inviare una newsletter, queste operazioni non vanno a buon fine se la newsletter non viene prima pubblicata nell’istanza Pubblica o se l’istanza Pubblica non è disponibile. Assicurati di pubblicare la newsletter e che l’istanza Pubblica sia attiva e funzionante.

## Creazione di un&#39;e-mail {#creating-an-email}

Un’e-mail o una newsletter da pubblicare in un servizio e-mail può essere creata in una campagna utilizzando **Newsletter Geometrixx** modello. È inoltre possibile utilizzare **E-mail Geometrixx Outdoors** modello. Esempio di e-mail/newsletter basato su **E-mail Geometrixx Outdoors** modello disponibile in `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`.

Per creare un nuovo messaggio e-mail pubblicato nel servizio e-mail configurato:

1. Vai a **Siti Web** e poi **Campagne**. Selezionate una campagna.
1. Fai clic su **Nuovo** per aprire la finestra **Crea pagina**.
1. Inserisci il titolo e il nome e seleziona il modello **Geometrixx Newsletter** dall’elenco di modelli disponibili.
1. Fai clic su **Crea**.
1. Apri il messaggio e-mail creato.
1. Passa alla modalità di progettazione per selezionare i componenti da visualizzare nella barra laterale.
1. Passa alla modalità di modifica e inizia ad aggiungere contenuto (testo, immagini, [strumenti e-mail](#adding-exacttarget-email-tools-to-your-email), [variabili di personalizzazione](#adding-text-and-personalization-tool-to-your-e-mail)e così via) alla tua e-mail.

### Aggiunta di strumenti e-mail ExactTarget all&#39;e-mail {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>Questa sezione descrive il servizio ExactTarget.

La **Strumenti e-mail** per ExactTarget puoi aggiungere ulteriori funzionalità e-mail all’e-mail o alla newsletter.

1. Apri un messaggio e-mail da pubblicare su ExactTarget.
1. Aggiungi il componente **ET - Strumenti e-mail** alla tua pagina usando la barra laterale. Apri il componente in modalità Modifica.

   ![chlimage_1](assets/chlimage_1.gif)

1. Selezionate un’opzione dal menu **Opzioni**:

<table>
 <tbody>
  <tr>
   <td>Indirizzo postale (obbligatorio)</td>
   <td>Questo componente inserisce l’indirizzo postale dell’organizzazione nell’e-mail.</td>
  </tr>
  <tr>
   <td>Centro profili (obbligatorio)</td>
   <td>Il centro profili è una pagina Web in cui gli utenti iscritti possono inserire e gestire le informazioni personali memorizzate nel loro profilo.</td>
  </tr>
  <tr>
   <td>Visualizza e-mail come pagina Web</td>
   <td>Questo componente consente agli utenti di visualizzare il messaggio e-mail sotto forma di pagina Web,.</td>
  </tr>
  <tr>
   <td>Informativa sulla privacy</td>
   <td>Questo componente inserisce il collegamento all’informativa sulla privacy nell’e-mail.<br /> </td>
  </tr>
  <tr>
   <td>Centro per annullamento sottoscrizioni</td>
   <td>Offre all’utente la possibilità di annullare l’iscrizione e rimuovere il proprio nome dalla mailing list..</td>
  </tr>
  <tr>
   <td>Centro sottoscrizioni</td>
   <td>Un centro sottoscrizioni è una pagina web in cui un utente iscritto può controllare i messaggi ricevuti dall’organizzazione.</td>
  </tr>
  <tr>
   <td>Traccia aperture e-mail</td>
   <td>Componente nascosto che consente di utilizzare la funzione di tracciamento ExactTarget.<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Il menu a discesa **Opzioni** viene compilato solo se la configurazione di ExactTarget viene applicata al messaggio e-mail. Vedi [Applicazione della configurazione del servizio e-mail alle impostazioni e-mail](#applying-e-mail-service-configuration-to-e-mail-settings) per ulteriori informazioni.

1. Pubblica l&#39;e-mail su ExactTarget.

   L&#39;e-mail con gli strumenti e-mail è disponibile per l&#39;utilizzo nell&#39;account ExactTarget configurato.

>[!NOTE]
>
>* Gli URL all’interno degli strumenti e-mail vengono sostituiti (nell’e-mail ricevuta) dai loro valori effettivi solo quando un’e-mail viene inviata utilizzando **Invio semplice** o **Invio guidato** ma non **Invia test**.
>
>* Sono necessari due degli strumenti e-mail: **Indirizzo postale (obbligatorio)** e **Centro profili (obbligatorio)**. Quando l&#39;e-mail viene pubblicata su ExactTarget, questi due strumenti e-mail vengono aggiunti in fondo a ogni e-mail per impostazione predefinita.
>


### Aggiunta dello strumento di Testo e Personalizzazione al messaggio e-mail {#adding-text-and-personalization-tool-to-your-e-mail}

Si possono aggiungere campi personalizzati in un&#39;e-mail aggiungendo il componente **Testo e Personalizzazione** alla pagina:

1. Apri il messaggio e-mail da pubblicare sul servizio e-mail.
1. Per abilitare il campo di personalizzazione dal servizio e-mail, aggiungi la configurazione del framework durante la configurazione del servizio e-mail. Vedi [configurazione di Silverpop Engage](/help/sites-administering/silverpop.md) e [configurazione di Exact Target](/help/sites-administering/exacttarget.md) per ulteriori informazioni.
1. Aggiungi il componente **Testo e personalizzazione** dalla barra laterale. Questo componente è la parte del gruppo newsletter. Apri questo componente nella modalità di modifica.

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. Aggiungi al testo il campo personalizzato desiderato selezionandolo dal menu a discesa e facendo clic su **Inserisci**.
1. Fai clic su **OK** per terminare.

## Applicazione della configurazione del servizio e-mail alle impostazioni e-mail {#applying-e-mail-service-configuration-to-e-mail-settings}

Per applicare la configurazione del servizio e-mail a una newsletter:

1. Crea una configurazione del servizio e-mail.
1. Apri l&#39;e-mail o la newsletter.
1. Apri le impostazioni e-mail/newsletter facendo clic su **Impostazioni** o facendo clic su **Proprietà pagina in** la barra laterale.
1. Fai clic su **Aggiungi servizio** nella scheda **Servizi cloud**. Viene visualizzato l’elenco dei servizi disponibili. Seleziona la configurazione richiesta (**ExactTarget** o **Silverpop**) dal menu a discesa.

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. Fai clic su **OK**.

## Pubblicazione di e-mail sul servizio e-mail {#publishing-emails-to-email-service}

Le e-mail e le newsletter possono essere pubblicate sul servizio e-mail seguendo questi passaggi:

1. Apri il messaggio e-mail.
1. Prima di pubblicare un messaggio e-mail, verifica di aver applicato la configurazione corretta al messaggio.
1. Fai clic su **Pubblica**. Viene aperta la **Pubblica newsletter sul provider di servizi e-mail** finestra.
1. Compila il campo **Nome newsletter**. L&#39;e-mail o newsletter viene pubblicata sul provider di servizi e-mail con questo nome. Se non viene fornito un nome e-mail, l’e-mail viene pubblicata utilizzando il nome della pagina della newsletter in AEM.
1. Fate clic su **Pubblica**. 

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   Se l&#39;esito è positivo, AEM conferma che è possibile visualizzare l&#39;e-mail in ExactTarget o Silverpop Engage.

   Nel caso di ExactTarget, l’e-mail pubblicata può essere visualizzata facendo clic su **Visualizza e-mail pubblicata**. Viene visualizzata direttamente la newsletter pubblicata in ExactTarget ([https://members.exacttarget.com/](https://members.exacttarget.com/).).

>[!NOTE]
>
>Se un&#39;e-mail o newsletter viene pubblicata con lo stesso nome di un&#39;altra già pubblicata, l&#39;e-mail o newsletter precedente non viene sostituita. Viene invece creata una nuova e-mail o newsletter con lo stesso nome (gli ID di due newsletter sono però diversi).
>
>La pubblicazione dell&#39;e-mail o newsletter sul provider di servizi e-mail pubblica anche l&#39;e-mail o newsletter sull&#39;istanza di pubblicazione AEM.

### Aggiornamento di un&#39;e-mail pubblicata {#updating-a-published-e-mail}

La **Aggiorna** nella finestra di dialogo Pubblica puoi aggiornare una newsletter già pubblicata su un provider di servizi e-mail. Nel caso in cui la newsletter non sia ancora stata pubblicata e si faccia clic sul pulsante **Aggiorna**, viene visualizzato il messaggio **La newsletter non è pubblicata**.

Per aggiornare un messaggio e-mail pubblicato:

1. Apri l&#39;e-mail o newsletter che è stata precedentemente pubblicata a un provider di servizi e-mail che si desidera ripubblicare dopo aver apportato modifiche all&#39;e-mail o newsletter.
1. Fai clic su **Pubblica**. La **Pubblica newsletter su Email Service Provider** viene visualizzata la finestra . Fai clic su **Aggiorna**.

   Per verificare se l’e-mail o newsletter è stata aggiornata su ExactTarget, fai clic su **Visualizza e-mail pubblicata**. Questo ti porta all&#39;e-mail pubblicata su ExactTarget.

   Per verificare che l&#39;e-mail o newsletter sia stata aggiornata sul Silverpop Email Service, visita il sito di Silverpop Engage.
