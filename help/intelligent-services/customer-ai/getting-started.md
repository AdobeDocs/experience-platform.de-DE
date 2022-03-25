---
keywords: Experience Platform; Erste Schritte; Kundenunterstützung; beliebte Themen
solution: Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Erste Schritte mit Customer AI
topic-legacy: Getting started
description: In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 71%

---

# Erste Schritte in Customer AI

Die Anleitungen für Customer AI setzen ein grundlegendes Verständnis der verschiedenen Platform-Dienste voraus, die an der Verwendung von Customer AI beteiligt sind. Bevor Sie beginnen, lesen Sie bitte folgende Dokumente:

- [Übersicht über das Experience-Datenmodell (XDM)-System](../../xdm/home.md): XDM ist das grundlegende Framework, das Folgendes ermöglicht [!DNL Adobe Experience Cloud], unterstützt von Experience Platform, um genau zum richtigen Zeitpunkt die richtige Nachricht an die richtige Person auf dem richtigen Kanal zu senden. Das XDM-System ist die Methode, auf der Experience Platform basiert. Es stellt Experience-Datenmodell-Schemata zur Verwendung durch Platform-Dienste bereit.
- [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Dieses Dokument bietet eine Einführung in Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in verwendet werden sollen [!DNL Adobe Experience Platform].
- [Erstellen von Schemas](../../xdm/tutorials/create-schema-ui.md): In diesem Tutorial werden die Schritte zum Erstellen eines Schemas mit dem Schema Editor in Experience Platform beschrieben.
- [Übersicht über das Echtzeit-Kundenprofil](../../rtcdp/overview.md): Erstellt auf [!DNL Adobe Experience Platform], hilft Real-time Customer Data Platform (Echtzeit-Kundendatenplattform) Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile durch intelligente Entscheidungen auf der gesamten Journey zu aktivieren. Die Echtzeit-Kundendatenplattform fasst unterschiedliche Unternehmensdatenquellen zusammen, um in Echtzeit einheitliche Profile zu erstellen, die über alle Kanäle und Geräte hinweg ein personalisiertes Kundenerlebnis möglich machen.
- [Segmentation Service – Übersicht](../../segmentation/home.md): Bei Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die von einer Untergruppe von Profilen in Ihrem Profilspeicher geteilt werden, sodass Sie eine vermarktbare Gruppe von Personen aus Ihrem Kundenstamm ermitteln können. In einer E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Schuhe zu kaufen?“ wollen Sie möglicherweise eine Zielgruppe aller Anwender auswählen, die in den letzten 30 Tagen nach Laufschuhen gesucht haben, den Kauf jedoch nicht abgeschlossen haben. Mithilfe unterschiedlicher Segmente können Sie sich auf verschiedene Zielgruppen konzentrieren und so für ein besser angepasstes Marketing-Erlebnis sorgen.
- [Benutzerhandbuch zu Segment Builder](../../segmentation/tutorials/create-a-segment.md): Platform ermöglicht Ihnen das einfache Erstellen und Aufrufen von Segmenten sowie eine Verwendung verschiedener Bausteine zur weiteren Charakterisierung Ihrer Segmente.

## Herunterladen von Customer AI-Werten

>[!NOTE]
>
>Wenn Sie keine Rohdaten herunterladen müssen, können Sie diesen Schritt überspringen und mit dem [Konfigurationshandbuch](./user-guide/configure.md).

Das Herunterladen von Customer AI-Werten erfolgt über eine Kombination von API-Aufrufen. Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für Experience Platform.

## Nächste Schritte

Nachdem Sie die im obigen Dokument beschriebenen Schritte ausgeführt haben, besuchen Sie die [Eingabe und Ausgabe](./input-output.md) Dokumentation. In diesem Dokument erhalten Sie einen kurzen Überblick darüber, welche Datentypen in Customer AI verwendet und erstellt werden.
