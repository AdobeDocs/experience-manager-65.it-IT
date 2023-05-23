---
title: Procedura dettagliata sul sito di riferimento per il rinnovo dell'assicurazione automatica We.Finance
seo-title: We.Finance Auto Insurance Renewal reference site walkthrough
description: Procedura dettagliata sul sito di riferimento per il rinnovo dell'assicurazione automatica We.Finance
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# Procedura dettagliata sul sito di riferimento per il rinnovo dell&#39;assicurazione automatica We.Finance{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## Scenario del sito di riferimento We.Finance  {#we-finance-reference-site-scenario}

Il sito We.Finance è un sito di servizi finanziari progettato per aiutarti ad apprendere le funzionalità di comunicazione interattiva di AEM Forms.

Leggi la procedura dettagliata del caso d’uso di We.Finance Auto Insurance che illustra come AEM si forma e la sua integrazione con Microsoft Dynamics consente di personalizzare l’esperienza del cliente in una società di servizi finanziari. La procedura dettagliata interattiva è progettata per facilitare l’implementazione di transazioni digitali complesse e la comunicazione con i clienti in una società finanziaria.

**Il percorso inizia con il caso d’uso:**

Sarah Rose è un cliente We.Finance esistente e ha acquistato una polizza di assicurazione auto. Ora è il momento dell’anno per il rinnovo della sua polizza assicurativa. Gloria Rios, Agente di Assicurazione, We.Finance invia un promemoria a Sarah in merito al rinnovo della sua polizza. Sarah segue le istruzioni fornite nell’e-mail e completa correttamente il processo.

## Procedura dettagliata per l&#39;applicazione di assicurazione automatica {#auto-insurance-application-walkthrough}

Lo scenario di applicazione di Assicurazione automatica We.Finance è una narrazione visiva per l’utente e si basa su due utenti tipo:

* Sarah Rose, cliente We.Finance
* Gloria Rios, Agente Assicurativo, We.Finance

### Gloria invia una comunicazione di rinnovo della polizza assicurativa da We.Finance {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria accede all’istanza AEM e fa clic su **Rinnovo Assicurazione Automatica,** e quindi clic su **Apri l’interfaccia utente dell’agente.** Il clic precompila il documento di assicurazione con i dettagli della polizza di Sarah Rose. Clic su Gloria **Invia** e viene visualizzato un messaggio sullo schermo &quot;Invio avviato&quot; e quindi tra pochi secondi &quot;Invio completato&quot;.

Sarah riceve un’e-mail con l’oggetto &quot;Rinnovo dell’assicurazione automatica&quot;.

![Interfaccia utente agente](assets/agent_ui_email_new.png)

#### Vedi tu stesso {#see-it-yourself}

Vai a **Adobe Experience Manager** > **Forms** > **Forms e documenti** > **We.Finance** > **Assicurazione automatica**. Seleziona il rinnovo dell’assicurazione automatica **comunicazione interattiva** e fai clic su **Apri interfaccia utente agente**. La comunicazione interattiva si apre nell’interfaccia utente dell’agente. Inserisci un indirizzo e-mail valido per ricevere l’e-mail con il documento dei criteri allegato e fai clic su Invia.

Puoi accedere e rivedere la comunicazione interattiva Auto Insurance Renewal direttamente da `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah riceve una comunicazione di rinnovo della polizza assicurativa da We.Finance e decide di rinnovare {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah riceve un&#39;e-mail con un allegato da We.Finance che le ricorda che la sua polizza di assicurazione automatica sta per scadere. L&#39;allegato è la versione stampata della lettera di Assicurazione automatica.

Sarah fa clic su **Rinnova ora** ed è diretto alla versione web della sua lettera di Assicurazione Automatica. In cima a questa lettera, Sarah trova il numero di giorni rimanenti per la scadenza della sua polizza. La pagina fornisce a Sarah una panoramica di base dei dettagli della sua polizza assicurativa come il numero della polizza, l’importo dovuto e altre informazioni come le offerte di sconto e i premi fedeltà. Sarah fa di nuovo clic su **Rinnova ora** in fondo alla politica.

![ref1](assets/ref1.png)

#### Come funziona {#how-it-works}

L’output web e cartaceo della lettera di Assicurazione automatica viene creato utilizzando le funzionalità multicanale delle comunicazioni interattive.

Il pulsante Rinnova ora nell’e-mail è collegato all’applicazione Rinnova assicurazione automatica, che è una comunicazione interattiva su un’istanza pubblicata.

#### Vedi tu stesso {#see-it-yourself-1}

Devi aver ricevuto un&#39;e-mail con un PDF allegato. Il PDF è una versione stampata della lettera di Assicurazione automatica. Clic **Rinnova ora** per accedere alla versione web del criterio. Controlla le tue informazioni personali e i dettagli della policy e fai clic su **Rinnova ora** che ti porta a un&#39;altra comunicazione interattiva.

Il **Rinnova ora** Il pulsante nell’e-mail indirizza Sarah alla versione web del criterio. Puoi visitare il seguente URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

Puoi controllare il riepilogo dettagliato del rinnovo dell’assicurazione automatica e fare clic su **Rinnova ora** nella parte inferiore della pagina.

### Sarah raggiunge la pagina dei pagamenti {#sarah-reaches-the-payment-page}

We.Finance porta Sarah alla pagina Pagamento. Sarah controlla nuovamente i suoi documenti dal numero della polizza e dalla data di scadenza. Sul lato destro della pagina, controlla il Riepilogo pagamenti del rinnovo con uno sconto del 10% sull&#39;importo totale.

#### Come funziona {#how-it-works-1}

Il pulsante Rinnova ora indirizza Sarah alla pagina di pagamento. La pagina di pagamento è un modulo adattivo.

#### Vedi tu stesso {#see-it-yourself-2}

Clic **Rinnova ora** per accedere alla pagina Pagamento. Inserisci le informazioni sulla carta di credito e fai clic su **Effettua pagamento**.

Puoi accedere alla pagina dei pagamenti nell’istanza di authoring all’indirizzo

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah effettua il pagamento e completa la procedura {#sarah-makes-the-payment-and-completes-the-process}

Sarah compila i dati della sua carta di credito e i suoi clic **Effettua pagamento**.

#### Come funziona {#how-it-works-2}

Quando Sarah compila i dettagli della carta di credito e fa clic su Invia, il pagamento con la sua carta di credito viene elaborato e sullo schermo viene visualizzato un messaggio di ringraziamento configurato nel modulo adattivo.

#### Vedi tu stesso {#see-it-yourself-3}

Puoi visualizzare il messaggio di conferma dopo aver fatto clic su Effettua pagamento all’indirizzo

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
