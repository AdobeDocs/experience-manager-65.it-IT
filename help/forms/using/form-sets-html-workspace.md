---
title: Utilizzo dei set di moduli nell’area di lavoro Moduli AEM
seo-title: Utilizzo dei set di moduli nell’area di lavoro Moduli AEM
description: Un set di moduli è un insieme di moduli HTML5 raggruppati e presentati come un singolo set di moduli agli utenti finali. Scopri come utilizzare i set di moduli nell’area di lavoro Moduli AEM.
seo-description: Un set di moduli è un insieme di moduli HTML5 raggruppati e presentati come un singolo set di moduli agli utenti finali. Scopri come utilizzare i set di moduli nell’area di lavoro Moduli AEM.
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Utilizzo dei set di moduli nell’area di lavoro Moduli AEM{#working-with-formsets-in-aem-forms-workspace}

Un set di moduli è un insieme di moduli HTML5 raggruppati e presentati come un singolo set di moduli agli utenti finali. Quando gli utenti finali iniziano a compilare un set di moduli, si passa direttamente da un modulo all&#39;altro. Il set di moduli può essere inviato con un solo clic. Per ulteriori informazioni sui set di moduli e su come configurarli, consultate [Set di moduli in AEM Forms](../../forms/using/formset-in-aem-forms.md).

L&#39;area di lavoro Moduli AEM supporta i set di moduli. Con i formati, è possibile raggruppare più moduli relativi a un servizio o a un processo per automatizzare un processo aziendale e presentarli agli utenti finali. In questo caso, gli utenti possono compilare l&#39;intero set come un unico set e non è necessario archiviare, inviare e tenere traccia dei singoli moduli o processi.

## Collegamento di un set di moduli per iniziare in un’app dell’area di lavoro AEM Forms {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Creare il flusso di lavoro del processo aziendale in Workbench. Per ulteriori informazioni, vedere la Guida [di](https://www.adobe.com/go/learn_aemforms_workbench_63)Workbench.
1. Dalle proprietà del processo del punto di partenza, selezionate **Usa una risorsa** CRX in Presentazione e dati.

   ![1-3](assets/1-3.png)

1. Fate clic su ![Sfoglia](assets/browse.png) (Sfoglia) accanto al percorso della risorsa CRX. Viene visualizzata la finestra di dialogo Seleziona risorsa modulo.

   ![2-1](assets/2-1.png)

1. Fare clic sulla scheda **Set** di moduli, selezionare il set di moduli appropriato dall&#39;elenco, quindi fare clic su **OK**.

1. Distribuire l&#39;applicazione dopo l&#39;aggiornamento di altre proprietà di processo rilevanti.

## Utilizzo di formset nell&#39;area di lavoro Moduli AEM {#using-formset-in-nbsp-aem-forms-workspace}

Una volta che un set di moduli è collegato a un punto di avvio, è possibile richiamare il punto di avvio, come qualsiasi altro punto di avvio, dall&#39;area di lavoro Moduli AEM.

Le operazioni supportate dai moduli impostati nell’area di lavoro Moduli AEM sono:

* Salva come bozza
* Blocca
* Abbandona
* Invia
* Aggiungi allegati
* Aggiungi note
* Spostarsi tra i moduli in un set di moduli utilizzando i pulsanti Indietro e Avanti

![3-1](assets/3-1.png)

>[!NOTE]
>
>Per migliorare le prestazioni durante lo spostamento dai moduli precedenti e successivi in un set di moduli, tutti i pulsanti dell&#39;area di lavoro (Indietro, Avanti, Salva, Invia e ... (Altro)) vengono disattivati fino al completo rendering del modulo corrispondente.

