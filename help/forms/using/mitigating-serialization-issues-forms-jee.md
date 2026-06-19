---
title: Mitigazione dei problemi di serializzazione in AEM Forms JEE | ADOBE EXPERIENCE MANAGER
description: Scopri come attenuare i problemi di deserializzazione Java in AEM Forms JEE in esecuzione su JDK 8.
solution: Experience Manager, Experience Manager Forms
feature: Security
version: Experience Manager 6.5
type: Documentation
role: Admin
source-git-commit: ec3941675081255879065c3be9d5af77474b2072
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---


# Mitigazione dei problemi di serializzazione in AEM Forms JEE {#mitigating-serialization-issues-in-aem-forms-jee}

AEM Forms JEE include un firewall di deserializzazione che aggiunge un controllo preliminare prima di qualsiasi tentativo di deserializzare un oggetto. Questo controllo verifica il nome di una classe rispetto a un elenco Consentiti di classe di tipo firewall, a un elenco Bloccati di o a entrambi e rifiuta le classi che sono note per essere sfruttabili tramite attacchi di deserializzazione Java™. L&#39;agente sottostante è la distribuzione modificata di Adobe del progetto open-source [NotSoSerial](https://github.com/kantega/notsoserial), con licenza [Apache 2 license](https://www.apache.org/licenses/LICENSE-2.0).

Nelle installazioni che eseguono **JDK 11 o versione successiva**, questa protezione viene attivata dal filtro di serializzazione nativo della piattaforma e non richiede passaggi manuali. Nelle installazioni che eseguono **JDK 8**, il filtro di serializzazione nativo non è efficace, pertanto l&#39;agente deve essere associato in modo esplicito alla JVM all&#39;avvio. Questo articolo descrive come farlo.

>[!NOTE]
>
>Se il controllo di integrità del filtro di deserializzazione risulta già attivo sul server (vedere [Verifica dell&#39;attivazione dell&#39;agente](#verifying-the-agents-activation)), il server applicazioni è già protetto ed è possibile saltare i passaggi rimanenti in questo documento.

## Prima di iniziare {#before-you-begin}

Conferma la versione Java™ eseguita dal server applicazioni con:

```shell
java -version
```

Se la versione segnalata è `1.8.x` (JDK 8), si applicano i passaggi descritti in questo articolo. Se è 11 o successiva, non è richiesta alcuna azione manuale; verificare la protezione utilizzando il controllo di integrità descritto in [Verifica dell&#39;attivazione dell&#39;agente](#verifying-the-agents-activation).

Nei passaggi seguenti, `<jee-installation-directory>` fa riferimento alla directory principale dell&#39;installazione di AEM Forms JEE.

## Applicazione dell’agente {#applying-the-agent}

>[!IMPORTANT]
>
>Questi passaggi richiedono il riavvio del server applicazioni. Applicale a ogni istanza interessata.

1. **Convalida lo stato corrente.** Passare alla verifica stato filtro di deserializzazione:

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   Se il controllo segnala come attivo, l’istanza è già protetta e non è necessaria alcuna ulteriore azione. In caso di errore, procedere come segue.

1. **Verificare che il file JAR dell&#39;agente sia già presente.** Controlla `notsoserial.jar` nel seguente percorso:

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/
   ```

1. **Aggiungere il file JAR se manca.** Scarica [`notsoserial.jar`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/notsoserial.jar) e copialo nella cartella precedente in ogni istanza:

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Sostituisci questo passaggio con il percorso di download ufficiale di Adobe per la distribuzione Forms JEE dell’agente prima della pubblicazione.

1. **Aggiorna i parametri di avvio JVM** del server applicazioni per collegare l&#39;agente. Aggiungi la seguente opzione alla riga di esecuzione Java™:

   ```shell
   -javaagent:<jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   La posizione esatta della riga di esecuzione Java™ dipende dal server applicazioni (ad esempio, JBoss, WebLogic o WebSphere®). Aggiungi l’opzione alle opzioni JVM utilizzate per avviare il server applicazioni AEM Forms JEE.

1. **Riavviare il server JEE** in modo che l&#39;agente venga caricato all&#39;avvio di JVM.

1. **Riconvalida.** Sfoglia di nuovo per il controllo dello stato:

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   Il controllo di integrità deve ora essere segnalato come integro.

## Verifica dell&#39;attivazione dell&#39;agente {#verifying-the-agents-activation}

Puoi verificare la configurazione dell’agente di deserializzazione in qualsiasi momento individuando il seguente URL:

```text
https://<server>:<port>/system/console/healthcheck?tags=deserialization
```

Viene visualizzato un elenco di controlli di integrità relativi all&#39;agente. Se i controlli sono superati, l’agente viene attivato correttamente. Se si verifica un errore in un&#39;istanza JDK 8, l&#39;agente non è stato caricato ed è necessario allegarlo manualmente utilizzando i passaggi descritti in [Applicazione dell&#39;agente](#applying-the-agent).

## Configurazione dell’agente {#configuring-the-agent}

I passaggi seguenti si applicano se la versione Java™ del server applicazioni è in esecuzione con JDK 8. Puoi configurare l&#39;agente dopo averlo collegato e caricato seguendo i passaggi descritti in [Applicazione dell&#39;agente](#applying-the-agent).

La configurazione predefinita è adeguata per la maggior parte delle installazioni. Include un inserisco nell&#39;elenco Bloccati di di classi sfruttabili in remoto note e un elenco Consentiti di pacchetti in cui la deserializzazione dei dati attendibili è sicura. Il inserisco nell&#39;elenco Bloccati di viene applicato prima di qualsiasi voce inserita nell&#39;elenco Consentiti.

La configurazione del firewall è dinamica e può essere modificata in qualsiasi momento:

1. Passare alla console Web all&#39;indirizzo `https://<server>:<port>/system/console/configMgr`.

1. Cercare e fare clic su **Configurazione firewall deserializzazione**.

Questa configurazione contiene le opzioni di inserisco nell&#39;elenco Consentiti di, di inserisco nell&#39;elenco Bloccati di e di registrazione diagnostica:

* **Inserimento nell&#39;elenco Consentiti** - classi o prefissi di pacchetti consentiti per la deserializzazione. Se deserializzi classi personalizzate, aggiungi qui le classi o i pacchetti pertinenti.
* **Elenco blocchi** - classi che non sono mai consentite per la deserializzazione. Il set iniziale è limitato alle classi trovate vulnerabili agli attacchi di esecuzione remota.
* **Registrazione diagnostica**: opzioni per la registrazione in caso di deserializzazione. Il valore predefinito **class-name-only** indica le classi da deserializzare. L&#39;opzione **full-stack** registra uno stack Java™ per il primo tentativo di deserializzazione, utile per individuare e rimuovere la deserializzazione non attendibile nell&#39;utilizzo. Queste opzioni vengono registrate solo al primo utilizzo.

## Altre considerazioni {#other-considerations}

* L’agente ha lo scopo di attenuare le classi vulnerabili attualmente note. Se il progetto deserializza dati non attendibili, potrebbe comunque essere esposto ad attacchi di denial-of-service, out-of-memory o a deserializzazione futura sconosciuta.
* Se si esegue su un ambiente JRE (Java™ Runtime Environment) anziché su un JDK (Java™ Development Kit), gli strumenti necessari per il caricamento dell&#39;agente dinamico non sono disponibili e l&#39;agente deve essere collegato manualmente all&#39;avvio come descritto in [Applicazione dell&#39;agente](#applying-the-agent).
* Se esegui su una JVM IBM®, consulta la documentazione sul supporto per l’API Java™ Attach.
