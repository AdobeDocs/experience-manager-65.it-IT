---
title: Best practice per i modelli e-mail
seo-title: Best practice per i modelli e-mail
description: Best practice per la creazione di modelli per le e-mail in AEM.
seo-description: Best practice per la creazione di modelli per le e-mail in AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
translation-type: tm+mt
source-git-commit: 4333cfde433d00ddc4cb013b31fe52956791da46
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 1%

---


# Best practice per i modelli di e-mail {#best-practices-for-email-templates}

>[!CAUTION]
>
>I componenti e-mail AEM sono obsoleti. A causa della natura dell’e-mail, che unisce contenuto e stile, i componenti e-mail forniti out-of-the-box AEM diventano un riutilizzo limitato per i clienti, a causa della necessità di implementare stili personalizzati in qualsiasi componente sia necessario per i progetti.
>
>I componenti e-mail possono essere implementati a livello di progetto, e i componenti e-mail AEM obsoleti illustrano come ottenere questo risultato. Tuttavia, questi componenti obsoleti non devono essere utilizzati per i progetti.

Questo documento descrive alcune delle procedure ottimali per la progettazione delle e-mail e fornisce un modello di campagna e-mail ben sviluppato.

La campagna demo disponibile in AEM segue tutte queste best practice. Per ogni best practice viene descritto in che modo vengono implementate le best practice nella campagna demo.

Utilizzate queste best practice per la creazione di newsletter.

>[!NOTE]
>
>Tutto il contenuto della campagna deve essere creato in una pagina `master` di tipo `cq/personalization/components/ambitpage`.
>
>Ad esempio, se la struttura della campagna pianificata è simile a
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Assicurarsi che si trovi sotto una pagina `master`
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Durante la creazione di un modello di posta per  Adobe Campaign, è necessario includere la proprietà **acMapping** con il valore **mapRecipient** nel nodo **jcr:content** del modello, oppure non sarà possibile selezionare il modello di Adobe Campaign  in **Proprietà pagina** di AEM (campo disabilitato).

## Componente modello/pagina {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpagina***

<table>
 <tbody>
  <tr>
   <td><strong>Best practice</strong></td>
   <td><strong>Implementazione</strong></td>
  </tr>
  <tr>
   <td><p>Specificate il tipo di documento per garantire un rendering coerente.</p> <p>Aggiungi DOCTYPE all'inizio (HTML o XHTML)</p> </td>
   <td><p>È configurabile tramite la modifica della proprietà <i>cq:doctype</i> in<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>Il valore predefinito è "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Può essere modificato in "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Specificate la definizione del carattere per garantire il corretto rendering dei caratteri speciali.</p> <p>Aggiungi la dichiarazione CHARSET (ad esempio iso-8859-15, UTF-8) a &lt;head&gt;</p> </td>
   <td><p>È impostato su UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codificate tutta la struttura utilizzando l'elemento &lt;table&gt;. Per i layout più complessi, è necessario nidificare le tabelle per creare strutture complesse.</p> <p>L'e-mail dovrebbe avere un buon aspetto anche senza css.</p> </td>
   <td><p>Le tabelle vengono utilizzate in tutto il modello per strutturare il contenuto. Attualmente è possibile utilizzare un massimo di quattro tabelle nidificate (1 tabella di base + max. 3 livelli di nidificazione)</p> <p>&lt;div&gt; i tag vengono utilizzati solo in modalità di creazione per garantire la corretta modifica dei componenti.</p> </td>
  </tr>
  <tr>
   <td>Utilizzate gli attributi dell'elemento (come Margine di celle, Valore e Larghezza) per impostare le dimensioni della tabella. Questo forza una struttura di modello a scatola.</td>
   <td><p>Tutte le tabelle contengono gli attributi necessari come <i>border</i>, <i>cellpadding</i>, <i>cellespace</i> e <i>width</i>.</p> <p>Per armonizzare il posizionamento degli elementi all'interno delle tabelle, tutte le celle delle tabelle dispongono dell'attributo <i>valign="top"</i> impostato.</p> </td>
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
   <td>La <i>larghezza</i> della tabella di contenuti è limitata a 600 px nella progettazione demo.</td>
  </tr>
 </tbody>
</table>

### Immagini {#images}

/libs/mcm/campaign/components/image

| **Best practice** | **Implementazione** |
|---|---|
| Aggiungere gli attributi *alt* alle immagini | L&#39;attributo *alt* è stato definito come obbligatorio per il componente immagine. |
| Utilizzare il formato *jpg* anziché *png* per le immagini | Le immagini saranno sempre servite come JPG dal componente immagine. |
| Utilizzate l&#39;elemento `<img>` invece delle immagini di sfondo in una tabella. | Nei modelli non vengono utilizzati dati immagine di sfondo. |
| Aggiungi attribute style=&quot;display block&quot; sulle immagini. Consente di visualizzare bene su Gmail. | Tutte le immagini contengono per impostazione predefinita l&#39;attributo *style=&quot;display block&quot;*. |

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
   <td>Utilizzate i font di base tra piattaforme come <i>Arial, Verdana, Georgia</i> e <i>Times New Roman</i>.</td>
   <td><p>Dipende dalla progettazione della newsletter.</p> <p>Per la progettazione demo viene utilizzato il font "Helvetica", ma, se non presente, ritornerà al font sans-serif generico.</p> </td>
  </tr>
 </tbody>
</table>

### Generico {#generic}

| **Best practice** | **Implementazione** |
|---|---|
| Utilizzate la funzione di convalida W3C per correggere il codice HTML. Accertatevi che tutti i tag aperti siano chiusi correttamente. | Il codice è stato convalidato. Per XHTML Transitional Doctype manca solo l&#39;attributo xmlns mancante per l&#39;elemento `<html>`. |
| Non preoccupatevi di JavaScript o di Flash; tali tecnologie non sono in gran parte supportate dai client e-mail. | Né JavaScript né Flash vengono utilizzati nel modello per newsletter. |
| Aggiungete una versione di testo normale per l’invio multiparte. | Un nuovo widget è stato creato nelle proprietà della pagina per estrarre facilmente una versione in testo normale dal contenuto della pagina. Può essere utilizzato come punto di partenza per la versione normale finale. |

## Modelli ed esempi per newsletter per campagne {#campaign-newsletter-templates-and-examples}

AEM con diversi modelli e componenti per la creazione di newsletter per le campagne. Potete usare questi modelli e componenti per creare newsletter personalizzate.

### Modelli {#templates}

Per offrire una base solida e ampliare le possibilità di flusso dei contenuti, sono disponibili tre tipi di modelli leggermente diversi. Potete facilmente utilizzarli per creare una newsletter personalizzata.

Tutti hanno una sezione **header**, un **piè di pagina** e una sezione **body**. Sotto la sezione corpo, ogni modello è diverso in **struttura delle colonne** (1, 2 o 3 colonne).

![](assets/chlimage_1-69.png)

### Componenti {#components}

Attualmente sono disponibili [sette componenti da utilizzare nei modelli delle campagne](/help/sites-authoring/adobe-campaign-components.md). Tutti questi componenti sono basati sul linguaggio di marcatura  Adobe **HTL**.

| **Nome componente** | **Percorso componente** |
|---|---|
| Intestazione | /libs/mcm/campaign/components/heading |
| Immagine | /libs/mcm/campaign/components/image |
| Testo e personalizzazione | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Collegamento | /libs/mcm/campaign/components/reference |
| Modello per immagini Dynamic Media Classic (già Scene7) | /libs/mcm/campaign/s7image |
| Riferimento mirato | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Questi componenti sono ottimizzati per il contenuto della posta; in altre parole, aderiscono alle best practice illustrate nel presente documento. L&#39;utilizzo di altri componenti forniti di solito viola tali regole.

Questi componenti sono descritti in dettaglio in [ componenti Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).