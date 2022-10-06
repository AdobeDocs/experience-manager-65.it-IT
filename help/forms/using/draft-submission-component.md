---
title: Componente Bozze e invii
seo-title: Drafts and submissions component
description: Il componente Bozze e invii elenca i moduli che si trovano nello stato di bozza e che sono già inviati. Puoi personalizzare l’aspetto e lo stile del componente.
seo-description: Drafts and submissions component lists forms that are in the draft state and are already submitted. You can customize appearance and style of the component.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# Componente Bozze e invii{#drafts-and-submissions-component}

Il componente Bozze e invii elenca tutti i moduli in stato di bozza e i moduli già inviati. Il componente dispone di sezioni separate (schede) per le bozze e i moduli inviati. Gli utenti possono visualizzare solo le bozze e i moduli inviati.

## Configurazione del componente {#configuring-the-component}

Il componente Bozze e invii dispone di due schede: Bozze e invii.

Per abilitare l’invio di un modulo adattivo alla visualizzazione nella scheda Invii, impostare **Invia azione** a **[Azione di invio Forms Portal](../../forms/using/configuring-submit-actions.md). In alternativa,** abilitare l’opzione Invia di Forms Portal. Ogni volta che un utente invia il modulo, questo viene aggiunto alla scheda Invii.

La funzionalità delle bozze è abilitata come predefinita. Quando un utente fa clic su **Salva** in un modulo adattivo, il modulo viene aggiunto alla scheda bozze.

Esegui i seguenti passaggi per aggiungere e configurare un componente Bozze e invii:

1. Trascina e rilascia la **Bozze e invii** nella categoria Document Services del browser componenti sulla pagina.
1. Tocca il componente, quindi tocca ![settings_icon](assets/settings_icon.png) per aprire la finestra di dialogo Modifica per il componente.

   ![Componente Bozze e invio](assets/drafts-submissions-edit.png)

1. Nella finestra di dialogo Modifica , specifica i dettagli seguenti e tocca **Fine** per salvare le impostazioni.

<table>
 <tbody>
  <tr>
   <th>Tabulazione</th>
   <th>Configurazione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Generale</td>
   <td>Risultato totale</td>
   <td>Specifica il numero massimo di risultati da visualizzare. Se il conteggio dei risultati aumenta il limite di Risultato totale, un <strong>Altro </strong>il collegamento viene visualizzato nella parte inferiore del componente. Clic <strong>Altro </strong>mostra tutti i moduli. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo di stile</td>
   <td>Specifica lo stile del componente. Puoi specificare <strong>Nessuno stile</strong>, <strong>Stile predefinito</strong>oppure <strong>Stile personalizzato</strong> per elencare i moduli. Per l’opzione Stile personalizzato, puoi specificare il percorso del file CSS personalizzato nel <strong>Percorso stile personalizzato </strong>field<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Percorso stile personalizzato</td>
   <td>Se scegli <strong>Stile personalizzato</strong> in <strong>Tipo di stile</strong> campo , utilizza <strong>Percorso stile personalizzato</strong> per specificare il percorso del file CSS personalizzato. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opzioni di visualizzazione</td>
   <td><p>Specifica le schede da visualizzare. È possibile scegliere di visualizzare le bozze dei moduli, i moduli inviati o entrambi. </p> <p><strong>Nota</strong>:<em> Per <strong>Opzioni di visualizzazione</strong>, se selezioni un’opzione diversa da <strong>Entrambi</strong>, <strong>Scheda predefinita</strong> l’opzione campo non è utilizzata.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Scheda predefinita</td>
   <td>Specifica la scheda da visualizzare quando viene caricata la pagina del portale dei moduli. Puoi scegliere tra <strong>Scheda Forms bozza</strong> e <strong>Scheda Forms inviata</strong>.</td>
  </tr>
  <tr>
   <td>Configurazione della scheda Forms Bozza</td>
   <td>Titolo personalizzato</td>
   <td>Specifica il titolo del <strong>Bozza Forms</strong> scheda . Il valore predefinito è <strong>Bozza Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per l'elenco Bozza di Forms.</td>
  </tr>
  <tr>
   <td>Configurazione scheda Forms inviata</td>
   <td>Titolo personalizzato </td>
   <td>Specifica il titolo del <strong>Forms inviato </strong>scheda . Il valore predefinito è <strong>Forms inviato.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per l'invio di Forms<strong> </strong>elenco. </td>
  </tr>
 </tbody>
</table>

## Personalizzazione dello storage {#customizing-the-storage}

Quando si utilizza l’azione Invia di Forms Portal o si abilita l’opzione Archivia dati in forms portal in forma adattiva, i dati del modulo vengono memorizzati AEM archivio. In un ambiente di produzione, si consiglia di non archiviare le bozze o i dati del modulo inviati in AEM archivio. Per memorizzare le bozze e i dati dei moduli inviati, è invece necessario integrare le bozze e il componente di invio con un archivio protetto, ad esempio un database aziendale.

Il portale Forms consente di memorizzare i dati nell’archivio AEM locale, nell’archivio AEM remoto o in un database. AEM Forms consente di personalizzare l’implementazione della memorizzazione dei dati utente per bozze e invii. È possibile ignorare i metodi predefiniti per specificare la modalità di memorizzazione dei dati delle bozze e degli invii in un archivio di tua scelta. Ad esempio, puoi archiviare i dati in un archivio dati attualmente implementato nella tua organizzazione.

Il portale Forms fornisce servizi preconfigurati (API) per memorizzare i dati sull’archivio crx delle istanze di pubblicazione AEM Forms locali e remote. Puoi sostituire le implementazioni predefinite, descritte in [Configurazione dei servizi di archiviazione per bozze e invii](/help/forms/using/configuring-draft-submission-storage.md) con implementazioni personalizzate per sostituire la funzionalità predefinita. Per informazioni dettagliate sui metodi richiesti in un&#39;implementazione personalizzata per memorizzare il contenuto in una posizione protetta, consulta [Personalizzazione dei servizi di dati Bozza e Invio](/help/forms/using/custom-draft-submission-data-services.md) e [Archiviazione personalizzata per le bozze e i componenti inviati.](/help/forms/using/adding-custom-storage-provider-forms.md)

La documentazione di AEM Forms fornisce un [Esempio per l&#39;integrazione del componente bozze e invii con il database](integrate-draft-submission-database.md). Puoi utilizzare l’implementazione di esempio per sviluppare una tua implementazione personalizzata.

## Articoli correlati

* [Abilitare i componenti del portale moduli](/help/forms/using/enabling-forms-portal-components.md)
* [Pagina del portale dei moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare moduli in una pagina web utilizzando le API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usa componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per l&#39;integrazione del componente bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale dei moduli](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
