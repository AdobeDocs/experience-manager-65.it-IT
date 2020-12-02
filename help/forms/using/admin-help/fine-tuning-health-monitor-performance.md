---
title: Ottimizzazione delle prestazioni del monitor di stato
seo-title: Ottimizzazione delle prestazioni del monitor di stato
description: Scoprite come ottimizzare le prestazioni di Health Monitor
seo-description: Scoprite come ottimizzare le prestazioni di Health Monitor
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---


# Ottimizzazione delle prestazioni del monitor integrità{#fine-tuning-health-monitor-performance}

La raccolta delle statistiche di sistema che popolano il Monitor integrità ha un impatto sulle prestazioni dell&#39;ambiente dei moduli AEM. Questo impatto può essere controllato impostando le opzioni Java elencate di seguito nel server delle applicazioni.

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
   <td><p>Attivare o disattivare il filetto del monitor integrità</p></td>
   <td><p>vero</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Attivare o disattivare la cache GemFire</p></td>
   <td><p>vero</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>L'intervallo in millisecondi dopo il quale il thread di Monitoraggio integrità raccoglie le statistiche</p></td>
   <td><p>10 minuti (600.000 millisecondi)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>La porta multicast utilizzata per comunicare con altri membri del sistema distribuito. Se è impostata su zero, il multicast è disabilitato sia per l'individuazione dei membri che per la distribuzione. </p><p>Nota: Selezionare indirizzi e porte multicast diversi per i diversi sistemi distribuiti. Non utilizzate solo indirizzi diversi.</p></td>
   <td><p>Nessun valore predefinito. I valori validi sono compresi tra 0 e 65535.</p></td>
  </tr>
  <tr>
   <td><p>tasso di campionamento statistico</p></td>
   <td><p>Frequenza in millisecondi alla quale vengono campionate le statistiche. Le statistiche del sistema operativo vengono aggiornate solo quando si preleva un campione.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Questa proprietà abilita o disabilita la raccolta statistica di Work Manager, ad esempio il conteggio di OdL o di elementi di lavoro.</p></td>
   <td><p>vero</p></td>
  </tr>
 </tbody>
</table>

## Aggiungere opzioni Java a JBoss {#add-java-options-to-jboss}

1. Arrestate il server applicazioni JBoss.
1. Aprite la *[directory principale dell&#39;appserver]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) in un editor e aggiungete le opzioni Java richieste.
1. Riavviate il server.

## Aggiungere opzioni Java a WebLogic {#add-java-options-to-weblogic}

1. Avviate la console di amministrazione WebLogic digitando https://[nome host]:&#39;porta&#39;/console nella riga URL di un browser Web.
1. Digitare il nome utente e la password creati per il dominio WebLogic Server e fare clic su Log In Change Center, quindi fare clic su Lock &amp; Edit (Blocca e modifica).
1. In Struttura dominio, fare clic su Ambiente > Server e, nel riquadro a destra, fare clic sul nome del server gestito.
1. Nella schermata successiva, fate clic sulla scheda Configurazione > scheda Avvio server.
1. Nella casella Argomenti, aggiungere gli argomenti richiesti alla fine del contenuto corrente. Ad esempio, se si aggiunge - `Dadobe.healthmonitor.enabled=false` viene disattivato il monitoraggio integrità.
1. Fate clic su Salva, quindi su Attiva modifiche.
1. Riavviare il server gestito WebLogic.

## Aggiungere opzioni Java a WebSphere {#add-java-options-to-websphere}

1. Nella struttura di navigazione della console di amministrazione di WebSphere effettuare le seguenti operazioni per il server applicazione:

   (WebSphere 6.x) Fare clic su Server > Server applicazioni

   (WebSphere 7.x) Fare clic su Server > Tipi di server > Server applicazioni WebSphere

1. Nel riquadro a destra, fare clic sul nome del server.
1. In Infrastruttura server, fare clic su Flusso di lavoro Java e moduli > Definizione processo.
1. In Proprietà aggiuntive fare clic su Java Virtual Machine.
1. Nella casella Argomenti JVM generici, digitare gli argomenti richiesti.
1. Fate clic su OK o Applica, quindi fate clic su Salva direttamente nella configurazione principale.

