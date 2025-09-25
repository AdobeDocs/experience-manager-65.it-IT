---
title: Visualizzare le informazioni di sistema
description: Scopri come visualizzare i grafici di monitoraggio delle risorse e le informazioni sul server che esegue AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '541'
ht-degree: 100%

---

# Visualizzare le informazioni di sistema {#view-system-information}

Nella scheda Sistema vengono visualizzati i grafici di monitoraggio delle risorse e le informazioni sul server che esegue AEM Forms. Per accedere a queste informazioni, nella console di amministrazione fai clic su Health Monitor nell’angolo superiore destro della pagina. Se esegui AEM Forms in un ambiente cluster, le informazioni visualizzate si riferiscono al nodo selezionato dall’elenco Server.

Per salvare le informazioni di sistema correnti come file delle proprietà, fai clic su Salva.

Nel riquadro destro della scheda Sistema vengono visualizzate rappresentazioni grafiche delle seguenti informazioni:

* Elementi di lavoro e numero lavori
* Utilizzo memoria heap e memoria heap allocata
* Utilizzo memoria non-heap e memoria non-heap allocata

È possibile trascinare il puntatore lungo la timeline per ottenere i valori di un particolare punto nel tempo.

>[!NOTE]
>
>I dati del grafico, i valori delle informazioni sul server e l’ora locale vengono aggiornati ogni 10 minuti. Le informazioni non vengono visualizzate in tempo reale.

Nel riquadro sinistro della scheda Sistema vengono visualizzate le seguenti informazioni sul server o sul nodo:

**Virtual Machine:** versione della Virtual Machine Java (JVM) sul server.

**Fornitore Virtual Machine:** produttore della JVM.

**Versione Virtual Machine:** numero versione JVM

**Nome computer:** nome host del server su cui è installato AEM Forms.

**Tempo di attività:** il tempo, in ore e minuti, di funzionamento del server.

**Just-In-Time Compiler:** nome del compiler utilizzato.

**Tempo di compilazione:** tempo impiegato per la compilazione.

**Numero di thread attivi:** il numero totale di thread attualmente presenti nel sistema AEM Forms.

**Numero del picco di thread:** il numero maggiore di thread attivi mai registrati nel sistema.

**Numero di classi caricate:** numero di classi caricate in JVM.

**Numero di classi scaricate:** numero di classi scaricate dalla JVM.

**Memoria heap minima:** la quantità minima di memoria heap utilizzata.

**Memoria heap massima:** la quantità massima di memoria heap utilizzata.

**Nome sistema operativo:** il nome del sistema operativo in esecuzione sul server AEM Forms.

**Versione sistema operativo:** numero di versione del sistema operativo in esecuzione sul server AEM Forms.

**Arco sistema operativo:** architettura del sistema operativo su cui è in esecuzione JVM.

**Numero di processori:** il numero di processori nel sistema.

**Argomenti Virtual Machine:** l’argomento utilizzato da JVM.

**Percorso classe:** il percorso di classe utilizzato da JVM.

**Percorso libreria:** il percorso della libreria utilizzato da JVM.

**Percorso classe di avvio:** il percorso della classe di avvio utilizzato dalla JVM.

**Tipo di server applicazioni:** tipo di server applicazioni utilizzato per eseguire AEM Forms.

**Versione server applicazioni:** il numero di versione del server applicazioni utilizzato per eseguire AEM Forms.

**Fornitore server applicazioni:** produttore del server applicazioni utilizzato per eseguire AEM Forms.

**Data di installazione:** data (in formato dd-mm-yyyy) in cui è stato installato AEM Forms.

**Versione di AEM Forms:** versione di AEM Forms installata.

**Versione patch:** numero patch AEM Forms.

**Nome database:** tipo di database utilizzato da AEM Forms.

**Versione database:** numero di versione del database utilizzato da AEM Forms.

**Nome unità di database:** il nome del driver utilizzato da JVM per connettersi al database.

**Versione driver di database:** versione del driver utilizzata dalla JVM per connettersi al database.

Il pulsante **Salva** consente di salvare le informazioni di sistema in un file delle proprietà.
