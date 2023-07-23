---
title: Utilizzo del flusso di lavoro di traduzione AEM per localizzare i moduli adattivi e i documenti di record
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: Scopri come utilizzare i flussi di lavoro di traduzione dell’AEM per localizzare i moduli adattivi e i documenti di record.
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 14%

---

# Utilizzo del flusso di lavoro di traduzione AEM per localizzare i moduli adattivi e i documenti di record {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

I moduli localizzati consentono di fornire servizi a un pubblico più ampio in aree geografiche diverse. Il flusso di lavoro di traduzione Adobe Experience Manager consente di localizzare i moduli adattivi e i relativi documenti di record . È possibile utilizzare **traduzione automatica** o **traduttori umani** per localizzare un modulo adattivo.

Questo articolo spiega il processo per utilizzare il flusso di lavoro di traduzione AEM con moduli adattivi e documenti di record.

## Localizzazione di un modulo adattivo e di un documento di record tramite traduzione automatica {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Il servizio di traduzione automatica traduce immediatamente il contenuto in formato adattivo e documento di record. AEM Forms è preconfigurato per utilizzare una versione di prova di Microsoft Translator per la traduzione automatica. Per abilitare la traduzione automatica per i moduli adattivi e il documento di record, effettua le seguenti operazioni:

1. Nell’interfaccia utente di AEM Forms, seleziona un modulo e tocca il **Aggiungi dizionario** opzione.
1. In entrata **Aggiungi dizionario a progetto di traduzione** , seleziona la **Crea un nuovo progetto di traduzione** o **Aggiungi a un progetto di traduzione esistente** opzione.
1. In **Titolo progetto** , specificare il titolo. Ad esempio `Government Reference Site - German locale.`
1. In **Lingue di destinazione** , specificare una lingua (ad esempio, `German(de)`) e fai clic su **Fine**. È possibile specificare più impostazioni internazionali. Il modulo viene tradotto in tutte le lingue specificate in **Lingue di destinazione** campo.
1. Nella finestra di dialogo Dizionario aggiunto fare clic su **Progetti aperti**. Nella schermata Progetti, apri il progetto appena creato.
1. Fai clic su **ellissi** nella parte inferiore della sezione **Riepilogo traduzione** affiancare. Viene visualizzata la schermata Riepilogo traduzione.
1. Fai clic su **Modifica** nella parte superiore della sezione **Riepilogo traduzione** schermo. Apri **Traduzione** e selezionare Traduzione automatica in **Metodo di traduzione** schermo. Seleziona la scheda appropriata **Provider traduzione** e **Configurazione cloud**. Fai clic su **Fine** nella parte superiore dello schermo.
1. Il giorno **Lavoro di traduzione** , fai clic su ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fai clic su **Inizio**. Lo stato della sezione diventa Bozza. Al termine della traduzione, lo stato cambia in **Pronto per la revisione**. Aggiorna la pagina dopo alcuni minuti e verifica lo stato.
1. Dopo che lo stato diventa **Pronto per la revisione** il **Lavoro di traduzione** riquadro, aprire il modulo in una finestra del browser. Viene visualizzata una versione localizzata del modulo.

   >[!NOTE]
   >
   >* Prima di aprire la versione localizzata del modulo nella finestra del browser, verificare che le impostazioni internazionali del browser corrispondano a quelle del modulo. Ad esempio, se il modulo è tradotto in lingua tedesca (de), impostare le impostazioni internazionali del browser su Tedesco (de).
   >* I componenti dei moduli adattivi non supportano le lingue da destra a sinistra (RTL). Ad esempio, ebraico.

   Insieme al modulo adattivo, viene localizzato anche il documento di record generato automaticamente.

   Per ulteriori informazioni sulle impostazioni e sulla configurazione del documento record, vedi:

[Configurazione modello del documento record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Impostazioni del documento record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizzare le informazioni di branding del documento record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e assicurati che le impostazioni locali del browser siano impostate sulla stessa lingua in cui hai localizzato il modulo adattivo utilizzando la lingua del computer. Le impostazioni locali del browser consentono di localizzare le informazioni di branding nel documento di record.
1. Per visualizzare il documento localizzato del record, tocca Genera anteprima. Il documento di record PDF viene generato e aperto in una nuova scheda nel browser.

## Localizzazione di un modulo adattivo e del relativo documento di record tramite Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Traduzione umana il contenuto viene inviato a un fornitore di traduzione e tradotto da traduttori professionisti. Una volta completato, il contenuto tradotto viene rinviato e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.

Per la traduzione, un dizionario contenente file in formato XLIFF viene condiviso con i traduttori professionisti. Il dizionario include un file XLIFF separato per ciascuna lingua. Ogni file XLIFF contiene testo che verrà visualizzato agli utenti finali e segnaposto per il testo localizzato corrispondente.

Per localizzare un modulo e il relativo documento di record mediante Human Translators, effettuare le seguenti operazioni:

1. [Connetti AEM con il provider di servizi di traduzione](/help/sites-administering/tc-tic.md) e [crea configurazioni del Translation Integration Framework](/help/sites-administering/tc-tic.md).

1. [Associa le pagine della lingua master](/help/sites-administering/tc-tic.md) con il servizio di traduzione e le configurazioni del framework.

1. [Identifica il tipo di contenuto](/help/sites-administering/tc-rules.md) da tradurre.

1. [Prepara il contenuto per la traduzione](/help/sites-administering/tc-prep.md) creando la lingua master e le pagine root delle copie in lingua.

1. [Crea progetti di traduzione](/help/sites-administering/tc-manage.md) per raccogliere il contenuto da tradurre e preparare il processo di traduzione.

1. Utilizza i progetti di traduzione per [gestire il processo di traduzione dei contenuti](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* I componenti dei moduli adattivi non supportano le lingue da destra a sinistra (RTL). Ad esempio, ebraico.
>
