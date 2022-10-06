---
title: Introduzione alla sequenza di moduli a più passaggi
seo-title: Introduction to multi-step form sequence
description: Con AEM Forms è possibile definire una sequenza di pannelli di moduli in cui gli utenti devono navigare e compilare un modulo adattivo.
seo-description: With AEM Forms, you can define a sequence of form panel in which you want users to navigate and fill an adaptive form.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Introduzione alla sequenza di moduli a più passaggi{#introduction-to-multi-step-form-sequence}

I moduli adattivi consentono agli autori dei moduli di creare con grande facilità un’esperienza di acquisizione dati in più passaggi. Offre supporto integrato per la creazione di più pannelli e l’associazione di ciascun pannello a diversi pattern di navigazione. Gli autori dei moduli possono raggruppare i campi modulo in sezioni logiche e rappresentare un gruppo come pannello. La navigazione tra i pannelli viene controllata mediante il layout del pannello. Gli autori possono scegliere di disporre i pannelli in layout diversi, ad esempio per posizionarli in sequenza utilizzando il layout della procedura guidata o in modo ad hoc utilizzando il layout a schede. Per informazioni sui layout dei pannelli, consulta [Funzionalità di layout dei moduli adattivi](../../forms/using/layout-capabilities-adaptive-forms.md).

In una tipica esperienza di compilazione dei moduli, sono necessari più passaggi rispetto all’acquisizione dei dati. L’invio completo di un modulo può comprendere altri passaggi, ad esempio la firma digitale del modulo, la verifica delle informazioni inserite nel modulo, l’elaborazione dei pagamenti e così via. Si differenzia da caso a caso.

Se il tuo caso d’uso richiede una serie di passaggi per l’acquisizione dei dati o se sono previste normative che richiedono l’esecuzione di determinati passaggi, AEM Forms offre un modo per applicare tale struttura comune nei diversi moduli. L’implementazione premeditata della struttura del modulo definisce la sequenza di passaggi per un modulo. ![Esempio di sequenza di moduli a più passaggi](assets/formpipeline.png)

Esempio di sequenza di moduli a più passaggi

Prendiamo un caso d’uso in cui è necessario creare una sequenza per compilare, verificare, firmare e confermare i passaggi di un modulo. La procedura per creare una sequenza di questo tipo è la seguente:

1. Definire un modello di modulo e aggiungergli il pannello richiesto. Tieni presente che per ogni passaggio della sequenza deve essere presente un pannello. Tuttavia, puoi includere pannelli secondari all’interno di un pannello.

   In questo esempio, possiamo aggiungere i seguenti pannelli:

   * **Riempimento**: Contiene campi dei moduli per l’acquisizione dei dati. In questo caso puoi includere pannelli secondari nidificati per creare sezioni per diversi tipi di informazioni, ad esempio personali, familiari, finanziarie e così via.

   * **Verifica**: Contiene il **Verifica** che può essere utilizzato in un modulo adattivo basato su XFA. Visualizza le informazioni acquisite nel pannello Riempimento in modalità di sola lettura per la verifica.

   * **E-sign**: Contiene il **Sign** che può essere utilizzato in un modulo adattivo basato su XFA. fornisce i seguenti servizi di firma:

      * Servizi eSign di Adobe Document Cloud
      * Firma scarabocchio
   * **Conferma**: Contiene il **Riepilogo** che visualizza un messaggio di conferma dell’invio del modulo dopo che un utente firma il modulo e raggiunge il passaggio Conferma (riepilogo) nella sequenza. Gli autori possono configurare il testo del componente Riepilogo, visualizzare un messaggio di ringraziamento, visualizzare un collegamento al PDF generato e così via.


1. Seleziona il layout del pannello principale come **[!UICONTROL Creazione guidata]**.
1. Completare i passaggi successivi per creare il modello di modulo. Per ulteriori informazioni, consulta [Creazione di un modello di modulo adattivo personalizzato](../../forms/using/custom-adaptive-forms-templates.md).

Dopo aver definito la sequenza del modulo nel modello di modulo, è possibile utilizzarla per creare moduli che avranno la struttura di base definita come sequenza in posizione, anche se è sempre possibile personalizzare il modulo in base alle proprie esigenze.
