---
title: Ottimizzazione delle prestazioni di Health Monitor
description: Scopri come ottimizzare le prestazioni di Health Monitor. Controlla le statistiche del sistema che influiscono sulle prestazioni dell’ambiente Forms utilizzando l’opzione di impostazione JAVA.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---

# Ottimizzazione delle prestazioni di Health Monitor{#fine-tuning-health-monitor-performance}

La raccolta delle statistiche di sistema che popolano Health Monitor ha un certo impatto sulle prestazioni dell&#39;ambiente dei moduli AEM. Questo impatto può essere controllato impostando le opzioni Java elencate di seguito nel server applicazioni.

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
   <td><p>Attiva o disattiva il thread di Health Monitor</p></td>
   <td><p>vero</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Attiva o disattiva la memorizzazione nella cache di Gemfire</p></td>
   <td><p>vero</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>Intervallo in millisecondi dopo il quale il thread di Monitoraggio integrità raccoglie le statistiche</p></td>
   <td><p>10 minuti (600.000 millisecondi)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>Porta multicast utilizzata per comunicare con altri membri del sistema distribuito. Se è impostato su zero, il multicast viene disabilitato sia per l'individuazione dei membri che per la distribuzione. </p><p>Nota: selezionare indirizzi e porte multicast diversi per i diversi sistemi distribuiti. Non utilizzare solo indirizzi diversi.</p></td>
   <td><p>Nessun valore predefinito. I valori validi sono compresi tra 0 e 65535.</p></td>
  </tr>
  <tr>
   <td><p>tasso di campionamento statistico</p></td>
   <td><p>Velocità in millisecondi di campionamento delle statistiche. Le statistiche del sistema operativo vengono aggiornate solo quando si acquisisce un campione.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Questa proprietà abilita o disabilita la raccolta di statistiche di Work Manager, ad esempio il numero di job o di elementi di lavoro.</p></td>
   <td><p>vero</p></td>
  </tr>
 </tbody>
</table>

## Aggiungere opzioni Java a JBoss {#add-java-options-to-jboss}

1. Arresta il server applicazioni JBoss.
1. Apri *[directory principale del server applicazioni]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) in un editor e aggiungi le opzioni Java necessarie.
1. Riavviare il server.

## Aggiungere opzioni Java a WebLogic {#add-java-options-to-weblogic}

1. Avviare la console di amministrazione WebLogic digitando https://[nome host]:&quot;porta&quot;/console nella riga URL di un browser web.
1. Digitare il nome utente e la password creati per il dominio del server WebLogic e fare clic su Registra In Centro modifiche fare clic su Blocca e modifica.
1. In Struttura dominio fare clic su Ambiente > Server e nel riquadro di destra fare clic sul nome del server gestito.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > scheda Avvio server.
1. Nella casella Argomenti aggiungere gli argomenti necessari alla fine del contenuto corrente. Ad esempio, aggiungendo - `Dadobe.healthmonitor.enabled=false` disabilita Health Monitor.
1. Fai clic su Salva, quindi su Attiva modifiche.
1. Riavviare il server gestito WebLogic.

## Aggiungere opzioni Java a WebSphere {#add-java-options-to-websphere}

1. Nella struttura di navigazione della Console di amministrazione WebSphere, effettuare le seguenti operazioni per il server applicazioni:

   (WebSphere 6.x) Click Server > Application Server

   (WebSphere 7.x) Fare clic su Server > Tipi di server > Application Server WebSphere

1. Nel riquadro di destra fare clic sul nome del server.
1. In Infrastruttura server fare clic su Java e su Flusso di lavoro moduli > Definizione processo.
1. In Proprietà aggiuntive fare clic su Java Virtual Machine.
1. Nella casella Argomenti JVM generici digitare gli argomenti richiesti.
1. Fare clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.
