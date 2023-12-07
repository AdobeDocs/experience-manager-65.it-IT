---
title: "Tutorial: pianificare la comunicazione interattiva"
description: Pianificare l'anatomia per la comunicazione interattiva
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
exl-id: ea0c8971-56f4-4094-87e4-1b222b73951f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 2%

---

# Tutorial: pianificare la comunicazione interattiva {#tutorial-plan-the-interactive-communication}

Pianificare l&#39;anatomia per la comunicazione interattiva

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Questo tutorial è un passaggio del [Creare la prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md) serie. Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

Il primo passo nella pianificazione di una comunicazione interattiva è finalizzare il contenuto della comunicazione interattiva. Esperti in materia provenienti da dipartimenti legali, finanziari, di supporto o di marketing possono aiutarti a finalizzare i contenuti. Dopo aver finalizzato il contenuto, devi analizzarlo per identificare i vari tipi di risorse necessari per creare la comunicazione interattiva.

## Considerazioni sulla pianificazione {#planning-considerations}

Una comunicazione interattiva include i seguenti elementi:

* **Testo statico** include principalmente le parti della comunicazione interattiva che sono di natura generica e sono incluse nella comunicazione a tutti i clienti. Ad esempio, intestazione, piè di pagina, formula introduttiva o disclaimer.
* **Dati originati da un sistema back-end (modello dati modulo)** è specifico per il cliente ed è unito in modo dinamico alla comunicazione interattiva. Ad esempio, il numero o l’indirizzo del criterio può essere originato utilizzando il modello dati del modulo.
* **Layout o modelli** per la versione a stampa e web della comunicazione interattiva.
* **Ordine** in cui i vari paragrafi di testo compaiono nella comunicazione interattiva.
* **Dati immessi da un dipendente in prima linea (interfaccia utente agente)** che personalizza la comunicazione prima di inviarla. Ad esempio, la data di scadenza del pagamento.

* **Dati condizionali** che viene popolato in base a condizioni predefinite. Ad esempio, la data in cui viene generata la comunicazione interattiva.
* **Immagini memorizzate in un archivio**, ad esempio loghi e immagini della firma. Immagini come i logo aziendali appaiono nella maggior parte o in tutta la comunicazione interattiva.
* **Grafici e tabelle** necessario per semplificare la rappresentazione di dati complessi in una comunicazione interattiva

## Anatomia della comunicazione interattiva {#anatomy-of-the-interactive-communication}

Dopo aver finalizzato i contenuti e gli elementi utilizzati per creare la comunicazione interattiva, puoi creare un’anatomia della comunicazione interattiva. L&#39;anatomia deve avere i dettagli elencati nella [Considerazioni sulla pianificazione](/help/forms/using/planning-interactive-communications.md#planning-considerations) sezione. In base al nostro caso d’uso, il seguente è un esempio di anatomia della fattura mensile che un operatore di telecomunicazioni invia ai suoi clienti.

L&#39;anatomia include dati con le seguenti modalità di input:

* Testo statico
* Modello dati modulo
* Interfaccia utente agente
* Dati condizionali
* Immagini

In ogni sezione, il testo in grassetto rappresenta un testo statico. Il database include tabelle relative a clienti, fatture e chiamate. Un modello di dati modulo può ricevere dati da una qualsiasi di queste tabelle. Per ulteriori informazioni, consulta [Crea modello dati modulo](/help/forms/using/create-form-data-model0.md).

La tabella seguente illustra l’origine dei dati per ciascun campo nell’anatomia della comunicazione interattiva:

<table>
 <tbody>
  <tr>
   <td>Sezione</td>
   <td>Testo statico</td>
   <td>FDM (Form Data Model - modello dati modulo) </td>
   <td>Interfaccia utente agente</td>
   <td>Immagini</td>
  </tr>
  <tr>
   <td>Dettagli fattura</td>
   <td><p>N. fattura</p> <p>Data di fatturazione</p> <p>Periodo di fatturazione</p> <p>Il piano</p> </td>
   <td><p>Valore per <strong>Il piano </strong>campo</p> <p>Tabella - Cliente</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>N. fattura</li>
     <li>Data di fatturazione</li>
     <li>Periodo di fatturazione</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Dettagli cliente</td>
   <td><p>Luogo della prestazione</p> <p>Codice stato</p> <p>Numero cellulare</p> <p>Numero di contatto alternativo</p> <p>Numero di relazione</p> <p>Numero di connessioni</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>Nome</li>
     <li>Indirizzo</li>
     <li>Numero cellulare</li>
     <li>Numero di contatto alternativo</li>
     <li>Numero di relazione</li>
    </ul> <p>Tabella - Cliente</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>Luogo della prestazione</li>
     <li>Codice stato</li>
     <li>Numero di connessioni</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Riepilogo fatture</td>
   <td><p>Saldo precedente</p> <p>Pagamenti</p> <p>Adeguamenti</p> <p>Addebiti periodo di fatturazione corrente</p> <p>Importo dovuto</p> <p>Data di scadenza</p> </td>
   <td><p>Valore per <strong>Addebiti periodo di fatturazione corrente </strong> campo</p> <p>Tabella - fatture</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>Saldo precedente</li>
     <li>Pagamenti</li>
     <li>Adeguamenti</li>
     <li>Importo dovuto</li>
     <li>Data di scadenza</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Riepilogo delle spese</td>
   <td><p>Spese di chiamata</p> <p>Spese di conferenza telefonica</p> <p>Spese SMS </p> <p>Tariffe Internet mobile</p> <p>Tariffe nazionali di roaming</p> <p>Tariffe di roaming internazionale</p> <p>Spese per servizi a valore aggiunto</p> <p>Oneri totali</p> <p>TOTALE DA PAGARE</p> <p>Condizione per il campo Spese servizi a valore aggiunto</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>Spese di chiamata</li>
     <li>Spese di conferenza telefonica</li>
     <li>Spese SMS </li>
     <li>Tariffe Internet mobile</li>
     <li>Tariffe nazionali di roaming</li>
     <li>Tariffe di roaming internazionale</li>
     <li>Spese per servizi a valore aggiunto</li>
     <li>Totale addebiti (campo calcolato addebiti utilizzo)</li>
     <li>TOTALE DA PAGARE (campo calcolato spese d’uso)</li>
    </ul> <p>Tabella - fatture</p> </td>
   <td>Nessun campo</td>
   <td>—</td>
  </tr>
  <tr>
   <td>Chiamate dettagliate - In uscita</td>
   <td><p>Nomi colonne:</p>
    <ul>
     <li>Data</li>
     <li>stimato</li>
     <li>Numero</li>
     <li>Durata</li>
     <li>Spese</li>
    </ul> </td>
   <td><p>Tutti i valori</p> <p>Tabella - chiamate</p> </td>
   <td>Nessun campo</td>
   <td>—</td>
  </tr>
  <tr>
   <td>Paga ora</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>Servizi a valore aggiunto</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>
