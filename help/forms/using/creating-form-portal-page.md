---
title: Creazione di una pagina del portale dei moduli
seo-title: Creating a forms portal page
description: Forms Portal fornisce agli sviluppatori web componenti per creare e personalizzare un portale di moduli su siti web creati con Adobe Experience Manager (AEM).
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 2%

---

# Creazione di una pagina del portale dei moduli{#creating-a-forms-portal-page}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | Questo articolo |

I componenti del portale Forms forniscono ai Web Developers i componenti necessari per creare e personalizzare un portale dei moduli nei siti Web creati con Adobe Experience Manager (AEM). Per una rapida panoramica del portale Forms, vedi [Introduzione alla pubblicazione di moduli su un portale](../../forms/using/introduction-publishing-forms.md).

## Prerequisiti {#prerequisites}

Per impostazione predefinita, i componenti di Forms portal non sono disponibili per l&#39;uso. Assicurati che le seguenti categorie di componenti del portale dei moduli siano abilitate come descritto in [Abilitazione dei componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md).

**Document Services** Include i componenti Ricerca e elenco, Collegamento, Bozze e Invio.

**Predicati Document Services** Include i componenti Predicato data, Predicato full-text, Predicato proprietà e Predicato tag. Questi componenti vengono utilizzati per configurare la ricerca nel componente Ricerca ed elenco.

Una volta abilitate in una pagina dei siti AEM, queste categorie di componenti sono disponibili per l’utilizzo nel browser Componenti.

![Componenti di AEM Forms Portal nel browser dei componenti](assets/component-categories.png)

Categorie di componenti di Forms Portal

## Componente Ricerca ed elenco {#search-amp-lister-component}

Il componente Ricerca ed elenco, disponibile nella categoria di componenti Servizi basati su documenti, viene utilizzato per elencare i moduli in una pagina e per implementare la ricerca nei moduli elencati. Il componente include due riquadri:

* Riquadro elenco in cui sono elencati i moduli.
* Riquadro di ricerca in cui aggiungere la funzionalità di ricerca.

Puoi trascinare il componente Ricerca ed Elenco dalla categoria del componente Servizi documentali nel browser dei componenti alla pagina. Il componente, se aggiunto, ha un aspetto simile al seguente.

![Componente Ricerca ed elenco in una pagina](assets/fp-grid-viw.png)

Componente Ricerca ed elenco in una pagina con layout griglia

### Riquadro elenco {#list-pane}

Il riquadro Elenco è un&#39;area in cui sono elencati i moduli. Il componente Ricerca ed elenco fornisce varie opzioni di configurazione che è possibile utilizzare per controllare la visualizzazione dei moduli nel riquadro Elenco.

Per configurare il riquadro Elenco, tocca il componente Ricerca ed Elenco e quindi tocca ![icona_impostazioni](assets/settings_icon.png). Il **[!UICONTROL Modifica componente]** viene visualizzata una finestra di dialogo.

![Riquadro elenco in modalità di modifica](assets/edit-list.png)

Riquadro elenco in modalità di modifica

Il **Modifica** La finestra di dialogo include diverse schede che forniscono le opzioni di configurazione descritte nella tabella seguente. Tocca **OK** al termine, per salvare la configurazione.

<table>
 <tbody>
  <tr>
   <th>Tabulazione</th>
   <th>Configurazione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Cartelle risorse</strong></code></td>
   <td>Aggiungi elemento</td>
   <td>Configura le cartelle in cui vengono caricate le risorse tramite l’interfaccia utente di AEM Forms. Per impostazione predefinita, elenca tutte le risorse caricate. Per ulteriori informazioni sull’interfaccia utente di AEM Forms, consulta <a href="../../forms/using/introduction-managing-forms.md" target="_blank">Introduzione alla gestione dei moduli</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>Visualizzazione</strong></code></p> </td>
   <td>Testo titolo</td>
   <td>Titolo per il componente Ricerca ed elenco. Il titolo predefinito è <strong>Forms Portal</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modello di layout</td>
   <td>Layout delle risorse. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Disabilita ricerca avanzata</td>
   <td>Quando è attivata, nasconde l’icona di ricerca avanzata.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Disattiva ricerca testo</td>
   <td>Quando è attivata, nasconde la barra di ricerca full-text.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Risultato</strong></code></td>
   <td>Numero Di Risultati Per Pagina</td>
   <td>Configura il numero massimo di moduli da visualizzare in una pagina.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Testo risultati</td>
   <td><p>Configura il testo dei risultati (ad esempio, 1-12 di 601 <strong>Risultati</strong>). Il valore predefinito è <strong>Risultati</strong>.</p> <p>Ad esempio, se specifichi <strong>Forms </strong>in questo campo, con un totale di 601 moduli, il testo risultante diventa 1-12 di 601 <strong>Forms.</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Testo pagina</td>
   <td><p>Configura il testo della pagina (ad esempio, <strong>Pagina </strong>1 di 51). Il valore predefinito è <strong>Pagina</strong>.</p> <p>Ad esempio, se specifichi <strong>Modulo di richiesta </strong>in questo campo, se sono presenti 51 pagine, il testo della pagina diventa <strong>Modulo di richiesta </strong>1 di 51.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Di testo</td>
   <td><p>Sostituisce la parola <strong>di</strong> con il testo specificato (pagina 1) <strong>di </strong>51 ). Il valore predefinito è <strong>di</strong>.</p> <p>Ad esempio, se specifichi <strong>su </strong>in questo campo, il testo diventa Pagina 1 <strong>su </strong>51</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Collegamento modulo</strong></code></td>
   <td>Tipo di rendering</td>
   <td>Controlla l'elenco dei moduli in base al tipo di rendering specificato. Le opzioni disponibili sono PDF e HTML. Ad esempio, se selezioni solo HTML come tipo di rendering, i PDF forms vengono filtrati.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Profilo HTML</td>
   <td>Configura il profilo HTML da utilizzare per il rendering. Tutti i profili disponibili sono elencati nell’elenco a discesa.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Invia URL</td>
   <td><p>Configura un servlet in cui vengono inviati i dati del modulo.</p> <p><strong>Nota:</strong> <em>È possibile specificare l'URL di invio per un modulo in più posizioni e il relativo ordine di precedenza è il seguente:</em></p>
    <ol>
     <li><em>L’URL di invio incorporato nel modulo (nel pulsante Invia ) ha la priorità più alta.</em></li>
     <li><em>L’URL di invio menzionato nell’interfaccia utente di AEM Forms ha la seconda priorità più alta.</em></li>
     <li><em>L’URL di invio menzionato nel portale dei moduli ha la priorità più bassa.</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Descrizione comando azione rendering HTML</td>
   <td>Configura il testo della descrizione, visualizzato quando si passa il puntatore del mouse sopra di esso <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (icona di HTML5).</td>
  </tr>
  <tr>
   <td> </td>
   <td>Descrizione comando azione rendering PDF</td>
   <td>Configura il testo della descrizione, visualizzato quando si passa il puntatore del mouse sopra di esso <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (l’icona PDF ).</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Stile</strong></code></td>
   <td>Tipo di stile</td>
   <td>Consente di specificare <strong>Nessuno stile, stile predefinito</strong>, o <strong>Stile personalizzato </strong>per l’elenco dei moduli.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Percorso stile personalizzato</td>
   <td>Se hai selezionato Personalizzato come Tipo di stile, cerca il percorso del CSS personalizzato, altrimenti seleziona Predefinito.</td>
  </tr>
 </tbody>
</table>

### Riquadro di ricerca {#search-pane}

Il riquadro di ricerca consente di aggiungere i componenti Predicato data, Predicato testo completo, Predicato proprietà e Predicato tag dalla categoria Predicati di Document Services in AEM Sidekick. Questi componenti implementano la funzionalità di ricerca per consentire agli utenti di eseguire ricerche nei moduli elencati.

**Suggerimento** *È possibile controllare l&#39;elenco dei moduli visualizzati nel portale dei moduli in base a criteri predefiniti e nascondere la funzionalità di ricerca per gli utenti finali. Per controllare l’elenco dei moduli, utilizza i componenti Predicato per applicare i filtri di ricerca. Puoi anche specificare i valori di filtro predefiniti e disattivare la ricerca dalla scheda Visualizzazione della finestra di dialogo Modifica componente.*

![Pannello di ricerca con predicato Data, Testo completo, Proprietà e Tag](assets/search-with-predicates.png)

Pannello di ricerca con predicato Data, Testo completo, Proprietà e Tag

#### Predicato data {#date-predicate}

Il componente Predicato data, se aggiunto, consente la ricerca nei moduli elencati modificati durante una determinata durata.

Per configurare il componente Predicato data:

1. Tocca il componente, quindi tocca ![icona_impostazioni](assets/settings_icon.png). Viene visualizzata la finestra di dialogo Modifica.
1. Specifica quanto segue:

   * **Tipo:** L’unica opzione disponibile è **Data ultima modifica**

   * **Testo:** Etichetta o didascalia del componente predicato data. Il valore predefinito è **Data ultima modifica.**

   * **Etichetta data di inizio:** Etichetta o didascalia del campo data di inizio
   * **Etichetta data di fine:** Etichetta o didascalia per il campo data di fine
   * **Nascondi:** Per applicare un filtro date predefinito per elencare i moduli

1. Tocca **OK**

#### Predicato full-text {#full-text-predicate}

Il componente Predicato full-text implementa la ricerca full-text nei dati del modulo, ad esempio nome e descrizione. Gli utenti possono cercare qualsiasi stringa di testo per restituire i moduli che contengono il testo nel nome o nella descrizione.

Per configurare il componente Predicato full-text:

1. Tocca il componente, quindi tocca ![icona_impostazioni](assets/settings_icon.png). Viene visualizzata la finestra di dialogo Modifica.
1. Specifica il titolo nella **Titolo principale** campo.
1. Tocca **Ok**

#### Predicato proprietà {#properties-predicate}

Il componente Predicato proprietà implementa la ricerca di moduli in base alle proprietà del modulo, come titolo, autore e descrizione.

Per configurare il componente Predicato proprietà:

1. Tocca il componente, quindi tocca ![icona_impostazioni](assets/settings_icon.png). Viene visualizzata la finestra di dialogo Modifica.
1. Nella scheda Generale, specifica l’etichetta di ricerca. Il valore predefinito è **Proprietà**

1. Nella scheda Opzioni, tocca **Aggiungi elemento.**
1. Seleziona una proprietà dall’elenco a discesa e specifica un’etichetta di ricerca nel campo sotto l’elenco a discesa.
1. Ripeti il passaggio 4 per aggiungere altre proprietà. È inoltre possibile specificare un valore di filtro predefinito per elencare i moduli in base ai criteri specificati e nascondere la proprietà per la ricerca da parte degli utenti finali. Seleziona la casella di controllo Nascondi per una proprietà e specifica il valore di filtro predefinito.
Ad esempio, se si desidera visualizzare i moduli che contengono &quot;Viaggio&quot; nei titoli, selezionare Nascondi accanto alla proprietà Titolo. Specificare inoltre la casella di testo Viaggio nel valore di filtro predefinito.

1. Tocca **OK**

#### Predicato tag {#tags-predicate}

Il componente Predicato tag implementa la ricerca di moduli basati sui tag definiti in Forms Manager.

Per configurare il componente Predicato tag:

1. Tocca il componente, quindi tocca ![icona_impostazioni](assets/settings_icon.png). Viene visualizzata la finestra di dialogo Modifica.
1. Tocca il pulsante freccia giù accanto al campo Tag.
1. Seleziona i tag appropriati
1. Tocca **OK**

I tag selezionati vengono visualizzati nel riquadro di ricerca insieme alle caselle di controllo per la selezione. Gli utenti possono ora restringere la ricerca in base ai tag.

## Elencare moduli su una pagina {#list-forms-on-a-page-br}

Per elencare i moduli in una pagina, aggiungi **[!UICONTROL Ricerca ed elenco]** alla pagina e configura il **[!UICONTROL Riquadro elenco]**. Per consentire agli utenti finali di cercare i moduli con data, testo e tag, aggiungere una **[!UICONTROL Riquadro di ricerca]** componente.

Per collegare un modulo da qualsiasi punto della pagina, utilizza il componente Collega. Per ulteriori informazioni sul componente collegamento, vedi [Incorporazione di un componente collegamento in una pagina](../../forms/using/embedding-link-component-page.md).

Per elencare i moduli in stato di bozza e quelli già inviati, utilizzare **[!UICONTROL Bozze e invii]** componente. Per ulteriori informazioni, consulta [Personalizzazione del componente Bozze e invii](../../forms/using/draft-submission-component.md).

## Compatibilità con i dispositivi mobili {#mobile-device-friendliness}

Il componente Ricerca ed elenco di Forms Portal è compatibile con i dispositivi mobili e si adatta di conseguenza. Tutte e tre le visualizzazioni predefinite: Griglia, Scheda, Relayout pannello in base al dispositivo in cui è aperto il sito, con il fatto che la pagina web si adatta anche. Il fatto è che Search &amp; List è solo un componente e non regola lo stile a livello di pagina.

L’immagine seguente mostra il componente Ricerca ed Elenco quando viene aperto su un dispositivo mobile:

![Schermata del componente Ricerca ed elenco](assets/search_lister.png)

Componente Ricerca ed elenco

## Personalizzazione di una pagina del portale dei moduli {#customizing-a-forms-portal-page-br}

È possibile personalizzare una pagina del portale dei moduli per conferire un aspetto distinto alla pagina. Puoi anche aggiungere metadati per migliorare l’esperienza di ricerca, modificare il layout della pagina e aggiungere stili CSS personalizzati. Per ulteriori informazioni, consulta [Personalizzazione dei modelli per i componenti di Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md).

L’interfaccia utente di AEM Forms consente di aggiungere metadati personalizzati ai moduli. I metadati personalizzati sono utili per fornire agli utenti finali un’esperienza di elenco e ricerca nei moduli. Per ulteriori informazioni sui metadati personalizzati, consulta [Personalizzazione dei modelli per i componenti di Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md).

Il portale dei moduli fornisce azioni di rendering pronte all’uso. È possibile personalizzare il portale dei moduli per aggiungere altre azioni. Per informazioni dettagliate, consulta [Aggiunta di azioni personalizzate agli elementi del lister del modulo.](../../forms/using/add-custom-action-form-lister.md)

## Articoli correlati

* [Abilitare i componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md)
* [Crea pagina portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare moduli su una pagina web utilizzando API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utilizzare il componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale Forms](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
