---
title: Utilizzo AEM flusso di lavoro di traduzione per localizzare i moduli adattivi e il documento di registrazione
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: Scopri come utilizzare AEM flussi di lavoro di traduzione per localizzare moduli adattivi e documenti di record.
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 15%

---

# Utilizzo AEM flusso di lavoro di traduzione per localizzare i moduli adattivi e il documento di registrazione {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

I moduli localizzati consentono di distribuire un pubblico più ampio in più aree geografiche. Il flusso di lavoro di traduzione di Adobe Experience Manager consente di localizzare i moduli adattivi e i relativi documenti record . È possibile utilizzare **traduzione automatica** o **traduttori** per localizzare un modulo adattivo.

Questo articolo spiega il processo per utilizzare AEM flusso di lavoro di traduzione con moduli adattivi e documenti di record.

## Localizzazione di un modulo adattivo e di un documento di record utilizzando la traduzione automatica {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Il servizio di traduzione automatica traduce immediatamente il contenuto in forma adattiva e in un documento di registrazione. AEM Forms è preconfigurato per utilizzare una versione di prova di Microsoft Translator per la traduzione automatica. Esegui i seguenti passaggi per abilitare la traduzione automatica per i moduli adattivi e il documento di record:

1. Nell’interfaccia utente di AEM Forms, seleziona un modulo e tocca il **Aggiungi dizionario** opzione .
1. In **Aggiungi dizionario al progetto di traduzione** seleziona la **Crea un nuovo progetto di traduzione** o **Aggiungi a un progetto di traduzione esistente** opzione .
1. In **Titolo del progetto** Specifica il titolo. Esempio, `Government Reference Site - German locale.`
1. In **Lingue di destinazione** specificare un&#39;impostazione internazionale (ad esempio, `German(de)`) e fai clic su **Fine**. È possibile specificare più impostazioni internazionali. Il modulo viene convertito in tutte le impostazioni internazionali specificate nella **Lingue di destinazione** campo .
1. Nella finestra di dialogo Dizionario aggiunto fare clic su **Apri progetti**. Nella schermata Progetti , apri il progetto appena creato.
1. Fai clic sul pulsante **ellissi** nella parte inferiore del **Riepilogo della traduzione** piastrelle. Viene visualizzata la schermata Riepilogo traduzioni.
1. Fai clic sul pulsante **Modifica** nella parte superiore della **Riepilogo della traduzione** schermo. Apri **Traduzione** e selezionare Traduzione automatica nel **Metodo di traduzione** schermo. Selezionare il **Provider di traduzione** e **Configurazione cloud**. Fai clic sul pulsante **Fine** nella parte superiore dello schermo.
1. Sulla **Processo di traduzione** riquadro, fai clic su ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fai clic su **Inizio**. Lo stato della tessera diventa Bozza. Al termine della traduzione, lo stato cambia in **Pronto per la revisione**. Aggiorna la pagina dopo alcuni minuti e verifica lo stato.
1. Dopo che lo stato cambia in **Pronto per la revisione** sulla **Processo di traduzione** aprire il modulo in una finestra del browser. Viene visualizzata una versione localizzata del modulo.

   >[!NOTE]
   >
   >* Prima di aprire la versione localizzata del modulo nella finestra del browser, assicurarsi che le impostazioni internazionali del browser corrispondano alle impostazioni internazionali del modulo. Ad esempio, se il modulo è tradotto in tedesco(de), impostare le impostazioni internazionali del browser su Tedesco(de).
   >* I componenti per moduli adattivi non supportano le lingue RTL (da destra a sinistra). Per esempio, l&#39;ebraico.


   Insieme al modulo adattivo, viene localizzato anche il documento di record generato automaticamente.

   Per ulteriori informazioni sulle impostazioni e sulla configurazione del documento di record, vedere:

[Configurazione modello del documento record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Impostazioni del documento di registrazione](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizzare le informazioni di branding del documento di registrazione](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e assicurarsi che le impostazioni internazionali del browser siano impostate sulla stessa lingua in cui è stato localizzato il modulo adattivo utilizzando la lingua della macchina. Le impostazioni internazionali del browser consentono di localizzare le informazioni sul marchio nel documento di registrazione.
1. Per visualizzare il documento localizzato del record, toccare Genera anteprima. Il documento di record PDF viene generato e aperto in una nuova scheda nel browser.

## Localizzazione di un modulo adattivo e del relativo documento di registrazione utilizzando la traduzione umana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Nella traduzione umana il contenuto viene inviato ad un fornitore di traduzione e tradotto da traduttori professionisti. Una volta completato, il contenuto tradotto viene rinviato e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.

Per la traduzione, un dizionario contenente file in formato XLIFF viene condiviso con i traduttori professionisti. Il dizionario include un file XLIFF separato per ogni impostazione internazionale. Ogni file XLIFF contiene testo che verrà visualizzato agli utenti finali e ai segnaposto per il testo localizzato corrispondente.

Esegui i seguenti passaggi per localizzare un modulo e il relativo documento di registrazione utilizzando Human Translators:

1. [Connetti AEM con il provider di servizi di traduzione](/help/sites-administering/tc-tic.md) e [crea configurazioni del Translation Integration Framework](/help/sites-administering/tc-tic.md).

1. [Associa le pagine della lingua master](/help/sites-administering/tc-tic.md) con il servizio di traduzione e le configurazioni del framework.

1. [Identifica il tipo di contenuto](/help/sites-administering/tc-rules.md) da tradurre.

1. [Prepara il contenuto per la traduzione](/help/sites-administering/tc-prep.md) creando la lingua master e le pagine root delle copie in lingua.

1. [Crea progetti di traduzione](/help/sites-administering/tc-manage.md) per raccogliere il contenuto da tradurre e preparare il processo di traduzione.

1. Utilizza i progetti di traduzione per [gestire il processo di traduzione dei contenuti](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* I componenti per moduli adattivi non supportano le lingue RTL (da destra a sinistra). Per esempio, l&#39;ebraico.
>

