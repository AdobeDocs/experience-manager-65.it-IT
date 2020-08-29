---
title: Configurazione di Microsoft Dynamics 365 per il flusso di lavoro del mutuo home del sito di riferimento We.Finance
seo-title: Configurazione di Microsoft Dynamics 365 per il flusso di lavoro del mutuo home del sito di riferimento We.Finance
description: Scoprite come sfruttare i servizi di Microsoft® Dynamics 365 tramite moduli adattivi per il flusso di lavoro mutui per la casa del sito di riferimento We.Finance
seo-description: Scoprite come sfruttare i servizi di Microsoft® Dynamics 365 tramite moduli adattivi per il flusso di lavoro mutui per la casa del sito di riferimento We.Finance
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---


# Configurazione di Microsoft Dynamics 365 per il flusso di lavoro del mutuo home del sito di riferimento We.Finance {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

Scoprite come sfruttare i servizi di Microsoft® Dynamics 365 tramite moduli adattivi per il flusso di lavoro mutui per la casa del sito di riferimento We.Finance

## Panoramica {#overview}

Microsoft® Dynamics 365 è un software CRM (Customer Relationship Management) ed ERP (Enterprise Resource Planning) che fornisce soluzioni aziendali per la creazione e la gestione di account cliente, contatti, lead, opportunità e casi.

 AEM Forms fornisce un servizio cloud per integrare Dynamics 365 con il modulo [Forms Data Integration](/help/forms/using/data-integration.md) . Prima di poter utilizzare la procedura dettagliata dell&#39;applicazione Home Mortgage con lo scenario Microsoft® Dynamics, è necessario configurare Microsoft® Dynamics 365 per l&#39;utilizzo con il sito di riferimento We.Finance.

## Prerequisiti {#prerequisites}

Prima di iniziare a configurare Dynamics 365, accertati di disporre di:

* AEM 6.3 Forms Service Pack 1 e versioni successive
* Account Microsoft® Dynamics 365
* Applicazione registrata per il servizio Dynamics 365 con Microsoft® Azure Active Directory
* ID client e segreto client per l’applicazione registrata

## Collegare il calcolatore del mutuo casa con la pagina principale del sito {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. Nell’istanza di creazione, passate alla pagina seguente:

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Scorri verso il basso fino al calcolatore ipotecario principale.
1. Evidenziare il pannello della colonna destra (calcolatore) e toccare per visualizzare il menu a comparsa. Nel menu a comparsa, toccate Configura. Viene visualizzata la finestra di dialogo Modifica  contenitore AEM Forms.

   ![calcolatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. Nella finestra di dialogo Modifica  contenitore AEM Forms, individuate il percorso della risorsa e selezionate home-mutuo-calcolatore nel percorso seguente, quindi toccate **Conferma**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectNazionetpath](assets/selectassetpath.png)

1. Toccate **Chiudi**.
1. Pubblicate la pagina modificata.

   >[!NOTE]
   >
   >Il binding dei campi del calcolatore con FDM è preconfigurato tramite il pacchetto del sito di riferimento We.Finance. Per visualizzare il binding, è possibile aprire il modulo in modalità di creazione e visualizzare i riferimenti ai binding dei campi.

1. Per creare un&#39;entità personalizzata per l&#39;archiviazione del record del richiedente per l&#39;applicazione mutuo per la casa, importa il pacchetto della soluzione AEMFormsFSIRefsite_1_0.zip nell&#39;istanza di Microsoft® Dynamics:

   1. Scaricate il pacchetto da:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. Importa il pacchetto della soluzione nell&#39;istanza di Microsoft® Dynamics. Nell&#39;istanza di Microsoft® Dynamics, accedete a **Settings** (Impostazioni) > **Solutions** (Soluzioni) **e toccate** Import (Importa).

1. Per impostare i dettagli di contatto utente utilizzati nel refsite, importate il pacchetto Sarah Rose Contact.CSV nell&#39;istanza di Microsoft® Dynamics:

   1. Scaricate il pacchetto da:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. Importa il pacchetto nella tua istanza di Microsoft® Dynamics. Nell&#39;istanza di Microsoft® Dynamics, accedete a **Vendite** > **Contatti** e toccate **Importa dati**.

