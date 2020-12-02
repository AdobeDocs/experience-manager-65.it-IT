---
title: Componenti Bozze e invii
seo-title: Componenti Bozze e invii
description: Le bozze e i componenti di invio elencano i moduli che si trovano nello stato bozza e che sono già stati inviati. Potete personalizzare l’aspetto e lo stile del componente.
seo-description: Le bozze e i componenti di invio elencano i moduli che si trovano nello stato bozza e che sono già stati inviati. Potete personalizzare l’aspetto e lo stile del componente.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
translation-type: tm+mt
source-git-commit: 23252989bb8649b2f0b96a58972c831257e0c5dc
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# Componente Bozze e invii{#drafts-and-submissions-component}

Il componente Bozze e invii elenca tutti i moduli che si trovano nello stato bozza e i moduli che sono già stati inviati. Il componente dispone di sezioni (schede) distinte per le bozze e i moduli inviati. Gli utenti possono visualizzare solo le bozze e i moduli inviati.

## Configurazione del componente {#configuring-the-component}

Il componente Bozze e invii dispone di due schede: Bozze e invii.

Per abilitare l&#39;invio di un modulo adattivo nella scheda di invio, impostare l&#39;azione **Invia** su **[Forms Portal Submit Action](../../forms/using/configuring-submit-actions.md). In alternativa,** abilitare l&#39;opzione di invio di Forms Portal. Ogni volta che un utente invia il modulo, quest&#39;ultimo viene aggiunto alla scheda di invio.

La funzionalità delle bozze è attivata automaticamente. Quando un utente fa clic su **Salva** in un modulo adattivo, il modulo viene aggiunto alla scheda delle bozze.

Per aggiungere e configurare un componente Bozze e invii, effettuate le seguenti operazioni:

1. Trascinare il componente **Bozze e invii** nella categoria Document Services del browser Componenti sulla pagina.
1. Toccate il componente, quindi toccate ![settings_icon](assets/settings_icon.png) per aprire la finestra di dialogo Modifica per il componente.

   ![Bozze e invio, componente](assets/drafts-submissions-edit.png)

1. Nella finestra di dialogo Modifica, specificate i seguenti dettagli e toccate **Fine** per salvare le impostazioni.

<table>
 <tbody>
  <tr>
   <th>Scheda</th>
   <th>Configurazione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Generale</td>
   <td>Risultato totale</td>
   <td>Specifica il numero massimo di risultati da visualizzare. Se il conteggio dei risultati aumenta il limite del risultato totale, nella parte inferiore del componente viene visualizzato un collegamento <strong>Altro </strong>collegamento. Facendo clic su <strong>Altro </strong>vengono visualizzati tutti i moduli. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo di stile</td>
   <td>Specifica lo stile del componente. Per elencare i moduli è possibile specificare <strong>No Style</strong>, <strong>Default Style</strong> o <strong>Custom Style</strong>. Per l'opzione Stile personalizzato, potete specificare il percorso del file CSS personalizzato nel <strong>Percorso stile personalizzato </strong>campo<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Percorso stile personalizzato</td>
   <td>Se scegliete l'opzione <strong>Stile personalizzato</strong> nel campo <strong>Tipo di stile</strong>, utilizzate il campo <strong>Percorso stile personalizzato</strong> per specificare il percorso del file CSS personalizzato. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opzioni di visualizzazione</td>
   <td><p>Specifica le schede da visualizzare. È possibile scegliere di visualizzare le bozze, i moduli inviati o entrambi. </p> <p><strong>Nota</strong>:<em> per le opzioni <strong> </strong>Visualizzazione, se selezionate un'opzione diversa da  <strong>Entrambe</strong>, l'opzione  <strong>Predefinito </strong> campo di tabulazione non viene utilizzata.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Scheda Predefinita</td>
   <td>Specifica la scheda da visualizzare quando viene caricata la pagina del portale dei moduli. È possibile scegliere tra <strong>Bozza scheda Forms</strong> e <strong>Scheda Forms inviata</strong>.</td>
  </tr>
  <tr>
   <td>Configurazione bozza scheda Forms</td>
   <td>Titolo personalizzato</td>
   <td>Specifica il titolo della scheda <strong>Bozza Forms</strong>. Il valore predefinito è <strong>Draft Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per l'elenco Forms Bozza.</td>
  </tr>
  <tr>
   <td>Configurazione scheda Forms inviata</td>
   <td>Titolo personalizzato </td>
   <td>Specifica il titolo della scheda <strong>Forms inviata </strong>. Il valore predefinito è <strong>Forms inviato.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per l'elenco Forms<strong> </strong>inviato. </td>
  </tr>
 </tbody>
</table>

## Personalizzazione dello storage {#customizing-the-storage}

Se si utilizza l&#39;azione di invio di Forms Portal o si abilita l&#39;opzione Archivia dati nel portale moduli in un modulo adattivo, i dati del modulo vengono memorizzati AEM archivio. In un ambiente di produzione, si consiglia di non memorizzare i dati delle bozze o dei moduli inviati AEM repository. Al contrario, è necessario integrare le bozze e il componente di invio con un archivio protetto come il database aziendale per memorizzare le bozze e i dati dei moduli inviati.

Il portale Forms consente di archiviare i dati AEM repository locale, AEM repository remoto o in un database.  AEM Forms consente di personalizzare l’implementazione della memorizzazione dei dati utente per bozze e invii. È possibile ignorare i metodi predefiniti per specificare il modo in cui i dati delle bozze e degli invii vengono memorizzati in un archivio di vostra scelta. Ad esempio, puoi archiviare i dati in un archivio dati attualmente implementato nell&#39;organizzazione.

Il portale Forms fornisce servizi out-of-box (API) per memorizzare i dati nell&#39;archivio crx delle istanze di pubblicazione AEM Forms locali e remote . È possibile sostituire le implementazioni predefinite, descritte in [Configurazione dei servizi di archiviazione per bozze e invii](/help/forms/using/configuring-draft-submission-storage.md), con implementazioni personalizzate per sostituire la funzionalità predefinita. Per informazioni dettagliate sui metodi richiesti in un&#39;implementazione personalizzata per memorizzare il contenuto in una posizione protetta, vedere [Customizing Draft and Submission data services](/help/forms/using/custom-draft-submission-data-services.md) e [Storage personalizzato per le bozze e i componenti di invio.](/help/forms/using/adding-custom-storage-provider-forms.md)

 documentazione AEM Forms fornisce un [Esempio per l&#39;integrazione di bozze e invii con database](integrate-draft-submission-database.md). Potete utilizzare l&#39;implementazione di esempio per sviluppare un&#39;implementazione personalizzata.

## Articoli correlati

* [Abilitare i componenti del portale moduli](/help/forms/using/enabling-forms-portal-components.md)
* [Pagina del portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare i moduli in una pagina Web utilizzando le API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzazione dell&#39;archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per l’integrazione del componente bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale moduli](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
