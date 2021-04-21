---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: Erste Schritte mit der Echtzeit-Profil-API
topic-legacy: guide
type: Documentation
description: In der Anleitung zum Einstieg in die Profil-API werden die wichtigsten Konzepte und grundlegenden Funktionen erläutert, die Sie kennen müssen, um mit API-Endpunkten für Echtzeit-Kunden-Profile grundlegende CRUD-Vorgänge für Profil-Daten durchzuführen.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 20%

---

# Erste Schritte mit der [!DNL Real-time Customer Profile]-API {#getting-started}

Mithilfe von Echtzeit-API-Endpunkten für Kunden-Profil können Sie grundlegende CRUD-Vorgänge für Profil-Daten durchführen, z. B. die Konfiguration berechneter Attribute, den Zugriff auf Entitäten, den Export von Profil-Daten und das Löschen nicht benötigter Datensätze oder Stapel.

Die Verwendung des Entwicklerhandbuchs erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die mit [!DNL Profile]-Daten arbeiten. Bevor Sie mit der [!DNL Real-time Customer Profile]-API arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Real-time Customer Profile]](../home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Erhalten Sie eine bessere Ansicht Ihres Kundenverhaltens, indem Sie Identitäten zwischen verschiedenen Geräten und Systemen überbrücken.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um erfolgreich Aufrufe an [!DNL Profile]-API-Endpunkte durchzuführen.

## Lesen von Beispiel-API-Aufrufen

Die API-Dokumentation für [!DNL Real-time Customer Profile] enthält Beispiel-API-Aufrufe, die zeigen, wie Anforderungen korrekt formatiert werden. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Die API-Dokumentation erfordert auch, dass Sie das [Authentifizierungstraining](https://www.adobe.com/go/platform-api-authentication-en) abgeschlossen haben, um erfolgreich Aufrufe an [!DNL Platform]-Endpunkte durchzuführen. Wenn Sie das Authentifizierungstreutorial abschließen, werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Anforderungen an [!DNL Platform]-APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte, die für jeden Aufruf spezifisch sind, werden in den Aufrufparametern angegeben.

## Nächste Schritte

Um mit dem Aufrufen der API zu beginnen, wählen Sie eine der verfügbaren Endpunktleitfäden aus.[!DNL Real-time Customer Profile]
