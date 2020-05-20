---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Erste Schritte mit der Kunden-API
topic: Getting started
translation-type: tm+mt
source-git-commit: f7c59ef097c00073fbf9f6522b6e70ed24cc8bf1
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 15%

---


# Erste Schritte mit der Kunden-API

Die Leitfäden für die Kundentechnik erfordern ein Verständnis der verschiedenen Plattformdienste, die bei der Verwendung der Kundentechnik erforderlich sind. Bevor Sie den Beginn ausführen, lesen Sie bitte die folgenden Dokumente:

- [Systemübersicht](../../xdm/home.md)zum Erlebnis-Datenmodell (XDM): XDM ist das grundlegende Framework, mit dem Adobe Experience Cloud, powered by Experience Platform, die richtige Botschaft an die richtige Person im richtigen Kanal und genau zum richtigen Zeitpunkt senden kann. Die Methode, auf der Experience Platform aufgebaut ist, XDM-System, operalisiert Experience Data Model-Schema für die Verwendung durch Plattformdienste.
- [Grundlagen der Zusammensetzung](../../xdm/schema/composition.md)des Schemas: Dieses Dokument bietet eine Einführung in Experience Data Model-(XDM-)Schema und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in Adobe Experience Platform verwendet werden sollen.
- [Erstellen von Schemas](../../xdm/tutorials/create-schema-ui.md): In diesem Lernprogramm werden die Schritte zum Erstellen eines Schemas mit dem Schema-Editor in Experience Platform beschrieben.
- [Überblick über](../../rtcdp/overview.md)das Echtzeit-Profil von Kunden: Die auf der Adobe Experience Platform aufbauende Adobe Echtzeit-Kundendatenplattform (Echtzeit-CDP) hilft Firmen, bekannte und unbekannte Daten zusammenzuführen, um Profil während der gesamten Customer Journey mit intelligenten Entscheidungen zu aktivieren. Die Echtzeit-Kundendatenplattform fasst unterschiedliche Unternehmensdatenquellen zusammen, um in Echtzeit einheitliche Profile zu erstellen, die über alle Kanäle und Geräte hinweg ein personalisiertes Kundenerlebnis möglich machen.
- [Übersicht über](../../segmentation/home.md)den Segmentierungsdienst: Bei der Segmentierung werden bestimmte Attribute oder Verhaltensweisen definiert, die von einer Untergruppe von Profilen aus Ihrem Profil-Store gemeinsam verwendet werden, um eine vermarktbare Personengruppe von Ihrer Kundenbasis zu unterscheiden. In einer E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Schuhe zu kaufen?“ wollen Sie möglicherweise eine Zielgruppe aller Anwender auswählen, die in den letzten 30 Tagen nach Laufschuhen gesucht haben, den Kauf jedoch nicht abgeschlossen haben. Mithilfe unterschiedlicher Segmente können Sie sich auf verschiedene Zielgruppen konzentrieren und so für ein besser angepasstes Marketing-Erlebnis sorgen.
- [Segment Builder-Benutzerhandbuch](../../segmentation/tutorials/create-a-segment.md): Plattform ermöglicht Ihnen das einfache Erstellen und Zugreifen auf Segmente sowie die Verwendung verschiedener Bausteine zur weiteren Charakterisierung Ihrer Segmente.

## Herunterladen von Kunden-AI-Ergebnissen

>[!NOTE] Wenn Sie keine Rohdaten herunterladen müssen, können Sie diesen Schritt überspringen und zum [Konfigurationshandbuch](./user-guide/configure.md)fortfahren.

Das Herunterladen von Kunden-AI-Ergebnissen erfolgt über eine Kombination von API-Aufrufen. Um Aufrufe an Plattform-APIs durchführen zu können, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für Experience Platform.

## Nächste Schritte

Nachdem Sie die im obigen Dokument beschriebenen Schritte ausgeführt haben, lesen Sie die Dokumentation zu [Eingabe und Ausgabe](./input-output.md) . In diesem Dokument erhalten Sie einen kurzen Überblick darüber, welche Datentypen in der Kundentechnik verwendet und produziert werden.