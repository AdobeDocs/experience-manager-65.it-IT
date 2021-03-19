---
title: Caratteri speciali personalizzati in Gestione Corrispondenza
seo-title: Caratteri speciali personalizzati in Gestione Corrispondenza
description: Scopri come aggiungere caratteri speciali personalizzati in Gestione della corrispondenza.
seo-description: Scopri come aggiungere caratteri speciali personalizzati in Gestione della corrispondenza.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
feature: Gestione della corrispondenza
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 1%

---


# Caratteri speciali personalizzati in Gestione Corrispondenza{#custom-special-characters-in-correspondence-management}

## Panoramica {#overview}

Gestione corrispondenza ha un supporto predefinito integrato per 210 caratteri speciali che è possibile inserire in lettere con facilità.

Ad esempio, puoi inserire i seguenti caratteri speciali:

* Simboli di valuta come €,¥ e £
* Simboli matematici come ∑, Ö, , e ^
* Simboli di punteggiatura come ‟ e&quot;

È possibile inserire caratteri speciali nelle lettere:

* Nell’ [editor di testo](/help/forms/using/document-fragments.md#createtext)
* In un modulo in linea [modificabile in una corrispondenza](../../forms/using/create-correspondence.md#managecontent)

![specialtisinlinemodule](assets/specialcharactersinlinemodule.png)

L’amministratore può aggiungere il supporto per caratteri speciali più o personalizzati tramite la personalizzazione. Questo articolo fornisce istruzioni su come aggiungere supporto per caratteri speciali aggiuntivi personalizzati.

## Aggiungi o modifica il supporto per i caratteri speciali personalizzati in Gestione corrispondenza {#creatingfolderstructure}

Utilizza i seguenti passaggi per aggiungere il supporto per i caratteri speciali personalizzati:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata **[!UICONTROL caratteri speciali]** con percorso/struttura simile alla cartella dei caratteri speciali (che si trova nella cartella textEditorConfig sotto libs):

   1. Fai clic con il pulsante destro del mouse sulla cartella **caratteri speciali** al seguente percorso e seleziona **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialfonts

      **Posizione di sovrapposizione:** /apps/

      **Tipi di nodo di corrispondenza:** controllati

      >[!NOTE]
      >
      >Non apportare modifiche al ramo /libs. Eventuali modifiche apportate potrebbero andare perse, in quanto questo ramo è soggetto a modifiche ogni volta che:
      >
      >
      >
      >    * Aggiorna l&#39;istanza
      >    * Applicare un hotfix
      >    * Installare un feature pack


   1. Fare clic su **OK**, quindi fare clic su **Salva tutto**. La cartella dei caratteri speciali viene creata nel percorso specificato.

      Dopo aver creato la sovrapposizione, verifica i tag della struttura del nodo. Ogni nodo creato in /apps utilizzando la sovrapposizione deve avere la stessa classe e le stesse proprietà definite in /libs per quel nodo. Se manca una proprietà o un tag nella struttura del nodo sotto la posizione /apps, sincronizza i tag con il nodo corrispondente in /libs.



1. Assicurati che il nodo **[!UICONTROL textEditorConfig]** abbia le seguenti proprietà e valori:

   | Nome | Tipo | Valore |
   |---|---|---|
   | cmConfigurationType | Stringa | cmTextEditorConfiguration |
   | cssPath | Stringa | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Fai clic con il pulsante destro del mouse sulla cartella **[!UICONTROL caratteri speciali]** al seguente percorso e seleziona **Crea > Nodo figlio**, quindi fai clic su **Salva tutto**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialCharac/&lt;YourChildNode>

1. Aggiorna la pagina Editor di testo\Crea interfaccia utente Corrispondenza . Il nodo aggiunto è l’ultimo nell’elenco dei caratteri speciali nell’interfaccia utente.
1. Fare clic su **Salva tutto**.
1. Apporta le modifiche necessarie ai caratteri speciali:

<table>
 <tbody>
  <tr>
   <td><strong>A...</strong></td>
   <td><strong>Completa i seguenti passaggi</strong></td>
  </tr>
  <tr>
   <td>Aggiungi un carattere speciale personalizzato</td>
   <td>
    <ol>
     <li>Aggiungi un nodo figlio sotto "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialCharac" con proprietà obbligatorie.</li>
     <li>Fai clic su Salva tutto</li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente Corrispondenza per visualizzare le modifiche.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Aggiornare le proprietà di un carattere speciale esistente</td>
   <td>
    <ol>
     <li>Sovrapponi il nodo da aggiornare come spiegato in precedenza e verifica tag e classi.</li>
     <li>Modificare qualsiasi valore, ad esempio didascalia, valore, endValue e multipleCaption. </li>
     <li>Fai clic su Salva tutto. </li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente Corrispondenza per visualizzare le modifiche.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Nascondere un carattere speciale</td>
   <td>
    <ol>
     <li>Sovrapponi il nodo da nascondere sotto "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialCharac"</li>
     <li>Aggiungi la proprietà sling:hideResource (Boolean) al nodo (sotto le app) da nascondere. </li>
     <li>Fai clic su Salva tutto. </li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente Corrispondenza per visualizzare le modifiche.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Nascondere più caratteri speciali</td>
   <td>
    <ol>
     <li>Aggiungi la proprietà "sling:hideChildren (String o String[])" a "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialCharac". </li>
     <li>Aggiungi i nomi dei nodi (caratteri speciali da nascondere) come valori per la proprietà "sling:hideChildren". </li>
     <li>Fai clic su Salva tutto. </li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente Corrispondenza per visualizzare le modifiche.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ordinare caratteri speciali</td>
   <td>
    <ol>
     <li>Aggiungi un nodo figlio sotto "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialCharac" con proprietà obbligatorie. </li>
     <li>Aggiungi la proprietà "sling:orderBefore (String)" al nodo figlio appena creato. </li>
     <li>Aggiungi il nome del nodo come valore prima del quale verrà mostrato il nuovo carattere speciale aggiunto. </li>
     <li>Fai clic su Salva tutto. </li>
     <li>Aggiorna l'Editor di testo\Crea interfaccia utente Corrispondenza per visualizzare le modifiche.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

