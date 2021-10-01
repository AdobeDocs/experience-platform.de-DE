---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; API;
solution: Experience Platform
title: Erste Schritte mit der Segmentation Service-API
topic-legacy: developer guide
description: Die folgende Dokumentation enthält zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der Segmentation-API arbeiten zu können.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 50%

---

# Erste Schritte mit der Segmentation Service-API {#getting-started}

Mit Adobe Experience Platform [!DNL Segmentation Service] können Sie aus Ihren [!DNL Real-time Customer Profile]-Daten Segmente erstellen und Zielgruppen in Adobe Experience Platform generieren.

Das Entwicklerhandbuch setzt ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste voraus, die mit der Verwendung von [!DNL Segmentation Service] verbunden sind.

- [[!DNL Segmentation]](../home.md): Ermöglicht das Erstellen von Zielgruppensegmenten anhand von  [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der [!DNL Segmentation]-API arbeiten zu können.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation der [!DNL Segmentation Service]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abgeschlossen haben, um [!DNL Platform]-Endpunkte erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Für alle Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandboxes - Übersichtsdokumentation für Sandboxes](../../sandboxes/home.md).

## Nächste Schritte

Um Aufrufe mit der [!DNL Segmentation Service]-API durchzuführen, wählen Sie eine der verfügbaren Endpunkthandbücher entweder mithilfe der linken Navigation oder in der [Übersicht über das Entwicklerhandbuch](./overview.md) aus.
