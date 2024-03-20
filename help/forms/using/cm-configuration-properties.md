---
title: Proprietà di configurazione di Gestione corrispondenza
description: Questo argomento spiega come modificare Asset Composer con configurazioni specifiche per le soluzioni. Questo argomento descrive le proprietà che è possibile modificare, con la relativa descrizione, i valori predefiniti e i valori accettabili.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 3%

---

# Proprietà di configurazione di Gestione corrispondenza {#correspondence-management-configuration-properties}

Per configurare queste proprietà, apri il seguente URL in un browser: `https://<server>:<port>/<contextPath>/system/console/configMgr` e seleziona **Configurazioni gestione corrispondenza**.

Gestione corrispondenza dispone delle seguenti proprietà di configurazione:

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
   <td>Rientro nei moduli<p> </p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Qualsiasi numero</p> </td>
  </tr>
  <tr>
   <td>Larghezza minima numero</td>
   <td>Larghezza minima da applicare al campo punto elenco/numero quando si utilizzano elenchi numerati diversi dai numeri romani</td>
   <td>8 mm</td>
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
   <td>Tipo di rappresentazione utilizzato dall'applicazione Create Correspondence per eseguire il rendering dell'anteprima della lettera. </td>
   <td>Rappresentazione HTML</td>
   <td>Rendering HTML/PDF</td>
  </tr>
  <tr>
   <td><p>Abilita evidenziazione CCR PDF</p> </td>
   <td><p>Abilita l’evidenziazione su PDF nell’applicazione Create Correspondence</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Tipo evidenziazione destinazione</p> </td>
   <td><p>Tipo di evidenziazione target nell’applicazione Create Correspondence</p> </td>
   <td><p>bordo</p> </td>
   <td><p>bordo/riempimento/nessuno</p> </td>
  </tr>
  <tr>
   <td><p>Colore evidenziazione destinazione</p> </td>
   <td><p>Colore evidenziazione destinazione nell’applicazione Crea corrispondenza</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>Qualsiasi colore RGB in formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo evidenziazione contenuto</p> </td>
   <td><p>Tipo di evidenziazione contenuto nell’applicazione Create Correspondence</p> </td>
   <td><p>Riempimento</p> </td>
   <td><p>bordo/riempimento/nessuno</p> </td>
  </tr>
  <tr>
   <td><p>Colore evidenziazione contenuto</p> </td>
   <td><p>Colore evidenziazione contenuti nell’applicazione Create Correspondence</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualsiasi colore RGB in formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo evidenziazione campo</p> </td>
   <td><p>Tipo di evidenziazione campo nell’applicazione Crea corrispondenza</p> </td>
   <td><p>riempimento</p> </td>
   <td><p>bordo/riempimento/nessuno</p> </td>
  </tr>
  <tr>
   <td><p>Colore evidenziazione campo</p> </td>
   <td><p>Colore evidenziazione campo nell'applicazione Crea corrispondenza</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualsiasi colore RGB in formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Timeout applicazione</p> </td>
   <td><p>Timeout applicazione in secondi</p> </td>
   <td><p>1200</p> </td>
   <td><p>Qualsiasi numero</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro documento PDF</p> </td>
   <td><p>Nome del parametro per il documento PDF nella fase di post-elaborazione</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro dati XML</p> </td>
   <td><p>Nome del parametro per il documento XML (dati) nella fase di post-elaborazione</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro documento XDP</p> </td>
   <td><p>Nome del parametro per il documento XDP inviato al post-processo</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro URL di reindirizzamento</p> </td>
   <td><p>Nome del parametro per l’URL di reindirizzamento inviato dal processo post Questo valore può essere qualsiasi nome di variabile stringa</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Tipo di invio PDF</p> </td>
   <td><p>Tipo di invio PDF (tipo di PDF generato al momento dell'invio dall'applicazione Create Correspondence)</p> </td>
   <td><p>non interattivo</p> </td>
   <td><p>interattivo/non interattivo</p> </td>
  </tr>
  <tr>
   <td><p>Ottimizza istanza dizionario dati</p> </td>
   <td><p>Consente il trasferimento ottimizzato dell’istanza del dizionario dati tra server e client</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Correzione automatica delle incoerenze </p> </td>
   <td><p>Quando questa opzione è attivata, gestisce automaticamente le possibili incoerenze nelle assegnazioni di lettere</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Usa formati dati configurati</p> </td>
   <td><p>Controlla se utilizzare i formati di modifica dati configurati e il formato di visualizzazione dati</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Formati di visualizzazione dei dati</p> </td>
   <td><p>Specifica il formato di visualizzazione specifico per la lingua per i dati</p> </td>
   <td><p>locale=en_US; dateFormat=gg-MM-aaaa; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=gg-MM-aaaa; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=gg-MM-aaaa; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>Formato di modifica dati</p> </td>
   <td><p>Modifica il formato dei dati. Utilizzato per scrivere dati come stringa o analizzare dati da stringa</p> </td>
   <td><p>locale=en_US; dateFormat=gg-MM-aaaa; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>Gestisci istanze lettere al momento della pubblicazione</p> </td>
   <td><p>Attiva/disattiva la funzionalità Gestisci lettera (applicabile solo al server di pubblicazione)</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo</p> </td>
   <td><p>Attiva/disattiva la funzionalità di controllo. Se è false, i registri di audit per tutte le azioni vengono disabilitati</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo lettura</p> </td>
   <td><p>Attiva/disattiva la funzionalità di controllo per la lettura delle risorse</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita Crea controllo</p> </td>
   <td><p>Attivare/disattivare la funzionalità di controllo per la creazione di risorse</p> </td>
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
   <td><p>Abilita Ripristina controllo</p> </td>
   <td><p>Attivare/disattivare la funzionalità di controllo per il ripristino delle risorse</p> </td>
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
   <td><p>Abilita controllo Salva come bozza</p> </td>
   <td><p>Attiva/disattiva la funzionalità di controllo per il salvataggio delle bozze di lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo invio</p> </td>
   <td><p>Attiva/disattiva la funzionalità di controllo per l'invio di lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo e-mail</p> </td>
   <td><p>Attiva/disattiva la funzionalità di controllo per l'invio di lettere tramite posta elettronica</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo di stampa</p> </td>
   <td><p>Attiva/disattiva la funzionalità di controllo per la stampa delle lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Abilita controllo consegna personalizzato</p> </td>
   <td><p>Attiva/disattiva la funzionalità di controllo per la consegna personalizzata delle lettere</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Nome parametro documenti allegati</p> </td>
   <td><p>Nome del parametro per i documenti allegati inviati al processo successivo</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>Qualsiasi nome di variabile stringa</p> </td>
  </tr>
  <tr>
   <td><p>Directory principale utente CM</p> </td>
   <td><p>URL della cartella contenente tutte le risorse utente di Gestione della corrispondenza</p> </td>
   <td><p>—</p> </td>
   <td><p>Percorso cartella valido</p> </td>
  </tr>
  <tr>
   <td><p>Letter Cache Size</p> </td>
   <td><p>Specifica il numero massimo di lettere da mantenere nella cache.</p> <p>La modifica di questo valore determinerà la pulizia di <code>in-memory</code> cache.</p> </td>
   <td><p>100</p> </td>
   <td><p>Qualsiasi valore numerico</p> </td>
  </tr>
  <tr>
   <td><p>Abilita cache lettere</p> </td>
   <td><p>Attiva/disattiva la cache delle lettere.</p> <p>La modifica di questo valore determinerà la pulizia di <code>in-memory </code> cache.</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Ordinamento elementi dati</p> </td>
   <td><p>Mantiene l’ordine degli elementi dati nell’interfaccia per la creazione di corrispondenza in base alla sequenza in Lettera</p> </td>
   <td><p>vero</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Ricaricamento supporto</p> </td>
   <td><p>Abilita/disabilita il supporto per il ricaricamento nelle lettere sottoposte a rendering sul lato server.</p> <p>La disattivazione di questa opzione migliorerà le prestazioni di rendering delle lettere.</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Cartella Temp</td>
   <td>Posizione della cartella temporanea.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Salvataggio remoto</td>
   <td>Salva le istanze di lettere sull'autore di elaborazione specificato.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Opzioni di compatibilità</td>
   <td>Opzioni di compatibilità del formato nomeconfigurazione:valore separato da virgole.</td>
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
