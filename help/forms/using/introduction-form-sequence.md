---
title: Introduzione a una sequenza di moduli con più fasi
seo-title: Introduzione a una sequenza di moduli con più fasi
description: Con  AEM Forms, è possibile definire una sequenza di pannelli di moduli in cui gli utenti possono navigare e compilare un modulo adattivo.
seo-description: Con  AEM Forms, è possibile definire una sequenza di pannelli di moduli in cui gli utenti possono navigare e compilare un modulo adattivo.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# Introduzione alla sequenza di moduli con più fasi{#introduction-to-multi-step-form-sequence}

I moduli adattivi consentono agli autori dei moduli di creare esperienze di acquisizione dei dati con più passaggi con grande facilità. Viene fornito con un supporto integrato per la creazione di più pannelli e l’associazione di ciascun pannello a diversi pattern di navigazione. Gli autori dei moduli possono raggruppare i campi modulo in sezioni logiche e rappresentare un gruppo come pannello. La navigazione tra i pannelli è controllata mediante il layout del pannello. Gli autori possono scegliere di disporre i pannelli in layout diversi, ad esempio per inserirli in sequenza con il layout Procedura guidata o in modo ad hoc utilizzando il layout a schede. Per informazioni sui layout dei pannelli, vedere [Funzionalità di layout dei moduli adattivi](../../forms/using/layout-capabilities-adaptive-forms.md).

In una tipica esperienza di compilazione dei moduli, sono necessari più passaggi rispetto all&#39;acquisizione dei dati. L&#39;invio completo del modulo può comprendere altri passaggi, ad esempio la firma digitale del modulo, la verifica delle informazioni compilate nel modulo, l&#39;elaborazione dei pagamenti e così via. È diverso da caso a caso.

Se il caso d&#39;uso richiede una serie di passaggi per l&#39;acquisizione dei dati o se è necessario seguire alcuni passaggi,  AEM Forms fornisce un modo per applicare tale struttura comune a tutti i moduli. L&#39;implementazione premeditata della struttura del modulo definisce la sequenza di passaggi per un modulo. ![Esempio di una sequenza di moduli con più fasi](assets/formpipeline.png)

Esempio di una sequenza di moduli con più fasi

Si consideri un caso d’uso in cui è necessario creare una sequenza per la compilazione, la verifica, la firma e i passaggi di conferma di un modulo. Per creare una sequenza di questo tipo, effettuate le seguenti operazioni:

1. Definire un modello di modulo e aggiungervi il pannello richiesto. Si noti che deve essere presente un pannello per ogni passaggio della sequenza. Tuttavia, potete includere pannelli secondari all’interno di un pannello.

   In questo esempio, è possibile aggiungere i seguenti pannelli:

   * **Riempimento**: Contiene campi per l&#39;acquisizione dei dati. Qui è possibile includere pannelli secondari nidificati per creare sezioni per diversi tipi di informazioni, ad esempio personali, familiari, finanziarie e così via.

   * **Verifica**: Contiene il componente  **** Verifycomponent che può essere utilizzato in un modulo adattivo basato su XFA. Visualizza le informazioni acquisite nel pannello Riempimento in modalità di sola lettura per la verifica.

   * **Firma** elettronica: Contiene il componente  **** Firma che può essere utilizzato in un modulo adattivo basato su XFA. fornisce i seguenti servizi di firma:

      * Servizi eSign di Adobe Document Cloud
      * Firma scarabocchio
   * **Conferma**: Contiene il componente  **** Riepilogo che visualizza un messaggio di conferma dell’invio del modulo dopo che l’utente ha firmato il modulo e ha raggiunto il passaggio Conferma (Riepilogo) nella sequenza. Gli autori possono configurare il testo del componente Riepilogo, visualizzare un messaggio di ringraziamento, visualizzare un collegamento al PDF generato e così via.


1. Selezionare il layout del pannello principale come **[!UICONTROL Procedura guidata]**.
1. Completare i passaggi successivi per creare il modello di modulo. Per ulteriori informazioni, vedere [Creazione di un modello di modulo adattivo personalizzato](../../forms/using/custom-adaptive-forms-templates.md).

Dopo aver definito la sequenza di moduli nel modello di modulo, è possibile utilizzarla per creare moduli con la struttura di base definita come sequenza in posizione, anche se è sempre possibile personalizzare il modulo in base alle proprie esigenze.

