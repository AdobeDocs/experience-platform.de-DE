---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für die DUL Policy Service API
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---


# Entwicklerhandbuch für die DUL Policy Service API

Die Datenbenennung und -durchsetzung (DULE) ist der Kernmechanismus der Datenverwaltung in der Adobe Experience Platform. Der DULE Policy Service stellt eine RESTful-API bereit, mit der Sie Datenverwendungsrichtlinien erstellen und verwalten können, um festzustellen, welche Marketingaktionen für Daten durchgeführt werden können, die mit bestimmten Datenverwendungsbezeichnungen gekennzeichnet wurden.

Dieses Dokument enthält Anweisungen zum Ausführen der Schlüsselvorgänge, die in der Policy Service-API verfügbar sind. Wenn Sie dies noch nicht getan haben, überprüfen Sie zunächst den Überblick über die [Datenverwaltung](../home.md) , um sich mit dem DULE-Framework vertraut zu machen. Eine schrittweise Anleitung zum Erstellen und Erzwingen von DULE-Richtlinien finden Sie im [DUL-Richtlinientutorial](../policies/create.md).

In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die Policy Service API durchführen.

## Erste Schritte mit dem DUL Policy Service

Bevor Sie mit der Arbeit mit dem Policy-Dienst beginnen, müssen für die Daten in Experience Platform geeignete DULE-Beschriftungen angewendet werden. Eine vollständige Anleitung zum Anwenden von Bezeichnungen für die Datenverwendung auf Datensätze und Felder finden Sie im Benutzerhandbuch [für die](../labels/user-guide.md)DULE-Bezeichnungen.

## Voraussetzungen

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Datenverwaltung](../home.md): Das Framework, mit dem Experience Platform die Einhaltung der Datenverwendungskonformität erzwingt.
   * [DULE-Beschriftungen](../labels/overview.md): Datenverwendungsbeschriftungen werden auf Erlebnisdatenmodell-Datenfelder (XDM) angewendet und geben Einschränkungen für den Zugriff auf diese Daten an.
* [Erlebnis-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

## Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen, die zur Datenverwaltung gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

* Content-Type: application/json

## Core- und benutzerdefinierte Ressourcen

Innerhalb der Policy Service-API werden alle Richtlinien und Marketingaktionen als entweder `core` oder `custom` Ressourcen bezeichnet.

Die `core` Ressourcen werden von Adobe definiert und gepflegt, während `custom` Ressourcen von einzelnen Kunden erstellt und gepflegt werden und daher nur für die IMS-Organisation sichtbar sind, die sie erstellt hat. Somit sind Auflisten- und Suchvorgänge (`GET`) die einzigen Vorgänge, die für `core` Ressourcen zulässig sind, während Auflisten-, Such- und Aktualisierungsvorgänge (`POST`, `PUT`, `PATCH`und `DELETE`) für `custom` Ressourcen verfügbar sind.

## Politikstatus

Datenverwendungsrichtlinien können einen von drei möglichen Status haben: `DRAFT`, `ENABLED`oder `DISABLED`.

Standardmäßig werden nur &quot;AKTIVIERTE&quot;Richtlinien an der Richtlinienbewertung beteiligt.

&quot;ENTWURF&quot;-Richtlinien können auch bei der Politikbewertung berücksichtigt werden, allerdings nur durch Festlegung des Abfrage-Parameters `?includeDraft=true`. Weitere Informationen über die Bewertung der Politik finden Sie im Dokument über die [Durchsetzung](../enforcement/overview.md) der Politik am Ende dieses Dokuments.

## Marketingaktionsstiteln {#marketing-actions}

Marketingaktionsnamen sind eindeutige Bezeichner für Marketingaktionen. Jede `core` Marketingaktion hat einen eindeutigen Namen, der für alle IMS-Orgs gilt. Diese Namen werden von Adobe definiert und verwaltet. In der Zwischenzeit sind alle kundenspezifischen Marketingaktionen (`custom` Ressourcen) innerhalb Ihres Unternehmens eindeutig und nicht sichtbar oder mit anderen IMS-Orgs freigegeben.

Die Schritte zum Arbeiten mit Marketingaktionen in der Policy-Service-API werden im Abschnitt [Marketingaktionen](#marketing-actions) weiter unten in diesem Dokument beschrieben.

## Nächste Schritte

Nachdem Sie über die erforderlichen Kenntnisse und Berechtigungen verfügen, können Sie die in diesem Entwicklerhandbuch bereitgestellten Muster-API-Aufrufe weiter lesen:

* [Marketingaktionen](marketing-actions.md)
* [Richtlinien](policies.md)