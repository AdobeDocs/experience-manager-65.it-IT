---
title: Best practice per i modelli e-mail
seo-title: Best Practices for Email Templates
description: Scopri le best practice per la creazione di modelli e-mail in AEM.
seo-description: Find best practices on creating email templates in AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: 70be796a50a93267b965d00db1b359d9a809ec08
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 1%

---

# Best practice per i modelli e-mail {#best-practices-for-email-templates}

>[!CAUTION]
>
>Questo articolo si applica ai componenti e-mail AEM basati su Componenti di base obsoleti.
>
>Gli utenti sono incoraggiati a sfruttare il moderno [Componenti core E-mail.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)

Questo documento descrive alcune delle best practice relative alla progettazione delle e-mail, che si traducono in un modello di campagna e-mail ben sviluppato.

La campagna dimostrativa disponibile nell’AEM segue tutte queste best practice. Per ogni best practice viene descritto come implementare le best practice nella campagna demo.

Utilizza queste best practice per creare una newsletter personalizzata.

>[!NOTE]
>
>Tutto il contenuto della campagna deve essere creato in un `master` pagina di tipo `cq/personalization/components/ambitpage`.
>
>Ad esempio, se la struttura pianificata della campagna è simile a
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Assicurati che risieda in un `master` pagina
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Quando crei un modello di posta per Adobe Campaign, devi includere la proprietà **acMapping** con il valore **mapRecipient** nel **jcr:content** del modello, oppure non sarà possibile selezionare il modello Adobe Campaign in **Proprietà pagina** dell’AEM (campo disabilitato).

## Componente modello/pagina {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>Best practice</strong></td>
   <td><strong>Implementazione</strong></td>
  </tr>
  <tr>
   <td><p>Specificare il tipo di documento per garantire un rendering coerente.</p> <p>Aggiungi DOCTYPE all’inizio (HTML o XHTML)</p> </td>
   <td><p>È configurabile modificando il <i>cq:doctype</i> proprietà in<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>Il valore predefinito è "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Può essere modificato in "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Specifica la definizione del carattere per garantire il rendering corretto dei caratteri speciali.</p> <p>Aggiungere la dichiarazione CHARSET (ad esempio iso-8859-15, UTF-8) a &lt;head&gt;</p> </td>
   <td><p>È impostato su UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codifica tutta la struttura utilizzando &lt;table&gt;elemento. Per i layout più complessi, è consigliabile nidificare le tabelle per creare strutture complesse.</p> <p>L’e-mail dovrebbe avere un buon aspetto anche senza CSS.</p> </td>
   <td><p>Le tabelle vengono utilizzate in tutto il modello per strutturare il contenuto. Attualmente in uso un massimo di quattro tabelle nidificate (1 tabella di base + max. 3 livelli di nidificazione)</p> <p>&lt;div&gt; I tag vengono utilizzati solo in modalità di authoring per garantire la modifica corretta dei componenti.</p> </td>
  </tr>
  <tr>
   <td>Utilizzare gli attributi degli elementi (come cellpadding, valign e width) per impostare le dimensioni della tabella. In questo modo viene forzata una struttura del modello di casella.</td>
   <td><p>Tutte le tabelle contengono attributi necessari come <i>bordo</i>, <i>cellpadding</i>, <i>cellspacing</i> e <i>larghezza</i>.</p> <p>Per armonizzare il posizionamento degli elementi all'interno delle tabelle, tutte le celle delle tabelle hanno l'attributo <i>valign="top"</i> in fase di impostazione.</p> </td>
  </tr>
  <tr>
   <td><p>Conto per la cordialità mobile, se possibile. Utilizza le query multimediali per aumentare le dimensioni del testo su schermi di piccole dimensioni e fornire aree di hit di dimensioni ridotte per i collegamenti.</p> <p>Se la progettazione lo consente, rendi dinamico un’e-mail.</p> </td>
   <td>Per quanto riguarda l’utilizzo degli stili CSS per illustrare la progettazione demo, le query multimediali vengono utilizzate per offrire una versione mobile.</td>
  </tr>
  <tr>
   <td>CSS in linea è meglio che inserire tutti i CSS all’inizio.</td>
   <td><p>Per dimostrare meglio la struttura di base dei HTML e facilitare la possibilità di personalizzare la struttura delle newsletter, sono state allineate solo alcune definizioni CSS.</p> <p>Gli stili di base e le varianti di modello sono stati estratti in un blocco di stile nel &lt;head&gt; della pagina. Al momento della presentazione finale della newsletter, queste definizioni CSS devono essere allineate nel HTML. È previsto un meccanismo di inlinening automatico, ma al momento non disponibile.</p> </td>
  </tr>
  <tr>
   <td>Semplifica il tuo CSS. Evita dichiarazioni di stile composte, codice abbreviato, proprietà di layout CSS, selettori complessi e pseudo-elementi.</td>
   <td>Per quanto riguarda l’utilizzo degli stili CSS per illustrare la progettazione demo, vengono seguiti i consigli CSS.</td>
  </tr>
  <tr>
   <td>La larghezza massima delle e-mail deve essere 600-800 pixel. In questo modo si comportano meglio all’interno delle dimensioni del riquadro di anteprima fornite da molti client.</td>
   <td>Il <i>larghezza</i> della tabella dei contenuti è limitato a 600 px nella progettazione demo.</td>
  </tr>
 </tbody>
</table>

### Immagini {#images}

/libs/mcm/campaign/components/image

| **Best practice** | **Implementazione** |
|---|---|
| Aggiungi *Alt* attributi per le immagini | Il *Alt* L’attributo è stato definito come obbligatorio per il componente immagine. |
| Utilizzare *jpg* invece di *png* formato per le immagini | Le immagini verranno sempre utilizzate come JPG dal componente immagine. |
| Utilizzare `<img>` anziché immagini di sfondo in una tabella. | Nei modelli non vengono utilizzati dati immagine di sfondo. |
| Aggiungi attributo style=&quot;display block&quot; sulle immagini. Permette una buona visualizzazione su Gmail. | Per impostazione predefinita, tutte le immagini contengono *style=&quot;display block&quot;* attributo. |

### Testo e collegamenti {#text-and-links}

/libs/mcm/campaign/components/header, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Best practice</strong></td>
   <td><strong>Implementazione</strong></td>
  </tr>
  <tr>
   <td>Utilizza html invece dello stile in CSS (font-family)</td>
   <td>RichTextEditor (ad esempio, nel componente textimage) ora supporta la scelta e l’applicazione di famiglie e dimensioni di font ai testi selezionati. Verrà eseguito il rendering come tag.</td>
  </tr>
  <tr>
   <td>Utilizza font di base multipiattaforma, ad esempio <i>Arial, Verdana, Georgia</i> e <i>Times New Roman</i>.</td>
   <td><p>Dipende dalla progettazione delle newsletter.</p> <p>Per la progettazione demo viene utilizzato il font "Helvetica", ma se non presente, tornerà al font sans-serif generico.</p> </td>
  </tr>
 </tbody>
</table>

### Generico {#generic}

| **Best practice** | **Implementazione** |
|---|---|
| Utilizza la convalida W3C per correggere il codice HTML. Assicurati che tutti i tag aperti siano chiusi correttamente. | Il codice è stato convalidato. Per il Doctype transitorio XHTML, solo l’attributo xmlns mancante per il `<html>` elemento mancante. |
| Non preoccuparti di JavaScript o Flash: queste tecnologie non sono in gran parte supportate dai client e-mail. | Nel modello di newsletter non viene utilizzato né JavaScript né Flash. |
| Aggiungi una versione in testo normale per l’invio in più parti. | Un nuovo widget è stato creato nelle proprietà della pagina per estrarre facilmente una versione di testo normale dal contenuto della pagina. Questo può essere utilizzato come punto di partenza per la versione finale del testo normale. |

## Modelli ed esempi di newsletter di Campaign {#campaign-newsletter-templates-and-examples}

L’AEM viene fornito con diversi modelli e componenti pronti all’uso per la creazione di newsletter di campagne. È possibile utilizzare questi modelli e componenti per creare newsletter personalizzate.

### Modelli {#templates}

Per offrire una base solida e ampliare la varietà di possibilità di flusso dei contenuti, sono disponibili tre tipi di modelli leggermente diversi. Puoi utilizzarli facilmente per creare una newsletter personalizzata.

Tutti hanno un **intestazione**, a **footer** e un **corpo** sezione. Sotto la sezione del corpo, ogni modello differisce in **progettazione colonna** (1, 2 o 3 colonne)

![](assets/chlimage_1-69.png)

### Componenti {#components}

Al momento sono presenti [sette componenti disponibili per l’utilizzo all’interno dei modelli di campagna](/help/sites-authoring/adobe-campaign-components.md). Questi componenti sono tutti basati sul linguaggio di markup Adobe **HTL**.

| **Nome componente** | **Percorso componente** |
|---|---|
| Intestazione | /libs/mcm/campaign/components/header |
| Immagine | /libs/mcm/campaign/components/image |
| Testo e personalizzazione | /libs/mcm/campaign/components/personalization |
| Texttimage | /libs/mcm/campaign/components/textimage |
| Collegamento | /libs/mcm/campaign/components/reference |
| Modello immagine Dynamic Media Classic (precedentemente Scene7) | /libs/mcm/campaign/s7image |
| Riferimento di destinazione | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Questi componenti sono ottimizzati per il contenuto della posta, ovvero sono conformi alle best practice descritte in questo documento. L’utilizzo di altri componenti pronti all’uso generalmente viola queste regole.

Questi componenti sono descritti in dettaglio in [Componenti di Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).
