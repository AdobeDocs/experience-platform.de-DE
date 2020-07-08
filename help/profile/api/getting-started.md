---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Erste Schritte mit der Echtzeit-Profil-API
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Erste Schritte mit der Echtzeit-Profil-API {#getting-started}

Mithilfe der Echtzeit-Client-Profil-API können Sie grundlegende CRUD-Vorgänge für Profil-Ressourcen durchführen, z. B. die Konfiguration berechneter Attribute, den Zugriff auf Entitäten, den Export von Profil-Daten und das Löschen nicht benötigter Datensätze oder Stapel.

Die Verwendung des Entwicklerhandbuchs erfordert ein Verständnis der verschiedenen Adobe Experience Platformen, die mit der Arbeit mit Profil-Daten verbunden sind. Bevor Sie mit der Echtzeit-Client-Profil-API arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [Echtzeit-Profil](../home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Identitätsdienst](../../identity-service/home.md)der Adobe Experience Platform: Erhalten Sie eine bessere Ansicht Ihres Kundenverhaltens, indem Sie Identitäten zwischen verschiedenen Geräten und Systemen überbrücken.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
* [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
* [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um Profil-API-Endpunkte erfolgreich aufrufen zu können.

## Lesen von Beispiel-API-Aufrufen

Die Dokumentation zur Echtzeit-Client-Profil-API enthält Beispiele für API-Aufrufe, die zeigen, wie Anforderungen korrekt formatiert werden. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

## Erforderliche Kopfzeilen

Die API-Dokumentation erfordert auch, dass Sie das [Authentifizierungstraining](../../tutorials/authentication.md) abgeschlossen haben, um Platform-Endpunkte erfolgreich aufzurufen. Wenn Sie das Authentifizierungstraining abschließen, werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform API-Aufrufen bereitgestellt, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Anforderungen an Platform-APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* x-sandbox-name: `{SANDBOX_NAME}`

Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Alle Anforderungen mit einer Nutzlast im Anforderungstext (wie POST-, PUT- und PATCH-Aufrufe) müssen einen `Content-Type` Header enthalten. Akzeptierte Werte, die für jeden Aufruf spezifisch sind, werden in den Aufrufparametern bereitgestellt.

## Nächste Schritte

Um mit dem Aufrufen mit der Echtzeit-Customer Profil API zu beginnen, wählen Sie eine der verfügbaren Endpunktleitfäden aus.