---
keywords: Experience Platform;Erste Schritte;Kunden-KI;beliebte Themen
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Erste Schritte in Kunden-KI
description: In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 58%

---

# Erste Schritte in Customer AI

Die Anleitungen für Customer AI setzen ein grundlegendes Verständnis der verschiedenen Platform-Dienste voraus, die an der Verwendung von Customer AI beteiligt sind. Bevor Sie beginnen, lesen Sie bitte folgende Dokumente:

- [Experience-Datenmodell (XDM) - Systemübersicht](../../xdm/home.md): XDM ist das grundlegende Framework, mit dem [!DNL Adobe Experience Cloud] auf Basis von Experience Platform die richtige Botschaft zur richtigen Zeit an die richtige Person auf dem richtigen Kanal senden kann. Das XDM-System ist die Methode, auf der Experience Platform basiert. Es stellt Experience-Datenmodell-Schemata zur Verwendung durch Platform-Dienste bereit.
- [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Dieses Dokument bietet eine Einführung in Experience-Datenmodell(XDM)-Schemata und die Bausteine, Prinzipien und Best Practices zum Erstellen von Schemata, die in [!DNL Adobe Experience Platform] verwendet werden können.
- [Erstellen von Schemata](../../xdm/tutorials/create-schema-ui.md): In diesem Tutorial werden die Schritte zum Erstellen eines Schemas mit dem Schema Editor in Experience Platform beschrieben.
- [Übersicht über das Echtzeit-Kundenprofil](../../rtcdp/overview.md): Adobe Real-time Customer Data Platform (Real-Time CDP) unterstützt Unternehmen dabei, auf [!DNL Adobe Experience Platform] aufbauend bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile mit intelligenten Entscheidungen auf der gesamten Kunden-Journey zu aktivieren. Real-Time CDP kombiniert mehrere Unternehmensdatenquellen, um in Echtzeit einheitliche Profile zu erstellen, mit denen eine personalisierte Eins-zu-eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitgestellt werden kann.
- [Segmentierungs-Service - Überblick](../../segmentation/home.md) Bei der Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die von einer Untergruppe von Profilen in Ihrem Profilspeicher geteilt werden, um eine vermarktbare Personengruppe in Ihrem Kundenstamm zu unterscheiden. In einer E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Schuhe zu kaufen?“ wollen Sie möglicherweise eine Zielgruppe aller Anwender auswählen, die in den letzten 30 Tagen nach Laufschuhen gesucht haben, den Kauf jedoch nicht abgeschlossen haben. Mithilfe unterschiedlicher Segmente können Sie sich auf verschiedene Zielgruppen konzentrieren und so für ein besser angepasstes Marketing-Erlebnis sorgen.
- [Benutzerhandbuch zu Segment Builder](../../segmentation/tutorials/create-a-segment.md): Platform ermöglicht Ihnen das einfache Erstellen und Aufrufen von Segmenten sowie eine Verwendung verschiedener Bausteine zur weiteren Charakterisierung Ihrer Segmente.

## Herunterladen von Customer AI-Werten

>[!NOTE]
>
>Wenn Sie die Rohdaten der Scores nicht herunterladen müssen, können Sie diesen Schritt überspringen und mit dem [Konfigurationshandbuch](./user-guide/configure.md) fortfahren.

Das Herunterladen von Customer AI-Werten erfolgt über eine Kombination von API-Aufrufen. Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für Experience Platform.

## Nächste Schritte

Nachdem Sie die im obigen Dokument beschriebenen Schritte ausgeführt haben, konsultieren Sie die [Eingabe und Ausgabe](./data-requirements.md)-Dokumentation. Dieses Dokument gibt einen kurzen Überblick darüber, welche Datentypen in Kunden-KI verwendet und produziert werden.
