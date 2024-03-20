---
title: Caratteri speciali personalizzati nella gestione della corrispondenza
description: Scopri come aggiungere caratteri speciali personalizzati in Gestione della corrispondenza.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Caratteri speciali personalizzati nella gestione della corrispondenza{#custom-special-characters-in-correspondence-management}

## Panoramica {#overview}

Gestione della corrispondenza dispone del supporto predefinito per 210 caratteri speciali che è possibile inserire facilmente nelle lettere.

Ad esempio, puoi inserire i seguenti caratteri speciali:

* Simboli di valuta come €,¥ e £
* Simboli matematici come ∑, √, ∂ e ^
* Simboli di punteggiatura come ‟ e &quot;

È possibile inserire caratteri speciali nelle lettere:

* In [editor di testo](/help/forms/using/document-fragments.md#createtext)
* In un [modulo inline modificabile in una corrispondenza](../../forms/using/create-correspondence.md#managecontent)

![modulato speciale di sinlinio](assets/specialcharactersinlinemodule.png)

L’amministratore può aggiungere il supporto di caratteri speciali aggiuntivi/personalizzati tramite personalizzazione. In questo articolo vengono fornite istruzioni su come aggiungere supporto per caratteri speciali aggiuntivi personalizzati.

## Aggiunta o modifica del supporto per caratteri speciali personalizzati in Gestione corrispondenza {#creatingfolderstructure}

Per aggiungere il supporto per i caratteri speciali personalizzati, effettua le seguenti operazioni:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedere come amministratore.
1. Nella cartella delle app, crea una cartella denominata **[!UICONTROL caratteri speciali]** con un percorso/struttura simile alla cartella dei caratteri speciali (nella cartella textEditorConfig in libs):

   1. Fare clic con il pulsante destro del mouse **caratteri speciali** cartella nel percorso seguente e selezionare **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **Posizione sovrapposizione:** /apps/

      **Corrispondenza tipi di nodo:** Selezionato

      >[!NOTE]
      >
      >Non modificare il ramo /libs. Qualsiasi modifica apportata potrebbe andare persa, poiché questo ramo potrebbe cambiare quando:
      >
      >
      >
      >    * Eseguire l’aggiornamento all’istanza
      >    * Applicare un hotfix
      >    * Installare un feature pack
      >
      >

   1. Clic **OK** e quindi fare clic su **Salva tutto**. La cartella dei caratteri speciali viene creata nel percorso specificato.

      Dopo aver creato la sovrapposizione, verifica i tag della struttura del nodo. Ogni nodo creato in /apps utilizzando la sovrapposizione deve avere la stessa classe e le stesse proprietà definite in /libs per quel nodo. Se manca una proprietà o un tag nella struttura del nodo nella posizione /apps, sincronizza i relativi tag con il nodo corrispondente in /libs.

1. Assicurati che **[!UICONTROL textEditorConfig]** Il nodo ha le seguenti proprietà e valori:

   | Nome | Tipo | Valore |
   |---|---|---|
   | cmConfigurationType | Stringa | cmTextEditorConfiguration |
   | cssPath | Stringa | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Fare clic con il pulsante destro del mouse **[!UICONTROL caratteri speciali]** cartella nel percorso seguente e selezionare **Crea > Nodo figlio** e quindi fare clic su **Salva tutto**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;yourchildnode>

1. Aggiorna la pagina Editor di testo\Crea interfaccia utente per la corrispondenza. Il nodo aggiunto è l’ultimo nell’elenco dei caratteri speciali dell’interfaccia utente.
1. Clic **Salva tutto**.
1. Modifiche ai caratteri speciali come richiesto:

<table>
 <tbody>
  <tr>
   <td><strong>A...</strong></td>
   <td><strong>Completa i seguenti passaggi</strong></td>
  </tr>
  <tr>
   <td>Aggiungere un carattere speciale personalizzato</td>
   <td>
    <ol>
     <li>Aggiungi un nodo figlio in "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" con proprietà obbligatorie.</li>
     <li>Fai clic su Salva tutto</li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente per la corrispondenza per visualizzare le modifiche.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Aggiornare le proprietà di un carattere speciale esistente</td>
   <td>
    <ol>
     <li>Sovrapponi il nodo da aggiornare come descritto in precedenza e verifica tag e classi.</li>
     <li>Modificare i valori, ad esempio caption, value, endValue e multipleCaption. </li>
     <li>Fai clic su Salva tutto. </li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente per la corrispondenza per visualizzare le modifiche.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Nascondi carattere speciale</td>
   <td>
    <ol>
     <li>Sovrapponi il nodo da nascondere in "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters"</li>
     <li>Aggiungi la proprietà sling:hideResource (booleana) al nodo (sotto le app) da nascondere. </li>
     <li>Fai clic su Salva tutto. </li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente per la corrispondenza per visualizzare le modifiche.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Nascondi più caratteri speciali</td>
   <td>
    <ol>
     <li>Aggiungi la proprietà "sling:hideChildren (String o String[])" a "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters". </li>
     <li>Aggiungi nomi di nodo (caratteri speciali da nascondere) come valori per la proprietà "sling:hideChildren". </li>
     <li>Fai clic su Salva tutto. </li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente per la corrispondenza per visualizzare le modifiche.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ordinare caratteri speciali</td>
   <td>
    <ol>
     <li>Aggiungi un nodo figlio in "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" con proprietà obbligatorie. </li>
     <li>Aggiungi la proprietà "sling:orderBefore (String)" al nodo figlio appena creato. </li>
     <li>Aggiungi il nome del nodo come valore prima del quale deve essere visualizzato il nuovo carattere speciale aggiunto. </li>
     <li>Fai clic su Salva tutto. </li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente per la corrispondenza per visualizzare le modifiche.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
