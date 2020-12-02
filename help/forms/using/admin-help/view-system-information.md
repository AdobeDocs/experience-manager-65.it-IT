---
title: Visualizzazione delle informazioni sul sistema
seo-title: Visualizzazione delle informazioni sul sistema
description: Informazioni su come visualizzare i grafici di monitoraggio delle risorse e informazioni sul server che esegue AEM moduli.
seo-description: Informazioni su come visualizzare i grafici di monitoraggio delle risorse e informazioni sul server che esegue AEM moduli.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Visualizza informazioni sul sistema {#view-system-information}

Nella scheda Sistema sono visualizzati i grafici di monitoraggio delle risorse e le informazioni sul server che esegue AEM moduli. Per accedere a queste informazioni, nella console di amministrazione fate clic su Monitoraggio stato nell’angolo in alto a destra della pagina. Se si esegue AEM moduli in un ambiente cluster, le informazioni visualizzate sono relative al nodo selezionato nell&#39;elenco Server.

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

**Macchina virtuale: versione** Java Virtual Machine (JVM) sul server.

**Virtual Machine Vendor:** Produttore della JVM.

**Versione macchina virtuale:numero di versione** JVM

**Nome computer: nome** host del server in cui sono installati AEM moduli.

**Ora di attivazione:** tempo, in ore e minuti, in cui il server è stato in esecuzione.

**Compilatore Just-In-Time:** il nome del compilatore in uso.

**Tempo di compilazione:** il tempo impiegato nella compilazione.

**Numero di thread live:** Il numero totale di thread attualmente presenti nel sistema di moduli AEM.

**Numero di thread picco: numero** maggiore di thread live mai registrati sul sistema.

**Numero di classi caricate:** numero di classi caricate nella JVM.

**Numero di classi scaricate:** numero di classi scaricate dalla JVM.

**Heap minimo:** la quantità minima di heap utilizzata.

**Heap massimo:** la quantità massima di heap utilizzata.

**Nome del sistema operativo:** il nome del sistema operativo in esecuzione sul server moduli AEM.

**Versione sistema operativo: numero di** versione del sistema operativo in esecuzione sul server moduli AEM.

**Arco del sistema operativo:** l&#39;architettura del sistema operativo su cui è in esecuzione la JVM.

**Numero di processori:** il numero di processori sul sistema.

**Argomenti della macchina virtuale:** argomento utilizzato dalla JVM.

**Percorso classe:** percorso di classe utilizzato dalla JVM.

**Percorso libreria:** percorso della libreria utilizzato dalla JVM.

**Percorso classe di avvio:** percorso della classe di avvio utilizzato dalla JVM.

**Tipo server applicazione:** tipo di server applicazione utilizzato per eseguire AEM moduli.

**Versione server applicazione:numero** di versione del server applicazione utilizzato per eseguire AEM moduli.

**Fornitore server applicazioni:** produttore del server applicazioni utilizzato per eseguire AEM moduli.

**Data di installazione:** Data (in formato aaaa-mm-gg) in cui sono stati installati AEM moduli.

**AEM moduli Versione:** Versione dei moduli AEM installati.

**Versione patch:** AEM numero della patch per i moduli.

**Nome database:** tipo di database utilizzato dai moduli AEM.

**Versione database: numero** di versione del database utilizzato dai moduli AEM.

**Nome unità del database:** il nome del driver utilizzato dalla JVM per connettersi al database.

**Versione driver di database:** versione del driver utilizzato dalla JVM per connettersi al database.

Il pulsante **Salva** consente di salvare le informazioni del sistema in un file di proprietà.
