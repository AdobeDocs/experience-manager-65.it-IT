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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

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
