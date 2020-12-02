---
title: '"Esercitazione: Pianificare la comunicazione interattiva"'
seo-title: Pianificare la comunicazione interattiva
description: Pianificare l'anatomia della comunicazione interattiva
seo-description: Pianificare l'anatomia della comunicazione interattiva
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
translation-type: tm+mt
source-git-commit: 1449ce9aba3014b13421b32db70c15ef09967375
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 3%

---


# Esercitazione: Pianificare la comunicazione interattiva {#tutorial-plan-the-interactive-communication}

Pianificare l&#39;anatomia della comunicazione interattiva

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Questa esercitazione è un passaggio della serie [Crea la tua prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

Il primo passo nella pianificazione di una comunicazione interattiva consiste nel finalizzare il contenuto della comunicazione interattiva. Gli esperti in materia provenienti da dipartimenti come legali, finanziari, assistenza o marketing possono aiutarti a finalizzare i contenuti. Una volta completato il contenuto, è necessario analizzarlo per identificare i vari tipi di risorse necessari per creare la comunicazione interattiva.

## Considerazioni sulla pianificazione {#planning-considerations}

Una comunicazione interattiva include i seguenti elementi:

* **I** testi statici comprendono principalmente le parti della comunicazione interattiva che sono di natura generica e sono incluse nella comunicazione a tutti i clienti. Ad esempio, intestazione, piè di pagina, formula introduttiva o clausole di non responsabilità.
* **I dati provenienti da un sistema di backend (modello dati modulo)** sono specifici per il cliente e vengono uniti dinamicamente con la comunicazione interattiva. Ad esempio, il numero o l&#39;indirizzo del criterio può essere originato utilizzando il modello dati del modulo.
* **Layout o** modelli per la versione Stampa e Web della comunicazione interattiva.
* **Ordine in** cui i vari paragrafi di testo compaiono nella comunicazione interattiva.
* **Dati immessi da un dipendente in prima linea (interfaccia utente agente)** che sta personalizzando la comunicazione prima di inviarla. Ad esempio, la data di scadenza del pagamento.

* **I** dati condizionali vengono compilati in base a condizioni predefinite. Ad esempio, la data in cui viene generata la comunicazione interattiva.
* **Immagini memorizzate in un archivio**, ad esempio logo e immagini della firma. Immagini come il logo aziendale apparirebbero nella maggior parte o nella totalità della comunicazione interattiva.
* **Grafici e** tabelle necessarie per semplificare la rappresentazione di dati complessi in una comunicazione interattiva

## Anatomia della comunicazione interattiva {#anatomy-of-the-interactive-communication}

Una volta completati i contenuti e gli elementi utilizzati per creare la comunicazione interattiva, potete creare un&#39;anatomia della comunicazione interattiva. L&#39;anatomia deve avere i dettagli elencati nella sezione [Considerazioni sulla pianificazione](/help/forms/using/planning-interactive-communications.md#planning-considerations). In base al nostro caso d&#39;uso, quanto segue è un esempio di anatomia della fattura mensile che un operatore di telecomunicazioni invia ai suoi clienti.

L&#39;anatomia include i dati con le seguenti modalità di input:

* Testo statico
* Modello dati modulo
* Interfaccia utente agente
* Dati condizionali
* Immagini

In ogni sezione, il testo in grassetto rappresenta testo statico. Il database include tabelle cliente, fatture e chiamate. Un modello dati modulo può ricevere dati da una qualsiasi di queste tabelle. Per ulteriori informazioni, vedere [Creare un modello dati del modulo](/help/forms/using/create-form-data-model0.md).

Nella tabella seguente è illustrata l’origine dati di ciascun campo nell’anatomia della comunicazione interattiva:

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
   <td><p>Numero fattura</p> <p>Data fatturazione</p> <p>Periodo fatturazione</p> <p>Il tuo piano</p> </td>
   <td><p>Valore per il campo <strong>Piano </strong></p> <p>Tabella - cliente</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>Numero fattura</li>
     <li>Data fatturazione</li>
     <li>Periodo fatturazione</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Dettagli cliente</td>
   <td><p>Luogo di fornitura</p> <p>Codice di stato</p> <p>Numero cellulare</p> <p>Numero di contatto alternativo</p> <p>Numero relazione</p> <p>Numero di connessioni</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>Nome</li>
     <li>Indirizzo</li>
     <li>Numero cellulare</li>
     <li>Numero di contatto alternativo</li>
     <li>Numero relazione</li>
    </ul> <p>Tabella - cliente</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>Luogo di fornitura</li>
     <li>Codice di stato</li>
     <li>Numero di connessioni</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Riepilogo fatturazione</td>
   <td><p>Saldo precedente</p> <p>Pagamenti</p> <p>Regolazioni</p> <p>Addebito periodo corrente</p> <p>Importo dovuto</p> <p>Data di scadenza</p> </td>
   <td><p>Valore per il campo <strong>Addebito periodo corrente fatturazione </strong></p> <p>Tabella - fatture</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>Saldo precedente</li>
     <li>Pagamenti</li>
     <li>Regolazioni</li>
     <li>Importo dovuto</li>
     <li>Data di scadenza</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Riepilogo delle spese</td>
   <td><p>Spese di chiamata</p> <p>Spese di chiamata conferenza</p> <p>Tariffe SMS </p> <p>Tariffe Internet per dispositivi mobili</p> <p>Tariffe di roaming nazionali</p> <p>Tariffe internazionali di roaming</p> <p>Spese per servizi a valore aggiunto</p> <p>Oneri totali</p> <p>TOTALE PAGABILE</p> <p>Condizione nel campo Spese servizi aggiunti</p> </td>
   <td><p>Valori per i campi seguenti:</p>
    <ul>
     <li>Spese di chiamata</li>
     <li>Spese di chiamata conferenza</li>
     <li>Tariffe SMS </li>
     <li>Tariffe Internet per dispositivi mobili</li>
     <li>Tariffe di roaming nazionali</li>
     <li>Tariffe internazionali di roaming</li>
     <li>Spese per servizi a valore aggiunto</li>
     <li>Addebiti totali (campo calcolato spese di utilizzo)</li>
     <li>TOTALE PAYABLE (campo calcolato spese d'uso)</li>
    </ul> <p>Tabella - fatture</p> </td>
   <td>Nessun campo</td>
   <td>—</td>
  </tr>
  <tr>
   <td>Chiamate dettagliate - In uscita</td>
   <td><p>Nomi colonna:</p>
    <ul>
     <li>Data</li>
     <li>Tempo</li>
     <li>Numero</li>
     <li>Durata</li>
     <li>Oneri</li>
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

