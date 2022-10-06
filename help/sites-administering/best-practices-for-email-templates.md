---
title: Tecniche consigliate per i modelli e-mail
seo-title: Best Practices for Email Templates
description: Trova le best practice per la creazione di modelli e-mail in AEM.
seo-description: Find best practices on creating email templates in AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 1%

---

# Tecniche consigliate per i modelli e-mail {#best-practices-for-email-templates}

>[!CAUTION]
>
>I componenti e-mail AEM sono stati dichiarati obsoleti. A causa della natura dell’e-mail, che unisce contenuto e stile, i componenti e-mail forniti come predefiniti AEM diventano di uso limitato per i clienti a causa della necessità di implementare stili personalizzati in tutti i componenti necessari per i progetti.
>
>I componenti e-mail possono essere implementati a livello di progetto e i componenti e-mail AEM componenti e-mail obsoleti illustrano come ottenere questo risultato. Tuttavia, questi componenti obsoleti non devono essere utilizzati nei progetti.

Questo documento descrive alcune delle best practice relative alla progettazione delle e-mail con conseguente modello di campagna e-mail ben sviluppato.

La campagna demo disponibile in AEM segue tutte queste best practice. Per ogni best practice, viene descritto come implementare le best practice nella campagna demo.

Utilizza queste best practice per creare una newsletter personalizzata.

>[!NOTE]
>
>Tutti i contenuti della campagna devono essere creati in un `master` pagina di tipo `cq/personalization/components/ambitpage`.
>
>Ad esempio, se la struttura della campagna pianificata è simile a
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Assicurati che si trovi sotto a `master` page
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Quando crei un modello di posta per Adobe Campaign, devi includere la proprietà **acMapping** con il valore **mapRecipient** in **jcr:content** nodo del modello, oppure non potrai selezionare il modello Adobe Campaign in **Proprietà pagina** di AEM (campo disabilitato).

## Modello/componente pagina {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>Best practice</strong></td>
   <td><strong>Implementazione</strong></td>
  </tr>
  <tr>
   <td><p>Specifica il tipo di documento per garantire la coerenza del rendering.</p> <p>Aggiungi DOCTYPE all'inizio (HTML o XHTML)</p> </td>
   <td><p>È configurabile modificando la progettazione <i>cq:doctype</i> proprietà in<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>Il valore predefinito è "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Può essere modificato in "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Specifica la definizione del carattere per garantire il rendering corretto dei caratteri speciali.</p> <p>Aggiungi la dichiarazione CHARSET (ad esempio iso-8859-15, UTF-8) a &lt;head&gt;</p> </td>
   <td><p>È impostato su UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codifica tutta la struttura utilizzando &lt;table&gt;elemento. Per i layout più complessi, è necessario nidificare le tabelle per creare strutture complesse.</p> <p>L’e-mail dovrebbe avere un bell’aspetto anche senza css.</p> </td>
   <td><p>Le tabelle vengono utilizzate in tutto il modello per strutturare il contenuto. Attualmente utilizza un massimo di quattro tabelle nidificate (1 tabella base + max. 3 livelli di nidificazione)</p> <p>&lt;div&gt; I tag vengono utilizzati solo in modalità di authoring per garantire la corretta modifica dei componenti.</p> </td>
  </tr>
  <tr>
   <td>Per impostare le dimensioni della tabella, utilizza gli attributi degli elementi (ad esempio spaziatura interna, valori e larghezza). In questo modo si forza una struttura basata su un modello a scatola.</td>
   <td><p>Tutte le tabelle contengono attributi necessari come <i>border</i>, <i>spaziatura interna</i>, <i>spaziatura</i> e <i>larghezza</i>.</p> <p>Per armonizzare il posizionamento degli elementi all’interno delle tabelle, tutte le celle della tabella hanno l’attributo <i>valign="top"</i> impostato.</p> </td>
  </tr>
  <tr>
   <td><p>Tenete conto, se possibile, della facilità di utilizzo dei dispositivi mobili. Utilizza le query multimediali per aumentare le dimensioni del testo su schermi di piccole dimensioni, fornire aree hit di dimensioni pollici per i collegamenti.</p> <p>Rendi l’e-mail reattiva se la progettazione lo consente.</p> </td>
   <td>Per quanto riguarda gli stili CSS utilizzati per illustrare la progettazione demo, le query multimediali vengono utilizzate per offrire una versione semplice per dispositivi mobili.</td>
  </tr>
  <tr>
   <td>I CSS in linea sono migliori che mettere tutti i CSS all’inizio.</td>
   <td><p>Per illustrare meglio la struttura HTML sottostante e semplificare la possibilità di personalizzare la struttura della newsletter, sono state allineate solo alcune definizioni CSS.</p> <p>Gli stili di base e le varianti di modello sono stati estratti in un blocco di stile nel &lt;head&gt; della pagina. Al momento dell’invio finale della newsletter, queste definizioni CSS devono essere inserite in HTML. È previsto un meccanismo di inlinizzazione automatica, ma al momento non disponibile.</p> </td>
  </tr>
  <tr>
   <td>Mantieni il tuo CSS semplice. Evita dichiarazioni di stile composte, codice abbreviato, proprietà di layout CSS, selettori complessi e pseudo-elementi.</td>
   <td>Per quanto riguarda gli stili CSS utilizzati per illustrare la progettazione demo, i consigli CSS vengono seguiti.</td>
  </tr>
  <tr>
   <td>Le e-mail devono avere una larghezza massima di 600-800 pixel. In questo modo, si comportano meglio con le dimensioni del riquadro di anteprima fornite da molti client.</td>
   <td>La <i>larghezza</i> della tabella dei contenuti è limitata a 600 px nella progettazione demo.</td>
  </tr>
 </tbody>
</table>

### Immagini {#images}

/libs/mcm/campaign/components/image

| **Best practice** | **Implementazione** |
|---|---|
| Aggiungi *alt* attributi delle immagini | La *alt* è stato definito come obbligatorio per il componente immagine. |
| Utilizzo *jpg* anziché *png* formato per le immagini | Il componente Immagine fungerà sempre da JPG per le immagini. |
| Utilizzo `<img>` anziché immagini di sfondo in una tabella. | Nei modelli non vengono utilizzati dati immagine di sfondo. |
| Aggiungi attribute style=&quot;display block&quot; sulle immagini. Permette di visualizzare bene su Gmail. | Tutte le immagini contengono per impostazione predefinita il *style=&quot;display block&quot;* attributo. |

### Testo e collegamenti {#text-and-links}

/libs/mcm/campaign/components/header, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Best practice</strong></td>
   <td><strong>Implementazione</strong></td>
  </tr>
  <tr>
   <td>Utilizza l’html invece dello stile in CSS (font-family)</td>
   <td>L'editor RichText (ad esempio nel componente di testo) ora supporta la scelta e l'applicazione delle famiglie di font e delle dimensioni dei font ai testi selezionati. Saranno resi come tag.</td>
  </tr>
  <tr>
   <td>Utilizza font di base multipiattaforma come <i>Arial, Verdana, Georgia</i> e <i>Times New Roman</i>.</td>
   <td><p>Dipende dalla progettazione della newsletter.</p> <p>Per la progettazione demo viene utilizzato il carattere "Helvetica", ma se non presente, torna al carattere generico sans-serif.</p> </td>
  </tr>
 </tbody>
</table>

### Generico {#generic}

| **Best practice** | **Implementazione** |
|---|---|
| Utilizza la convalida W3C per correggere il codice HTML. Assicurati che tutti i tag aperti siano chiusi correttamente. | Codice convalidato. Per XHTML Transition Doctype solo l&#39;attributo xmlns mancante per `<html>` elemento mancante. |
| Non preoccuparti di JavaScript o Flash: le tecnologie non sono in gran parte supportate dai client e-mail. | Né JavaScript né Flash vengono utilizzati nel modello di newsletter. |
| Aggiungi una versione di testo normale per l’invio in più parti. | Un nuovo widget è stato creato nelle proprietà della pagina per estrarre facilmente una versione di testo normale dal contenuto della pagina. Può essere utilizzato come punto di partenza per la versione normale finale. |

## Modelli ed esempi per newsletter di Campaign {#campaign-newsletter-templates-and-examples}

AEM include diversi modelli e componenti pronti all’uso per la creazione di newsletter per le campagne. È possibile utilizzare questi modelli e componenti per creare newsletter personalizzate.

### Modelli {#templates}

Per offrire una base solida e ampliare la varietà di possibilità di flusso dei contenuti, sono disponibili tre tipi di modelli leggermente diversi. Potete utilizzarli facilmente per creare una newsletter personalizzata.

Tutti hanno un **header**, **piè di pagina** e **corpo** sezione . Sotto la sezione corpo, ogni modello differisce in **struttura a colonne** (1, 2 o 3 colonne).

![](assets/chlimage_1-69.png)

### Componenti {#components}

Al momento [sette componenti disponibili per l’utilizzo all’interno dei modelli di campagna](/help/sites-authoring/adobe-campaign-components.md). Questi componenti sono tutti basati sul linguaggio di markup Adobe **HTL**.

| **Nome componente** | **Percorso componente** |
|---|---|
| Intestazione | /libs/mcm/campaign/components/header |
| Immagine | /libs/mcm/campaign/components/image |
| Testo e personalizzazione | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Collegamento | /libs/mcm/campaign/components/reference |
| Modello immagini Dynamic Media Classic (precedentemente Scene7) | /libs/mcm/campaign/s7image |
| Riferimento mirato | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Questi componenti sono ottimizzati per il contenuto della posta; in altre parole, aderiscono alle best practice descritte nel presente documento. L’utilizzo di altri componenti predefiniti in genere viola queste regole.

Questi componenti sono descritti in dettaglio in [Componenti Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).
