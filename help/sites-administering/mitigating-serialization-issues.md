---
title: Riduzione dei problemi di serializzazione in AEM
seo-title: Mitigating serialization issues in AEM
description: Scopri come attenuare i problemi di serializzazione in AEM.
seo-description: Learn how to mitigate serialization issues in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: 614c4c88f3f09feb5a400ade9f45f634ac4fbcd5
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# Riduzione dei problemi di serializzazione in AEM{#mitigating-serialization-issues-in-aem}

## Panoramica {#overview}

Il team AEM di Adobe ha lavorato a stretto contatto con il progetto open-source [NotSoSerial](https://github.com/kantega/notsoserial) per contribuire a mitigare le vulnerabilità descritte in **CVE-2015-7501**. NotSoSerial è concesso in licenza in base al [Licenza Apache 2](https://www.apache.org/licenses/LICENSE-2.0) e include il codice ASM sotto licenza propria [Licenza BSD](https://asm.ow2.io/).

Il jar dell&#39;agente incluso in questo pacchetto è la distribuzione modificata di Adobe di NotSoSerial.

NotSoSerial è una soluzione a livello Java™ per un problema a livello di Java™ e non è specifica AEM. Aggiunge un controllo di verifica preliminare a un tentativo di deserializzare un oggetto. Questo controllo verifica il nome di una classe rispetto a un inserire nell&#39;elenco Consentiti, un inserire nell&#39;elenco Bloccati o un  in stile firewall o entrambi. A causa del numero limitato di classi nell&#39;inserire nell&#39;elenco Bloccati predefinito, è improbabile che questo test abbia un impatto sui sistemi o sul codice.

Per impostazione predefinita, l&#39;agente esegue un controllo inserire nell&#39;elenco Bloccati rispetto alle classi vulnerabili note correnti. Questo inserire nell&#39;elenco Bloccati è inteso a proteggerti dall’elenco corrente di exploit che utilizzano questo tipo di vulnerabilità.

L’inserire nell&#39;elenco Bloccati e l’inserire nell&#39;elenco Consentiti possono essere configurati seguendo le istruzioni contenute nella [Configurazione dell’agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) sezione di questo articolo.

L&#39;agente ha lo scopo di mitigare le ultime classi vulnerabili conosciute. Se il progetto deserializza dati non attendibili, potrebbe comunque essere vulnerabile agli attacchi di negazione del servizio, agli attacchi di memoria esaurita e agli abusi di deserializzazione futura sconosciuti.

Adobe supporta ufficialmente Java™ 6, 7 e 8. Tuttavia, Adobe è consapevole del fatto che NotSoSerial supporta anche Java™ 5.

## Installazione dell&#39;agente {#installing-the-agent}

>[!NOTE]
>
>Se in precedenza hai installato l&#39;hotfix di serializzazione per AEM 6.1, rimuovi i comandi di avvio dell&#39;agente dalla riga di esecuzione Java™.

1. Installa il **com.adobe.cq.cq-serialization-tester** pacchetto.

1. Vai alla console Web del bundle all&#39;indirizzo `https://server:port/system/console/bundles`
1. Cerca il bundle di serializzazione e avvialo. In questo modo l&#39;agente NotSoSerial viene caricato in modo dinamico.

## Installazione dell&#39;agente sui server applicazioni {#installing-the-agent-on-application-servers}

L&#39;agente NotSoSerial non è incluso nella distribuzione standard di AEM per i server applicazioni. Tuttavia, è possibile estrarlo dalla distribuzione jar AEM e utilizzarlo con la configurazione del server applicazioni:

1. Per prima cosa, scarica il file quickstart AEM ed estrailo:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Vai alla posizione del nuovo quickstart AEM decompresso e copia il `crx-quickstart/opt/notsoserial/` nella cartella `crx-quickstart` cartella dell&#39;installazione del server dell&#39;applicazione AEM.

1. Cambiare la proprietà di `/opt` all&#39;utente che esegue il server:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configura e controlla che l’agente sia stato attivato correttamente come mostrato nelle sezioni seguenti di questo articolo.

## Configurazione dell’agente {#configuring-the-agent}

La configurazione predefinita è adeguata per la maggior parte delle installazioni. Questa configurazione include un inserii nell&#39;elenco Bloccati di classi vulnerabili di esecuzione remota note e un inserire nell&#39;elenco Consentiti di pacchetti in cui la deserializzazione dei dati affidabili è sicura.

La configurazione del firewall è dinamica e può essere modificata in qualsiasi momento:

1. Andando alla console Web in `https://server:port/system/console/configMgr`
1. Ricerca e clic **Configurazione del firewall di deserializzazione.**

   >[!NOTE]
   Puoi anche raggiungere la pagina di configurazione direttamente dall’URL all’indirizzo:
   * `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Questa configurazione contiene l&#39;inserire nell&#39;elenco Consentiti, l&#39;inserire nell&#39;elenco Bloccati e la registrazione della deserializzazione.

**Consenti elenco**

Nella sezione per l’elenco Consentiti , questi elenchi sono classi o prefissi di pacchetti consentiti per la deserializzazione. Se stai deserializzando le classi personalizzate, aggiungi le classi o i pacchetti a questo inserire nell&#39;elenco Consentiti.

**Elenco Bloccati**

Nella sezione elenco Bloccati sono presenti classi che non sono mai consentite per la deserializzazione. Il set iniziale di queste classi è limitato alle classi che sono state ritenute vulnerabili agli attacchi di esecuzione remota. L’inserire nell&#39;elenco Bloccati viene applicato prima di qualsiasi voce nell’elenco Consentiti.

**Registrazione diagnostica**

Nella sezione per la registrazione diagnostica, puoi scegliere diverse opzioni di registrazione quando avviene la deserializzazione. Queste opzioni sono registrate solo al primo utilizzo e non vengono registrate nuovamente negli utilizzi successivi.

Il valore predefinito di **solo nome-classe** informa le classi che vengono deserializzate.

È inoltre possibile impostare **pieno** opzione che registra uno stack Java™ del primo tentativo di deserializzazione per informarti dove si sta verificando la deserializzazione. Questa opzione è utile per trovare e rimuovere la deserializzazione dall’utilizzo.

## Verifica dell&#39;attivazione dell&#39;agente {#verifying-the-agent-s-activation}

Puoi verificare la configurazione dell’agente di deserializzazione navigando all’URL all’indirizzo:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Dopo aver effettuato l’accesso all’URL, viene visualizzato un elenco di controlli di integrità relativi all’agente. È possibile determinare se l&#39;agente è correttamente attivato verificando che i controlli di integrità passino. In caso di errore, è necessario caricare l’agente manualmente.

Per ulteriori informazioni sulla risoluzione dei problemi con l&#39;agente, vedi [Gestione Degli Errori Con Il Caricamento Dell’Agente Dinamico](#handling-errors-with-dynamic-agent-loading) sotto.

>[!NOTE]
Se aggiungi `org.apache.commons.collections.functors` all&#39;inserire nell&#39;elenco Consentiti, il controllo dello stato di salute fallisce sempre.

## Gestione degli errori con caricamento dell’agente dinamico {#handling-errors-with-dynamic-agent-loading}

Se nel registro sono presenti errori o i passaggi di verifica rilevano un problema durante il caricamento dell&#39;agente, caricalo manualmente. Questo flusso di lavoro è consigliato anche se utilizzi un ambiente JRE (Java™ Runtime Environment) invece di un JDK (Java™ Development Toolkit), in quanto gli strumenti per il caricamento dinamico non sono disponibili.

Per caricare l&#39;agente manualmente, procedi come segue:

1. Modifica i parametri di avvio JVM del jar CQ, aggiungendo la seguente opzione:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   Richiede di utilizzare anche l&#39;opzione -nofork CQ/AEM, insieme alle impostazioni di memoria JVM appropriate, in quanto l&#39;agente non è abilitato su una JVM con forking.

   >[!NOTE]
   L&#39;Adobe di distribuzione del jar dell&#39;agente NotSoSerial si trova nel `crx-quickstart/opt/notsoserial/` cartella dell&#39;installazione AEM.

1. Arrestare e riavviare la JVM;

1. Verifica nuovamente l&#39;attivazione dell&#39;agente seguendo i passaggi descritti in precedenza in [Verifica dell&#39;attivazione dell&#39;agente](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Altre considerazioni {#other-considerations}

Se utilizzi una JVM IBM®, consulta la documentazione sul supporto per l’API Java™ Attach in [questa posizione](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
