---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: Erste Schritte mit der Echtzeit-Kundenprofil-API
type: Documentation
description: In den ersten Schritten der Profil-API werden die wichtigsten Konzepte und grundlegenden Funktionen beschrieben, die Sie kennen müssen, um mit API-Endpunkten für Echtzeit-Kundenprofil grundlegende CRUD-Vorgänge für Profildaten durchführen zu können.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 53%

---

# Erste Schritte mit der [!DNL Real-Time Customer Profile]-API {#getting-started}

Mithilfe der API-Endpunkte für das Echtzeit-Kundenprofil können Sie grundlegende CRUD-Vorgänge für Profildaten durchführen, z. B. die Konfiguration berechneter Attribute, den Zugriff auf Entitäten, den Export von Profildaten und das Löschen nicht benötigter Datensätze oder Batches.

Die Verwendung des Entwicklerhandbuchs setzt ein Verständnis der verschiedenen Adobe Experience Platform-Dienste voraus, die an der Arbeit mit [!DNL Profile] Daten. Bevor Sie die [!DNL Real-Time Customer Profile]-API nutzen, lesen Sie die Dokumentation für folgende Services:

* [[!DNL Real-Time Customer Profile]](../home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Verschaffen Sie sich einen besseren Überblick über Ihren Kunden und sein Verhalten, indem Sie Identitäten zwischen Geräten und Systemen überbrücken.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Ermöglicht das Erstellen von Zielgruppensegmenten aus Echtzeit-Kundenprofildaten.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten ordnet.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich Aufrufe an [!DNL Profile] API-Endpunkte.

## Lesen von Beispiel-API-Aufrufen

Die [!DNL Real-Time Customer Profile] Die API-Dokumentation enthält Beispiel-API-Aufrufe, die zeigen, wie Anfragen korrekt formatiert werden. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Platform]-Endpunkte erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Anforderungen an [!DNL Platform] APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte, die für jeden Aufruf spezifisch sind, werden in den Aufrufparametern angegeben.

## Nächste Schritte

Um mit dem Aufrufen der [!DNL Real-Time Customer Profile]-API zu beginnen, wählen Sie eines der verfügbaren Handbücher zu Endpunkten.
