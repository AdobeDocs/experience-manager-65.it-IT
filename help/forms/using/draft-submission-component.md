---
title: Componente Bozze e invii
description: Il componente Bozze e invii elenca i moduli che sono in stato Bozza e sono già stati inviati. Puoi personalizzare l’aspetto e lo stile del componente.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# Componente Bozze e invii{#drafts-and-submissions-component}

Il componente Bozze e invii elenca tutti i moduli in stato di bozza e quelli già inviati. Il componente dispone di sezioni (schede) separate per le bozze e i moduli inviati. Gli utenti possono visualizzare solo le bozze e i moduli inviati.

## Configurazione del componente {#configuring-the-component}

Il componente Bozze e invii dispone di due schede: Bozze e Invii.

Per abilitare l&#39;invio di un modulo adattivo nella scheda Invii, impostare **Azione invio** su **[Azione invio portale Forms](../../forms/using/configuring-submit-actions.md). In alternativa,** abilita l&#39;opzione di invio di Forms Portal. Ogni volta che un utente invia il modulo, questo viene aggiunto alla scheda Invii.

La funzionalità delle bozze è attivata come funzionalità integrata. Quando un utente fa clic su **Salva** in un modulo adattivo, il modulo viene aggiunto alla scheda delle bozze.

Per aggiungere e configurare un componente Bozze e invii, effettua le seguenti operazioni:

1. Trascina il componente **Bozze e invii** nella categoria Servizi basati su documenti nel browser componenti sulla pagina.
1. Seleziona il componente, quindi fai clic su ![settings_icon](assets/settings_icon.png) per aprire la finestra di dialogo Modifica del componente.

   ![Componente bozze e invio](assets/drafts-submissions-edit.png)

1. Nella finestra di dialogo Modifica, specifica i dettagli seguenti e seleziona **Fine** per salvare le impostazioni.

<table>
 <tbody>
  <tr>
   <th>Linguetta</th>
   <th>Configurazione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Generale</td>
   <td>Risultato totale</td>
   <td>Specifica il numero massimo di risultati da visualizzare. Se il conteggio dei risultati aumenta il limite di risultati totali, nella parte inferiore del componente viene visualizzato un collegamento <strong>Altro </strong>. Facendo clic su <strong>Altri </strong> vengono visualizzati tutti i moduli. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo di stile</td>
   <td>Specifica lo stile del componente. È possibile specificare <strong>Nessuno stile</strong>, <strong>Stile predefinito</strong> o <strong>Stile personalizzato</strong> per l'elenco dei moduli. Per l'opzione di stile personalizzato, puoi specificare il percorso del file CSS personalizzato nel <strong>campo Percorso di stile personalizzato </strong>campo<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Percorso stile personalizzato</td>
   <td>Se scegli l'opzione <strong>Stile personalizzato</strong> nel campo <strong>Tipo di stile</strong>, utilizza il campo <strong>Percorso di stile personalizzato</strong> per specificare il percorso del file CSS personalizzato. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opzioni di visualizzazione</td>
   <td><p>Specifica le schede da visualizzare. È possibile scegliere di visualizzare i moduli bozza, i moduli inviati o entrambi. </p> <p><strong>Nota</strong>:<em> Per <strong>Opzioni di visualizzazione</strong>, se selezioni un'opzione diversa da <strong>Entrambi</strong>, l'opzione di campo <strong>Linguetta predefinita</strong> non viene utilizzata.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Scheda predefinita</td>
   <td>Specifica la scheda da visualizzare al caricamento della pagina del portale dei moduli. Puoi scegliere tra <strong>Scheda Bozza di Forms</strong> e <strong>Scheda Forms inviata</strong>.</td>
  </tr>
  <tr>
   <td>Bozza configurazione scheda Forms</td>
   <td>Titolo personalizzato</td>
   <td>Specifica il titolo della scheda <strong>Bozza di Forms</strong>. Il valore predefinito è <strong>Bozza di Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per l'elenco Bozza di Forms.</td>
  </tr>
  <tr>
   <td>Configurazione scheda Forms inviata</td>
   <td>Titolo personalizzato </td>
   <td>Specifica il titolo della scheda </strong> di Forms <strong>Inviato. Il valore predefinito è <strong>Forms inviato.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Specifica il layout da utilizzare per l'elenco </strong> di Forms<strong> inviato. </td>
  </tr>
 </tbody>
</table>

## Personalizzazione dello storage {#customizing-the-storage}

Quando si utilizza l’azione di invio Forms Portal o si abilita l’opzione Memorizza dati nel portale dei moduli in un modulo adattivo, i dati del modulo vengono memorizzati nell’archivio AEM. In un ambiente di produzione, si consiglia di non memorizzare i dati delle bozze o dei moduli inviati nell’archivio AEM. Per memorizzare le bozze e i dati dei moduli inviati, è necessario integrare il componente bozze e invio con un archivio sicuro come il database aziendale.

Il portale Forms consente di archiviare i dati nell&#39;archivio AEM locale, nell&#39;archivio AEM remoto o in un database. AEM Forms consente di personalizzare l’implementazione della memorizzazione dei dati utente per le bozze e gli invii. È possibile sovrascrivere i metodi predefiniti per specificare in che modo i dati relativi a bozze e invii vengono memorizzati in un archivio scelto. Ad esempio, puoi archiviare i dati in un archivio dati attualmente implementato nella tua organizzazione.

Forms portal fornisce servizi pronti all’uso (API) per memorizzare i dati sull’archivio crx delle istanze di pubblicazione AEM Forms locali e remote. È possibile sostituire le implementazioni predefinite, descritte nell&#39;articolo [Configurazione dei servizi di archiviazione per le bozze e gli invii](/help/forms/using/configuring-draft-submission-storage.md), con implementazioni personalizzate per sostituire le funzionalità predefinite. Per informazioni dettagliate sui metodi necessari in un&#39;implementazione personalizzata per archiviare il contenuto in una posizione protetta, vedere [Personalizzazione dei servizi dati per bozze e invii](/help/forms/using/custom-draft-submission-data-services.md) e [Archiviazione personalizzata per le bozze e i componenti per invii.](/help/forms/using/adding-custom-storage-provider-forms.md)

La documentazione di AEM Forms fornisce un [esempio per integrare il componente Bozze e invii con il database](integrate-draft-submission-database.md). Puoi utilizzare l’implementazione di esempio per sviluppare un’implementazione personalizzata.

## Articoli correlati

* [Abilitare i componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md)
* [Crea pagina portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare moduli su una pagina web utilizzando API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utilizzare il componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale Forms](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
