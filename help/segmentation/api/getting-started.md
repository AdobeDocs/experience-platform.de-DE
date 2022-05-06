---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; API;
solution: Experience Platform
title: Erste Schritte mit der Segmentation Service-API
topic-legacy: developer guide
description: Die folgende Dokumentation enthält zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der Segmentation-API arbeiten zu können.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 47%

---

# Erste Schritte mit der Segmentation Service-API {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Zielgruppen in Adobe Experience Platform über Ihre [!DNL Real-time Customer Profile] Daten.

Das Entwicklerhandbuch setzt ein Verständnis der verschiedenen [!DNL Experience Platform] Dienste, die mit der Nutzung von [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Ermöglicht das Erstellen von Zielgruppensegmenten aus [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden. Um die Segmentierung optimal zu nutzen, stellen Sie bitte sicher, dass Ihre Daten als Profile und Ereignisse gemäß dem [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md).
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der [!DNL Segmentation] API.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation der [!DNL Segmentation Service]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Platform]-Endpunkte erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle Anfragen an [!DNL Platform] APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes finden Sie unter [!DNL Experience Platform], siehe [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Nächste Schritte

So führen Sie Aufrufe mit dem [!DNL Segmentation Service] -API eine der verfügbaren Endpunktleitfäden entweder über die linke Navigation oder innerhalb der [Übersicht über das Entwicklerhandbuch](./overview.md)
