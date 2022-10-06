---
title: Differenziazione delle funzioni tra moduli e PDF forms di HTML5
seo-title: Feature differentiation between HTML5 forms and PDF forms
description: Funzionalità supportata in HTML5 forms e PDF forms
seo-description: Feature supported in HTML5 forms and PDF forms
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 3%

---

# Differenziazione delle funzioni tra moduli e PDF forms di HTML5 {#feature-differentiation-between-html-forms-and-pdf-forms}

La tabella seguente specifica il supporto delle funzioni fornito per i moduli e i PDF forms di HTML5:

<table>
 <tbody>
  <tr>
   <th>Funzione obsoleta</th>
   <th>Moduli HTML5</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>Codici a barre<br /> </td>
   <td>Non disponibile a livello di interfaccia utente. </td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Campo firma<br /> </td>
   <td><strong>Firme digitali</strong> non sono supportati ma sono <strong>Firma scarabocchio</strong> viene aggiunto un campo per la stampa come le firme. È possibile scrivere la firma sul modulo utilizzando <strong>Firma scarabocchio</strong> campo . La firma viene salvata nel modulo come immagine. È possibile salvare le informazioni sulla geolocalizzazione nel <strong>Firma scarabocchio</strong> campo .</td>
   <td>Campo firma disponibile per <strong>Firme digitali</strong>.</td>
  </tr>
  <tr>
   <td>Unione dati</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Immagini</td>
   <td>Lo schema URI dati viene utilizzato per visualizzare le immagini. Tutte le versioni moderne dei browser supportano questo schema, ma esistono differenze nella gamma di formati immagine supportati da ciascun browser.<br /> </td>
   <td>Sono supportati i formati .gif, .png, .jpeg, .bmp e .tiff .</td>
  </tr>
  <tr>
   <td>Paginazione<br /> </td>
   <td><p>Un modulo HTML5 è diviso in pannelli e caselle per conferirgli un aspetto simile ai PDF forms. Le dimensioni della pagina vengono calcolate dinamicamente. Se tutti i contenuti di una pagina in un modulo HTML5 vengono eliminati o contrassegnati come nascosti, la pagina vuota è nascosta e non viene visualizzato uno spazio vuoto (spazio vuoto) tra le pagine sopra e sotto la pagina vuota.</p> <p>Se l’unione dei dati o gli script aggiungono contenuto a una pagina, la lunghezza della pagina si espande per adattarsi al contenuto appena aggiunto. Al modulo non vengono aggiunte nuove pagine per includere il contenuto appena aggiunto. </p> <p><strong>Nota:</strong> Quando tutti i contenuti di una pagina di un modulo HTML5 vengono eliminati o contrassegnati come nascosti, la pagina vuota (spazio vuoto) rimane visibile tra la prima e la seconda pagina ma non tra le altre pagine.</p> </td>
   <td>L’impaginazione in PDF dipende dal contenuto di dati unito o dal contenuto utente e il conteggio delle pagine viene aumentato o ridotto in base a esso.</td>
  </tr>
  <tr>
   <td>Intestazioni/piè di pagina </td>
   <td>Funzione supportata. <br /> <br /> Poiché i moduli mobili HTML5 non supportano le interruzioni di pagina, le intestazioni e i piè di pagina vengono visualizzati una sola volta. Tuttavia, è possibile impostarli nel layout in modo che vengano visualizzati in più posizioni nell’anteprima dei moduli mobili.<br /> </td>
   <td>Supportato.</td>
  </tr>
  <tr>
   <td>Widget personalizzati</td>
   <td>Puoi personalizzare i widget per migliorare l’esperienza utente sui dispositivi mobili.<br /> </td>
   <td>Tutti i widget sono bloccati e non è possibile collegare widget personalizzati.<br /> </td>
  </tr>
  <tr>
   <td>API script XFA</td>
   <td>Supporta i costrutti di script XFA più comunemente utilizzati. Per un elenco dettagliato dei costrutti supportati, consulta <a href="/help/forms/using/scripting-support.md">supporto per gli script</a>.</td>
   <td>Supporta tutti i costrutti di script XFA.</td>
  </tr>
  <tr>
   <td>API di Acrobat Script </td>
   <td>I moduli di HTML5 supportano le API più comunemente utilizzate. Per maggiori dettagli, vedi <a href="/help/forms/using/scripting-support.md">supporto per gli script</a>.</td>
   <td>Se il file PDF viene aperto in Acrobat o Reader, supporta anche tutte le API di script fornite da Acrobat.</td>
  </tr>
  <tr>
   <td>Supporto per le lingue da destra a sinistra </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
