---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: Erste Schritte mit der Datenaufnahme-API
type: Documentation
description: In den ersten Schritten mit der Datenaufnahme-API werden die wichtigsten Konzepte und grundlegenden Funktionen beschrieben, die Sie kennen sollten, bevor Sie mit der Aufnahme von Daten in Experience Platform mithilfe von APIs beginnen können.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 50%

---

# Erste Schritte mit der Datenaufnahme-API {#getting-started}

Mithilfe von API-Endpunkten für die Datenaufnahme können Sie grundlegende CRUD-Vorgänge durchführen, um Daten in Adobe Experience Platform aufzunehmen.

Die Verwendung der -API-Handbücher setzt ein grundlegendes Verständnis mehrerer Adobe Experience Platform-Services voraus, die an der Arbeit mit -Daten beteiligt sind. Bevor Sie die Datenaufnahme-API verwenden, lesen Sie die Dokumentation für die folgenden Services:

* [Batch-Erfassung](./overview.md): Erlaubt Ihnen das Erfassen von Daten in Adobe Experience Platform in Form von Batch-Dateien.
* [[!DNL Real-Time Customer Profile]](../home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von Platform organisiert werden.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Profile] API-Endpunkte erfolgreich aufrufen zu können.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation zur Datenaufnahme-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Platform]-Endpunkte erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte, die für jeden Aufruf spezifisch sind, werden in den Aufrufparametern angegeben.

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Anfragen an [!DNL Platform]-APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).
