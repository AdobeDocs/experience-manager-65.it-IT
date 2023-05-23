---
title: Componente Bozze e invii
seo-title: Drafts and submissions component
description: Il componente Bozze e invii elenca i moduli che sono in stato Bozza e sono già stati inviati. Puoi personalizzare l’aspetto e lo stile del componente.
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

Il componente Bozze e invii elenca tutti i moduli in stato di bozza e quelli già inviati. Il componente dispone di sezioni (schede) separate per le bozze e i moduli inviati. Gli utenti possono visualizzare solo le bozze e i moduli inviati.

## Configurazione del componente {#configuring-the-component}

Il componente Bozze e invii dispone di due schede: Bozze e Invii.

Per consentire la visualizzazione dell’invio di un modulo adattivo nella scheda invii, imposta **Azione di invio** a **[Azione di invio Forms Portal](../../forms/using/configuring-submit-actions.md). In alternativa:** abilita l’opzione Invio di Forms Portal. Ogni volta che un utente invia il modulo, questo viene aggiunto alla scheda Invii.

La funzionalità delle bozze è attivata come funzionalità integrata. Quando un utente fa clic su **Salva** in un modulo adattivo, il modulo viene aggiunto alla scheda bozze.

Per aggiungere e configurare un componente Bozze e invii, effettua le seguenti operazioni:

1. Trascina la selezione **Bozze e invii** nella categoria Servizi basati su documenti, nel browser Componenti di sulla pagina.
1. Tocca il componente, quindi tocca ![icona_impostazioni](assets/settings_icon.png) per aprire la finestra di dialogo Modifica del componente.

   ![Componente Bozze e invio](assets/drafts-submissions-edit.png)

1. Nella finestra di dialogo Modifica, specifica i seguenti dettagli e tocca **Fine** per salvare le impostazioni.

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
   <td>Specifica il numero massimo di risultati da visualizzare. Se il conteggio dei risultati aumenta il limite dei risultati totali, viene <strong>Altro </strong>nella parte inferiore del componente. Clic <strong>Altro </strong>mostra tutti i moduli. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo di stile</td>
   <td>Specifica lo stile del componente. È possibile specificare <strong>Nessuno stile</strong>, <strong>Stile predefinito</strong>, o <strong>Stile personalizzato</strong> per l’elenco dei moduli. Per l’opzione Stile personalizzato, puoi specificare il percorso del file CSS personalizzato nel file <strong>Percorso stile personalizzato </strong>campo<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Percorso stile personalizzato</td>
   <td>Se si sceglie <strong>Stile personalizzato</strong> opzione in <strong>Tipo di stile</strong> , utilizza il <strong>Percorso stile personalizzato</strong> per specificare il percorso del file CSS personalizzato. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opzioni di visualizzazione</td>
   <td><p>Specifica le schede da visualizzare. È possibile scegliere di visualizzare i moduli bozza, i moduli inviati o entrambi. </p> <p><strong>Nota</strong>:<em> Per <strong>Opzioni di visualizzazione</strong>, se selezioni un’opzione diversa da <strong>Entrambi</strong>, il <strong>Scheda predefinita</strong> opzione di campo non utilizzata.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Scheda predefinita</td>
   <td>Specifica la scheda da visualizzare al caricamento della pagina del portale dei moduli. Puoi scegliere tra <strong>Scheda Bozza di Forms</strong> e <strong>Scheda Forms inviata</strong>.</td>
  </tr>
  <tr>
   <td>Bozza configurazione scheda Forms</td>
   <td>Titolo personalizzato</td>
   <td>Specifica il titolo del <strong>Bozza di Forms</strong> scheda. Il valore predefinito è <strong>Draft Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per l'elenco Bozza di Forms.</td>
  </tr>
  <tr>
   <td>Configurazione scheda Forms inviata</td>
   <td>Titolo personalizzato </td>
   <td>Specifica il titolo del <strong>Forms inviato </strong>scheda. Il valore predefinito è <strong>Inviato Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per il Forms inviato<strong> </strong>elenco. </td>
  </tr>
 </tbody>
</table>

## Personalizzazione dello storage {#customizing-the-storage}

Quando si utilizza l’azione di invio Forms Portal o si abilita l’opzione Memorizza dati nel portale dei moduli in un modulo adattivo, i dati del modulo vengono memorizzati nell’archivio AEM. In un ambiente di produzione, si consiglia di non memorizzare i dati delle bozze o dei moduli inviati nell’archivio AEM. Per memorizzare le bozze e i dati dei moduli inviati, è necessario integrare il componente bozze e invio con un archivio sicuro come il database aziendale.

Il portale Forms consente di memorizzare i dati nell&#39;archivio AEM locale, nell&#39;archivio AEM remoto o in un database. AEM Forms consente di personalizzare l’implementazione della memorizzazione dei dati utente per le bozze e gli invii. È possibile sovrascrivere i metodi predefiniti per specificare in che modo i dati relativi a bozze e invii vengono memorizzati in un archivio scelto. Ad esempio, puoi archiviare i dati in un archivio dati attualmente implementato nella tua organizzazione.

Forms portal fornisce servizi pronti all’uso (API) per memorizzare i dati sull’archivio crx delle istanze di pubblicazione AEM Forms locali e remote. Puoi sostituire le implementazioni predefinite, descritte in [Configurazione dei servizi di archiviazione per le bozze e gli invii](/help/forms/using/configuring-draft-submission-storage.md) con implementazioni personalizzate per sostituire le funzionalità predefinite. Per informazioni dettagliate sui metodi necessari in un’implementazione personalizzata per memorizzare il contenuto in una posizione protetta, consulta [Personalizzazione dei servizi dati per bozze e invii](/help/forms/using/custom-draft-submission-data-services.md) e [Archiviazione personalizzata per il componente Bozze e invii.](/help/forms/using/adding-custom-storage-provider-forms.md)

La documentazione di AEM Forms fornisce [Esempio per integrare il componente Bozze e invii con il database](integrate-draft-submission-database.md). Puoi utilizzare l’implementazione di esempio per sviluppare un’implementazione personalizzata.

## Articoli correlati

* [Abilitare i componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md)
* [Crea pagina portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare moduli su una pagina web utilizzando API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utilizzare il componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale Forms](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
