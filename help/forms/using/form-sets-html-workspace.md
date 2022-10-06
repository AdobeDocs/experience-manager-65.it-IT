---
title: Utilizzo dei set di moduli nell’area di lavoro di AEM Forms
seo-title: Working with Formsets in AEM Forms workspace
description: Un set di moduli è una raccolta di moduli di HTML5 raggruppati e presentati come un singolo set di moduli agli utenti finali. Scopri come utilizzare i set di moduli nell’area di lavoro di AEM Forms.
seo-description: A formset is a collection of HTML5 forms grouped and presented as a single set of forms to end users. Learn how you can work with formsets in AEM Forms workspace.
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 2%

---

# Utilizzo dei set di moduli nell’area di lavoro di AEM Forms{#working-with-formsets-in-aem-forms-workspace}

Un set di moduli è una raccolta di moduli di HTML5 raggruppati e presentati come un singolo set di moduli agli utenti finali. Quando gli utenti finali iniziano a compilare un set di moduli, passano facilmente da un modulo all’altro. Il set di moduli può quindi essere inviato con un solo clic. Per ulteriori informazioni sui set di moduli e su come configurarli, consulta [Set di moduli in AEM Forms](../../forms/using/formset-in-aem-forms.md).

AEM Forms Workspace supporta i set di moduli. Con i set di moduli, è possibile raggruppare più moduli relativi a un servizio o a un processo per automatizzare un processo aziendale e presentarli agli utenti finali. In questo caso, gli utenti possono compilare l’intero set come un unico set e non è necessario archiviare, inviare e tenere traccia dei singoli moduli o processi.

## Collegamento di un set di moduli da avviare in un’app dell’area di lavoro di AEM Forms {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Crea il flusso di lavoro del processo aziendale in Workbench. Per ulteriori informazioni, consulta [Aiuto per Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).
1. Dalle proprietà del processo del punto iniziale, seleziona **Utilizzare Una Risorsa CRX** in Presentazione e dati.

   ![1-3](assets/1-3.png)

1. Fai clic su ![navigare](assets/browse.png) (Sfoglia) accanto al percorso della risorsa CRX. Viene visualizzata la finestra di dialogo Seleziona risorsa modulo .

   ![2-1](assets/2-1.png)

1. Fai clic sul pulsante **Formset** selezionare il set di moduli appropriato dall’elenco, quindi fare clic su **OK**.

1. Distribuisci l&#39;applicazione dopo aver aggiornato altre proprietà di processo rilevanti.

## Utilizzo del set di moduli nell’area di lavoro di AEM Forms {#using-formset-in-nbsp-aem-forms-workspace}

Una volta collegato un set di moduli a un punto iniziale, è possibile richiamare il punto iniziale, come viene richiamato qualsiasi altro punto iniziale, dall’area di lavoro di AEM Forms.

Le operazioni supportate sui moduli impostati tramite l’area di lavoro di AEM Forms sono le seguenti:

* Salva come bozza
* Blocca
* Abbandona
* Invia
* Aggiungi allegati
* Aggiungi note
* Spostarsi tra i moduli di un set di moduli utilizzando i pulsanti Indietro o Avanti

![3-1](assets/3-1.png)

>[!NOTE]
>
>Per migliorare le prestazioni durante lo spostamento dai moduli precedenti e successivi di un set di moduli, tutti i pulsanti dell’area di lavoro (Indietro, Avanti, Salva, Invia e ... (Altro)) sono disabilitati fino al rendering completo del modulo corrispondente.
