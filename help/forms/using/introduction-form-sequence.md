---
title: Introduzione alla sequenza di moduli a più passaggi
description: Con AEM Forms puoi definire una sequenza di pannelli dei moduli in cui gli utenti dovranno spostarsi e compilare un modulo adattivo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 26%

---

# Introduzione alla sequenza di moduli a più passaggi{#introduction-to-multi-step-form-sequence}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html) |
| AEM 6.5 | Questo articolo |


I moduli adattivi consentono agli autori di moduli di creare un’esperienza di acquisizione dati in più passaggi con grande facilità. Offre supporto integrato per la creazione di più pannelli e l’associazione di ciascun pannello a diversi pattern di navigazione. Gli autori dei moduli possono raggruppare i campi modulo in sezioni logiche e rappresentare un gruppo come pannello. La navigazione tra i pannelli viene controllata mediante il layout del pannello. Gli autori possono scegliere di disporre i pannelli in layout diversi, ad esempio posizionandoli in sequenza utilizzando il layout della procedura guidata o in modo ad hoc utilizzando il layout a schede. Per informazioni sui layout dei pannelli, consulta [Funzionalità di layout dei moduli adattivi](../../forms/using/layout-capabilities-adaptive-forms.md).

In una tipica esperienza di compilazione dei moduli, sono necessari più passaggi rispetto alla semplice acquisizione dei dati. L’invio completo di un modulo può includere altri passaggi, come la firma digitale del modulo, la verifica delle informazioni inserite nel modulo e l’elaborazione dei pagamenti. Si differenzia da caso a caso.

Se il caso d’uso richiede una serie di passaggi per l’acquisizione dei dati o esistono normative che richiedono determinati passaggi, AEM Forms fornisce un modo per applicare tale struttura comune nei moduli. L&#39;implementazione premeditata di una struttura di modulo definisce la sequenza di passaggi di un modulo. ![Esempio di sequenza di moduli a più passaggi](assets/formpipeline.png)

Esempio di sequenza di moduli a più passaggi

Prendiamo un caso d’uso in cui devi creare una sequenza per i passaggi di compilazione, verifica, firma e conferma di un modulo. Per creare una sequenza di questo tipo, effettuare le seguenti operazioni:

1. Definisci un modello di modulo e aggiungi il pannello richiesto. Dovrebbe essere disponibile un pannello per ogni passaggio della sequenza. Tuttavia, puoi includere pannelli secondari all’interno di un pannello.

   In questo esempio, è possibile aggiungere i pannelli seguenti:

   * **Riempimento**: contiene campi dei moduli per l’acquisizione dei dati. In questo caso, puoi includere pannelli secondari nidificati per creare sezioni per diversi tipi di informazioni, ad esempio personali, familiari e finanziarie.

   * **Verifica**: contiene il componente **Verifica** che può essere utilizzato in un modulo adattivo basato su XFA. Le informazioni acquisite nel pannello Riempimento vengono visualizzate in modalità di sola lettura per la verifica.

   * **E-sign**: contiene il componente **Sign** che può essere utilizzato in un modulo adattivo basato su XFA. fornisce i seguenti servizi di firma:

      * Servizi di firma elettronica di Adobe Document Cloud
      * Firma scarabocchio

   * **Conferma**: contiene il componente **Riepilogo** che visualizza un messaggio di conferma dell’invio del modulo dopo che un utente firma il modulo e raggiunge il passaggio Conferma (riepilogo) nella sequenza. Gli autori possono configurare il testo del componente Riepilogo, mostrare un messaggio di ringraziamento, mostrare un collegamento al PDF generato e così via.

1. Seleziona il layout del pannello principale come **[!UICONTROL Procedura guidata]**.
1. Completare i passaggi rimanenti per creare il modello di modulo. Consulta [Creazione di un modello di modulo adattivo personalizzato](../../forms/using/custom-adaptive-forms-templates.md).

Dopo aver definito la sequenza di moduli nel modello di modulo, è possibile utilizzarla per creare moduli con la struttura di base definita come sequenza. È sempre possibile personalizzare il modulo in base alle proprie esigenze.
