---
title: Caratteri speciali personalizzati in Gestione corrispondenza
seo-title: Caratteri speciali personalizzati in Gestione corrispondenza
description: Scoprite come aggiungere caratteri speciali personalizzati in Gestione corrispondenza.
seo-description: Scoprite come aggiungere caratteri speciali personalizzati in Gestione corrispondenza.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 1%

---


# Caratteri speciali personalizzati in Gestione corrispondenza{#custom-special-characters-in-correspondence-management}

## Panoramica {#overview}

Gestione corrispondenza ha un supporto predefinito integrato per 210 caratteri speciali che è possibile inserire in lettere con facilità.

Ad esempio, è possibile inserire i seguenti caratteri speciali:

* Simboli di valuta come €,⇒ e £
* Simboli matematici come i simboli all&#39;unisono, seguente:
* Simboli di punteggiatura come ‟ e&quot;

È possibile inserire caratteri speciali nelle lettere:

* Nell&#39; [editor di testo](/help/forms/using/document-fragments.md#createtext)
* In un modulo in linea [modificabile in una corrispondenza](../../forms/using/create-correspondence.md#managecontent)

![specialtisinlinemodulo](assets/specialcharactersinlinemodule.png)

L&#39;amministratore può aggiungere il supporto per più o più caratteri speciali personalizzati in base alla personalizzazione. Questo articolo fornisce istruzioni su come aggiungere supporto per caratteri speciali aggiuntivi e personalizzati.

## Aggiunta o modifica del supporto per i caratteri speciali personalizzati in Gestione corrispondenza {#creatingfolderstructure}

Per aggiungere il supporto per i caratteri speciali personalizzati, effettuate le seguenti operazioni:

1. Andate a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedete come amministratore.
1. Nella cartella delle app, create una cartella denominata **[!UICONTROL caratteri speciali]** con percorso/struttura simile alla cartella dei caratteri speciali (che si trova nella cartella textEditorConfig in libs):

   1. Fare clic con il pulsante destro del mouse sulla cartella **caratteri speciali** nel percorso seguente e selezionare **Overlay Node**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Verificate che la finestra di dialogo Nodo sovrapposizione contenga i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialfonts

      **Posizione overlay:** /apps/

      **Corrispondenza tipi di nodo:** Selezionati

      >[!NOTE]
      >
      >Non apportare modifiche al ramo /libs. Eventuali modifiche apportate potrebbero andare perse, in quanto il ramo potrebbe essere modificato ogni volta che:
      >
      >
      >
      >    * Aggiornamento dell’istanza
      >    * Applicazione di una correzione
      >    * Installare un pacchetto di funzioni


   1. Fare clic su **OK**, quindi fare clic su **Salva tutto**. La cartella dei caratteri speciali viene creata nel percorso specificato.

      Dopo aver creato la sovrapposizione, verificate i tag della struttura del nodo. Ogni nodo creato in /apps utilizzando la sovrapposizione deve avere la stessa classe e le stesse proprietà definite in /libs per quel nodo. Se manca una proprietà o un tag nella struttura del nodo nella posizione /apps, sincronizzatene i tag con il nodo corrispondente in /libs.



1. Assicurarsi che il nodo **[!UICONTROL textEditorConfig]** disponga delle proprietà e dei valori seguenti:

   | Nome | Tipo | Valore |
   |---|---|---|
   | cmConfigurationType | Stringa | cmTextEditorConfiguration |
   | cssPath | Stringa | /libs/fd/cm/ma/gui/components/admin/create-asset/textcontrol/clientlibs/textcontrol |

1. Fare clic con il pulsante destro del mouse sulla cartella **[!UICONTROL caratteri speciali]** nel percorso seguente e selezionare **Crea > Nodo figlio**, quindi fare clic su **Salva tutto**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialfonts/&lt;YourChildNode>

1. Aggiornate la pagina Editor di testo\Crea interfaccia utente di corrispondenza. Il nodo aggiunto è l’ultimo nell’elenco dei caratteri speciali nell’interfaccia utente.
1. Fare clic su **Salva tutto**.
1. Apportate le modifiche necessarie ai caratteri speciali:

<table>
 <tbody>
  <tr>
   <td><strong>A...</strong></td>
   <td><strong>Completa i seguenti passaggi</strong></td>
  </tr>
  <tr>
   <td>Aggiunta di un carattere speciale personalizzato</td>
   <td>
    <ol>
     <li>Aggiungete un nodo figlio in "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialfonts" con proprietà obbligatorie.</li>
     <li>Fai clic su Salva tutto</li>
     <li>Aggiornate l'Editor di testo\Create l'interfaccia utente di corrispondenza per visualizzare le modifiche.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Aggiornare le proprietà di un carattere speciale esistente</td>
   <td>
    <ol>
     <li>Sovrapporre il nodo da aggiornare come descritto sopra e verificare tag e classi.</li>
     <li>Modificate eventuali valori, ad esempio didascalia, valore, endValue e multipleCaption. </li>
     <li>Fate clic su Salva tutto. </li>
     <li>Aggiornate l'Editor di testo\Create l'interfaccia utente di corrispondenza per visualizzare le modifiche.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Nascondere un carattere speciale</td>
   <td>
    <ol>
     <li>Sovrapponi il nodo da nascondere in "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialfonts"</li>
     <li>Aggiungi la proprietà sling:hideResource (booleano) al nodo (sotto le app) da nascondere. </li>
     <li>Fate clic su Salva tutto. </li>
     <li>Aggiornate l'Editor di testo\Create l'interfaccia utente di corrispondenza per visualizzare le modifiche.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Nascondere più caratteri speciali</td>
   <td>
    <ol>
     <li>Aggiungete la proprietà "sling:hideChildren (String o String[])" a "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialfonts". </li>
     <li>Aggiungete i nomi dei nodi (caratteri speciali da nascondere) come valori per la proprietà "sling:hideChildren". </li>
     <li>Fate clic su Salva tutto. </li>
     <li>Aggiornate l'Editor di testo\Create l'interfaccia utente di corrispondenza per visualizzare le modifiche.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ordinare caratteri speciali</td>
   <td>
    <ol>
     <li>Aggiungete un nodo figlio in "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialfonts" con proprietà obbligatorie. </li>
     <li>Aggiungete la proprietà "sling:orderBefore (String)" al nodo figlio appena creato. </li>
     <li>Aggiungete il nome del nodo come valore prima del quale deve essere visualizzato il nuovo carattere speciale aggiunto. </li>
     <li>Fate clic su Salva tutto. </li>
     <li>Aggiornate l'Editor di testo\Create l'interfaccia utente di corrispondenza per visualizzare le modifiche.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

