---
title: Visualizzazione delle informazioni sul sistema
seo-title: Visualizzazione delle informazioni sul sistema
description: Scopri come visualizzare i grafici di monitoraggio delle risorse e le informazioni sul server che esegue i moduli AEM.
seo-description: Scopri come visualizzare i grafici di monitoraggio delle risorse e le informazioni sul server che esegue i moduli AEM.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Visualizzazione delle informazioni sul sistema {#view-system-information}

Nella scheda Sistema sono visualizzati i grafici di monitoraggio delle risorse e le informazioni sul server che esegue i moduli AEM. Per accedere a queste informazioni, nella console di amministrazione fate clic su Monitoraggio stato nell’angolo in alto a destra della pagina. Se si eseguono moduli AEM in un ambiente cluster, le informazioni visualizzate sono relative al nodo selezionato nell&#39;elenco Server.

Per salvare le informazioni di sistema correnti come file delle proprietà, fare clic su Salva.

Nel riquadro a destra della scheda Sistema sono visualizzate le rappresentazioni grafiche delle seguenti informazioni:

* Elementi di OdL e di conteggio del lavoro
* Utilizzo Heap e Heap impegnato
* Utilizzo non heap e non heap

Potete trascinare il puntatore lungo la timeline per ottenere i valori per un particolare punto nel tempo.

>[!NOTE]
>
>I dati del grafico, i valori delle informazioni sul server e l’ora dell’orologio vengono aggiornati ogni 10 minuti. Le informazioni non vengono visualizzate in tempo reale.

Nel riquadro a sinistra della scheda Sistema sono visualizzate le seguenti informazioni sul server o sul nodo:

**** Macchina virtuale: Versione Java Virtual Machine (JVM) sul server.

**** Fornitore macchina virtuale: Produttore della JVM.

**** Versione macchina virtuale: Numero versione JVM

**** Nome computer: Nome host del server in cui sono installati i moduli AEM.

**** Tempo Su: L&#39;ora, in ore e minuti, in cui il server è in esecuzione.

**** Compilatore Just-In-Time: Nome del compilatore utilizzato.

**** Tempo di compilazione: Il tempo impiegato nella compilazione.

**** Numero di thread live: Numero totale di thread attualmente presenti nel sistema di moduli AEM.

**** Numero massimo thread: Il maggior numero di thread live registrati sul sistema.

**** Numero di classi caricate: Numero di classi caricate nella JVM.

**** Numero di classi scaricate: Numero di classi scaricate dalla JVM.

**** Heap minimo: Quantità minima di heap utilizzata.

**** Heap massimo: Quantità massima di heap utilizzata.

**** Nome sistema operativo: Nome del sistema operativo in esecuzione sul server moduli AEM.

**** Versione sistema operativo: Numero di versione del sistema operativo in esecuzione sul server moduli AEM.

**** Arco del sistema operativo: Architettura del sistema operativo su cui è in esecuzione la JVM.

**** Numero di processori: Numero di processori sul sistema.

**** Argomenti della macchina virtuale: Argomento utilizzato dalla JVM.

**** Percorso classe: Percorso di classe utilizzato dalla JVM.

**** Percorso libreria: Percorso della libreria utilizzato dalla JVM.

**** Percorso classe di avvio: Percorso della classe di avvio utilizzato dalla JVM.

**** Tipo server applicazioni: Tipo di server applicazioni utilizzato per eseguire i moduli AEM.

**** Versione server applicazione: Numero di versione del server applicazione utilizzato per eseguire i moduli AEM.

**** Fornitore server applicazioni: Produttore del server applicazioni utilizzato per eseguire i moduli AEM.

**** Data di installazione: Data (in formato aaaa-mm-gg) in cui sono stati installati i moduli AEM.

**** Versione moduli AEM: Versione dei moduli AEM installati.

**** Versione patch: Numero patch moduli AEM.

**** Nome database: Tipo di database utilizzato dai moduli AEM.

**** Versione database: Numero di versione del database utilizzato dai moduli AEM.

**** Nome unità di database: Nome del driver utilizzato dalla JVM per connettersi al database.

**** Versione driver di database: Versione del driver utilizzato dalla JVM per connettersi al database.

Il pulsante **Salva** consente di salvare le informazioni del sistema in un file di proprietà.
