---
title: Ottimizzazione delle prestazioni di Health Monitor
seo-title: Fine-tuning Health Monitor performance
description: Scopri come ottimizzare le prestazioni di Health Monitor
seo-description: Learn how to fine-tune Health Monitor performance
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# Ottimizzazione delle prestazioni di Health Monitor{#fine-tuning-health-monitor-performance}

La raccolta delle statistiche di sistema che popolano Health Monitor ha un certo impatto sulle prestazioni dell&#39;ambiente dei moduli AEM. Questo impatto può essere controllato impostando le opzioni Java elencate di seguito nel server delle applicazioni.

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
   <td><p>Attiva o disattiva il thread di Monitoraggio integrità</p></td>
   <td><p>vero</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Attiva o disattiva la memorizzazione in cache Gemfire</p></td>
   <td><p>vero</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>Intervallo in millisecondi dopo il quale il thread di Monitoraggio integrità raccoglie le statistiche</p></td>
   <td><p>10 minuti (600.000 millisecondi)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>La porta multicast utilizzata per comunicare con altri membri del sistema distribuito. Se è impostato su zero, il multicast viene disabilitato sia per l'individuazione dei membri che per la distribuzione. </p><p>Nota: Selezionare indirizzi e porte multicast diversi per diversi sistemi distribuiti. Non utilizzare solo indirizzi diversi.</p></td>
   <td><p>Nessun valore predefinito. I valori validi sono compresi tra 0 e 65535.</p></td>
  </tr>
  <tr>
   <td><p>tasso di campionamento statistico</p></td>
   <td><p>Frequenza in millisecondi in cui vengono campionate le statistiche. Le statistiche del sistema operativo vengono aggiornate solo al momento del prelievo di un campione.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Questa proprietà abilita o disabilita la raccolta statistica di Work Manager, ad esempio il conteggio di un processo o di un elemento di lavoro.</p></td>
   <td><p>vero</p></td>
  </tr>
 </tbody>
</table>

## Aggiungi opzioni Java a JBoss {#add-java-options-to-jboss}

1. Arresta il server dell&#39;applicazione JBoss.
1. Apri *[root appserver]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) in un editor e aggiungi una delle opzioni Java necessarie.
1. Riavvia il server.

## Aggiungi opzioni Java a WebLogic {#add-java-options-to-weblogic}

1. Avvia la console di amministrazione WebLogic digitando https://[nome host]:&quot;port&quot;/console nella riga URL di un browser web.
1. Digita il nome utente e la password creati per il dominio del server WebLogic e fai clic su Log Under Change Center, quindi fai clic su Lock &amp; Edit.
1. In Struttura del dominio, fai clic su Ambiente > Server e, nel riquadro a destra, fai clic sul nome del server gestito.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > Avvio server .
1. Nella casella Argomenti , aggiungi gli argomenti necessari alla fine del contenuto corrente. Ad esempio, aggiungendo - `Dadobe.healthmonitor.enabled=false` disabilita Monitoraggio integrità.
1. Fare clic su Salva e quindi su Attiva modifiche.
1. Riavvia il server gestito WebLogic.

## Aggiungi opzioni Java a WebSphere {#add-java-options-to-websphere}

1. Nella struttura di navigazione della Console amministrativa WebSphere eseguire le operazioni seguenti per il server applicazioni:

   (WebSphere 6.x) Fai clic su Server > Server applicazioni

   (WebSphere 7.x) Fai clic su Server > Tipi di server > Server applicazioni WebSphere

1. Nel riquadro a destra, fare clic sul nome del server.
1. In Infrastruttura server, fai clic su Flusso di lavoro Java e moduli > Definizione del processo.
1. In Proprietà aggiuntive fare clic su Java Virtual Machine.
1. Nella casella Argomenti JVM generici digitare gli argomenti necessari.
1. Fare clic su OK o Applica, quindi fare clic su Salva direttamente nella configurazione principale.
