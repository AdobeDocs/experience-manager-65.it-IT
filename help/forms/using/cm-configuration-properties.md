---
title: Proprietà di configurazione della gestione della corrispondenza
seo-title: Proprietà di configurazione della gestione della corrispondenza
description: In questo argomento viene illustrato come modificare Asset Composer con configurazioni specifiche della soluzione. In questo argomento vengono descritte dettagliatamente le proprietà che è possibile modificare, con descrizione, valori predefiniti e valori accettabili.
seo-description: In questo argomento viene illustrato come modificare Asset Composer con configurazioni specifiche della soluzione. In questo argomento vengono descritte dettagliatamente le proprietà che è possibile modificare, con descrizione, valori predefiniti e valori accettabili.
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 3%

---


# Proprietà di configurazione della gestione della corrispondenza {#correspondence-management-configuration-properties}

Per configurare queste proprietà, aprite il seguente URL in un browser: `https://<server>:<port>/<contextPath>/system/console/configMgr` e selezionare **Configurazioni di gestione della corrispondenza**.

Gestione corrispondenza ha le seguenti proprietà di configurazione:

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
   <td><p>Numero qualsiasi</p> </td>
  </tr>
  <tr>
   <td>Larghezza minima</td>
   <td>Larghezza minima da applicare al campo punto elenco/numero quando si utilizzano elenchi numerati, ad eccezione dei numeri romani</td>
   <td>8,0 mm</td>
   <td>Numero qualsiasi</td>
  </tr>
  <tr>
   <td><p>Larghezza minima numeri romani</p> </td>
   <td><p>Larghezza minima da applicare al campo punto elenco/numero quando si utilizzano i numeri romani</p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Numero qualsiasi</p> </td>
  </tr>
  <tr>
   <td>Tipo di rappresentazione</td>
   <td>Il tipo di rappresentazione utilizzata dall'applicazione Crea corrispondenza per rappresentare l'anteprima della lettera. </td>
   <td>Rendering HTML</td>
   <td>Rappresentazione HTML/PDF</td>
  </tr>
  <tr>
   <td><p>Attiva evidenziazione CCR PDF</p> </td>
   <td><p>Abilita l'evidenziazione su PDF nell'applicazione Crea corrispondenza</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Tipo di evidenziazione destinazione</p> </td>
   <td><p>Tipo di evidenziazione di destinazione nell'applicazione Create Correspondence</p> </td>
   <td><p>border</p> </td>
   <td><p>border / fill / none</p> </td>
  </tr>
  <tr>
   <td><p>Colore evidenziazione destinazione</p> </td>
   <td><p>Colore evidenziazione destinazione nell’applicazione Crea corrispondenza</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>Qualsiasi colore RGB nel formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo di evidenziazione del contenuto</p> </td>
   <td><p>Tipo di evidenziazione del contenuto nell'applicazione Crea corrispondenza</p> </td>
   <td><p>Riempimento</p> </td>
   <td><p>border / fill / none</p> </td>
  </tr>
  <tr>
   <td><p>Colore evidenziazione contenuto</p> </td>
   <td><p>Colore evidenziazione contenuto nell’applicazione Crea corrispondenza</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualsiasi colore RGB nel formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo evidenziazione campo</p> </td>
   <td><p>Tipo di evidenziazione dei campi nell’applicazione Crea corrispondenza</p> </td>
   <td><p>fill</p> </td>
   <td><p>border / fill / none</p> </td>
  </tr>
  <tr>
   <td><p>Colore evidenziazione campo</p> </td>
   <td><p>Colore evidenziazione campo nell’applicazione Crea corrispondenza</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualsiasi colore RGB nel formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Timeout applicazione</p> </td>
   <td><p>Timeout applicazione in secondi</p> </td>
   <td><p>1200</p> </td>
   <td><p>Numero qualsiasi</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro del documento PDF</p> </td>
   <td><p>Nome parametro per il documento PDF in fase di post-elaborazione</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro dati XML</p> </td>
   <td><p>Nome del parametro per il documento XML (dati) in fase di post-elaborazione</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro documento XDP</p> </td>
   <td><p>Nome del parametro per il documento XDP inviato al processo post</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro URL di reindirizzamento</p> </td>
   <td><p>Nome del parametro per l'URL di reindirizzamento inviato dal processo post Questo valore può essere qualsiasi nome di variabile stringa</p> </td>
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
   <td><p>Ottimizza istanza dizionario dati</p> </td>
   <td><p>Abilita il trasferimento ottimizzato del server e del client dell'istanza del dizionario dati</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Correzione automatica delle incoerenze </p> </td>
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
   <td><p>Formato modifica dati</p> </td>
   <td><p>Modificare il formato dei dati. Viene utilizzato quando si scrivono dati come Stringa o si analizzano dati da Stringa</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>Gestisci istanze di lettere su Pubblica</p> </td>
   <td><p>Abilitare/disabilitare la funzionalità Gestisci lettere (applicabile solo per Publish Server)</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo</p> </td>
   <td><p>Abilitare/disabilitare la funzionalità di controllo. Se è false, i registri di controllo per tutte le azioni verranno disattivati</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo lettura</p> </td>
   <td><p>Abilitare/disabilitare la funzionalità di controllo per la lettura delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo</p> </td>
   <td><p>Abilita/Disattiva la funzionalità di controllo per la creazione di risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo aggiornamento</p> </td>
   <td><p>Abilitare/disabilitare la funzionalità di controllo per l'aggiornamento delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo ripristino</p> </td>
   <td><p>Abilitare/disabilitare la funzionalità di controllo per il ripristino delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo pubblicazione</p> </td>
   <td><p>Abilitare/disabilitare la funzionalità di controllo per la pubblicazione delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo SaveAsDraft</p> </td>
   <td><p>Abilitare/disabilitare la funzionalità di controllo per il salvataggio delle bozze di lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo invio</p> </td>
   <td><p>Attiva/Disattiva la funzionalità di controllo per l'invio di lettere</p> </td>
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
   <td><p>Abilitare/disabilitare la funzionalità di controllo per la consegna personalizzata di lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro documenti allegati</p> </td>
   <td><p>Nome parametro per i documenti allegati inviati al processo post</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Directory principale utente di CM</p> </td>
   <td><p>URL della cartella contenente tutte le risorse utente di Gestione corrispondenza</p> </td>
   <td><p>—</p> </td>
   <td><p>Percorso cartella valido</p> </td>
  </tr>
  <tr>
   <td><p>Dimensione cache lettera</p> </td>
   <td><p>Specificate il numero massimo di lettere da mantenere nella cache.</p> <p>Modificando questo valore si otterrà la pulizia della cache <code>in-memory</code>.</p> </td>
   <td><p>100</p> </td>
   <td><p>Qualsiasi valore numerico</p> </td>
  </tr>
  <tr>
   <td><p>Abilita cache lettere</p> </td>
   <td><p>Abilitare/disabilitare la cache delle lettere.</p> <p>Modificando questo valore si otterrà la pulizia della cache <code>in-memory </code>.</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Ordine degli elementi dati</p> </td>
   <td><p>Mantiene ordinati gli elementi dei dati nell'interfaccia per la creazione della corrispondenza in base alla sequenza in Lettera</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Ricarica assistenza</p> </td>
   <td><p>Abilitare/disabilitare il supporto per il ricaricamento in lettere sottoposte a rendering sul lato server.</p> <p>La disattivazione di questa opzione migliorerà le prestazioni di rendering delle lettere.</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Cartella Temp</td>
   <td>Posizione della cartella temp.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Salvataggio remoto</td>
   <td>Salva le istanze della lettera per l'autore di elaborazione specificato.</td>
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
   <td>Percorso cartella del file system per il debug. Se la directory non è <code>exists</code>, non verrà generato alcun dump di debug.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
