---
title: Differenziazione delle funzioni tra moduli HTML5 e moduli PDF
description: Scopri le differenze di funzionalità tra HTML5 Forms e PDF forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 6%
---
# Differenziazione delle funzioni tra moduli HTML5 e moduli PDF {#feature-differentiation-between-html-forms-and-pdf-forms}

La tabella seguente specifica il supporto delle funzioni fornito per i moduli HTML5 e PDF forms:

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
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Campo firma<br /> </td>
   <td><strong>Le firme digitali</strong> non sono supportate, ma è stato aggiunto un nuovo campo <strong>Firma scarabocchio</strong> per le firme cartacee. È possibile scrivere la firma nel modulo utilizzando il campo <strong>Firma scarabocchio</strong>. La firma viene salvata nel modulo come immagine. È possibile salvare le informazioni di geolocalizzazione nel campo <strong>Firma scarabocchio</strong>.</td>
   <td>Campo firma disponibile per <strong>firme digitali</strong>.</td>
  </tr>
  <tr>
   <td>Unione dati</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Immagini</td>
   <td>Lo schema URI dati viene utilizzato per visualizzare le immagini. Tutte le versioni moderne dei browser supportano questo schema, ma esistono differenze nell'intervallo di formati di immagine supportati da ogni browser.<br /> </td>
   <td>Sono supportati i formati .gif, .png, .jpeg, .bmp e .tiff.</td>
  </tr>
  <tr>
   <td>Paginazione<br /> </td>
   <td><p>Un modulo di HTML5 è diviso in pannelli e caselle per conferirgli un aspetto simile a quello di PDF forms. Le dimensioni della pagina vengono calcolate in modo dinamico. Se tutti i contenuti di una pagina in un modulo di HTML5 vengono eliminati o contrassegnati come nascosti, la pagina vuota viene nascosta. Tra le pagine sopra e sotto la pagina vuota non viene visualizzato uno spazio vuoto (spazio vuoto).</p> <p>Se l’unione dati o gli script aggiungono contenuto a una pagina, la lunghezza della pagina si espande per adattarsi al contenuto appena aggiunto. Non vengono aggiunte nuove pagine al modulo per includere il contenuto appena aggiunto. </p> <p><strong>Nota:</strong> quando tutti i contenuti di una pagina in un modulo di HTML5 vengono eliminati o contrassegnati come nascosti, la pagina vuota (spazio vuoto) rimane visibile tra la prima e la seconda pagina, ma non tra le altre pagine.</p> </td>
   <td>L’impaginazione in PDF dipende dal contenuto dei dati uniti o dal contenuto dell’utente e il conteggio delle pagine viene aumentato/ridotto in base a esso.</td>
  </tr>
  <tr>
   <td>Intestazioni/Piè di pagina </td>
   <td>Supportato. <br /> <br /> Poiché i moduli mobili HTML5 non supportano le interruzioni di pagina, le intestazioni e i piè di pagina vengono visualizzati una sola volta. È tuttavia possibile impostarle nel layout in modo che vengano visualizzate in più posizioni nell'anteprima dei moduli mobili.<br /> </td>
   <td>Supportato.</td>
  </tr>
  <tr>
   <td>Widget personalizzati</td>
   <td>È possibile personalizzare i widget per migliorare l'esperienza utente sui dispositivi mobili.<br /> </td>
   <td>Tutti i widget sono bloccati e nessun widget personalizzato può essere collegato.<br /> </td>
  </tr>
  <tr>
   <td>API script XFA</td>
   <td>Supporta i costrutti di script XFA più comunemente utilizzati. Per un elenco dettagliato dei costrutti supportati, vedere <a href="/help/forms/using/scripting-support.md">supporto script</a>.</td>
   <td>Supporta tutti i costrutti di script XFA.</td>
  </tr>
  <tr>
   <td>API di Acrobat Script </td>
   <td>I moduli HTML5 supportano le API più comunemente utilizzate. Per ulteriori dettagli, vedere <a href="/help/forms/using/scripting-support.md">supporto script</a>.</td>
   <td>Se il file PDF viene aperto all’interno di Acrobat o Reader, supporta anche tutte le API di script fornite da Acrobat.</td>
  </tr>
  <tr>
   <td>Supporto per le lingue da destra a sinistra </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
