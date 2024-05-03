---
title: Configura Microsoft Dynamics 365 per il flusso di lavoro mutui per la casa del sito di riferimento We.Finance
description: Scopri come utilizzare i servizi di Microsoft&reg; Dynamics 365 tramite moduli adattivi per il flusso di lavoro del mutuo per la casa del sito di riferimento We.Finance.
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Configura Microsoft Dynamics 365 per il flusso di lavoro mutui per la casa del sito di riferimento We.Finance {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

Scopri come utilizzare i servizi Microsoft® Dynamics 365 tramite moduli adattivi per il flusso di lavoro ipotecario per la casa del sito di riferimento We.Finance

## Panoramica {#overview}

Microsoft® Dynamics 365 è un software CRM (Customer Relationship Management) e ERP (Enterprise Resource Planning) che fornisce soluzioni aziendali per la creazione e la gestione di account, contatti, lead, opportunità e casi cliente.

AEM Forms fornisce un servizio cloud per integrare Dynamics 365 con [Integrazione dei dati di Forms](/help/forms/using/data-integration.md) modulo. Prima di poter utilizzare la procedura dettagliata per l&#39;applicazione Home Mortgage con Microsoft® Dynamics, è necessario configurare Microsoft® Dynamics 365 per l&#39;utilizzo con il sito di riferimento We.Finance.

## Prerequisiti {#prerequisites}

Prima di iniziare l’impostazione e la configurazione di Dynamics 365, assicurati di disporre di:

* AEM 6.3 Forms Service Pack 1 e versioni successive
* Account Microsoft® Dynamics 365
* Applicazione registrata per il servizio Dynamics 365 con Microsoft® Azure Active Directory
* ID client e segreto client per l&#39;applicazione registrata

## Collegare il calcolatore ipotecario domestico con la home page del sito {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. Nell’istanza di authoring, vai alla pagina seguente:

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Scorri verso il basso fino al Calcolatore ipotecario predefinito.
1. Evidenziate il pannello della colonna destra (calcolatrice) e selezionate per visualizzare il menu a comparsa. Nel menu a comparsa, selezionare Configura. Viene visualizzata la finestra di dialogo Modifica contenitore AEM Forms.

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. Nella finestra di dialogo Modifica contenitore AEM Forms, sfoglia il percorso del cespite e seleziona home-mortgage-calculator nel percorso seguente e seleziona **Conferma**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. Seleziona **Fine**.
1. Pubblica la pagina modificata.

   >[!NOTE]
   >
   >L’associazione dei campi della calcolatrice con FDM viene preconfigurata tramite il pacchetto per il sito di riferimento We.Finance. Per visualizzare il binding, è possibile aprire il modulo in modalità di creazione e visualizzare i riferimenti di associazione del campo.

1. Per creare un’entità personalizzata per la memorizzazione del record candidato per la richiesta di mutuo per la casa, importa il pacchetto della soluzione AEMFormsFSIRefsite_1_0.zip nell’istanza di Microsoft® Dynamics:

   1. Scarica il pacchetto da:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. Importa il pacchetto della soluzione nell’istanza di Microsoft® Dynamics. Nell’istanza di Microsoft® Dynamics, vai a **Impostazioni** > **Soluzioni** e quindi seleziona **Importa**.

1. Per impostare i dettagli di contatto dell&#39;utente utilizzati nel sito Web, importare il pacchetto Sarah Rose Contact.CSV nell&#39;istanza di Microsoft® Dynamics:

   1. Scarica il pacchetto da:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. Importa il pacchetto nell’istanza di Microsoft® Dynamics. Nell’istanza di Microsoft® Dynamics, vai a **Vendite** > **Contatti** e quindi seleziona **Importa dati**.
