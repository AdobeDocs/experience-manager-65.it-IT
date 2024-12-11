---
title: Aggiungi versioni, commenti e annotazioni al modulo adattivo dell’AEM 6.5.
description: Utilizza i componenti core per moduli adattivi AEM 6.5 per aggiungere commenti, annotazioni e versioni a un modulo adattivo.
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
exl-id: 91e6fca2-60ba-45f1-98c3-7b3fb1d762f5
source-git-commit: 94a9f4087e36bfe5701ad9aafd4e8446ca643ddf
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Controllo delle versioni, revisione e aggiunta di commenti in un modulo adattivo

<!--
<span class="preview"> This feature is under the early adopter program. If you’re interested in joining our early access program for this feature, send an email from your official address to aem-forms-ea@adobe.com to request access </span>
-->

<span class="preview">Questa funzionalità non è attivata per impostazione predefinita. È possibile scrivere dal proprio indirizzo ufficiale all&#39;indirizzo aem-forms-ea@adobe.com per richiedere l&#39;accesso alla funzionalità.</span>

I componenti core per moduli adattivi consentono agli autori dei moduli di aggiungere versioni, commenti e annotazioni ai moduli. Queste funzioni semplificano lo sviluppo dei moduli consentendo agli utenti di creare e gestire più versioni, collaborare tramite commenti e aggiungere note a sezioni di moduli specifiche, migliorando l’esperienza di creazione dei moduli.

## Prerequisito {#prerequisite-versioning}

Per utilizzare le funzioni di controllo delle versioni, inserimento di commenti e annotazioni in un modulo adattivo, assicurati che [Componenti core modulo adattivo](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components) sia abilitato nell&#39;ambiente Forms AEM 6.5.

## Controllo delle versioni dei moduli adattivi {#adaptive-form-versioning}

Il controllo delle versioni adattive dei moduli consente di aggiungere versioni a un modulo. Gli autori dei moduli possono creare facilmente più versioni di un modulo e infine utilizzare quella adatta agli obiettivi aziendali. Gli utenti del modulo possono inoltre ripristinare le versioni precedenti del modulo. Consente inoltre agli autori di confrontare due versioni qualsiasi di un modulo visualizzandole in anteprima, consentendo loro di analizzare i moduli in modo migliore dal punto di vista dell’interfaccia utente. Passiamo ora ai dettagli per ogni funzionalità di controllo delle versioni dei moduli adattivi:

### Creare una versione del modulo {#create-a-form-version}

Per creare una versione di un modulo, effettuare le seguenti operazioni:

1. Nel tuo ambiente AEM Forms, passa al **[!UICONTROL Modulo]**>**[!UICONTROL Forms e documenti]** e seleziona il tuo **Modulo**.
1. Dal menu a discesa di selezione nel pannello a sinistra, seleziona **[!UICONTROL Versioni]**.
   ![Seleziona modulo](assets/select-a-form.png)
1. Fai clic su **tre punti** nel pannello inferiore a sinistra, quindi fai clic su **[!UICONTROL Salva come versione]**.
1. Fornire un&#39;etichetta alla versione del modulo. È inoltre possibile aggiungere informazioni sul modulo tramite un commento.
   ![Crea una versione modulo](assets/create-a-form-version.png)

### Aggiornare una versione del modulo {#update-a-form-version}

Dopo aver modificato e aggiornato il modulo, è possibile aggiungervi una nuova versione. Per assegnare un nome a una nuova versione del modulo, come illustrato nell&#39;immagine, attenersi alla procedura descritta nell&#39;ultima sezione:

![Aggiorna una versione modulo](assets/update-a-form-version.png)

### Ripristinare una versione del modulo {#revert-a-form-version}

Per ripristinare una versione precedente di un modulo, selezionare una versione del modulo e fare clic su **[!UICONTROL Ripristina questa versione]**.

![Ripristina versione modulo](assets/revert-form-version.png)

### Confronta versioni modulo {#compare-form-versions}

Gli autori dei moduli possono confrontare due versioni diverse di un modulo a scopo di anteprima. Per confrontare le versioni, selezionare qualsiasi versione del modulo e fare clic su **[!UICONTROL Confronta con corrente]**. Vengono visualizzate due diverse versioni del modulo in modalità anteprima.

![Confronta versioni modulo](assets/compare-form-versions.png)

## Aggiungi commenti {#add-comments}

Una revisione è un meccanismo che consente a uno o più revisori di aggiungere commenti ai moduli. Qualsiasi utente di un modulo può aggiungere un commento a un modulo o esaminarlo tramite commenti. Per aggiungere un commento a un modulo, selezionare un **[!UICONTROL Modulo]** e aggiungere un **[!UICONTROL Commento]** al modulo.

>[!NOTE]
> Quando si utilizzano commenti nei componenti core per moduli adattivi come descritto in precedenza, la funzionalità del modulo [aggiunta di revisori ai moduli](/help/forms/using/create-reviews-forms.md) è disabilitata.


![Aggiungi commenti in un modulo](assets/form-comments.png)

## Aggiungi annotazioni {#adaptive-form-annotations}

In molti casi, agli utenti dei gruppi di moduli viene richiesto di aggiungere annotazioni a un modulo per scopi di revisione, ad esempio in una scheda specifica o in componenti specifici di un modulo. In questi casi, gli autori possono utilizzare le annotazioni.
Per aggiungere annotazioni a un modulo, effettuare le seguenti operazioni:

1. Aprire un modulo in modalità **[!UICONTROL Modifica]**.

1. Fai clic sull&#39;icona **aggiungi** che si trova nella barra superiore destra, come indicato nell&#39;immagine.
   ![Annotazione](assets/annotation.png)

1. A questo punto, fai clic sull&#39;icona **aggiungi** che si trova nella barra superiore sinistra come indicato nell&#39;immagine per aggiungere l&#39;annotazione.
   ![Aggiungi annotazione](assets/add-annotation.png)

1. Ora è possibile aggiungere commenti, disegnare schizzi con più colori per formare i componenti.

1. Per visualizzare tutte le annotazioni aggiunte a un modulo, selezionalo e visualizzerai le annotazioni aggiunte nel pannello sinistro, come illustrato nell’immagine.

   ![Visualizza annotazioni aggiunte](assets/see-annotations.png)

## Consulta anche

* [Confronto dei componenti core di Forms adattivi](/help/forms/using/compare-forms-core-components.md)
