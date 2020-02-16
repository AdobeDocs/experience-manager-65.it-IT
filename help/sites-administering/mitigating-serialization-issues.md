---
title: Riduzione dei problemi di serializzazione in AEM
seo-title: Riduzione dei problemi di serializzazione in AEM
description: Scopri come attenuare i problemi di serializzazione in AEM.
seo-description: Scopri come attenuare i problemi di serializzazione in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Riduzione dei problemi di serializzazione in AEM{#mitigating-serialization-issues-in-aem}

## Panoramica {#overview}

Il team AEM di Adobe ha lavorato a stretto contatto con il progetto open source [NotSoSerial](https://github.com/kantega/notsoserial) per aiutare a ridurre le vulnerabilità descritte in **CVE-2015-7501**. NotSoSerial è concesso in licenza con la licenza [](https://www.apache.org/licenses/LICENSE-2.0) Apache 2 e include il codice ASM concesso in licenza con la propria licenza [](https://asm.ow2.org/license.html)BSD.

L&#39;agente Jar incluso in questo pacchetto è la distribuzione modificata di NotSoSerial da parte di Adobe.

NotSoSerial è una soluzione a livello Java per un problema a livello Java e non è specifica per AEM. Aggiunge un controllo di verifica preliminare a un tentativo di deserializzazione di un oggetto. Questo controllo verifica il nome di una classe rispetto a una whitelist e/o blacklist in stile firewall. A causa del numero limitato di classi nella blacklist predefinita, è improbabile che ciò abbia un impatto sui sistemi o sul codice.

Per impostazione predefinita, l&#39;agente eseguirà un controllo della blacklist rispetto alle classi vulnerabili attualmente note. Questa blacklist ha lo scopo di proteggerti dall&#39;elenco corrente di sfruttatori che utilizzano questo tipo di vulnerabilità.

La blacklist e la whitelist possono essere configurate seguendo le istruzioni fornite nella sezione [Configurazione dell&#39;agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) di questo articolo.

L&#39;agente ha lo scopo di attenuare le ultime classi vulnerabili conosciute. Se il progetto sta deserializzando dati non attendibili, potrebbe comunque essere vulnerabile agli attacchi di negazione del servizio, agli attacchi di memoria esauriti e agli attacchi di deserializzazione futuri sconosciuti.

Adobe supporta ufficialmente Java 6, 7 e 8, ma la nostra comprensione è che NotSoSerial supporta anche Java 5.

## Installazione dell&#39;agente {#installing-the-agent}

>[!NOTE]
>
>Se in precedenza avete installato l&#39;hotfix di serializzazione per AEM 6.1, rimuovete i comandi di avvio dell&#39;agente dalla riga di esecuzione Java.

1. Installate il bundle **com.adobe.cq.cq-serialization-tester** .

1. Andate alla console Web del pacchetto all&#39;indirizzo `https://server:port/system/console/bundles`
1. Cercate il bundle di serializzazione e avviatelo. Questo dovrebbe caricare dinamicamente l&#39;agente NotSoSerial.

## Installazione dell&#39;agente sui server applicazioni {#installing-the-agent-on-application-servers}

L’agente NotSoSerial non è incluso nella distribuzione standard di AEM per i server delle applicazioni. Tuttavia, puoi estrarlo dalla distribuzione AEM Jar e utilizzarlo con la configurazione del server applicazione:

1. Innanzitutto, scaricate il file AEM QuickStart ed estraetelo:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Andate alla posizione del nuovo avvio rapido AEM decompresso e copiate la `crx-quickstart/opt/notsoserial/` cartella nella `crx-quickstart` cartella di installazione del server applicazione AEM.

1. Modificate la proprietà dell&#39;utente `/opt` che esegue il server:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configurate e verificate che l&#39;agente sia stato attivato correttamente, come illustrato nelle sezioni seguenti di questo articolo.

## Configurazione dell&#39;agente {#configuring-the-agent}

La configurazione predefinita è adeguata per la maggior parte delle installazioni. Ciò include una blacklist delle classi vulnerabili di esecuzione remota note e una whitelist di pacchetti in cui la deserializzazione di dati attendibili dovrebbe essere relativamente sicura.

La configurazione del firewall è dinamica e può essere modificata in qualsiasi momento:

1. Passate alla console Web in `https://server:port/system/console/configMgr`
1. Ricerca e clic su Configurazione firewall **di deserializzazione.**

   >[!NOTE]
   >
   >Potete inoltre accedere direttamente alla pagina di configurazione accedendo all’URL all’indirizzo:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Questa configurazione contiene la whitelist, la blacklist e la registrazione della deserializzazione.

**Whitelist**

Nella sezione whitelist, si tratta di classi o prefissi di pacchetti che saranno consentiti per la deserializzazione. È importante tenere presente che se si deserializzano le classi, sarà necessario aggiungere le classi o i pacchetti a questa whitelist.

**Blacklist**

Nella sezione della blacklist sono incluse le classi che non possono essere deserializzate. La serie iniziale di queste classi è limitata alle classi che sono state trovate vulnerabili agli attacchi di esecuzione remota. La blacklist viene applicata prima di qualsiasi voce presente nella white list.

**Registrazione diagnostica**

Nella sezione per la registrazione diagnostica, potete scegliere diverse opzioni di registro in fase di deserializzazione. Questi vengono registrati solo per il primo utilizzo e non vengono registrati di nuovo per gli usi successivi.

Per impostazione predefinita, solo **nome** classe contiene le classi che vengono deserializzate.

Potete anche impostare l’opzione **full-stack** che registrerà uno stack Java del primo tentativo di deserializzazione per informarvi su dove si svolge la deserializzazione. Questo può essere utile per trovare e rimuovere la deserializzazione dall’utilizzo.

## Verifica dell&#39;attivazione dell&#39;agente {#verifying-the-agent-s-activation}

Per verificare la configurazione dell&#39;agente di deserializzazione, andate all&#39;URL all&#39;indirizzo:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Una volta effettuato l&#39;accesso all&#39;URL, viene visualizzato un elenco di controlli di integrità relativi all&#39;agente. È possibile determinare se l&#39;agente è attivato correttamente verificando che i controlli di integrità siano superati. In caso di errore, potrebbe essere necessario caricare l&#39;agente manualmente.

Per ulteriori informazioni sulla risoluzione dei problemi con l&#39;agente, vedi [Gestione degli errori con il caricamento](#handling-errors-with-dynamic-agent-loading) dinamico dell&#39;agente di seguito.

>[!NOTE]
>
>Se aggiungete `org.apache.commons.collections.functors` alla whitelist, il controllo dello stato non riuscirà mai.

## Gestione degli errori con caricamento agente dinamico {#handling-errors-with-dynamic-agent-loading}

Se nel registro sono riportati errori o i passaggi di verifica rilevano un problema durante il caricamento dell&#39;agente, potrebbe essere necessario caricare l&#39;agente manualmente. Questo è consigliato anche nel caso in cui si utilizzi un JRE (Java Runtime Environment) invece di un JDK (Java Development Toolkit), poiché gli strumenti per il caricamento dinamico non sono disponibili.

Per caricare l&#39;agente manualmente, seguire le istruzioni riportate di seguito:

1. Modificare i parametri di avvio JVM del Jar CQ, aggiungendo la seguente opzione:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Questo richiede l&#39;utilizzo dell&#39;opzione -nofork CQ/AEM, insieme alle impostazioni di memoria JVM appropriate, in quanto l&#39;agente non sarà abilitato su una JVM biforcata.

   >[!NOTE]
   >
   >La distribuzione Adobe dell&#39;agente NotSoSerial Jar si trova nella `crx-quickstart/opt/notsoserial/` cartella di installazione di AEM.

1. Arrestare e riavviare la JVM;

1. Verifica di nuovo l&#39;attivazione dell&#39;agente seguendo i passaggi descritti in precedenza in [Verifica dell&#39;attivazione](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)dell&#39;agente.

## Altre considerazioni {#other-considerations}

Se utilizzi una JVM IBM, consulta la documentazione relativa al supporto per l&#39;API Java Attach in [questa posizione](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).

