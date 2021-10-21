---
keywords: Experience Platform;home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;API
solution: Experience Platform
title: Erste Schritte mit der Segmentierungsservice-API
topic-legacy: developer guide
description: Die folgende Dokumentation enthält zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der Segmentierungs-API arbeiten zu können.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 47%

---

# Erste Schritte mit der Segmentierungsservice-API {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] ermöglicht es Ihnen, Segmente zu erstellen und Audiencen in Adobe Experience Platform aus Ihrem [!DNL Real-time Customer Profile] Daten.

Das Entwicklerleitfaden erfordert ein Verständnis der verschiedenen [!DNL Experience Platform] Dienste, die [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Ermöglicht es Ihnen, Audiencen-Segmente zu erstellen von [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profil und Ereignis gemäß der [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md).
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um erfolgreich mit der [!DNL Segmentation] API.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation der [!DNL Segmentation Service]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abgeschlossen haben, um [!DNL Platform]-Endpunkte erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang stattfinden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxen in [!DNL Experience Platform], siehe [Sandboxübersicht](../../sandboxes/home.md).

## Nächste Schritte

Um Anrufe mit [!DNL Segmentation Service] API, wählen Sie eine der verfügbaren Endpunkt-Hilfslinien entweder mithilfe der linken Navigation oder innerhalb der [Entwicklerleitfaden - Übersicht](./overview.md)
