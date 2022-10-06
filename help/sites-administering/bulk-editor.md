---
title: Editor in serie
seo-title: The Bulk Editor
description: Scopri come utilizzare l’editor in blocco.
seo-description: Learn how to use the Bulk Editor.
uuid: 5f5e4190-d9b2-40a6-8cf4-4b7aebe35ad3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3649cffb-418a-4ad6-862f-56346a831b0b
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 1%

---

# Editor in serie{#the-bulk-editor}

L’editor in serie consente di effettuare modifiche molto efficienti quando il contesto visivo della pagina non è necessario in quanto consente di:

* cercare (e visualizzare) contenuti da più pagine; questa operazione viene eseguita utilizzando GQL (Google Query Language)
* modifica il contenuto direttamente nell’editor in serie
* salva le modifiche (nelle pagine originarie)
* esporta il contenuto in un file di foglio di calcolo separato da tabulazioni (.tsv)

>[!NOTE]
>
>Puoi anche importare contenuti nell’archivio, ma per impostazione predefinita questa opzione è disabilitata per l’editor in blocco come disponibile nel **Strumenti** console.

Questa sezione descrive come lavorare con l’editor in serie nel **Strumenti** console. In genere, gli amministratori utilizzano l’editor in blocco per cercare e modificare più elementi. A tal fine, compila la tabella utilizzando una query GQL e seleziona gli elementi di contenuto su cui lavorare. Gli autori generalmente utilizzano l&#39;editor in blocco come parte di un&#39;applicazione di editor in blocco personalizzata accessibile tramite [elenco prodotti](/help/sites-authoring/default-components.md#productlist) componente.

>[!CAUTION]
>
>Con la [deprecazione dell’interfaccia classica](/help/release-notes/deprecated-removed-features.md) nella AEM 6.4, anche l’editor di massa è stato dichiarato obsoleto e pertanto l’Adobe non prevede di migliorare ulteriormente l’editor di massa.

## Esempio di utilizzo per l’editor in serie {#example-use-case-for-the-bulk-editor}

Ad esempio, se hai bisogno di tutti i nomi e gli indirizzi e-mail degli utenti che hanno compilato un particolare sondaggio, l’editor bulk può fornire tali informazioni ed esportarle in un foglio di calcolo.

Un esempio per illustrare un tale caso d’uso è incluso nel sito web Geometrixx:

1. Passa a **Supporto** e quindi alla pagina **Soddisfazione del servizio clienti** indagine.
1. **Modifica** la **Inizio del modulo** paragrafo. Nella finestra di dialogo, fai clic su **Avanzate** scheda , espandi **Configurazione azione**, quindi fai clic su **Visualizza dati..**.

   ![](assets/custsatsurvey.png)

1. L&#39;editor di massa è completamente personalizzabile. Anche se in questo esempio l&#39;editor di massa non consente agli utenti di modificare il contenuto, ma consente loro solo di esportare le informazioni in un foglio di calcolo.

   ![](assets/bulkeditor.png)

## Come utilizzare l’editor in blocco {#how-to-use-the-bulk-editor}

L’editor in serie consente di:

* [cerca il contenuto in base ai parametri di query, visualizza le proprietà specificate dei risultati in colonne, modifica il contenuto e salva le modifiche](#searching-and-editing-content)
* [per esportare il contenuto in un foglio di calcolo separato da tabulazioni](#exporting-content)

* [importazione di contenuto da un foglio di calcolo separato da tabulazioni](#importing-content)

### Ricerca e modifica dei contenuti {#searching-and-editing-content}

Per utilizzare l&#39;editor in blocco per modificare più elementi contemporaneamente:

1. In **Strumenti** nella console, fai clic su **Importatori** per espanderla.
1. Fai doppio clic sul pulsante **Editor in serie** per aprirlo.
1. Inserisci i requisiti per la selezione:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Proprietà</td>
  </tr>
  <tr>
   <td>Percorso directory principale</td>
   <td>Indica il percorso principale che l'editor in blocco cerca.<br /> Esempio, <code>/content/geometrixx/en</code>. L’editor in blocco esegue ricerche su tutti i nodi figlio.</td>
  </tr>
  <tr>
   <td>Parametri della ricerca</td>
   <td>Utilizzando i parametri GQL, immetti la stringa di ricerca che desideri cercare nell’archivio dall’editor in serie; ad esempio, <code>type:Page</code> cerca tutte le pagine nel percorso principale, <code>text:professional</code> cerca tutte le pagine che contengono la parola "professionale", e <code>"jcr:title":English</code> cerca tutte le pagine che hanno come titolo "Inglese". È possibile cercare solo le stringhe.</td>
  </tr>
  <tr>
   <td>Casella di controllo Modalità contenuto</td>
   <td>Selezionare questa casella di controllo per leggere le proprietà all'interno di <code>jcr:content</code> sotto-nodo dei risultati della ricerca, se esiste. Utilizza solo per le pagine. I nomi delle proprietà hanno il prefisso <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>Proprietà/Colonne</td>
   <td>Seleziona le caselle di controllo relative alle proprietà che desideri vengano restituite dall’editor in blocco. Le proprietà selezionate sono le intestazioni di colonna nel riquadro dei risultati. Per impostazione predefinita, il percorso del nodo viene visualizzato nei risultati.</td>
  </tr>
  <tr>
   <td>Proprietà personalizzate/Colonne</td>
   <td>Immetti altre proprietà non elencate nella <strong>Proprietà/Colonne</strong> campo . Queste proprietà personalizzate vengono visualizzate nel riquadro dei risultati. È possibile aggiungere più proprietà utilizzando una virgola per separare le proprietà. <i>Nota:</i> Se si aggiunge una proprietà personalizzata che non esiste ancora, AEM WCM visualizza una cella vuota. Quando modifichi la cella vuota e la salvi, la proprietà viene aggiunta al nodo. La nuova proprietà creata deve rispettare i vincoli del tipo di nodo e i namespace della proprietà.</td>
  </tr>
 </tbody>
</table>

Esempio:

![](assets/searchfilter.png)

1. Fai clic su **Ricerca**. L’editor in blocco visualizza i risultati.
Per l’esempio precedente, tutte le pagine che soddisfano i criteri di ricerca vengono restituite e visualizzate con le colonne richieste.

   ![](assets/chlimage_1-39.png)

1. Apporta le modifiche necessarie facendo doppio clic in una cella.

   ![](assets/srchresultedit.png)

1. Fai clic su **Salva** per salvare le modifiche (il **Salva** viene attivato dopo la modifica di una cella).

   >[!CAUTION]
   >
   >Le modifiche apportate qui vengono scritte nel contenuto dell’archivio; ad esempio, la pagina a cui si fa riferimento in **Percorso**.

#### Parametri di query GQL aggiuntivi {#additional-gql-query-parameters}

* **percorso:** Cerca solo i nodi sotto questo percorso. Se specifichi più di un termine con un prefisso del percorso, verrà considerato solo l&#39;ultimo.
* **tipo:** restituisce solo i nodi dei tipi di nodo specificati. Ciò include sia i tipi primari che i tipi di mixin. È possibile specificare più tipi di nodo separati da virgole. GQL restituirà nodi di qualsiasi tipo specificato.
* **ordine:** ordinare il risultato per le proprietà specificate. È possibile specificare più nomi di proprietà separati da virgola. Per ordinare il risultato in ordine decrescente, devi solo preimpostare il nome della proprietà con un meno. Ad esempio: order:-name. L’utilizzo di un segno più restituisce il risultato in ordine crescente, che è anche l’impostazione predefinita.
* **limite:** limita il numero di risultati utilizzando un intervallo. Ad esempio: limit:10..20 Si prega di notare che l&#39;intervallo è basato su zero, l&#39;inizio è inclusivo e la fine è esclusiva. È inoltre possibile specificare un intervallo aperto:limit:10. o limite:..20 Se i punti vengono omessi e viene specificato un solo valore, GQL restituirà al massimo questo numero di risultati. Ad esempio, limit:10 (restituirà i primi 10 risultati)

### Esportazione del contenuto {#exporting-content}

Potrebbe essere necessario esportare il contenuto e apportare modifiche in un foglio di calcolo Excel. Ad esempio, è possibile esportare una mailing list e modificare il prefisso di tutti i numeri di telefono elencati direttamente in Excel, aggiungere linee aggiuntive e così via.

Per esportare il contenuto:

1. Cerca il contenuto come descritto in [Ricerca e modifica dei contenuti](#searching-and-editing-content).
1. Fai clic su **Esporta** per esportare le modifiche in un foglio di calcolo Excel separato da tabulazioni. AEM WCM chiede dove si desidera scaricare il file.

   >[!NOTE]
   >
   >Per impostazione predefinita, le modifiche vengono codificate in [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) (noto anche come CP-1252). È possibile selezionare UTF-8 per esportare le modifiche in UTF-8.

   ![](assets/srchrsesultexport.png)

1. Seleziona il percorso e conferma che desideri scaricare il file.
1. Dopo aver scaricato il file, è possibile aprirlo dal programma del foglio di calcolo, ad esempio Microsoft Excel. Il programma per fogli di calcolo importa il file e lo converte in un formato foglio di calcolo.

   ![](assets/exportinexcel.png)

### Importazione di contenuto {#importing-content}

Per impostazione predefinita, la funzionalità di importazione è nascosta all’apertura dell’editor in blocco. È sufficiente aggiungere il parametro `hib=false` all’URL viene visualizzato il **Importa** nella pagina Modifiche in serie. Puoi importare il contenuto da qualsiasi carattere separato da tabulazioni ( `.tsv`). Per il corretto funzionamento dell’importazione, le intestazioni di colonna (prima riga di celle) devono corrispondere alle intestazioni di colonna della tabella in cui si esegue l’importazione.

>[!NOTE]
>
>Quando reimporti il contenuto, cancelli qualsiasi contenuto precedente per tali nodi. Fai attenzione a non sovrascrivere informazioni importanti.

Per importare contenuti:

1. Apri l’editor in blocco.
1. Aggiungi `?hib=false` all’URL, ad esempio:
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. Fai clic su **Importa**.
1. Seleziona la `.tsv` file. I dati vengono importati nell’archivio.
