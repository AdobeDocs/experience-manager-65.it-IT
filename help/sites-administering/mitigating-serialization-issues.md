---
title: Mitigazione dei problemi di serializzazione nell’AEM
description: Scopri come attenuare i problemi di serializzazione nell’AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Mitigazione dei problemi di serializzazione nell’AEM{#mitigating-serialization-issues-in-aem}

## Panoramica {#overview}

Il team AEM di Adobe ha lavorato a stretto contatto con il progetto open-source [NotSoSerial](https://github.com/kantega/notsoserial) per contribuire a mitigare le vulnerabilità descritte in **CVE-2015-7501**. NotSoSerial è concesso in licenza con la [licenza Apache 2](https://www.apache.org/licenses/LICENSE-2.0) e include il codice ASM concesso in licenza con la propria [licenza BSD](https://asm.ow2.io/).

Il file jar dell’agente incluso in questo pacchetto è la distribuzione modificata di NotSoSerial di Adobe.

NotSoSerial è una soluzione Java™ a un problema di livello Java™ e non è specifica per l’AEM. Aggiunge un controllo preliminare a un tentativo di deserializzare un oggetto. Questo controllo verifica il nome di una classe in base a un inserisco nell&#39;elenco Consentiti di classe di tipo firewall-style, a un elenco Bloccati di classe di tipo o a entrambi. A causa del numero limitato di classi nel inserisco nell&#39;elenco Bloccati di predefinito, è improbabile che questo test influisca sui sistemi o sul codice.

Per impostazione predefinita, l&#39;agente esegue un controllo di inserisce nell&#39;elenco Bloccati basato su un valore di  per le classi vulnerabili correnti note. Questo inserisco nell&#39;elenco Bloccati di ha lo scopo di proteggerti dall’elenco corrente di exploit che utilizzano questo tipo di vulnerabilità.

La inserisce nell&#39;elenco Bloccati e il elenco Consentiti di dell&#39;agente di possono essere configurati seguendo le istruzioni riportate nella sezione [Configurazione dell&#39;agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) di questo articolo.

L’agente ha lo scopo di contribuire a mitigare le classi vulnerabili più recenti. Se il progetto deserializza dati non attendibili, potrebbe essere vulnerabile ad attacchi Denial of Service, attacchi di memoria insufficiente e attacchi di deserializzazione futuri sconosciuti.

Adobe supporta ufficialmente Java™ 6, 7 e 8. Tuttavia, Adobe è consapevole del fatto che NotSoSerial supporta anche Java™ 5.

## Installazione dell’agente {#installing-the-agent}

>[!NOTE]
>
>Se in precedenza è stato installato l&#39;hotfix di serializzazione per AEM 6.1, rimuovere i comandi di avvio agente dalla riga di esecuzione Java™.

1. Installa il bundle **com.adobe.cq.cq-serialization-tester**.

1. Passa alla console Web del bundle in `https://server:port/system/console/bundles`
1. Cerca il bundle di serializzazione e avvialo. In questo modo l’agente NotSoSerial viene caricato in modo dinamico.

## Installazione dell&#39;agente sui server applicazioni {#installing-the-agent-on-application-servers}

L&#39;agente NotSoSerial non è incluso nella distribuzione standard dell&#39;AEM per i server applicazioni. Tuttavia, puoi estrarlo dalla distribuzione del file jar dell’AEM e utilizzarlo con la configurazione del server applicazioni:

1. Per prima cosa, scarica il file quickstart dell’AEM ed estrailo:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Passare al percorso dell&#39;avvio rapido AEM appena decompresso e copiare la cartella `crx-quickstart/opt/notsoserial/` nella cartella `crx-quickstart` dell&#39;installazione del server applicazioni AEM.

1. Cambia la proprietà di `/opt` all&#39;utente che esegue il server:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configura e controlla che l’agente sia stato attivato correttamente come mostrato nelle sezioni seguenti di questo articolo.

## Configurazione dell’agente {#configuring-the-agent}

La configurazione predefinita è adeguata per la maggior parte delle installazioni. Questa configurazione include un inserisco nell&#39;elenco Bloccati di esecuzione remota vulnerabile di classi conosciute ed un inserisco nell&#39;elenco Consentiti di esecuzione remota di pacchetti in cui la deserializzazione dei dati attendibili è sicura.

La configurazione del firewall è dinamica e può essere modificata in qualsiasi momento:

1. Passaggio alla console Web in `https://server:port/system/console/configMgr`
1. Ricerca e clic su **Configurazione firewall deserializzazione.**

   >[!NOTE]
   >
   >Puoi anche raggiungere direttamente la pagina di configurazione accedendo all’URL all’indirizzo:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`

Questa configurazione contiene la registrazione del inserisco nell&#39;elenco Consentiti di, del inserisco nell&#39;elenco Bloccati di e della deserializzazione.

**Inserzione consentita**

Nella sezione dell’elenco Consentiti queste voci sono classi o prefissi di pacchetti consentiti per la deserializzazione. Se si desidera deserializzare classi personalizzate, aggiungere le classi o i pacchetti a questo inserisco nell&#39;elenco Consentiti di.

**Elenco Bloccati**

Nella sezione dell’elenco di blocchi sono incluse classi che non sono mai consentite per la deserializzazione. Il set iniziale di queste classi è limitato alle classi che sono state trovate vulnerabili ad attacchi di esecuzione remota. Il inserisco nell&#39;elenco Bloccati di viene applicato prima di qualsiasi voce inserita nell’elenco Consentiti.

**Registrazione diagnostica**

Nella sezione per la registrazione diagnostica, puoi scegliere diverse opzioni da registrare durante la deserializzazione. Queste opzioni vengono registrate solo al primo utilizzo e non agli utilizzi successivi.

Il valore predefinito di **class-name-only** informa l&#39;utente sulle classi che vengono deserializzate.

È inoltre possibile impostare l&#39;opzione **full-stack** che registra uno stack Java™ del primo tentativo di deserializzazione per indicare dove avviene la deserializzazione. Questa opzione è utile per trovare e rimuovere la deserializzazione dall’utilizzo.

## Verifica dell&#39;attivazione dell&#39;agente {#verifying-the-agent-s-activation}

Puoi verificare la configurazione dell’agente di deserializzazione consultando l’URL all’indirizzo:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Dopo aver effettuato l’accesso all’URL, viene visualizzato un elenco di controlli di integrità relativi all’agente. Puoi determinare se l’agente è attivato correttamente verificando che i controlli di integrità stiano passando. Se il problema persiste, è necessario caricare l&#39;agente manualmente.

Per ulteriori informazioni sulla risoluzione dei problemi con l&#39;agente, vedere [Gestione degli errori con il caricamento dell&#39;agente dinamico](#handling-errors-with-dynamic-agent-loading) di seguito.

>[!NOTE]
>
>Se aggiungi `org.apache.commons.collections.functors` al inserisco nell&#39;elenco Consentiti di, il controllo dello stato di integrità non riesce mai.

## Gestione degli errori con il caricamento degli agenti dinamici {#handling-errors-with-dynamic-agent-loading}

Se nel registro sono esposti errori o se i passaggi di verifica rilevano un problema durante il caricamento dell’agente, carica l’agente manualmente. Questo flusso di lavoro è consigliato anche se utilizzi un ambiente JRE (Java™ Runtime Environment) invece di un JDK (Java™ Development Toolkit), perché gli strumenti per il caricamento dinamico non sono disponibili.

Per caricare l&#39;agente manualmente, eseguire le operazioni seguenti:

1. Modifica i parametri di avvio JVM del file jar CQ, aggiungendo la seguente opzione:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Richiede che si utilizzi anche l&#39;opzione -nofork CQ/AEM, insieme alle impostazioni di memoria JVM appropriate, in quanto l&#39;agente non è abilitato su una JVM fork.

   >[!NOTE]
   >
   >La distribuzione di Adobe del file jar dell&#39;agente NotSoSerial si trova nella cartella `crx-quickstart/opt/notsoserial/` dell&#39;installazione dell&#39;AEM.

1. Arrestare e riavviare la JVM;

1. Verificare di nuovo l&#39;attivazione dell&#39;agente seguendo i passaggi descritti in precedenza in [Verifica dell&#39;attivazione dell&#39;agente](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Altre considerazioni {#other-considerations}

Se esegui su una JVM IBM®, consulta la documentazione sul supporto per l&#39;API Java™ Attach in [questa posizione](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
