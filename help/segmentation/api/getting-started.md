---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierung;Segmentierung;Segmentierungs-Service;API;
solution: Experience Platform
title: Erste Schritte mit der Segmentierungs-Service-API
description: Die folgende Dokumentation enthält zusätzliche Informationen, die Sie für eine erfolgreiche Arbeit mit der Segmentierungs-API benötigen.
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 62%

---

# Erste Schritte mit der Segmentierungs-Service-API {#getting-started}

Mit Adobe Experience Platform [!DNL Segmentation Service] können Sie Zielgruppen über Segmentdefinitionen oder andere Quellen in Adobe Experience Platform aus Ihren [!DNL Real-Time Customer Profile] erstellen.

Das Entwicklerhandbuch setzt Grundkenntnisse der verschiedenen [!DNL Experience Platform]-Services voraus, die mit der Verwendung von [!DNL Segmentation Service] zusammenhängen.

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht das Erstellen von Zielgruppen aus [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten durch [!DNL Experience Platform] organisiert werden. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der [!DNL Segmentation]-API erfolgreich arbeiten zu können.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation der [!DNL Segmentation Service]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Experience Platform]-Endpunkte erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle an [!DNL Experience Platform]-APIs gerichtete Anfragen müssen über eine Kopfzeile verfügen, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Nächste Schritte

Um Aufrufe mit der [!DNL Segmentation Service]-API durchzuführen, wählen Sie entweder über die linke Navigation oder im [Entwicklerhandbuch - Übersicht“ eines der verfügbaren Handbücher zu Endpunkten ](./overview.md)
