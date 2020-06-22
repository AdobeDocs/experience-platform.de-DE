---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Datenverwendungsrichtlinien
topic: policies
translation-type: tm+mt
source-git-commit: 92092620a7ba9129eef4bde852b1e0afc6612d74
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 1%

---


# Übersicht über die Datenverwendungsrichtlinien

Damit Datenverwendungsbeschriftungen die Datenkonformität effektiv unterstützen können, müssen Datenverwendungsrichtlinien implementiert werden. Datenverwendungsrichtlinien sind Regeln, die die Arten von Marketingaktionen beschreiben, von denen Sie Daten innerhalb der Experience Platform ausführen dürfen oder von denen Sie eingeschränkt sind.

Dieses Dokument bietet einen allgemeinen Überblick über die Richtlinien zur Datenverwendung und enthält Links zu weiteren Dokumentationen zum Arbeiten mit Richtlinien in der Benutzeroberfläche oder API.

## Marketingaktionen {#marketing-actions}

**Marketingaktionen**(auch als **Marketing-Nutzungsszenarien** bezeichnet) im Rahmen des Data Governance-Rahmens sind Aktionen, die ein Datennutzer ausführen kann und für die Ihr Unternehmen die Datenverwendung einschränken möchte. Daher wird eine Datenverwendungsrichtlinie wie folgt definiert:

1. Eine bestimmte Marketingaktion
2. Die Datenverwendungs-Beschriftungen, die für diese Aktion eingeschränkt sind, gegen

Ein Beispiel für eine Marketingaktion könnte der Wunsch sein, einen Datensatz in einen Drittanbieter-Service zu exportieren. Wenn es eine Richtlinie gibt, die besagt, dass bestimmte Datentypen (z. B. persönliche identifizierbare Informationen (PII)) nicht exportiert werden können, und Sie versuchen, einen Datensatz zu exportieren, der eine &quot;I&quot;-Beschriftung (Identitätsdaten) enthält, erhalten Sie eine Antwort des Policy Service, in der Sie darauf hingewiesen werden, dass eine Datenverwendungsrichtlinie verletzt wurde.

>[!NOTE] Marketingaktionen allein schränken die Datenverwendung nicht ein. Sie müssen in aktivierte Datenverwendungsrichtlinien eingeschlossen werden, damit diese Aktionen auf Richtlinienverletzungen hin bewertet werden können.

Wenn die Nutzung von Daten im Service Ihres Unternehmens stattfindet, sollten relevante Marketingaktionen angezeigt werden, damit Richtlinienverletzungen festgestellt werden können. Anschließend können Sie die API [für den](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DUL-Richtliniendienst verwenden, um Richtlinienverletzungen in Ihrer Integration zu prüfen.

>[!NOTE] Wenn Sie die Echtzeit-Platform von Kundendaten verwenden, können Sie Marketingverwendungsfälle für Ziele einrichten, um die Durchsetzung von Richtlinien zu automatisieren. Weitere Informationen finden Sie im Dokument zur [Datenverwaltung in Echtzeit-CDP](../../rtcdp/privacy/data-governance-overview.md) .

Eine Liste der [verfügbaren, von Adobe definierten Marketingaktionen](#core-actions)finden Sie im Anhang zu diesem Dokument. Sie können auch eigene benutzerspezifische Marketingaktionen mit der API des DULE Policy Service oder der Benutzeroberfläche der Experience Platform definieren. Weitere Informationen zum Arbeiten mit Marketingaktionen und -richtlinien finden Sie im nächsten Abschnitt.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Verwalten von Datenverwendungsrichtlinien {#manage}

Sobald die Beschriftungen für die Datenverwendung angewendet wurden, können Datenverwaltungen die DULE Policy Service API oder die Benutzeroberfläche für die Experience Platform verwenden, um Richtlinien zu verwalten und auszuwerten, die sich auf Marketingaktionen beziehen, die für Daten mit Datenverwendungsbeschriftungen durchgeführt werden. Sie können Richtlinien erstellen und aktualisieren, den Status einer Richtlinie bestimmen und mit Marketingaktionen arbeiten, um zu bewerten, ob eine bestimmte Aktion eine Datenverwendungsrichtlinie verletzt.

>[!IMPORTANT] Alle Datenverwendungsrichtlinien (einschließlich der von Adobe bereitgestellten Core-Richtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell über die API oder Benutzeroberfläche aktivieren.

Eine schrittweise Anleitung zum Arbeiten mit Marketingaktionen und Datenverwendungsrichtlinien in der API finden Sie im Lernprogramm zum [Erstellen und Auswerten von Datenverwendungsrichtlinien](create.md). Weitere Informationen zu den Schlüsselvorgängen, die von der Policy Service API bereitgestellt werden, finden Sie im Entwicklerhandbuch für den [Policy-Dienst](../api/getting-started.md).

Weitere Informationen zum Arbeiten mit Marketingaktionen und Richtlinien in der Benutzeroberfläche der Platform finden Sie im Benutzerhandbuch für die [Datenverwendungsrichtlinie](./user-guide.md).

## Nächste Schritte

Dieses Dokument bietet eine Einführung in die Datenverwendungsrichtlinien im DUL-Framework. Sie können nun die Prozessdokumentation, die mit diesem Handbuch verknüpft ist, lesen, um mehr über die Arbeit mit Richtlinien in der API und Benutzeroberfläche zu erfahren.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zu Datenverwendungsrichtlinien.

### Adobe-definierte Marketingaktionen {#core-actions}

In der folgenden Tabelle werden die wichtigsten Marketingaktionen beschrieben, die von Adobe standardmäßig bereitgestellt werden.

>[!NOTE] Die wichtigsten Marketingaktionen sollten als Ausgangspunkt zur Identifizierung der zu erstellenden und auf Verstöße hin zu prüfenden Nutzungsrichtlinien dienen. Die Definitionen und Interpretationen hängen von den Anforderungen und Richtlinien Ihres Unternehmens ab.

| Marketingaktion | Beschreibung |
| --- | --- |
| Analytics  | Eine Aktion, die Daten zu Analysezwecken verwendet, z. B. zur Messung, Analyse und zum Berichte der Nutzung der Sites oder Apps Ihres Unternehmens durch Kunden. |
| Kombination mit PII | Eine Aktion, die alle persönlichen identifizierbaren Informationen (PII) mit anonymen Daten kombiniert. Verträge über Daten, die aus Werbenetzwerken, Werbeservern und Drittanbietern von Daten bezogen werden, beinhalten häufig spezifische vertragliche Verbote der Verwendung solcher Daten mit direkt identifizierbaren Daten. |
| Site-übergreifendes Targeting | Eine Aktion, die Daten für das Site-übergreifende Anzeigen-Targeting verwendet. Die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Vor-Ort-Daten und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen, wird als Site-übergreifende Daten bezeichnet. Site-übergreifende Daten werden in der Regel gesammelt und verarbeitet, um Rückschlüsse auf die Interessen der Benutzer zu ziehen. |
| Datenwissenschaften | Eine Aktion, die Daten für Workflows verwendet. Einige Verträge beinhalten explizite Verbote der Datenverwendung für die Datenwissenschaft. Manchmal werden diese Begriffe in Begriffen ausgedrückt, die die Verwendung von Daten für künstliche Intelligenz (AI), maschinelles Lernen (ML) oder Modellierung verbieten. |
| E-Mail-Targeting | Eine Aktion, die Daten in E-Mail-Targeting-Kampagnen verwendet. |
| Exportieren in Dritte | Eine Aktion, die Daten an Prozessoren und Entitäten exportiert, die keine direkten Beziehungen zu Kunden haben. Viele Datenanbieter haben Vertragsbedingungen, die den Export von Daten, von denen sie ursprünglich erfasst wurden, verbieten. So wird beispielsweise die Übertragung von Daten, die Sie von sozialen Netzwerken erhalten, oft eingeschränkt. |
| Onsite-Werbung | Eine Aktion, die Daten für Onsite-Anzeigen verwendet, einschließlich der Auswahl und des Versands von Anzeigen auf den Websites oder Apps Ihres Unternehmens oder zur Messung des Versands und der Effektivität solcher Anzeigen. |
| Onsite-Personalisierung | Eine Aktion, die Daten zur Personalisierung von Inhalten auf der Site verwendet. Bei der Onsite-Personalisierung handelt es sich um Daten, die dazu dienen, Schlussfolgerungen über die Interessen der Benutzer zu ziehen, und die dazu dienen, anhand dieser Schlussfolgerungen festzulegen, welche Inhalte oder Anzeigen bereitgestellt werden. |
| Personalisierung einer einzelnen Identität | Eine Aktion, bei der eine einzelne Identität zu Personalisierungszwecken verwendet werden muss, anstatt Identitäten aus mehreren Quellen zu verbinden. |