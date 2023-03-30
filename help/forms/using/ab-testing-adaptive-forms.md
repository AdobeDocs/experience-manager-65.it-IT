---
title: Creazione e gestione di test A/B per i moduli adattivi
seo-title: Create and manage A/B test for adaptive forms
description: AEM Forms si integra con Adobe Target per consentire l’esecuzione di test A/B per i moduli adattivi al fine di migliorare la customer experience e i tassi di conversione.
seo-description: AEM Forms integrates with Adobe Target that allows running A/B tests for adaptive forms to enhance customer experience and improve conversion rates.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: ccbb6a33c2ee8029d2e82d9098c07de18af166ac
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 2%

---

# Creazione e gestione di test A/B per i moduli adattivi{#create-and-manage-a-b-test-for-adaptive-forms}

|Negativo|[!BADGE Disattivato]{type=negative tooltip="Questa funzione è ora terminata"}|
<div class="preview"> Il test A/B per la funzione Moduli adattivi ha raggiunto la fine del ciclo di vita e non è più supportato. </div>

## Panoramica {#overview-br}

È probabile che i clienti abbandonino un modulo se l’esperienza che offre non è coinvolgente. Anche se è frustrante per i clienti, può anche aumentare il volume di supporto e i costi per la tua organizzazione. È fondamentale e impegnativo identificare e fornire al cliente la giusta esperienza che aumenti il tasso di conversione. Adobe Experience Manager Forms è la chiave di questo problema.

AEM Forms si integra con Adobe Target, una soluzione Adobe Marketing Cloud, per fornire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Una delle funzionalità chiave di Target è il test A/B che ti consente di impostare rapidamente test A/B simultanei, presentare contenuti pertinenti agli utenti mirati e identificare l’esperienza che guida un migliore tasso di conversione.

Con AEM Forms, puoi impostare ed eseguire in tempo reale test A/B sui moduli adattivi. Offre inoltre funzionalità di reporting predefinite e personalizzabili per visualizzare le prestazioni in tempo reale delle esperienze del modulo e identificare quella che massimizza il coinvolgimento e la conversione degli utenti.

## Configurazione e integrazione di Target in AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Prima di iniziare a creare e analizzare i test A/B per i moduli adattivi, è necessario configurare il server Target e integrarlo in AEM Forms.

### Configurare Target {#set-up-target}

Per integrare AEM con Target, assicurati di disporre di un account Adobe Target valido. Quando ti registri ad Adobe Target, ricevi un codice cliente. Per connettersi a AEM con Target, è necessario disporre del codice client, dell’e-mail associata all’account Target e della password.

Il codice client identifica l’account cliente Adobe Target e viene utilizzato come sottodominio nell’URL quando si chiama il server Adobe Target. Prima di procedere, accedi a [https://experience.adobe.com/](https://experience.adobe.com/) e, se disponi dell&#39;accesso, visualizza il [!DNL Adobe Target] in [!UICONTROL Accesso rapido] sezione .

### Integrare Target in AEM Forms {#integrate-target-in-aem-forms}

Esegui i seguenti passaggi per integrare un server Target in esecuzione con AEM Forms:

1. Sul server AEM, vai su https://&lt;*hostname*>:&lt;*porta*>/libs/cq/core/content/tools/cloudservices.html.

1. In **Adobe Target** sezione, fai clic su **Mostra configurazioni** e poi **+** per aggiungere una nuova configurazione.
Se stai configurando target per la prima volta, fai clic su **Configura ora.**

1. Nella finestra di dialogo Crea configurazione , specifica un **Titolo** e facoltativamente a **Nome** per la configurazione.

1. Fai clic su **Crea**. Viene visualizzata la finestra di dialogo Modifica componente.
1. Specifica i dettagli del tuo account Target, ad esempio codice cliente, e-mail e password.
1. Seleziona **Resto** dall’elenco a discesa Tipo di API .

1. Fai clic su **Connetti ad Adobe Target** per inizializzare la connessione con Target. Se la connessione ha esito positivo, viene visualizzato il messaggio Connessione riuscita. Fai clic su **OK** sul messaggio e quindi **OK** nella finestra di dialogo. L’account Target è configurato.

1. Creare un framework Target come descritto in [Aggiungere un framework](/help/sites-administering/target.md).

1. Vai su https://&lt;*hostname*>:&lt;*porta*>/system/console/configMgr.

1. Fai clic su **Configurazione di AEM Forms Target**.
1. Seleziona una **Framework di Target**.
1. In **URL di destinazione** Specifica tutti gli URL in cui verranno eseguiti i test A/B. Ad esempio, https://&lt;*hostname*>:&lt;*porta*>/ per il server AEM Forms su OSGi o https://&lt;*hostname*>:&lt;*porta*>/lc/ per il server AEM Forms su JEE.
Se desideri configurare un URL di Target per un’istanza di pubblicazione e i tuoi clienti possono accedervi utilizzando il nome host o l’indirizzo IP, dovrai configurarlo sia come URL di Target, utilizzando sia il nome host che l’indirizzo IP. Se configuri solo uno degli URL, il test A/B non verrà eseguito per i clienti provenienti dall’altro URL. Fai clic su **+** per specificare più URL.

1. Fai clic su **Salva**.

Il server Target è integrato con AEM Forms. Ora puoi abilitare il test A/B se disponi di una licenza completa per utilizzare Adobe Target.

Se disponi di una licenza completa per utilizzare Adobe Target, avvia il server con i seguenti parametri dopo aver integrato Target con AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Se l&#39;istanza AEM è in esecuzione su JBoss, avviata come servizio da turnkey, in `jboss\bin\standalone.conf.bat` aggiungi il parametro -Dabtesting.enabled=true nella voce seguente:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Oltre al server jboss, puoi aggiungere l&#39;argomento jvm -Dabtesting.enabled=true nello script di avvio del server per qualsiasi server applicativo. Ora è possibile creare ed eseguire test A/B per i moduli adattivi.

>[!NOTE]
>
>Se aggiorni gli URL di Target configurati in un secondo momento, assicurati di aggiornare tutti i test A/B in esecuzione in modo che puntino agli URL correnti. Per informazioni sull’aggiornamento dei test A/B, vedi [Aggiorna test A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).

## Crea tipi di pubblico in AEM {#create-audiences-within-aem}

AEM consente di creare un pubblico e di utilizzarlo per un test A/B. Il pubblico creato in AEM è disponibile in AEM Forms. Esegui i seguenti passaggi per creare tipi di pubblico in AEM:

1. Nell’istanza di authoring, tocca **Adobe Experience Manager** > **Personalizzazione** > **Tipi di pubblico**.

1. Nella pagina Pubblico, tocca **Crea pubblico > Crea pubblico Target**.
1. Nella finestra di dialogo Configurazione Adobe Target, seleziona una configurazione di Target e fai clic su **Ok**.
1. Nella pagina Crea nuovo pubblico , crea delle regole. Le regole ti consentono di classificare il pubblico. Ad esempio, vuoi organizzare in categorie i tipi di pubblico in base al sistema operativo. Il tuo pubblico A viene da Windows, e il pubblico B viene da Linux.

   1. Per classificare il pubblico in base a Windows, nella regola n. 1, seleziona **OS** tipo di attributo. Dal menu a discesa Quando , seleziona **Windows.**

   1. Per classificare il pubblico in base a Linux, nella regola n. 2, seleziona **OS** tipo di attributo. Da **Quando** a discesa, seleziona **Linux** e fai clic su **Successivo**.

1. Specifica un nome per il pubblico creato e fai clic su **Salva**.

È possibile selezionare il pubblico quando si configurano i test A/B per un modulo, come illustrato di seguito.

## Creare un test A/B {#create-a-b-test}

Esegui i seguenti passaggi per creare un test A/B per un modulo adattivo.

1. Vai a **Forms e documenti** all’indirizzo https://&lt;*hostname*>:&lt;*porta*>/aem/forms.html/content/dam/formsanddocuments .

1. Passa alla cartella contenente il modulo adattivo.
1. Fai clic sul pulsante **Seleziona** nella barra degli strumenti e seleziona il modulo adattivo.
1. Fai clic su **Altro** nella barra degli strumenti e seleziona **Configurare il test A/B**. Viene visualizzata la pagina Configura test A/B .

[ ](assets/ab-test-configure-1.png)

1. Specifica un **Nome attività** per il test A/B.

1. Dall’elenco a discesa Pubblico , seleziona un pubblico a cui desideri indirizzare diverse esperienze del modulo. Ad esempio: **Visitatori che utilizzano Chrome**. L’elenco dei tipi di pubblico viene compilato dal server di Target configurato.

1. In **Distribuzione delle esperienze** nei campi per le esperienze A e B, specifica la distribuzione, in percentuale, per determinare la distribuzione delle esperienze tra il pubblico totale. Ad esempio, se specifichi rispettivamente 40, 60 per le esperienze A e B, l’esperienza A verrà servita al 40% del pubblico e il restante 60% vedrà l’esperienza B.
1. Fai clic su **Configura**. Viene visualizzata una finestra di dialogo per confermare la creazione del test A/B.
1. Fai clic su **Modifica esperienza B** per aprire il modulo adattivo in modalità di modifica. Modifica il modulo per creare un’esperienza diversa da quella predefinita A. Le possibili varianti consentite nell’Esperienza B sono le modifiche apportate in:

   * CSS o stile
   * Ordine dei campi in pannelli diversi o nello stesso pannello
   * Layout pannello
   * Titoli del pannello
   * Descrizione, etichetta e testo della guida per un campo
   * Script che non influiscono sul flusso di invio o ne annullano l’interruzione
   * Convalida (lato client e lato server)
   * Tema per l&#39;esperienza B. (È possibile selezionare un tema alternativo per l&#39;esperienza B)

1. Vai all’interfaccia utente Forms e Documenti, seleziona il modulo adattivo, fai clic su **Altro**, quindi seleziona **Avvia test A/B**.

Il test A/B è ora in esecuzione e al pubblico specificato verranno servite in modo casuale le esperienze in base alla distribuzione specificata.

## Aggiorna test A/B {#update-a-b-test}

Puoi aggiornare le distribuzioni di pubblico ed esperienza di un test A/B in esecuzione. Per eseguire questa operazione:

1. Nell’interfaccia utente Forms e documenti, individua la cartella contenente il modulo adattivo in cui è in esecuzione il test A/B.
1. Seleziona il modulo adattivo.
1. Fai clic su **Altro** quindi seleziona **Modificare il test A/B**. Viene visualizzata la pagina Aggiorna test A/B .

1. Aggiorna le distribuzioni di pubblico ed esperienza, a seconda delle esigenze.
1. Fai clic su **Aggiorna**.

## Visualizzare e analizzare il rapporto del test A/B {#view-and-analyze-a-b-test-report}

Dopo aver consentito l’esecuzione del test A/B per il periodo desiderato, puoi generare un rapporto e verificare quale esperienza ha portato a una migliore conversione. Puoi dichiarare vincente l’esperienza con prestazioni migliori o scegliere di eseguire un altro test A/B. A questo scopo, esegui le seguenti operazioni:

1. Seleziona il modulo adattivo, fai clic su **Altro**, quindi fai clic su **Rapporto sui test A/B**. Viene visualizzato il rapporto.

[ ](assets/ab-test-report-3.png)

1. Analizza il rapporto e verifica se hai abbastanza punti di dati per dichiarare vincente una delle esperienze con prestazioni migliori. Puoi scegliere di continuare con lo stesso test A/B per più tempo oppure dichiarare un vincitore e terminare il test A/B.
1. Per dichiarare un vincitore e terminare il test A/B, fai clic su **Test A/B finale** sul dashboard di reporting. Viene visualizzata una finestra di dialogo in cui viene richiesto di dichiarare vincente una delle due esperienze. Scegli un vincitore e conferma di terminare il test A/B.
In alternativa, per dichiarare un vincitore, fai clic sul pulsante **Dichiara vincitore** pulsante per la relativa esperienza. Viene richiesto di confermare il vincitore. Fai clic su **Sì** per terminare il test A/B.

Se hai scelto come vincitore l’esperienza A, il test A/B verrà messo al termine e, andando avanti, solo l’esperienza A verrà servita a tutti i tipi di pubblico.
