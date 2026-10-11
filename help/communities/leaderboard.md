---
title: Nozioni di base sulla classifica
description: Scopri come configurare il punteggio e i badge per community per utilizzare il componente Classifica nelle community Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 4%
---
# Nozioni di base sulla classifica {#leaderboard-essentials}

Questa pagina fornisce le informazioni essenziali per l&#39;utilizzo della funzione classifica.

Prima di includere il componente classifica in una pagina, è necessario configurare [Punteggio community e distintivi](implementing-scoring.md).

Consulta [Nozioni di base su punteggio e badge](configure-scoring.md).

## Nozioni di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>tiporisorsa</strong></td>
   <td>social/gamification/components/hbs/classifica</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includibile</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.lead</td>
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
   <td>Vedi <a href="enabling-leaderboard.md">Funzione classifica</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

### Funzione Libreria file {#file-library-function}

Una struttura del sito della community che include la funzione [Classifica](functions.md#leaderboard-function), include un componente `leaderboard` configurato.
