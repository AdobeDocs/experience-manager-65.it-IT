---
title: 'Test: quando e con chi?'
seo-title: Testing - when and with whom?
description: Possono essere coinvolti vari ruoli nel test e in varie fasi dello sviluppo del progetto
seo-description: Various roles can be involved in testing and at various stages of project development
uuid: 431e8f06-80eb-4fb3-a4c7-2580608b0a1c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 6148f8e6-ab62-4eb8-8a2d-c431b8318000
exl-id: 5a16be40-eede-4a47-b03b-3993e285232e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Test: quando e con chi?{#testing-when-and-with-whom}

Possono essere coinvolti diversi ruoli nel test e in varie fasi di sviluppo del progetto.

<table>
 <tbody>
  <tr>
   <td>Team di prova</td>
   <td>Responsabile di... </td>
   <td>Quando...</td>
  </tr>
  <tr>
   <td>Team di sviluppo</td>
   <td>Il team di sviluppo è responsabile degli unit test e di alcuni integration test.</td>
   <td>Questi test sono i primi nella catena, anche se saranno ripetuti / estesi durante lo sviluppo.</td>
  </tr>
  <tr>
   <td>Team di controllo qualità</td>
   <td><p>Sarà necessario un team di controllo qualità (di qualsiasi dimensione) per i test funzionali e delle prestazioni.</p> <p>Si tratta di tester neutrali e dedicati: una regola d'oro del software afferma sempre che uno sviluppatore non dovrebbe mai testare il proprio lavoro.</p> <p>I membri di questo team possono provenire dal team di progetto Day, dal partner e/o dal team del cliente.</p> </td>
   <td><p>La prima versione della funzione deve essere resa disponibile ai tester (non appena realisticamente possibile). Anche se una versione provvisoria anticipata può generare molti bug, può fornire un feedback anticipato su problemi critici.</p> </td>
  </tr>
  <tr>
   <td>Team di test cliente</td>
   <td><p>A seconda del modello di progetto selezionato, può essere pianificato il coinvolgimento dei membri del team del cliente nel test, in particolare degli autori della sede del cliente.</p> <p>La è vantaggiosa in quanto:</p>
    <ul>
     <li><p>Fornisce al cliente un’esperienza del progetto in fase di sviluppo.</p> </li>
     <li><p>Fornisce un feedback tempestivo dal cliente.</p> </li>
     <li><p>Gli utenti esprimono spesso le loro esigenze in termini di esperienza passata; il coinvolgimento dei clienti nei test il più presto possibile aumenta la loro esperienza del nuovo progetto in termini di <i>pratico</i> esperienza.</p> </li>
    </ul> </td>
   <td><p>Anche in questo caso il coinvolgimento anticipato è positivo, anche se qualsiasi versione utilizzata dai clienti dovrebbe essere stabile, con funzionalità ragionevoli.</p> <p>Le prime impressioni sono sempre importanti.</p> </td>
  </tr>
 </tbody>
</table>
