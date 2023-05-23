---
title: Refactoring SocialUtils
seo-title: SocialUtils Refactoring
description: Il pacchetto com.adobe.cq.social.ugcbase.SocialUtils è stato dichiarato obsoleto in AEM 6.1
seo-description: The package com.adobe.cq.social.ugcbase.SocialUtils was deprecated in AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---

# Refactoring SocialUtils {#socialutils-refactoring}

## Pacchetto SocialUtils obsoleto {#socialutils-package-deprecated}

Il pacchetto `com.adobe.cq.social.ugcbase.SocialUtils` è stato dichiarato obsoleto nell’AEM 6.1.

Nelle tabelle seguenti sono elencati i metodi da utilizzare al posto di `SocialUtils` metodi.

## Pacchetto SocialResourceUtilities  {#socialresourceutilities-package}

| Metodi in com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
| CheckPermission(ResourceResolver resolver, String path, String action) booleano |  |
| SocialResourceProvider getSocialResourceProvider(risorsa) |  |
| GetStorageConfig(Resource) di SocialResourceConfiguration |  |
| Risorsa getUGCResource(Resource userResource) |  |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rf) | nuovo |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rrf, String resourceTypeHint) | nuovo |
| Resource getUGCResource(Resource userResource, String resourceTypeHint) |  |
| booleano hasModeratePermissions(Risorsa) |  |
| Stringa resourceToACLPath(Risorsa) |  |
| Stringa resourceToUGCStoragePath(Resource) | sostituisce String resourceToUGCPath(Resource) |
| Stringa UGCToResourcePath(Risorsa) |  |
| Stringa UGCToResourcePath(Stringa ugcPath) | firma del metodo modificata |
| Stringa UGCToResourcePath(Stringa ugcPath, Risolutore ResourceResolver) | nuovo |

| Metodi in `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
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
