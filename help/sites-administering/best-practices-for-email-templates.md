---
title: Best practice per i modelli e-mail
seo-title: Best practice per i modelli e-mail
description: Best practice per la creazione di modelli di e-mail in AEM.
seo-description: Best practice per la creazione di modelli di e-mail in AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
translation-type: tm+mt
source-git-commit: bd0cb6abe024bc4ff77c9932c99b816c832377f5

---


# Best practice per i modelli e-mail {#best-practices-for-email-templates}

>[!CAUTION]
>
>I componenti e-mail di AEM non sono più disponibili. A causa della natura dell’e-mail, che unisce contenuto e stile, i componenti e-mail forniti out-of-the-box da AEM diventano un utilizzo limitato per i clienti, a causa della necessità di implementare stili personalizzati in qualsiasi componente sia necessario per i progetti.
>
>I componenti e-mail possono essere implementati a livello di progetto, e i componenti e-mail AEM obsoleti illustrano come ottenere questo risultato. Tuttavia, questi componenti obsoleti non devono essere utilizzati nei progetti.

Questo documento descrive alcune delle procedure ottimali per la progettazione delle e-mail e fornisce un modello di campagna e-mail ben sviluppato.

La campagna dimostrativa disponibile in AEM segue tutte queste best practice. Per ogni best practice viene descritto in che modo vengono implementate le best practice nella campagna demo.

Utilizzate queste best practice per la creazione di newsletter.

>[!NOTE]
>
>Tutto il contenuto della campagna deve essere creato sotto una `master` pagina di tipo `cq/personalization/components/ambitpage`.
>
>Ad esempio, se la struttura della campagna pianificata è simile a
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>È necessario assicurarsi che si trovi sotto una `master` pagina
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Quando crei un modello di posta elettronica per Adobe Campaign, devi includere la proprietà **acMapping** con il valore **mapRecipient** nel nodo **jcr:content** del modello, oppure non sarai in grado di selezionare il modello Adobe Campaign in Proprietà **** pagina di AEM (campo disabilitato).

## Modello/componente pagina {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpagina***

<table>
 <tbody>
  <tr>
   <td><strong>Best practice</strong></td>
   <td><strong>Implementazione</strong></td>
  </tr>
  <tr>
   <td><p>Specificate il tipo di documento per garantire un rendering coerente.</p> <p>Aggiungi DOCTYPE all'inizio (HTML o XHTML)</p> </td>
   <td><p>È configurabile tramite la modifica della proprietà <i>cq:doctype</i> in<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>Il valore predefinito è "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transition//IT" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Può essere modificato in "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Specificate la definizione del carattere per garantire il corretto rendering dei caratteri speciali.</p> <p>Aggiungi la dichiarazione CHARSET (ad esempio iso-8859-15, UTF-8) a &lt;head&gt;</p> </td>
   <td><p>È impostato su UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codificate tutta la struttura utilizzando l'elemento &lt;table&gt;. Per i layout più complessi, è necessario nidificare le tabelle per creare strutture complesse.</p> <p>Le e-mail dovrebbero avere un buon aspetto anche senza css.</p> </td>
   <td><p>Le tabelle vengono utilizzate in tutto il modello per strutturare il contenuto. Attualmente è possibile utilizzare un massimo di quattro tabelle nidificate (1 tabella di base + max. 3 livelli di nidificazione)</p> <p>I tag &lt;div&gt; vengono utilizzati solo in modalità di creazione per garantire la corretta modifica dei componenti.</p> </td>
  </tr>
  <tr>
   <td>Utilizzate gli attributi dell'elemento (come Margine di celle, Valore e Larghezza) per impostare le dimensioni della tabella. Questo forza una struttura di modello a scatola.</td>
   <td><p>Tutte le tabelle contengono attributi necessari come <i>bordo</i>, <i>margine</i>celle, <i>spaziatura</i> celle e <i>larghezza</i>.</p> <p>Per armonizzare il posizionamento degli elementi all'interno delle tabelle, tutte le celle delle tabelle presentano l'attributo <i>valign="top"</i> impostato.</p> </td>
  </tr>
  <tr>
   <td><p>Se possibile, tenete conto della facilità di utilizzo dei dispositivi mobili. Le media query consentono di aumentare le dimensioni del testo sugli schermi di piccole dimensioni e di fornire aree di hit di dimensioni ridotte per i collegamenti.</p> <p>Se la progettazione lo consente, rendete l'e-mail reattiva.</p> </td>
   <td>Per quanto riguarda gli stili CSS utilizzati per illustrare la progettazione demo, le media query vengono utilizzate per offrire una versione semplice per dispositivi mobili.</td>
  </tr>
  <tr>
   <td>Il CSS in linea è meglio che mettere tutti i CSS all'inizio.</td>
   <td><p>Per illustrare meglio la struttura HTML sottostante e semplificare la possibilità di personalizzare la struttura della newsletter, sono state allineate solo alcune definizioni CSS.</p> <p>Gli stili di base e le varianti di modello sono stati estratti in un blocco di stile in &lt;head&gt; della pagina. All’invio finale della newsletter, queste definizioni CSS devono essere allineate nell’HTML. È pianificato un meccanismo automatico di inlinening, ma attualmente non disponibile.</p> </td>
  </tr>
  <tr>
   <td>Semplificate il CSS. Evitate dichiarazioni di stile composto, codice abbreviato, proprietà di layout CSS, selettori complessi e pseudo-elementi.</td>
   <td>Per quanto riguarda gli stili CSS utilizzati per illustrare la progettazione demo, le raccomandazioni CSS vengono seguite.</td>
  </tr>
  <tr>
   <td>Le e-mail devono avere una larghezza massima di 600-800 pixel. Questo li renderà più efficienti nelle dimensioni del riquadro di anteprima fornite da molti client.</td>
   <td>La <i>larghezza</i> della tabella dei contenuti è limitata a 600 pixel nella progettazione demo.</td>
  </tr>
 </tbody>
</table>

### Immagini {#images}

/libs/mcm/campaign/components/image

| **Best practice** | **Implementazione** |
|---|---|
| Aggiungere attributi *alt* alle immagini | L’attributo *alt* è stato definito come obbligatorio per il componente immagine. |
| Per le immagini, usate *jpg* invece del formato *png* | Le immagini saranno sempre servite come JPG dal componente immagine. |
| Utilizzate <img> elementi invece delle immagini di sfondo in una tabella. | Nei modelli non vengono utilizzati dati immagine di sfondo. |
| Aggiungi attribute style=&quot;display block&quot; sulle immagini. Consente di visualizzare bene su Gmail. | Tutte le immagini contengono per impostazione predefinita l’attributo *style=&quot;display block&quot;* . |

### Testo e collegamenti {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/texttimage

<table>
 <tbody>
  <tr>
   <td><strong>Best practice</strong></td>
   <td><strong>Implementazione</strong></td>
  </tr>
  <tr>
   <td>Utilizzare html &lt;font&gt; invece dello stile in CSS (font-family)</td>
   <td>RichTextEditor (ad esempio, nel componente Textage) ora supporta la scelta e l'applicazione di famiglie di font e dimensioni di font ai testi selezionati. Il rendering verrà eseguito come tag &lt;font&gt;.</td>
  </tr>
  <tr>
   <td>Utilizzate font di base tra piattaforme come <i>Arial, Verdana, Georgia</i> e <i>Times New Roman</i>.</td>
   <td><p>Dipende dalla progettazione della newsletter.</p> <p>Per la progettazione demo viene utilizzato il font "Helvetica", ma, se non presente, ritornerà al font sans-serif generico.</p> </td>
  </tr>
 </tbody>
</table>

### Generico {#generic}

| **Best practice** | **Implementazione** |
|---|---|
| Utilizzate la funzione di convalida W3C per correggere il codice HTML. Accertatevi che tutti i tag aperti siano chiusi correttamente. | Il codice è stato convalidato. Per XHTML Transitional Doctype solo l&#39;attributo xmlns mancante per <html> elemento mancante. |
| Non preoccupatevi di JavaScript o Flash; tali tecnologie non sono in gran parte supportate dai client e-mail. | Nel modello per newsletter non vengono utilizzati JavaScript né Flash. |
| Aggiungete una versione di testo normale per l’invio multiparte. | Un nuovo widget è stato creato nelle proprietà della pagina per estrarre facilmente una versione in testo normale dal contenuto della pagina. Può essere utilizzato come punto di partenza per la versione normale finale. |

## Modelli ed esempi per newsletter per campagne {#campaign-newsletter-templates-and-examples}

Con AEM sono disponibili diversi modelli e componenti per la creazione di newsletter per le campagne. Potete usare questi modelli e componenti per creare newsletter personalizzate.

### Modelli {#templates}

Per offrire una base solida e ampliare le possibilità di flusso dei contenuti, sono disponibili tre tipi di modelli leggermente diversi. Potete facilmente utilizzarli per creare una newsletter personalizzata.

Tutti hanno un&#39; **intestazione**, un **piè di pagina** e una sezione **corpo** . Sotto la sezione body, ogni modello è diverso nella struttura **delle** colonne (1, 2 o 3 colonne).

![](assets/chlimage_1-69.png)

### Componenti {#components}

Al momento sono disponibili [sette componenti da utilizzare nei modelli](/help/sites-authoring/adobe-campaign-components.md)delle campagne. Tutti questi componenti sono basati sul linguaggio di marcatura Adobe **HTL**.

| **Nome componente** | **Percorso componente** |
|---|---|
| Intestazione | /libs/mcm/campaign/components/heading |
| Immagine | /libs/mcm/campaign/components/image |
| Testo e personalizzazione | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Collegamento | /libs/mcm/campaign/components/reference |
| Modello immagini Scene7 | /libs/mcm/campaign/s7image |
| Riferimento mirato | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Questi componenti sono ottimizzati per il contenuto della posta; in altre parole, aderiscono alle best practice illustrate nel presente documento. L&#39;utilizzo di altri componenti forniti di solito viola tali regole.

Questi componenti sono descritti dettagliatamente nei componenti [di](/help/sites-authoring/adobe-campaign-components.md)Adobe Campaign.