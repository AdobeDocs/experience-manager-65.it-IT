---
title: Proprietà di configurazione della gestione della corrispondenza
seo-title: Proprietà di configurazione della gestione della corrispondenza
description: Questo argomento spiega come modificare Asset Composer con configurazioni specifiche per la soluzione. Questo argomento descrive le proprietà che è possibile modificare, con la relativa descrizione, i valori predefiniti e i valori accettabili.
seo-description: Questo argomento spiega come modificare Asset Composer con configurazioni specifiche per la soluzione. Questo argomento descrive le proprietà che è possibile modificare, con la relativa descrizione, i valori predefiniti e i valori accettabili.
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 4%

---


# Proprietà di configurazione della gestione della corrispondenza {#correspondence-management-configuration-properties}

Per configurare queste proprietà, apri il seguente URL in un browser: `https://<server>:<port>/<contextPath>/system/console/configMgr` e seleziona **Configurazioni di gestione della corrispondenza**.

La gestione della corrispondenza ha le seguenti proprietà di configurazione:

<table>
 <tbody>
  <tr>
   <th><p><strong>Proprietà</strong></p> </th>
   <th><p><strong>Descrizione</strong></p> </th>
   <th><p><strong>Predefiniti</strong></p> </th>
   <th><p><strong>Valori accettabili</strong></p> </th>
  </tr>
  <tr>
   <td><p>Rientro</p> </td>
   <td>Rientro sui moduli<p> </p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Qualsiasi numero</p> </td>
  </tr>
  <tr>
   <td>Larghezza minima</td>
   <td>Larghezza minima da applicare al campo punto elenco/numero quando si utilizzano elenchi numerati diversi dai numeri romani</td>
   <td>8,0 mm</td>
   <td>Qualsiasi numero</td>
  </tr>
  <tr>
   <td><p>Larghezza minima numeri romani</p> </td>
   <td><p>Larghezza minima da applicare al campo punto elenco/numero quando si utilizzano numeri romani</p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Qualsiasi numero</p> </td>
  </tr>
  <tr>
   <td>Tipo di rappresentazione</td>
   <td>Il tipo di rendering utilizzato dall'applicazione Create Correspondence per eseguire il rendering dell'anteprima della lettera. </td>
   <td>Rendering HTML</td>
   <td>Rendering HTML / Rendering PDF</td>
  </tr>
  <tr>
   <td><p>Attiva evidenziazione PDF CCR</p> </td>
   <td><p>Abilita l’evidenziazione su PDF nell’applicazione Crea corrispondenza</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Tipo di evidenziazione di Target</p> </td>
   <td><p>Tipo di evidenziazione di Target nell’applicazione Crea corrispondenza</p> </td>
   <td><p>border</p> </td>
   <td><p>bordo / riempimento / nessuno</p> </td>
  </tr>
  <tr>
   <td><p>Colore evidenziazione destinazione</p> </td>
   <td><p>Colore evidenziazione target nell’applicazione Crea corrispondenza</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>Qualsiasi colore RGB nel formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo di evidenziazione del contenuto</p> </td>
   <td><p>Tipo di evidenziazione del contenuto nell’applicazione Crea corrispondenza</p> </td>
   <td><p>Riempimento</p> </td>
   <td><p>bordo / riempimento / nessuno</p> </td>
  </tr>
  <tr>
   <td><p>Colore evidenziazione contenuto</p> </td>
   <td><p>Colore evidenziazione contenuto nell’applicazione Crea corrispondenza</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualsiasi colore RGB nel formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo di evidenziazione del campo</p> </td>
   <td><p>Tipo di evidenziazione del campo nell’applicazione Crea corrispondenza</p> </td>
   <td><p>fill</p> </td>
   <td><p>bordo / riempimento / nessuno</p> </td>
  </tr>
  <tr>
   <td><p>Colore evidenziatore campo</p> </td>
   <td><p>Colore evidenziazione campo nell’applicazione Crea corrispondenza</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualsiasi colore RGB nel formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Timeout applicazione</p> </td>
   <td><p>Timeout applicazione in secondi</p> </td>
   <td><p>1200</p> </td>
   <td><p>Qualsiasi numero</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro del documento PDF</p> </td>
   <td><p>Nome del parametro per il documento PDF in fase di post-elaborazione</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro dati XML</p> </td>
   <td><p>Nome del parametro per il documento XML (dati) nel processo post</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Nome del parametro del documento XDP</p> </td>
   <td><p>Nome del parametro per il documento XDP inviato al processo post</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro URL di reindirizzamento</p> </td>
   <td><p>Nome del parametro per l'URL di reindirizzamento inviato dal processo post Questo valore può essere un nome di variabile stringa</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Tipo di invio PDF</p> </td>
   <td><p>Tipo di invio PDF (tipo di PDF generato all’invio dall’applicazione Crea corrispondenza)</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>interattivo/non interattivo</p> </td>
  </tr>
  <tr>
   <td><p>Ottimizza istanza del dizionario dati</p> </td>
   <td><p>Consente il trasferimento ottimizzato del server e del client dell’istanza del dizionario dati</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Correzione automatica delle incongruenze </p> </td>
   <td><p>Quando è attivata, gestisce automaticamente le eventuali incongruenze nelle assegnazioni di lettere</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Usa formati dati configurati</p> </td>
   <td><p>Controlla se utilizzare i formati di modifica dei dati configurati e il formato di visualizzazione dei dati</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Formati di visualizzazione dei dati</p> </td>
   <td><p>Specifica il formato di visualizzazione specifico per le impostazioni internazionali per i dati</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>Formato di modifica dati</p> </td>
   <td><p>Modifica il formato dei dati. Viene utilizzato quando si scrivono dati come String o si analizzano dati da String</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>Gestisci istanze lettera su pubblicazione</p> </td>
   <td><p>Attiva/Disattiva la funzionalità Gestisci lettere (applicabile solo per Publish Server)</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo. Se false, i registri di controllo per tutte le azioni verranno disabilitati.</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo lettura</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo per la lettura delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita creazione controllo</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo per la creazione delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo aggiornamento</p> </td>
   <td><p>Attivare/disattivare la funzionalità di controllo per l’aggiornamento delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo di ripristino</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo per il ripristino delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo pubblicazione</p> </td>
   <td><p>Attivare/disattivare la funzionalità di controllo per la pubblicazione delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo SaveAsDraft</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo per il salvataggio delle bozze di lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo invio</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo per l'invio delle lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo e-mail</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo per le lettere di posta elettronica</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo stampa</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo per la stampa delle lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo consegna personalizzato</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo per la consegna personalizzata delle lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Nome del parametro dei documenti allegati</p> </td>
   <td><p>Nome del parametro per i documenti allegati inviati al processo post</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Directory principale utente di CM</p> </td>
   <td><p>URL della cartella contenente tutte le risorse utente di Gestione Corrispondenza</p> </td>
   <td><p>—</p> </td>
   <td><p>Posizione cartella valida</p> </td>
  </tr>
  <tr>
   <td><p>Dimensione cache lettera</p> </td>
   <td><p>Specifica il numero massimo di lettere da conservare nella cache.</p> <p>La modifica di questo valore comporterà la pulizia della cache <code>in-memory</code>.</p> </td>
   <td><p>100</p> </td>
   <td><p>Qualsiasi valore numerico</p> </td>
  </tr>
  <tr>
   <td><p>Abilita cache lettera</p> </td>
   <td><p>Attiva/Disattiva la cache delle lettere.</p> <p>La modifica di questo valore comporterà la pulizia della cache <code>in-memory </code>.</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Ordinamento degli elementi dati</p> </td>
   <td><p>Mantiene l’ordinamento degli elementi dati in un’interfaccia per la corrispondenza in base alla sequenza in Letter</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Ricarica supporto</p> </td>
   <td><p>Attiva/Disattiva il supporto per il ricaricamento nelle lettere sottoposte a rendering sul lato server.</p> <p>La disattivazione di questa opzione migliorerà le prestazioni di rendering delle lettere.</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Cartella temporanea</td>
   <td>Posizione della cartella temporanea.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Salvataggio remoto</td>
   <td>Salva le istanze della lettera sull'autore di elaborazione specificato.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Opzioni di compatibilità</td>
   <td>Opzioni di compatibilità del formato configname:configvalue separate da virgola.</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Directory di debug </p> <p> </p> </td>
   <td>Percorso della cartella del file system per il debug. Se la directory non <code>exists</code>, non verranno generate immagini di debug.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
