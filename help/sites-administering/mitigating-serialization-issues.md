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
source-git-commit: 3cbbad3ce9d93a353f48fc3206df989a8bf1991a
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Riduzione dei problemi di serializzazione in AEM{#mitigating-serialization-issues-in-aem}

## Panoramica {#overview}

Il team AEM del Adobe  ha lavorato a stretto contatto con il progetto open source [NotSoSerial](https://github.com/kantega/notsoserial) per aiutare a mitigare le vulnerabilità descritte in **CVE-2015-7501**. NotSoSerial è concesso in licenza con la [licenza Apache 2](https://www.apache.org/licenses/LICENSE-2.0) e include il codice ASM concesso in licenza con la propria [licenza BSD](https://asm.ow2.org/license.html).

L&#39;agente Jar incluso con questo pacchetto è  Adobe  distribuzione modificata di NotSoSerial.

NotSoSerial è una soluzione a livello Java per un problema a livello Java e non è AEM specifico. Aggiunge un controllo di verifica preliminare a un tentativo di deserializzazione di un oggetto. Questo controllo verifica il nome di una classe rispetto a un elenco consentiti  e/o  in stile firewall. A causa del numero limitato di classi nel elenco Bloccati di  predefinito, è improbabile che questo abbia un impatto sui sistemi o sul codice.

Per impostazione predefinita, l&#39;agente eseguirà un controllo di elenco Bloccati  rispetto alle classi vulnerabili attualmente note. Questo  elenco Bloccati è inteso a proteggere l&#39;utente dall&#39;elenco corrente di sfruttatori che utilizzano questo tipo di vulnerabilità.

Il elenco Bloccati  e il elenco consentiti  possono essere configurati seguendo le istruzioni fornite nella sezione [Configuring the Agent](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) di questo articolo.

L&#39;agente ha lo scopo di attenuare le ultime classi vulnerabili conosciute. Se il progetto sta deserializzando dati non attendibili, potrebbe comunque essere vulnerabile agli attacchi di negazione del servizio, agli attacchi di memoria esauriti e agli attacchi di deserializzazione futuri sconosciuti.

 Adobe supporta ufficialmente Java 6, 7 e 8, tuttavia la nostra comprensione è che NotSoSerial supporta anche Java 5.

## Installazione dell&#39;agente {#installing-the-agent}

>[!NOTE]
>
>Se avete già installato in precedenza l&#39;hotfix di serializzazione per AEM 6.1, rimuovete i comandi di avvio dell&#39;agente dalla riga di esecuzione Java.

1. Installate il pacchetto **com.adobe.cq.cq-serialization-tester**.

1. Andate alla console Web del pacchetto all&#39;indirizzo `https://server:port/system/console/bundles`
1. Cercate il bundle di serializzazione e avviatelo. Questo dovrebbe caricare dinamicamente l&#39;agente NotSoSerial.

## Installazione dell&#39;agente sui server applicazioni {#installing-the-agent-on-application-servers}

L&#39;agente NotSoSerial non è incluso nella distribuzione standard di AEM per i server delle applicazioni. Tuttavia, è possibile estrarlo dalla distribuzione AEM Jar e utilizzarlo con la configurazione del server applicazione:

1. Innanzitutto, scaricate il AEM file quickstart ed estraetelo:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Andate al percorso del AEM rapido decompresso di recente e copiate la cartella `crx-quickstart/opt/notsoserial/` nella cartella `crx-quickstart` dell&#39;installazione del server dell&#39;applicazione AEM.

1. Modificare la proprietà di `/opt` per l&#39;utente che esegue il server:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configurate e verificate che l&#39;agente sia stato attivato correttamente, come illustrato nelle sezioni seguenti di questo articolo.

## Configurazione dell&#39;agente {#configuring-the-agent}

La configurazione predefinita è adeguata per la maggior parte delle installazioni. Ciò include un elenco Bloccati  di classi vulnerabili di esecuzione remota conosciute e un elenco consentiti  di pacchetti in cui la deserializzazione dei dati attendibili dovrebbe essere relativamente sicura.

La configurazione del firewall è dinamica e può essere modificata in qualsiasi momento:

1. Passate alla console Web all&#39;indirizzo `https://server:port/system/console/configMgr`
1. Ricerca e clic su **Configurazione firewall di deserializzazione.**

   >[!NOTE]
   >
   >Potete inoltre accedere direttamente alla pagina di configurazione accedendo all’URL all’indirizzo:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Questa configurazione contiene il elenco consentiti , il elenco Bloccati  e la registrazione della deserializzazione.

**Consenti elenco**

Nella sezione Consenti elenco, si tratta di classi o prefissi di pacchetti che saranno consentiti per la deserializzazione. È importante tenere presente che se si deserializzano le classi, sarà necessario aggiungere le classi o i pacchetti a questo elenco consentiti .

**Elenco blocchi**

Nella sezione elenco blocchi sono incluse le classi che non possono essere deserializzate. La serie iniziale di queste classi è limitata alle classi che sono state trovate vulnerabili agli attacchi di esecuzione remota. Il elenco Bloccati  viene applicato prima di qualsiasi voce di elenco di tipo Consenti.

**Registrazione diagnostica**

Nella sezione per la registrazione diagnostica, potete scegliere diverse opzioni di registrazione quando viene eseguita la deserializzazione. Questi vengono registrati solo per il primo utilizzo e non vengono registrati di nuovo per gli usi successivi.

Il valore predefinito di **class-name-only** vi informerà delle classi che vengono deserializzate.

Potete anche impostare l&#39;opzione **full-stack** che consente di registrare uno stack Java del primo tentativo di deserializzazione per informarvi in quale punto si trova la deserializzazione. Questo può essere utile per trovare e rimuovere la deserializzazione dall’utilizzo.

## Verifica dell&#39;attivazione dell&#39;agente {#verifying-the-agent-s-activation}

Per verificare la configurazione dell&#39;agente di deserializzazione, andate all&#39;URL all&#39;indirizzo:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Una volta effettuato l&#39;accesso all&#39;URL, viene visualizzato un elenco di controlli di integrità relativi all&#39;agente. È possibile determinare se l&#39;agente è attivato correttamente verificando che i controlli di integrità siano superati. In caso di errore, potrebbe essere necessario caricare l&#39;agente manualmente.

Per ulteriori informazioni sulla risoluzione dei problemi con l&#39;agente, vedere [Gestione degli errori con caricamento dinamico dell&#39;agente](#handling-errors-with-dynamic-agent-loading) di seguito.

>[!NOTE]
>
>Se aggiungete `org.apache.commons.collections.functors` al elenco consentiti , il controllo dello stato di salute avrà sempre esito negativo.

## Gestione degli errori con caricamento dell&#39;agente dinamico {#handling-errors-with-dynamic-agent-loading}

Se nel registro sono riportati degli errori o i passaggi di verifica rilevano un problema durante il caricamento dell&#39;agente, potrebbe essere necessario caricare l&#39;agente manualmente. Questo è consigliato anche nel caso in cui si utilizzi un JRE (Java Runtime Environment) invece di un JDK (Java Development Toolkit), poiché gli strumenti per il caricamento dinamico non sono disponibili.

Per caricare l&#39;agente manualmente, seguire le istruzioni riportate di seguito:

1. Modificate i parametri di avvio JVM del Jar CQ, aggiungendo la seguente opzione:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Questo richiede l&#39;utilizzo dell&#39;opzione -nofork CQ/AEM, insieme alle impostazioni di memoria JVM appropriate, in quanto l&#39;agente non sarà abilitato su una JVM biforcata.

   >[!NOTE]
   >
   >La distribuzione  Adobe del Jar agente NotSoSerial si trova nella cartella `crx-quickstart/opt/notsoserial/` dell&#39;installazione AEM.

1. Arrestare e riavviare la JVM;

1. Verificare nuovamente l&#39;attivazione dell&#39;agente seguendo i passaggi descritti in [Verifica dell&#39;attivazione dell&#39;agente](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Altre considerazioni {#other-considerations}

Se si è in esecuzione su una JVM IBM, consultare la documentazione relativa al supporto per l&#39;API Java Attach in [questo percorso](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).
