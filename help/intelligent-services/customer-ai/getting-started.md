---
keywords: Experience Platform; Erste Schritte; Kundenunterstützung; beliebte Themen
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Erste Schritte mit Customer AI
description: In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 58%

---

# Erste Schritte in Customer AI

Die Anleitungen für Customer AI setzen ein grundlegendes Verständnis der verschiedenen Platform-Dienste voraus, die an der Verwendung von Customer AI beteiligt sind. Bevor Sie beginnen, lesen Sie bitte folgende Dokumente:

- [Übersicht über das Experience-Datenmodell (XDM)-System](../../xdm/home.md): XDM ist das grundlegende Framework, das Folgendes ermöglicht [!DNL Adobe Experience Cloud], unterstützt von Experience Platform, um genau zum richtigen Zeitpunkt die richtige Nachricht an die richtige Person auf dem richtigen Kanal zu senden. Das XDM-System ist die Methode, auf der Experience Platform basiert. Es stellt Experience-Datenmodell-Schemata zur Verwendung durch Platform-Dienste bereit.
- [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Dieses Dokument bietet eine Einführung in Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in verwendet werden sollen [!DNL Adobe Experience Platform].
- [Erstellen von Schemas](../../xdm/tutorials/create-schema-ui.md): In diesem Tutorial werden die Schritte zum Erstellen eines Schemas mit dem Schema Editor in Experience Platform beschrieben.
- [Übersicht über das Echtzeit-Kundenprofil](../../rtcdp/overview.md): Erstellt auf [!DNL Adobe Experience Platform], Adobe Real-time Customer Data Platform (Real-Time CDP) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile durch intelligente Entscheidungen auf der gesamten Journey zu aktivieren. Real-Time CDP kombiniert mehrere Unternehmensdatenquellen, um in Echtzeit einheitliche Profile zu erstellen, die über alle Kanäle und Geräte hinweg personalisierte Kundenerlebnisse bieten.
- [Segmentation Service – Übersicht](../../segmentation/home.md): Bei Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die von einer Untergruppe von Profilen in Ihrem Profilspeicher geteilt werden, sodass Sie eine vermarktbare Gruppe von Personen aus Ihrem Kundenstamm ermitteln können. In einer E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Schuhe zu kaufen?“ wollen Sie möglicherweise eine Zielgruppe aller Anwender auswählen, die in den letzten 30 Tagen nach Laufschuhen gesucht haben, den Kauf jedoch nicht abgeschlossen haben. Mithilfe unterschiedlicher Segmente können Sie sich auf verschiedene Zielgruppen konzentrieren und so für ein besser angepasstes Marketing-Erlebnis sorgen.
- [Benutzerhandbuch zu Segment Builder](../../segmentation/tutorials/create-a-segment.md): Platform ermöglicht Ihnen das einfache Erstellen und Aufrufen von Segmenten sowie eine Verwendung verschiedener Bausteine zur weiteren Charakterisierung Ihrer Segmente.

## Herunterladen von Customer AI-Werten

>[!NOTE]
>
>Wenn Sie keine Rohdaten herunterladen müssen, können Sie diesen Schritt überspringen und mit dem [Konfigurationshandbuch](./user-guide/configure.md).

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

## Zugangssteuerung {#access-control}

Bei Verwendung der Zugriffssteuerung muss die **Anzeigen von Customer AI** und **Customer AI verwalten** -Berechtigungen gewähren Zugriff auf verschiedene Funktionen von Customer AI. Die **Customer AI verwalten** -Berechtigung **erstellen**,**update**, **delete**, **enable** oder **disable** eine Instanz während **Anzeigen von Customer AI** Sie können sie lesen oder anzeigen. Die **erstellen**, **update** und **delete** -Aktionen werden in Auditprotokollen aufgezeichnet.

Weitere Informationen finden Sie in der Dokumentation . [Zuweisen von Berechtigungen für die Zugriffskontrolle](../../../help/access-control/home.md) oder wie [Verwenden Sie Auditprotokolle zur Überwachung von Zugriff und Aktivität.](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Nächste Schritte

Nachdem Sie die im obigen Dokument beschriebenen Schritte ausgeführt haben, besuchen Sie die [Eingabe und Ausgabe](./input-output.md) Dokumentation. In diesem Dokument erhalten Sie einen kurzen Überblick darüber, welche Datentypen in Customer AI verwendet und erstellt werden.
