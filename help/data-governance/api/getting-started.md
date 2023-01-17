---
keywords: Experience Platform;Startseite;beliebte Themen;DULE;dule
solution: Experience Platform
title: Erste Schritte mit der Richtlinien-Service-API
description: Mit der Policy Service-API können Sie verschiedene Ressourcen im Zusammenhang mit der Data Governance von Adobe Experience Platform erstellen und verwalten. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die Policy Service-API durchführen.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: ht
source-wordcount: '444'
ht-degree: 100%

---

# Erste Schritte mit der [!DNL Policy Service]-API

Mit der [!DNL Policy Service]-API können Sie verschiedene Ressourcen im Zusammenhang mit Data Governance von Adobe Experience Platform erstellen und verwalten. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die [!DNL Policy Service]-API durchführen.

## Voraussetzungen

Die Verwendung des Entwicklerhandbuchs erfordert ein grundlegendes Verständnis der verschiedenen [!DNL Experience Platform]-Services, die bei der Arbeit mit Data Governance-Funktionen zum Einsatz kommen. Bevor Sie [!DNL Policy Service API] nutzen, lesen Sie die Dokumentation für folgende Services:

* [Data Governance](../home.md): Das Framework, mit dem [!DNL Experience Platform] die Einhaltung der Datennutzungsrichtlinien umsetzt.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation der [!DNL Policy Service]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abgeschlossen haben, um [!DNL Platform]-Endpunkte erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu Data Governance gehören, sind in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

## Kernressourcen und benutzerdefinierte Ressourcen

Innerhalb der [!DNL Policy Service]-API werden alle Richtlinien und Marketing-Aktionen entweder als `core`- oder als `custom`-Ressourcen bezeichnet.

`core`-Ressourcen sind die von Adobe definierten und verwalteten Ressourcen, während `custom`-Ressourcen von Ihrer Organisation erstellt und verwaltet werden und daher einzigartig und nur für Ihre IMS-Organisation sichtbar sind. Darum sind Auflistungs- und Nachschlagevorgänge (`GET`) die einzigen Vorgänge, die bei `core`-Ressourcen zulässig sind, während bei `custom`-Ressourcen Auflistungs-, Nachschlage- und Aktualisierungsvorgänge (`POST`, `PUT`, `PATCH` und `DELETE`) verfügbar sind.

## Nächste Schritte

Um mit dem Aufrufen der Richtlinien-Service-API zu beginnen, wählen Sie eines der verfügbaren Handbücher zu Endpunkten.
