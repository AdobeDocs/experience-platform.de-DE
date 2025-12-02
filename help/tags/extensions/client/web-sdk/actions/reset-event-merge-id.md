---
title: Zusammenführungs-ID zurücksetzen
description: Veraltete Aktion, mit der Sie Ereignisse trennen können, die auf derselben Seite aufgerufen werden.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Zusammenführungs-ID zurücksetzen

>[!IMPORTANT]
>
>Diese Aktion ist veraltet. Verwenden Sie stattdessen [Einstellungen Interne Link-Klicks erfassen](../configure/data-collection.md#collect-internal-link-clicks).

Mit dem Aktionstyp **[!UICONTROL Reset merge ID]** können Sie Ereignisse trennen, die auf derselben Seite aufgerufen werden. Sie wird in der Regel in Szenarien mit internen Links verwendet, in denen möglicherweise mehrere Payloads vorhanden sind, die an Adobe gesendet werden sollen. Mit dieser Aktion können Sie die Zusammenführungs-ID eines Ereignisses zurücksetzen, sodass sie nach dem Eintreffen in der Edge Network nicht als Teil desselben Ereignisses betrachtet werden.

Wenn Sie steuern möchten, wie mehrere Ereignisse auf derselben Seite getrennt oder zusammengeführt werden, verwenden Sie die Option [Interne Link-Klicks erfassen](../configure/data-collection.md#collect-internal-link-clicks) beim Konfigurieren der Tag-Erweiterung.
