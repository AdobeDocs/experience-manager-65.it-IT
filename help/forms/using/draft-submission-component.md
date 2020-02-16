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

---


# Componenti Bozze e invii{#drafts-and-submissions-component}

Il componente Bozze e invii elenca tutti i moduli che si trovano nello stato bozza e i moduli che sono già stati inviati. Il componente dispone di sezioni (schede) distinte per le bozze e i moduli inviati. Gli utenti possono visualizzare solo le bozze e i moduli inviati.

## Configurazione del componente {#configuring-the-component}

Il componente Bozze e invii dispone di due schede: Bozze e invii.

Per abilitare l&#39;invio di un modulo adattivo nella scheda di invio, impostare l&#39;azione **** Invia su Azione **[di invio](../../forms/using/configuring-submit-actions.md)Forms Portal. In alternativa,**abilitare l&#39;opzione di invio Forms Portal. Ogni volta che un utente invia il modulo, il modulo viene aggiunto alla scheda di invio.

La funzionalità delle bozze è attivata automaticamente. Quando un utente fa clic su **Salva** su un modulo adattivo, il modulo viene aggiunto alla scheda delle bozze.

Per aggiungere e configurare un componente Bozze e invii, effettuate le seguenti operazioni:

1. Trascinare il componente **Bozze e invii** nella categoria Document Services del Browser componenti sulla pagina.
1. Toccate il componente, quindi toccate ![settings_icon](assets/settings_icon.png) per aprire la finestra di dialogo Modifica per il componente.

   ![Bozze e invio, componente](assets/drafts-submissions-edit.png)

1. Nella finestra di dialogo Modifica, specificate i dettagli seguenti e toccate **Fine** per salvare le impostazioni.

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
   <td>Specifica il numero massimo di risultati da visualizzare. Se il conteggio dei risultati aumenta il limite del risultato totale, nella parte inferiore del componente viene visualizzato un <strong>altro </strong>collegamento. Facendo clic su <strong>Altro </strong>vengono visualizzati tutti i moduli. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo di stile</td>
   <td>Specifica lo stile del componente. È possibile specificare <strong>Nessuno stile</strong>, Stile <strong></strong>predefinito o Stile <strong></strong> personalizzato per elencare i moduli. Per l'opzione Stile personalizzato, potete specificare il percorso del file CSS personalizzato nel <strong>campo </strong>Percorso stile<strong>personalizzato.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Percorso stile personalizzato</td>
   <td>Se scegliete l'opzione Stile <strong></strong> personalizzato nel campo Tipo <strong>di</strong> stile, utilizzate il campo Percorso <strong>stile</strong> personalizzato per specificare il percorso del file CSS personalizzato. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opzioni di visualizzazione</td>
   <td><p>Specifica le schede da visualizzare. È possibile scegliere di visualizzare le bozze, i moduli inviati o entrambi. </p> <p><strong></strong> Nota<em>: Per le opzioni <strong>di</strong>visualizzazione, se si seleziona un'opzione diversa da <strong>Entrambe</strong>, non viene utilizzata l'opzione Campo tabulazione <strong></strong> predefinito.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Scheda Predefinita</td>
   <td>Specifica la scheda da visualizzare al caricamento della pagina del portale dei moduli. È possibile scegliere tra la scheda <strong>Moduli</strong> bozza e la scheda <strong>Moduli</strong>inviati.</td>
  </tr>
  <tr>
   <td>Configurazione scheda Moduli bozza</td>
   <td>Titolo personalizzato</td>
   <td>Specifica il titolo della scheda Moduli <strong></strong> bozza. Il valore predefinito è <strong>Bozza moduli.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per l'elenco Moduli bozza.</td>
  </tr>
  <tr>
   <td>Configurazione scheda Moduli inviati</td>
   <td>Titolo personalizzato </td>
   <td>Specifica il titolo della <strong>scheda Moduli </strong>inviati. Il valore predefinito è Moduli <strong>inviati.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per l'<strong> elenco Moduli </strong>inviati. </td>
  </tr>
 </tbody>
</table>

## Personalizzazione dello storage {#customizing-the-storage}

Quando si utilizza l&#39;azione di invio di Forms Portal o si abilita l&#39;opzione Archivia dati nel portale moduli in un modulo adattivo, i dati del modulo vengono memorizzati nell&#39;archivio di AEM. In un ambiente di produzione, si consiglia di non memorizzare i dati delle bozze o dei moduli inviati nell&#39;archivio AEM. Al contrario, è necessario integrare le bozze e il componente di invio con un archivio protetto come il database aziendale per memorizzare le bozze e i dati dei moduli inviati.

Il portale Forms consente di archiviare i dati nell’archivio locale di AEM, nell’archivio remoto di AEM o in un database. AEM Forms consente di personalizzare l’implementazione della memorizzazione dei dati utente per bozze e invii. È possibile ignorare i metodi predefiniti per specificare il modo in cui i dati delle bozze e degli invii vengono memorizzati in un archivio di vostra scelta. Ad esempio, puoi archiviare i dati in un archivio dati attualmente implementato nell&#39;organizzazione.

Il portale Forms offre servizi out-of-box (API) per memorizzare i dati nell&#39;archivio crx delle istanze di pubblicazione locali e remote di AEM Forms. È possibile sostituire le implementazioni predefinite, descritte in [Configurazione dei servizi di archiviazione per le bozze e gli invii](/help/forms/using/configuring-draft-submission-storage.md) articolo, con implementazioni personalizzate per sostituire la funzionalità predefinita. Per informazioni dettagliate sui metodi richiesti in un&#39;implementazione personalizzata per memorizzare il contenuto in una posizione protetta, vedere [Personalizzazione dei servizi](/help/forms/using/custom-draft-submission-data-services.md) dati Bozza e Invio e Archiviazione [personalizzata per le bozze e i componenti di invio.](/help/forms/using/adding-custom-storage-provider-forms.md)

La documentazione di AEM Forms fornisce un [esempio per l’integrazione del componente bozze e invii con il database](integrate-draft-submission-database.md). Potete utilizzare l&#39;implementazione di esempio per sviluppare un&#39;implementazione personalizzata.

## Articoli correlati

* [Abilitare i componenti del portale moduli](/help/forms/using/enabling-forms-portal-components.md)
* [Pagina del portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare i moduli in una pagina Web utilizzando le API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzazione dell&#39;archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per l’integrazione del componente bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale moduli](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
