---
title: Differenza tra le funzioni dei moduli HTML5 e dei moduli PDF
seo-title: Differenza tra le funzioni dei moduli HTML5 e dei moduli PDF
description: Funzionalità supportate nei moduli HTML5 e PDF
seo-description: Funzionalità supportate nei moduli HTML5 e PDF
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Differenza tra le funzioni dei moduli HTML5 e dei moduli PDF {#feature-differentiation-between-html-forms-and-pdf-forms}

La tabella seguente specifica la funzione di supporto fornita per i moduli HTML5 e PDF:

<table>
 <tbody>
  <tr>
   <th>Funzione</th>
   <th>Moduli HTML5</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>Codici a barre<br /> </td>
   <td>Non disponibile a livello di interfaccia utente. </td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Campo firma<br /> </td>
   <td><strong>Le firme</strong> digitali non sono supportate, ma è stato aggiunto un nuovo campo <strong>Firma</strong> scarabocchio per le firme cartacee. È possibile creare uno script per la firma sul modulo utilizzando il campo <strong>Firma</strong> scarabocchio. La firma viene salvata nel modulo come immagine. È possibile salvare le informazioni sulla geolocalizzazione nel campo <strong>Firma</strong> scarabocchio.</td>
   <td>Campo firma disponibile per <strong>Digital Signatures</strong>.</td>
  </tr>
  <tr>
   <td>Unione dati</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Immagini</td>
   <td>Lo schema URI dati viene utilizzato per visualizzare le immagini. Tutte le versioni moderne dei browser supportano questo schema, ma esistono differenze nella gamma di formati di immagine supportati da ciascun browser.<br /> </td>
   <td>Sono supportati i formati .gif, .png, .jpeg, .bmp e .tiff.</td>
  </tr>
  <tr>
   <td>Paginazione<br /> </td>
   <td><p>Un modulo HTML5 è suddiviso in pannelli e caselle per conferirgli un aspetto simile ai moduli PDF. Le dimensioni della pagina vengono calcolate in modo dinamico. Se tutti i contenuti di una pagina in un modulo HTML5 vengono eliminati o contrassegnati come nascosti, la pagina vuota viene nascosta e non viene visualizzato uno spazio vuoto (spazio vuoto) tra le pagine sopra e sotto la pagina vuota.</p> <p>Se l'unione dei dati o gli script aggiungono contenuto a una pagina, la lunghezza della pagina si espande per adattarsi al contenuto appena aggiunto. Al modulo non vengono aggiunte nuove pagine per contenere il contenuto appena aggiunto. </p> <p><strong></strong> Nota: Quando tutti i contenuti di una pagina in un modulo HTML5 vengono eliminati o contrassegnati come nascosti, la pagina vuota (spazio vuoto) rimane visibile tra la prima e la seconda pagina, ma non tra le altre.</p> </td>
   <td>L'impaginazione in PDF dipende dal contenuto dei dati unito o contenuto utente e il conteggio delle pagine viene aumentato o ridotto in base a tale contenuto.</td>
  </tr>
  <tr>
   <td>Intestazioni/Piè di pagina </td>
   <td>Supportato. <br /> <br /> Poiché i moduli mobili HTML5 non supportano le interruzioni di pagina, le intestazioni e i piè di pagina vengono visualizzati solo una volta. Tuttavia, è possibile impostarle nel layout in modo che vengano visualizzate in più posizioni nell'anteprima dei moduli per dispositivi mobili.<br /> </td>
   <td>Supportato.</td>
  </tr>
  <tr>
   <td>Widget personalizzati</td>
   <td>È possibile personalizzare i widget per migliorare l'esperienza utente sui dispositivi mobili.<br /> </td>
   <td>Tutti i widget sono bloccati e non è possibile collegare alcun widget personalizzato.<br /> </td>
  </tr>
  <tr>
   <td>API script XFA</td>
   <td>Supporta i costrutti di script XFA più comunemente utilizzati. Per un elenco dettagliato dei costrutti supportati, vedere <a href="/help/forms/using/scripting-support.md">Supporto</a>script.</td>
   <td>Supporta tutti i costrutti di script XFA.</td>
  </tr>
  <tr>
   <td>API di Acrobat Script </td>
   <td>I moduli HTML5 supportano le API più utilizzate. Per informazioni dettagliate, vedere <a href="/help/forms/using/scripting-support.md">Supporto</a>per gli script.</td>
   <td>Se il file PDF viene aperto in Acrobat o Reader, supporta anche tutte le API di script fornite da Acrobat.</td>
  </tr>
  <tr>
   <td>Supporto delle lingue da destra a sinistra </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
