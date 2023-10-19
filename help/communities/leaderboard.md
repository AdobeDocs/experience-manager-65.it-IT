---
title: Nozioni di base sulla classifica
description: Scopri come configurare il punteggio e i badge per community per utilizzare il componente Classifica nelle community Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 4%

---

# Nozioni di base sulla classifica {#leaderboard-essentials}

Questa pagina fornisce le informazioni essenziali per l&#39;utilizzo della funzione classifica.

Prima di includere il componente classifica in una pagina, è necessario configurare [Punteggio community e badge](implementing-scoring.md).

Consulta [Nozioni di base su punteggio e distintivi](configure-scoring.md).

## Nozioni di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/components/hbs/classifica</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluso</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>Consulta <a href="enabling-leaderboard.md">Funzione classifica</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

### Funzione Libreria file {#file-library-function}

Una struttura del sito della community che include [Funzione classifica](functions.md#leaderboard-function), include un `leaderboard` componente.
