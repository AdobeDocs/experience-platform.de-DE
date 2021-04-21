---
keywords: Experience Platform;Home;beliebte Themen;DULE;Modul
solution: Experience Platform
title: Erste Schritte mit der Policy Service API
topic-legacy: developer guide
description: Mit der Policy Service API können Sie verschiedene Ressourcen im Zusammenhang mit der Adobe Experience Platform-Datenverwaltung erstellen und verwalten. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die Policy Service-API durchführen.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 28%

---

# Erste Schritte mit der API[!DNL Policy Service]

Mit der API [!DNL Policy Service] können Sie verschiedene Ressourcen im Zusammenhang mit Adobe Experience Platform [!DNL Data Governance] erstellen und verwalten. Dieses Dokument bietet eine Einführung in die Kernkonzepte, die Sie kennen müssen, bevor Sie Aufrufe an die [!DNL Policy Service]-API durchführen.

## Voraussetzungen

Die Verwendung des Entwicklerhandbuchs erfordert ein grundlegendes Verständnis der verschiedenen [!DNL Experience Platform]-Dienste, die mit der Arbeit mit Data Governance-Funktionen verbunden sind. Bevor Sie mit der Arbeit mit [!DNL Policy Service API] beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Data Governance]](../home.md): Das Framework, mit dem die Einhaltung der Datenverwendung  [!DNL Experience Platform] erzwungen wird.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

## Lesen von Beispiel-API-Aufrufen

Die [!DNL Policy Service]-API-Dokumentation enthält Beispiel-API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Die API-Dokumentation erfordert auch, dass Sie das [Authentifizierungstraining](https://www.adobe.com/go/platform-api-authentication-en) abgeschlossen haben, um erfolgreich Aufrufe an [!DNL Platform]-Endpunkte durchzuführen. Wenn Sie das Authentifizierungstreutorial abschließen, werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Data Governance] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

## Kernressourcen und benutzerdefinierte Ressourcen

Innerhalb der API [!DNL Policy Service] werden alle Richtlinien und Marketingaktionen als `core`- oder `custom`-Ressourcen bezeichnet.

`core` Ressourcen sind die von der Adobe definierten und verwalteten Ressourcen, während  `custom` Ressourcen von Ihrer Organisation erstellt und verwaltet werden und daher einmalig und nur für Ihre IMS-Organisation sichtbar sind. Darum sind Auflistungs- und Nachschlagevorgänge (`GET`) die einzigen Vorgänge, die bei `core`-Ressourcen zulässig sind, während bei `custom`-Ressourcen Auflistungs-, Nachschlage- und Aktualisierungsvorgänge (`POST`, `PUT`, `PATCH` und `DELETE`) verfügbar sind.

## Nächste Schritte

Um mit dem Aufrufen der Policy Service API zu beginnen, wählen Sie eine der verfügbaren Endpunktleitfäden aus.
