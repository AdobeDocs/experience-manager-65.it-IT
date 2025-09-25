---
title: Ottimizzazione delle prestazioni del monitoraggio dello stato
description: Scopri come ottimizzare le prestazioni del monitoraggio dello stato Controlla le statistiche di sistema che influiscono sulle prestazioni dell’ambiente Forms utilizzando l’opzione di impostazione JAVA.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '426'
ht-degree: 100%

---

# Ottimizzazione delle prestazioni del monitoraggio dello stato{#fine-tuning-health-monitor-performance}

La raccolta delle statistiche di sistema che popolano il monitoraggio dello stato ha un certo impatto sulle prestazioni dell’ambiente AEM Forms. Questo impatto può essere controllato impostando le opzioni Java elencate di seguito nel server applicazioni.

<table>
 <thead>
  <tr>
   <th><p>Proprietà</p></th>
   <th><p>Scopo</p></th>
   <th><p>Valore predefinito</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>Attiva o disattiva il thread del monitoraggio dello stato</p></td>
   <td><p>vero</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Attiva o disattiva la memorizzazione nella cache di Gemfire</p></td>
   <td><p>vero</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>Intervallo in millisecondi dopo il quale il thread del monitoraggio dello stato raccoglie le statistiche</p></td>
   <td><p>10 minuti (600.000 millisecondi)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>Porta multicast utilizzata per comunicare con altri membri del sistema distribuito. Se è impostato su zero, il multicast viene disabilitato sia per l'individuazione dei membri che per la distribuzione. </p><p>Nota: seleziona indirizzi e porte multicast diversi per i diversi sistemi distribuiti. Non utilizzare solo indirizzi diversi.</p></td>
   <td><p>Nessun valore predefinito. I valori validi sono compresi tra 0 e 65535.</p></td>
  </tr>
  <tr>
   <td><p>statistic-sample-rate</p></td>
   <td><p>La velocità in millisecondi di campionamento delle statistiche. Le statistiche del sistema operativo vengono aggiornate solo quando si acquisisce un campione.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Questa proprietà abilita o disabilita la raccolta di statistiche di Work Manager, ad esempio il numero di processi o di elementi di lavoro.</p></td>
   <td><p>vero</p></td>
  </tr>
 </tbody>
</table>

## Aggiungere opzioni Java a JBoss {#add-java-options-to-jboss}

1. Arresta il server applicazioni di JBoss.
1. Apri la directory principale *[appserver]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) in un editor e aggiungi le opzioni Java necessarie.
1. Riavvia il server.

## Aggiungere opzioni Java a WebLogic {#add-java-options-to-weblogic}

1. Avvia la console di amministrazione WebLogic digitando https://[nome host]:&#39;porta&#39;/console nella riga URL di un browser web.
1. Digita il nome utente e la password creati per il dominio del server WebLogic e fai clic su Registra In Centro modifiche e su Blocca e modifica.
1. In Struttura dominio, fai clic su Ambiente > Server e nel riquadro di destra fai clic sul nome del server gestito.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > scheda Avvio server.
1. Nella casella Argomenti, aggiungi gli argomenti necessari alla fine del contenuto corrente. Ad esempio, l’aggiunta di - `Dadobe.healthmonitor.enabled=false` disabilita il monitoraggio dello stato.
1. Fai clic su Salva, quindi su Attiva modifiche.
1. Riavvia il server gestito da WebLogic.

## Aggiungere opzioni Java a WebSphere {#add-java-options-to-websphere}

1. Nella struttura di navigazione della console di amministrazione di WebSphere, effettua le seguenti operazioni per il server applicazioni:

   (WebSphere 6.x) Fai clic su Server > Server applicazioni

   (WebSphere 7.x) Fai clic su Server > Tipi di server > Server applicazioni WebSphere

1. Nel riquadro di destra, fai clic sul nome del server.
1. In Infrastruttura server fare fai clic su Java e Forms Workflow > Definizione processo.
1. In Proprietà aggiuntive, fai clic su Java Virtual Machine.
1. Nella casella Argomenti JVM generici digita gli argomenti richiesti.
1. Fai clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.
