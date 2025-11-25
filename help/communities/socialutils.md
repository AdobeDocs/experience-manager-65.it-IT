---
title: Refactoring SocialUtils
description: Il pacchetto com.adobe.cq.social.ugcbase.SocialUtils è stato dichiarato obsoleto in AEM 6.1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# Refactoring SocialUtils {#socialutils-refactoring}

## Pacchetto SocialUtils obsoleto {#socialutils-package-deprecated}

Il pacchetto `com.adobe.cq.social.ugcbase.SocialUtils` è obsoleto in AEM 6.1.

Nelle tabelle seguenti sono elencati i metodi da utilizzare al posto dei metodi `SocialUtils`.

## Pacchetto SocialResourceUtilities  {#socialresourceutilities-package}

| Metodi in com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities | Note |
|---|---|
| CheckPermission(ResourceResolver resolver, String path, String action) booleano |  |
| SocialResourceProvider getSocialResourceProvider(risorsa) |  |
| GetStorageConfig(Resource) di SocialResourceConfiguration |  |
| Risorsa getUGCResource(Resource userResource) |  |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rf) | novità |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rrf, String resourceTypeHint) | novità |
| Resource getUGCResource(Resource userResource, String resourceTypeHint) |  |
| booleano hasModeratePermissions(Risorsa) |  |
| Stringa resourceToACLPath(Risorsa) |  |
| Stringa resourceToUGCStoragePath(Resource) | sostituisce String resourceToUGCPath(Resource) |
| Stringa UGCToResourcePath(Risorsa) |  |
| Stringa UGCToResourcePath(Stringa ugcPath) | firma del metodo modificata |
| Stringa UGCToResourcePath(Stringa ugcPath, Risolutore ResourceResolver) | novità |

| Metodi in `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities | Note |
|---|---|
| SocialResourceProvider getSocialResourceProvider(risorsa) | sostituisce SocialResourceProvider getConfiguredProvider(risorsa risorsa) |

## Pacchetto SCFUtilities {#scfutilities-package}

| Metodi in `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| Stringa getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE) |
| Page getContainingPage(Resource resource) |
| Stringa getSocialProfileURL(nome utente stringa, risolutore ResourceResolver, pagina Pagina) |
| UserProperties getUserProperties(ResourceResolver resolver, String userId) |

## Solo per uso interno {#for-internal-use-only}

| booleano canAddNode(Session session, String path) |
|---|
| String createUniqueNameHint(String message) |
| String createUniqueNameHint(String message, int numRandomChars) |
| String generateRandomString(int length) |
| GetDefaultStorageConfig() di SocialResourceConfiguration |
| Page getPage(Percorso stringa, Risolutore risorse) |
| Stringa getPagePath(risorsa) |
| String getPagePath(String path) |
| String getResourceTypeForIncludedResource(componente Resource, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Resource, String styleProperty, String defaultValue) |
| booleano isResourceOwner(Resource resource) |
| Stringa mapUGCPath(Risorsa) |
| String mapUGCPath(String ugcPath, ResourceResolver resolver) |
| booleano mayPost(ResourceResolver resolver, risorsa Resource) |
| String preparationUserGeneratedContent(ResourceResolver resolver, percorso stringa) |

## Metodi non più disponibili {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, String path, String nodeType) |
|---|
| Resource getResourceAtPath(ResourceResolver resolver, percorso stringa) |
| Resource getResourceAtPath(ResourceResolver resolver, percorso stringa, tipo risorsa stringa) |
| Configurazione getStorageCloudServiceConfig(Resource) |
| Gestione traduzioni getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| valore booleano mayAccessUGC(ResourceResolver resolver) |
