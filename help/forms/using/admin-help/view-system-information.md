---
title: Visualizza informazioni di sistema
description: Scopri come visualizzare i grafici di monitoraggio delle risorse e le informazioni sul server che esegue i moduli AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Visualizza informazioni di sistema {#view-system-information}

Nella scheda Sistema vengono visualizzati i grafici di monitoraggio delle risorse e le informazioni relative al server che esegue i moduli AEM. Per accedere a queste informazioni, nella console di amministrazione fare clic su Health Monitor nell&#39;angolo superiore destro della pagina. Se si eseguono moduli AEM in un ambiente cluster, le informazioni visualizzate si riferiscono al nodo selezionato dall&#39;elenco Server.

Per salvare le informazioni di sistema correnti come file delle proprietà, fare clic su Salva.

Nel riquadro destro della scheda Sistema vengono visualizzate rappresentazioni grafiche delle seguenti informazioni:

* Elementi di lavoro e numero lavori
* Utilizzo heap e heap confermato
* Utilizzo non heap e non heap confermato

È possibile trascinare il puntatore lungo la linea temporale per ottenere i valori di un particolare punto nel tempo.

>[!NOTE]
>
>I dati del grafico, i valori delle informazioni sul server e l’ora di clock vengono aggiornati ogni 10 minuti. Le informazioni non vengono visualizzate in tempo reale.

Nel riquadro sinistro della scheda Sistema vengono visualizzate le seguenti informazioni sul server o sul nodo:

**Macchina virtuale:** versione di Java Virtual Machine (JVM) nel server.

**Fornitore macchina virtuale:** produttore della JVM.

**Versione macchina virtuale:** Numero versione JVM

**Nome computer:** Nome host del server in cui sono installati i moduli AEM.

**Tempo di attività:** il tempo, in ore e minuti, in cui il server è in esecuzione.

**Compilatore JIT:** Nome del compilatore utilizzato.

**Tempo di compilazione:** Tempo impiegato per la compilazione.

**Numero di Live Threads:** Il numero totale di thread attualmente presenti nel sistema di moduli AEM.

**Numero massimo di Threads:** Il numero massimo di thread live mai registrati nel sistema.

**Numero di classi caricate:** Numero di classi caricate nella JVM.

**Numero di classi scaricate:** Numero di classi scaricate dalla JVM.

**Heap minimo:** La quantità minima di heap utilizzata.

**Memoria heap massima:** La quantità massima di heap utilizzata.

**Nome sistema operativo:** Il nome del sistema operativo in esecuzione sul server AEM Forms.

**Versione sistema operativo:** Numero di versione del sistema operativo in esecuzione sul server AEM Forms.

**Arco sistema operativo:** Architettura del sistema operativo su cui è in esecuzione JVM.

**Numero di processori:** Numero di processori nel sistema.

**Argomenti macchina virtuale:** Argomento utilizzato da JVM.

**Percorso classe:** Percorso di classe utilizzato da JVM.

**Percorso libreria:** Percorso della libreria utilizzato da JVM.

**Percorso classe di avvio:** Percorso della classe di avvio utilizzato dalla JVM.

**Tipo di server applicazioni:** Tipo di server applicazioni utilizzato per eseguire i moduli AEM.

**Versione server applicazioni:** Numero di versione del server applicazioni utilizzato per eseguire i moduli AEM.

**Fornitore server applicazioni:** Produttore del server applicazioni utilizzato per eseguire i moduli AEM.

**Data di installazione:** Data (in formato aaaa-mm-gg) in cui sono stati installati i moduli AEM.

**Versione moduli AEM:** versione dei moduli AEM installata.

**Versione patch:** AEM forma il numero di patch.

**Nome database:** Tipo di database utilizzato dai moduli AEM.

**Versione database:** Numero di versione del database utilizzato dai moduli AEM.

**Nome unità di database:** Il nome del driver utilizzato dalla JVM per connettersi al database.

**Versione driver di database:** versione del driver utilizzata dalla JVM per connettersi al database.

Il pulsante **Salva** consente di salvare le informazioni di sistema in un file delle proprietà.
