---
title: Visualizza informazioni sul sistema
seo-title: View system information
description: Scopri come visualizzare i grafici di monitoraggio delle risorse e le informazioni sul server che esegue AEM moduli.
seo-description: Learn how you can view resource monitoring charts and information about the server that is running AEM forms.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Visualizza informazioni sul sistema {#view-system-information}

Nella scheda Sistema sono visualizzati i grafici di monitoraggio delle risorse e le informazioni sul server che esegue AEM moduli. Per accedere a queste informazioni, nella console di amministrazione fai clic su Monitoraggio integrità nell’angolo in alto a destra della pagina. Se si esegue AEM moduli in un ambiente cluster, le informazioni visualizzate sono relative al nodo selezionato dall&#39;elenco Server.

Per salvare le informazioni di sistema correnti come file di proprietà, fare clic su Salva.

Nel riquadro a destra della scheda Sistema vengono visualizzate rappresentazioni grafiche delle seguenti informazioni:

* Elementi per il conteggio di lavoro e di lavoro
* Uso Heap a Heap e Impegnato
* Utilizzo non heap e non heap

È possibile trascinare il puntatore lungo la timeline per ottenere i valori per un particolare punto nel tempo.

>[!NOTE]
>
>I dati del grafico, i valori delle informazioni sul server e l’ora dell’orologio vengono aggiornati ogni 10 minuti. Le informazioni non vengono visualizzate in tempo reale.

Nel riquadro a sinistra della scheda Sistema vengono visualizzate le seguenti informazioni sul server o sul nodo:

**Macchina virtuale:** Java Virtual Machine (JVM) versione sul server.

**Fornitore di macchine virtuali:** Produttore della JVM.

**Versione macchina virtuale:** Numero della versione JVM

**Nome macchina:** Nome host del server in cui sono installati AEM moduli.

**Tempo di accensione:** Tempo di esecuzione del server, in ore e minuti.

**Compilatore Just-In-Time:** Nome del compilatore utilizzato.

**Tempo di compilazione:** Quantità di tempo impiegato nella compilazione.

**Numero di thread live:** Numero totale di thread attualmente presenti nel sistema di moduli AEM.

**Numero massimo di thread:** Il maggior numero di thread live mai registrati sul sistema.

**Numero di classi caricate:** Numero di classi caricate nella JVM.

**Numero di classi non caricate:** Numero di classi scaricate dalla JVM.

**Heap minimo:** Quantità minima di heap utilizzata.

**Heap massimo:** La quantità massima di heap utilizzata.

**Nome del sistema operativo:** Nome del sistema operativo in esecuzione sul server dei moduli AEM.

**Versione sistema operativo:** Numero di versione del sistema operativo in esecuzione sul server dei moduli AEM.

**Arco del sistema operativo:** Architettura del sistema operativo su cui è in esecuzione la JVM.

**Numero di processori:** Numero di processori presenti nel sistema.

**Argomenti della macchina virtuale:** Argomento utilizzato dalla JVM.

**Percorso classe:** Percorso classe utilizzato dalla JVM.

**Percorso libreria:** Percorso della libreria utilizzato dalla JVM.

**Percorso classe di avvio:** Percorso della classe di avvio utilizzato dalla JVM.

**Tipo di server applicazioni:** Tipo di server applicazioni utilizzato per eseguire AEM moduli.

**Versione server applicazioni:** Numero di versione dell’application server utilizzato per eseguire AEM moduli.

**Fornitore server applicazioni:** Produttore dell’application server utilizzato per eseguire AEM moduli.

**Data di installazione:** Data (in formato aaaa-mm-gg) in cui sono stati installati AEM moduli.

**Versione moduli AEM:** Versione dei moduli AEM installati.

**Versione patch:** AEM il numero della patch.

**Nome database:** Tipo di database utilizzato dai moduli AEM.

**Versione database:** Numero di versione del database utilizzato dai moduli AEM.

**Nome unità di database:** Nome del driver utilizzato dalla JVM per la connessione al database.

**Versione driver di database:** Versione del driver utilizzato dalla JVM per la connessione al database.

La **Salva** pulsante consente di salvare le informazioni di sistema in un file di proprietà.
