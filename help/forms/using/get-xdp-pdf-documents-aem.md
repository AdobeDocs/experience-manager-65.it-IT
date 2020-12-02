---
title: Ottenimento di documenti XDP e PDF in  AEM Forms
seo-title: Ottenimento di documenti XDP e PDF in  AEM Forms
description: ' AEM Forms consente di caricare moduli e risorse supportate da utilizzare con i moduli adattivi. È inoltre possibile caricare in massa moduli e risorse correlate come file ZIP.'
seo-description: ' AEM Forms consente di caricare moduli e risorse supportate da utilizzare con i moduli adattivi. È inoltre possibile caricare in massa moduli e risorse correlate come file ZIP.'
uuid: cd49b4a8-c282-4059-95a0-c98f6c92ab14
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 28b9f1d6-6a52-458f-a8ed-a206502eda0d
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---


# Ottenimento di documenti XDP e PDF in  AEM Forms{#getting-xdp-and-pdf-documents-in-aem-forms}

## Panoramica {#overview}

È possibile importare i moduli dal file system locale nell&#39;archivio CRX, caricandoli in  AEM Forms. L’operazione di caricamento è supportata per i seguenti tipi di risorse:

* Modelli per moduli (moduli XFA)
* PDF forms
* Documento (documenti PDF semplici)

Potete caricare i tipi di risorse supportati singolarmente o come archivio ZIP. Potete caricare una risorsa di tipo `Resource`, solo accanto a un modulo XFA in un archivio ZIP.

>[!NOTE]
>
>Assicuratevi di essere membri del gruppo `form-power-users` per poter caricare i file XDP. Contattate l’amministratore per diventare membro del gruppo.

## Caricamento di moduli {#uploading-forms}

1. Accedete all&#39;interfaccia utente  AEM Forms accedendo a `https://'[server]:[port]'/aem/forms.html`.
1. Passare alla cartella in cui si desidera caricare il modulo o la cartella che contiene i moduli.
1. Nella barra degli strumenti delle azioni, toccate **Crea > Caricamento file**.

   ![File dall&#39;opzione di archiviazione locale in Crea](assets/step.png)

1. La finestra di dialogo Carica moduli o pacchetti consente di individuare e scegliere il file da caricare. Nel browser dei file vengono visualizzati solo i formati di file supportati (ZIP, XDP e PDF).

   >[!NOTE]
   >
   >Un nome file può contenere solo caratteri alfanumerici, trattini o caratteri di sottolineatura.

1. Fate clic su Carica dopo la selezione del file per caricare i file oppure su Annulla per annullare il caricamento. Un elenco a comparsa elenca le risorse aggiunte e quelle aggiornate nella posizione corrente.

   >[!NOTE]
   >
   >Per un file ZIP, vengono visualizzati i percorsi relativi di tutte le risorse supportate. Le risorse non supportate all&#39;interno dello ZIP vengono ignorate e non sono elencate. Tuttavia, se l&#39;archivio ZIP contiene solo le risorse non supportate, al posto della finestra di dialogo a comparsa viene visualizzato un messaggio di errore.

   ![Finestra di dialogo Carica durante il caricamento di un modulo XFA](assets/upload-scr.png)

1. Se una o più risorse hanno un nome file non valido, viene visualizzato un errore. Correggete i nomi dei file evidenziati in rosso e ricaricate.

   ![Messaggio di errore durante il caricamento di un modulo XFA](assets/upload-scr-err.png)

Al termine del caricamento, un flusso di lavoro in background genera le miniature per ciascuna risorsa, in base all’anteprima della risorsa. Le versioni più recenti delle risorse, se caricate, ignorano le risorse esistenti.

### Modalità protetta {#protected-mode}

 server AEM Forms consente di eseguire il codice JavaScript. Un codice JavaScript dannoso può danneggiare un ambiente AEM Forms . La modalità protetta limita  AEM Forms all&#39;esecuzione di file XDP solo da risorse e posizioni affidabili. Tutti i file XDP disponibili nell’interfaccia  AEM Forms sono considerati risorse affidabili.

Per impostazione predefinita, la modalità protetta è attivata. Se necessario, potete disattivare la modalità protetta:

1. Accedete AEM console Web come amministratore. L&#39;URL è https://&#39;[server]:[porta]&#39;/system/console/configMgr
1. Aprire le configurazioni Forms per dispositivi mobili per la modifica.
1. Deselezionare l&#39;opzione Modalità protetta e fare clic su **Salva**. La modalità protetta è disabilitata.

## Aggiornamento dei moduli XFA di riferimento {#updating-referenced-xfa-forms}

In  AEM Forms, è possibile fare riferimento a un modello di modulo XFA in un modulo adattivo o in un altro modello di modulo XFA. Inoltre, un modello può fare riferimento a una risorsa o a un altro modello XFA.

I campi di un modulo adattivo che fa riferimento a un XFA sono associati ai campi disponibili in XFA. Quando si aggiorna un modello di modulo, il modulo adattivo associato tenta di eseguire la sincronizzazione con XFA. Per ulteriori dettagli, vedere [Sincronizzazione dei moduli adattivi con l&#39;XFA](../../forms/using/synchronizing-adaptive-forms-xfa.md) associato.

La rimozione di un modello di modulo danneggia il modulo adattivo o il modello di modulo dipendente. Tale modulo adattivo viene talvolta definito informalmente come un modulo non corretto.  interfaccia utente di AEM Forms, è possibile individuare i moduli sporchi in due modi.

* Quando si posiziona il puntatore sull’icona di avviso, viene visualizzata un’icona di avviso sulla miniatura del modulo adattivo nell’elenco delle risorse.\
   `Schema/Form Template for this adaptive form has been updated so please go to Authoring mode and rebase it with new version.`

![Avviso per un modulo adattivo non sincronizzato dopo l&#39;aggiornamento dell&#39;XFA associato](assets/dirtyaf.png)

Viene mantenuto un flag per indicare se un modulo adattivo è sporco. Queste informazioni sono disponibili nella pagina delle proprietà del modulo, insieme ai metadati del modulo. Solo per i moduli adattivi sporchi, una proprietà di metadati `Model Refresh` visualizza il valore `Recommended`.

![Indicazione di un modulo adattivo non sincronizzato con il modello XFA](assets/model-refresh.png)

