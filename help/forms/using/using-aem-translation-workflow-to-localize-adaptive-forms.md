---
title: Utilizzo AEM flusso di lavoro di traduzione per localizzare moduli adattivi e documenti di registrazione
seo-title: Utilizzo AEM flusso di lavoro di traduzione per localizzare moduli adattivi e documenti di registrazione
description: Scoprite come utilizzare AEM flussi di lavoro di traduzione per localizzare moduli adattivi e documenti di registrazione.
seo-description: Scoprite come utilizzare AEM flussi di lavoro di traduzione per localizzare moduli adattivi e documenti di registrazione.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---


# Utilizzo AEM flusso di lavoro di traduzione per localizzare moduli adattivi e documenti di record {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

I moduli localizzati consentono di distribuire un pubblico più ampio su più aree geografiche. Il flusso di lavoro di traduzione di Adobe Experience Manager consente di localizzare i moduli adattivi e i relativi documenti da record. È possibile utilizzare **traduzione automatica** o **traduttori umani** per localizzare un modulo adattivo.

In questo articolo viene illustrato come utilizzare AEM flusso di lavoro di traduzione con moduli adattivi e documenti di registrazione.

## Localizzazione di un modulo adattivo e di un documento di registrazione mediante traduzione automatica {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Il servizio di traduzione automatica traduce immediatamente il contenuto in forma adattiva e nel documento di registrazione.  AEM Forms è preconfigurato per utilizzare una versione di prova di Microsoft Translator per la traduzione automatica. Per abilitare la traduzione automatica per i moduli adattivi e il documento di record, procedere come segue:

1. Nell&#39;interfaccia  di AEM Forms, selezionare un modulo e toccare l&#39;opzione **Aggiungi dizionario**.
1. Nella schermata **Aggiungi dizionario al progetto di traduzione**, selezionare l&#39;opzione **Crea un nuovo progetto di traduzione** o **Aggiungi a un progetto di traduzione esistente**.
1. Nel campo **Titolo progetto**, specificate il titolo. Esempio, `Government Reference Site - German locale.`
1. Nel campo **Lingue di destinazione**, specificare una lingua (ad esempio, `German(de)`), quindi fare clic su **Fine**. Potete specificare più impostazioni internazionali. Il modulo viene convertito in tutte le impostazioni internazionali specificate nel campo **Lingue di destinazione**.
1. Nella finestra di dialogo Dizionario aggiunto, fare clic su **Apri progetti**. Nella schermata Progetti, aprite il progetto appena creato.
1. Fare clic sulle **ellissi** nella parte inferiore della sezione **Riepilogo traduzione**. Viene visualizzata la schermata Riepilogo conversione.
1. Fare clic sull&#39;icona **Edit** nella parte superiore della schermata **Translation Summary**. Aprire la scheda **Traduzione** e selezionare Traduzione automatica nella schermata **Metodo di traduzione**. Selezionare il **Provider di traduzione** e **Configurazione cloud** appropriato. Fate clic sull&#39;icona **Done** nella parte superiore dello schermo.
1. Nella sezione **Processo di traduzione**, fare clic sull&#39;icona ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e fare clic su **Start**. Lo stato della sezione diventa Bozza. Al termine della traduzione, lo stato cambia in **Pronto per la revisione**. Aggiorna la pagina dopo alcuni minuti e verifica lo stato.
1. Dopo che lo stato è stato modificato in **Pronto per la revisione** nella sezione **Processo di traduzione**, aprire il modulo in una finestra del browser. Viene visualizzata una versione localizzata del modulo.

   >[!NOTE]
   >
   >* Prima di aprire la versione localizzata del modulo nella finestra del browser, assicurarsi che le impostazioni internazionali del browser siano impostate in modo che corrispondano alle impostazioni internazionali del modulo. Ad esempio, se il modulo è tradotto in tedesco(de) language, impostare le impostazioni internazionali del browser su Tedesco(de).
   >* I componenti per moduli adattivi non supportano i linguaggi RTL (Right to Left). Ad esempio, ebraico.


   Insieme al modulo adattivo, anche il documento di record generato automaticamente viene localizzato.

   Per ulteriori informazioni sulle impostazioni e sulla configurazione del documento di registrazione, vedi:

   [Configurazione modello del documento record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Impostazioni del documento di registrazione](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizzare le informazioni di branding del documento di ](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) registrazione e assicurarsi che le impostazioni internazionali del browser siano impostate sulla stessa lingua in cui è stato localizzato il modulo adattivo utilizzando la lingua del computer. Le impostazioni internazionali del browser consentono di localizzare le informazioni sul marchio nel documento di registrazione.
1. Per visualizzare il documento localizzato del record, toccate Genera anteprima. Il documento PDF del record viene generato e aperto in una nuova scheda del browser.

## Localizzazione di un modulo adattivo e del relativo documento di registrazione mediante la traduzione umana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Traduzione Umana il contenuto viene inviato a un fornitore di traduzioni e tradotto da traduttori professionisti. Al termine, il contenuto convertito viene restituito e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.

Per la traduzione, un dizionario contenente file in formato XLIFF è condiviso con i traduttori professionisti. Il dizionario include un file XLIFF separato per ciascuna lingua. Ciascun file XLIFF contiene testo che verrà visualizzato agli utenti finali e ai segnaposto per il testo localizzato corrispondente.

Effettuare le seguenti operazioni per localizzare un modulo e il relativo documento di registrazione utilizzando l&#39;espressione Traduttori umani:

1. [Collega AEM al ](/help/sites-administering/tc-tic.md) provider del servizio di traduzione e  [crea configurazioni](/help/sites-administering/tc-tic.md) del framework di integrazione delle traduzioni.

1. [Associate le pagine del vostro ](/help/sites-administering/tc-tic.md) maestro di lingua alle configurazioni del servizio di traduzione e del framework.

1. [Identificare il tipo di ](/help/sites-administering/tc-rules.md) contenuto da tradurre.

1. [Preparate il contenuto per la ](/help/sites-administering/tc-prep.md) traduzione creando il master della lingua e le pagine principali delle copie della lingua.

1. [Create ](/help/sites-administering/tc-manage.md) progetti di traduzione per raccogliere il contenuto da tradurre e preparare il processo di traduzione.

1. Utilizzate i progetti di traduzione per [gestire il processo di traduzione del contenuto](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* I componenti per moduli adattivi non supportano i linguaggi RTL (Right to Left). Ad esempio, ebraico.

>



