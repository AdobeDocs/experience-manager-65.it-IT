---
title: Linee guida per la codifica
description: Linee guida per sviluppatori, suggerimenti e trucchi per community
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Linee guida per la codifica {#coding-guidelines}

## Linee guida, suggerimenti {#guidelines-tips-and-tricks}

L’utilizzo di AEM Communities si è evoluto da una forte dipendenza dalle pagine Java Server a una flessibilità nella scelta di linguaggi di script basati su modelli in cui la logica di business, lo stile e il contenuto delle pagine sono distinti gli uni dagli altri.

Un’ulteriore flessibilità nell’utilizzo dei contenuti generati dagli utenti (UGC, User-Generated Content) è offerta dall’API SocialResourceProvider, che elimina la necessità di sapere quali [SRP](srp.md) è stata scelta l&#39;opzione per la distribuzione.

Di seguito sono riportate varie linee guida per la codifica e best practice per gli sviluppatori di AEM Communities:

### Codice {#code}

* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) : come evitare di scrivere un’applicazione che funziona solo quando UGC è memorizzato in JCR (JSRP).
* [Refactoring SocialUtils](socialutils.md) - metodi di utilità per SRP che sostituiscono SocialUtils.
* [Convenzioni di denominazione](naming-conventions.md) : convenzioni di denominazione per le classi Java personalizzate.

### Script {#scripts}

* [Sideload dei componenti community](sideloading.md) : come aggiungere in modo dinamico un componente dopo il caricamento della pagina.
* [Nozioni di base sull’editor Rich Text](rte.md) : come personalizzare l’interfaccia utente Rich Text fornita ai membri per la pubblicazione dei contenuti.

### IDE {#ide}

* [Utilizzo di Maven per le community](maven.md) : come includere il file jar dell’API Communities.
* [Refactoring SocialUtils](socialutils.md) - metodi di utilità per SRP che sostituiscono SocialUtils.
