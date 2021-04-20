---
title: Utilizzo AEM flusso di lavoro di traduzione per localizzare i moduli adattivi e il documento di registrazione
seo-title: Utilizzo AEM flusso di lavoro di traduzione per localizzare i moduli adattivi e il documento di registrazione
description: Scopri come utilizzare AEM flussi di lavoro di traduzione per localizzare moduli adattivi e documenti di record.
seo-description: Scopri come utilizzare AEM flussi di lavoro di traduzione per localizzare moduli adattivi e documenti di record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---


# Utilizzo AEM flusso di lavoro di traduzione per localizzare i moduli adattivi e il documento di record {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

I moduli localizzati consentono di distribuire un pubblico più ampio in più aree geografiche. Il flusso di lavoro di traduzione di Adobe Experience Manager consente di localizzare i moduli adattivi e i relativi documenti record . Puoi utilizzare **traduzioni automatiche** o **traduttori umani** per localizzare un modulo adattivo.

Questo articolo spiega il processo per utilizzare AEM flusso di lavoro di traduzione con moduli adattivi e documenti di record.

## Localizzazione di un modulo adattivo e di un documento di record utilizzando la traduzione automatica {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Il servizio di traduzione automatica traduce immediatamente il contenuto in forma adattiva e in un documento di registrazione. AEM Forms è preconfigurato per utilizzare una versione di prova di Microsoft Translator per la traduzione automatica. Esegui i seguenti passaggi per abilitare la traduzione automatica per i moduli adattivi e il documento di record:

1. Nell’interfaccia utente di AEM Forms, seleziona un modulo e tocca l’opzione **Aggiungi dizionario** .
1. Nella schermata **Aggiungi dizionario al progetto di traduzione**, seleziona l&#39;opzione **Crea un nuovo progetto di traduzione** o **Aggiungi a un progetto di traduzione esistente** .
1. Nel campo **Titolo progetto** , specifica il titolo. Esempio, `Government Reference Site - German locale.`
1. Nel campo **Lingue di destinazione**, specifica un&#39;impostazione internazionale (ad esempio, `German(de)`) e fai clic su **Fine**. È possibile specificare più impostazioni internazionali. Il modulo viene convertito in tutte le impostazioni internazionali specificate nel campo **Lingue di destinazione** .
1. Nella finestra di dialogo Dizionario aggiunto fare clic su **Apri progetti**. Nella schermata Progetti , apri il progetto appena creato.
1. Fai clic sui **puntini di sospensione** nella parte inferiore del riquadro **Riepilogo di traduzione** . Viene visualizzata la schermata Riepilogo traduzioni.
1. Fai clic sull&#39;icona **Modifica** nella parte superiore della schermata **Riepilogo traduzione**. Apri la scheda **Traduzione** e seleziona Traduzione automatica nella schermata **Metodo di traduzione** . Seleziona il **Provider di traduzione** e **Configurazione cloud** appropriato. Fai clic sull&#39;icona **Fine** nella parte superiore dello schermo.
1. Nella sezione **Processo di traduzione** , fai clic sull&#39;icona ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fai clic su **Start**. Lo stato della tessera diventa Bozza. Al termine della traduzione, lo stato cambia in **Pronto per la revisione**. Aggiorna la pagina dopo alcuni minuti e verifica lo stato.
1. Dopo che lo stato cambia in **Pronto per la revisione** nel riquadro **Processo di traduzione**, apri il modulo in una finestra del browser. Viene visualizzata una versione localizzata del modulo.

   >[!NOTE]
   >
   >* Prima di aprire la versione localizzata del modulo nella finestra del browser, assicurarsi che le impostazioni internazionali del browser corrispondano alle impostazioni internazionali del modulo. Ad esempio, se il modulo è tradotto in tedesco(de), impostare le impostazioni internazionali del browser su Tedesco(de).
   >* I componenti per moduli adattivi non supportano le lingue RTL (da destra a sinistra). Per esempio, l&#39;ebraico.


   Insieme al modulo adattivo, viene localizzato anche il documento di record generato automaticamente.

   Per ulteriori informazioni sulle impostazioni e sulla configurazione del documento di record, vedere:

   [Configurazione modello del documento record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Impostazioni del documento di registrazione](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizza le informazioni di branding del documento del ](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) record e assicurati che le impostazioni internazionali del browser siano impostate sulla stessa lingua in cui hai localizzato il modulo adattivo utilizzando la lingua della macchina. Le impostazioni internazionali del browser consentono di localizzare le informazioni sul marchio nel documento di registrazione.
1. Per visualizzare il documento localizzato del record, toccare Genera anteprima. Il documento PDF del record viene generato e aperto in una nuova scheda nel browser.

## Localizzazione di un modulo adattivo e del relativo documento di registrazione utilizzando la traduzione umana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Nella traduzione umana il contenuto viene inviato ad un fornitore di traduzione e tradotto da traduttori professionisti. Una volta completato, il contenuto tradotto viene restituito e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.

Per la traduzione, un dizionario contenente file in formato XLIFF viene condiviso con i traduttori professionisti. Il dizionario include un file XLIFF separato per ogni impostazione internazionale. Ogni file XLIFF contiene testo che verrà visualizzato agli utenti finali e ai segnaposto per il testo localizzato corrispondente.

Esegui i seguenti passaggi per localizzare un modulo e il relativo documento di registrazione utilizzando Human Translators:

1. [Collega AEM al tuo ](/help/sites-administering/tc-tic.md) provider di servizi di traduzione e  [crea configurazioni](/help/sites-administering/tc-tic.md) del framework di integrazione della traduzione.

1. [Associa le pagine del tuo ](/help/sites-administering/tc-tic.md) masterizzatore di linguaggio alle configurazioni del servizio di traduzione e del framework.

1. [Identifica il tipo di ](/help/sites-administering/tc-rules.md) contenuto da tradurre.

1. [Prepara il contenuto per la ](/help/sites-administering/tc-prep.md) traduzione creando il master lingua e le pagine principali delle copie della lingua.

1. [Crea progetti di traduzione per ](/help/sites-administering/tc-manage.md) raccogliere i contenuti da tradurre e preparare il processo di traduzione.

1. Utilizza i progetti di traduzione per [gestire il processo di traduzione dei contenuti](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* I componenti per moduli adattivi non supportano le lingue RTL (da destra a sinistra). Per esempio, l&#39;ebraico.

>



