---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API
title: Erste Schritte mit der Data Ingestion-API
type: Documentation
description: Im Erste-Schritte-Handbuch zur Datenerfassungs-API werden die wichtigsten Konzepte und grundlegenden Funktionen vorgestellt, die Sie kennen müssen, bevor Sie Daten mithilfe von APIs in die Experience Platform aufnehmen können.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 51%

---

# Erste Schritte mit der Data Ingestion-API {#getting-started}

Mithilfe von API-Endpunkten für die Datenaufnahme können Sie grundlegende CRUD-Vorgänge durchführen, um Daten in Adobe Experience Platform zu erfassen.

Die Verwendung der API-Handbücher setzt ein Verständnis der verschiedenen Adobe Experience Platform-Dienste voraus, die am Arbeiten mit Daten beteiligt sind. Bevor Sie die Data Ingestion-API verwenden, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [Batch-Erfassung](./overview.md): Erlaubt Ihnen das Erfassen von Daten in Adobe Experience Platform in Form von Batch-Dateien.
* [[!DNL Real-Time Customer Profile]](../home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten ordnet.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich Aufrufe an [!DNL Profile] API-Endpunkte.

## Lesen von Beispiel-API-Aufrufen

Die Dokumentation zur Datenerfassungs-API enthält Beispiel-API-Aufrufe, die zeigen, wie Anfragen richtig formatiert werden. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Platform]-Endpunkte erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte, die für jeden Aufruf spezifisch sind, werden in den Aufrufparametern angegeben.

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Anforderungen an [!DNL Platform] APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).
