---
title: Linee guida per la codifica
description: Linee guida per sviluppatori, suggerimenti e trucchi per community
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
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
source-wordcount: '180'
ht-degree: 3%
---
# Linee guida per la codifica {#coding-guidelines}

## Linee guida, suggerimenti {#guidelines-tips-and-tricks}

L’utilizzo di AEM Communities si è evoluto da una forte dipendenza dalle pagine Java Server a una flessibilità nella scelta di linguaggi di script basati su modelli in cui la logica di business, lo stile e il contenuto delle pagine sono distinti gli uni dagli altri.

L&#39;utilizzo di contenuti generati dagli utenti (UGC, User Generated Content) è più flessibile grazie all&#39;API SocialResourceProvider, che elimina la necessità di sapere quale opzione [SRP](srp.md) è stata scelta per la distribuzione.

Di seguito sono riportate varie linee guida per la codifica e best practice per gli sviluppatori di AEM Communities:

### Codice {#code}

* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - come evitare di scrivere un&#39;applicazione che funziona solo quando UGC è archiviato in JCR (JSRP).
* [Refactoring SocialUtils](socialutils.md) - Metodi di utilità per SRP che sostituiscono SocialUtils.
* [Convenzioni di denominazione](naming-conventions.md) - convenzioni di denominazione per le classi Java personalizzate.

### Script {#scripts}

* [Sideloading Communities Components](sideloading.md) - come aggiungere dinamicamente un componente dopo il caricamento della pagina.
* [Nozioni di base sull&#39;editor Rich Text](rte.md) - personalizzare l&#39;interfaccia utente Rich Text fornita ai membri per la pubblicazione dei contenuti.

### IDE {#ide}

* [Utilizzo di Maven per le community](maven.md): come includere il file jar dell&#39;API Communities.
* [Refactoring SocialUtils](socialutils.md) - Metodi di utilità per SRP che sostituiscono SocialUtils.
