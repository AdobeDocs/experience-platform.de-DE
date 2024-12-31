---
solution: Experience Platform
title: Erste Schritte mit der API für einheitliche Tags
description: Die folgende Dokumentation enthält zusätzliche Informationen, die Sie für eine erfolgreiche Arbeit mit der Unified Tags-API benötigen.
role: Developer
exl-id: 8f33707f-b46d-4054-802c-9e42ecabd9ba
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 44%

---

# Erste Schritte mit der API für einheitliche Tags {#getting-started}

Mit der Unified Tags-API können Sie Ihre Geschäftsobjekte in Adobe Experience Platform kategorisieren und verwalten.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der Unified Tags-API erfolgreich arbeiten zu können.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation zur API für einheitliche Tags wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie [ Abschnitt zum Lesen von Beispiel](../../landing/troubleshooting.md#how-do-i-format-an-api-request)API-Aufrufen im Handbuch zur Fehlerbehebung bei Experience Platform.

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um Platform-Endpunkte erfolgreich aufrufen zu können. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle an [!DNL Platform]-APIs gerichtete Anfragen müssen über eine Kopfzeile verfügen, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Nächste Schritte

Um Aufrufe mit der Unified Tags-API durchzuführen, wählen Sie eines der verfügbaren Handbücher zu Endpunkten entweder über die linke Navigationsleiste oder im [Entwicklerhandbuch - Übersicht](./overview.md)
