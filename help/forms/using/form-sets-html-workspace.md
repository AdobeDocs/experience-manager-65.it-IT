---
title: Utilizzo dei set di moduli nell’area di lavoro di AEM Forms
description: Un set di moduli è un insieme di moduli di HTML5 raggruppati e presentati come un unico insieme di moduli agli utenti finali. Scopri come utilizzare i set di moduli nell’area di lavoro di AEM Forms.
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 8%
---
# Utilizzo dei set di moduli nell’area di lavoro di AEM Forms{#working-with-formsets-in-aem-forms-workspace}

Un set di moduli è un insieme di moduli di HTML5 raggruppati e presentati come un unico insieme di moduli agli utenti finali. Quando gli utenti finali iniziano a compilare un set di moduli, passano facilmente da un modulo all’altro. Il set di moduli può quindi essere inviato con un solo clic. Per ulteriori informazioni sui set di moduli e su come configurarli, vedere [Set di moduli in AEM Forms](../../forms/using/formset-in-aem-forms.md).

L’area di lavoro di AEM Forms supporta i set di moduli. Con i set di moduli, è possibile raggruppare più moduli relativi a un servizio o a un processo per automatizzare un processo aziendale e presentarli agli utenti finali. In questo caso, gli utenti possono compilare l’intero set in un’unica soluzione e non è necessario archiviare, inviare e tenere traccia di singoli moduli o processi.

## Associazione di un set di moduli al punto d’inizio in un’app dell’area di lavoro AEM Forms {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Crea il flusso di lavoro del processo aziendale in Workbench. Per ulteriori informazioni, vedere la [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_it).
1. Dalle proprietà di processo del punto iniziale, selezionare **Usa risorsa CRX** in Presentazione e dati.

   ![1-3](assets/1-3.png)

1. Fai clic su ![sfoglia](assets/browse.png) (Sfoglia) accanto al percorso della risorsa CRX. Viene visualizzata la finestra di dialogo Seleziona risorsa modulo.

   ![2-1](assets/2-1.png)

1. Fare clic sulla scheda **Set di moduli**, selezionare il set di moduli appropriato dall&#39;elenco, quindi fare clic su **OK**.

1. Distribuire l&#39;applicazione dopo l&#39;aggiornamento di altre proprietà di processo rilevanti.

## Utilizzo del set di moduli nell’area di lavoro di AEM Forms {#using-formset-in-nbsp-aem-forms-workspace}

Una volta collegato un set di moduli a un punto iniziale, quest’ultimo può essere richiamato dall’area di lavoro di AEM Forms, come qualsiasi altro punto iniziale.

Le operazioni supportate sul set di moduli tramite l’area di lavoro di AEM Forms sono:

* Salva come bozza
* Blocco
* Abbandona
* Invia
* Aggiungi allegati
* Aggiungi note
* Spostarsi tra le maschere di un set di maschere utilizzando i pulsanti Indietro o Avanti

![3-1](assets/3-1.png)

>[!NOTE]
>
>Per migliorare le prestazioni durante lo spostamento dai moduli precedenti e successivi in un set di moduli, tutti i pulsanti dell&#39;area di lavoro (Indietro, Avanti, Salva, Invia e Altro) vengono disattivati fino al completo rendering del modulo corrispondente.
