---
keywords: Experience Platform;Home;beliebte Themen;Zeitplan;DULE
solution: Experience Platform
title: Übersicht über Datenverwendungsrichtlinien
topic-legacy: policies
description: Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in Experience Platform ausführen bzw. nicht ausführen dürfen.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 10%

---

# Datennutzungsrichtlinien – Übersicht

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datenverwendungsrichtlinien sind Regeln, die die Arten von Marketingaktionen beschreiben, von denen Sie Daten innerhalb von [!DNL Experience Platform] ausführen dürfen oder von denen Sie eingeschränkt sind.

Dieses Dokument bietet einen allgemeinen Überblick über die Richtlinien zur Datenverwendung und enthält Links zu weiteren Dokumentationen zum Arbeiten mit Richtlinien in der Benutzeroberfläche oder API.

## Marketing-Aktionen {#marketing-actions}

Marketingaktionen (auch als Marketing-Nutzungsszenarien bezeichnet) im Rahmen des Data Governance-Frameworks sind Aktionen, die ein [!DNL Experience Platform]-Benutzer ausführen kann und für die Ihr Unternehmen die Datenverwendung einschränken möchte. Daher wird eine Datenverwendungsrichtlinie wie folgt definiert:

1. Eine bestimmte Marketingaktion
2. Die Datenverwendungs-Beschriftungen, die für diese Aktion eingeschränkt sind, gegen

Ein Beispiel für eine Marketing-Aktion könnte der Wunsch sein, einen Datensatz an den Dienst eines Drittanbieters zu exportieren. Wenn es eine Richtlinie gibt, die besagt, dass bestimmte Datentypen (z. B. persönliche identifizierbare Informationen (PII)) nicht exportiert werden können, und Sie versuchen, einen Datensatz zu exportieren, der eine &quot;I&quot;-Beschriftung (Identitätsdaten) enthält, erhalten Sie eine Antwort von [!DNL Policy Service], in der Sie darauf hingewiesen werden, dass eine Datenverwendungsrichtlinie verletzt wurde.

>[!NOTE]
>
>Marketingaktionen allein schränken die Datenverwendung nicht ein. Sie müssen in aktivierte Datenverwendungsrichtlinien eingeschlossen werden, damit diese Aktionen auf Richtlinienverletzungen hin bewertet werden können.

Wenn die Nutzung von Daten im Service Ihres Unternehmens stattfindet, sollten relevante Marketingaktionen angezeigt werden, damit Richtlinienverletzungen festgestellt werden können. Anschließend können Sie die [Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) verwenden, um Richtlinienverletzungen in Ihrer Integration zu prüfen.

>[!NOTE]
>
>Wenn Sie [!DNL Real-time Customer Data Platform] verwenden, können Sie Anwendungsfälle für das Marketing für Ziele einrichten, um die Durchsetzung der Richtlinie zu automatisieren. Weitere Informationen finden Sie im Dokument [Datenverwaltung in Echtzeit-CDP](../../rtcdp/privacy/data-governance-overview.md).

Eine Liste von [verfügbaren, von der Adobe definierten Marketingaktionen](#core-actions) finden Sie im Anhang zu diesem Dokument. Sie können Ihre eigenen benutzerspezifischen Marketingaktionen auch mit der API oder der [!DNL Policy Service]-Benutzeroberfläche definieren. [!DNL Experience Platform ] Weitere Informationen zum Arbeiten mit Marketingaktionen und -richtlinien finden Sie im nächsten Abschnitt.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Verwalten von Datenverwendungsrichtlinien {#manage}

Sobald die Beschriftungen für die Datenverwendung angewendet wurden, können Datenverwaltungen die API oder die Benutzeroberfläche [!DNL Policy Service] verwenden, um Richtlinien zu verwalten und auszuwerten, die mit Marketingaktionen in Verbindung stehen, die Daten mit Datenverwendungsbeschriftungen enthalten. [!DNL Experience Platform] Sie können Richtlinien erstellen und aktualisieren, den Status einer Richtlinie bestimmen und mit Marketingaktionen arbeiten, um zu bewerten, ob eine bestimmte Aktion eine Datenverwendungsrichtlinie verletzt.

>[!IMPORTANT]
>
>Alle Datenverwendungsrichtlinien (einschließlich der von der Adobe bereitgestellten Kernrichtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell über die API oder Benutzeroberfläche aktivieren.

Eine schrittweise Anleitung zum Arbeiten mit Marketingaktionen und Datenverwendungsrichtlinien in der API finden Sie im Lernprogramm [Erstellen und Auswerten von Datenverwendungsrichtlinien](create.md). Weitere Informationen zu den Schlüsselvorgängen, die von der [!DNL Policy Service]-API bereitgestellt werden, finden Sie im [Policy Service-Entwicklerhandbuch](../api/getting-started.md).

Informationen zum Arbeiten mit Marketingaktionen und Richtlinien in der [!DNL Platform]-Benutzeroberfläche finden Sie im Benutzerhandbuch [Datenverwendungsrichtlinie](./user-guide.md).

## Nächste Schritte

In diesem Dokument wurde eine Einführung in die Datenverwendungsrichtlinien im [!DNL Data Governance]-Framework bereitgestellt. Sie können nun die Prozessdokumentation, die mit diesem Handbuch verknüpft ist, lesen, um mehr über die Arbeit mit Richtlinien in der API und Benutzeroberfläche zu erfahren.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zu Datenverwendungsrichtlinien.

### Adobe-definierte Marketingaktionen {#core-actions}

Die folgende Tabelle beschreibt die wichtigsten Marketingaktionen, die standardmäßig für jede Adobe bereitgestellt werden.

>[!NOTE]
>
>Die wichtigsten Marketingaktionen sollten als Ausgangspunkt zur Identifizierung der zu erstellenden und auf Verstöße hin zu prüfenden Nutzungsrichtlinien dienen. Die Definitionen und Interpretationen hängen von den Anforderungen und Richtlinien Ihres Unternehmens ab.

| Marketing-Aktion | Beschreibung |
| --- | --- |
| Analytics  | Eine Aktion, die Daten zu Analysezwecken verwendet, z. B. zur Messung, Analyse und zum Berichte der Nutzung der Sites oder Apps Ihres Unternehmens durch Kunden. |
| Kombination mit PII | Eine Aktion, die alle persönlichen identifizierbaren Informationen (PII) mit anonymen Daten kombiniert. Verträge über Daten, die aus Werbenetzwerken, Werbeservern und Drittanbietern von Daten bezogen werden, beinhalten häufig spezifische vertragliche Verbote der Verwendung solcher Daten mit direkt identifizierbaren Daten. |
| Site-übergreifendes Targeting | Eine Aktion, die Daten für das Site-übergreifende Anzeigen-Targeting verwendet. Die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Vor-Ort-Daten und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen, wird als Site-übergreifende Daten bezeichnet. Site-übergreifende Daten werden in der Regel gesammelt und verarbeitet, um Rückschlüsse auf die Interessen der Benutzer zu ziehen. |
| Data Science | Eine Aktion, die Daten für Workflows verwendet. Einige Verträge beinhalten explizite Verbote der Datenverwendung für die Datenwissenschaft. Manchmal werden diese Begriffe in Begriffen ausgedrückt, die die Verwendung von Daten für künstliche Intelligenz (AI), maschinelles Lernen (ML) oder Modellierung verbieten. |
| E-Mail-Targeting | Eine Aktion, die Daten in E-Mail-Targeting-Kampagnen verwendet. |
| Exportieren in Dritte | Eine Aktion, die Daten an Prozessoren und Entitäten exportiert, die keine direkten Beziehungen zu Kunden haben. Viele Datenanbieter haben Vertragsbedingungen, die den Export von Daten, von denen sie ursprünglich erfasst wurden, verbieten. So wird beispielsweise die Übertragung von Daten, die Sie von sozialen Netzwerken erhalten, oft eingeschränkt. |
| Onsite-Werbung | Eine Aktion, die Daten für Onsite-Anzeigen verwendet, einschließlich der Auswahl und des Versands von Anzeigen auf den Websites oder Apps Ihres Unternehmens oder zur Messung des Versands und der Effektivität solcher Anzeigen. |
| Onsite-Personalisierung | Eine Aktion, die Daten zur Personalisierung von Inhalten auf der Site verwendet. Bei der Onsite-Personalisierung handelt es sich um Daten, die dazu dienen, Schlussfolgerungen über die Interessen der Benutzer zu ziehen, und die dazu dienen, anhand dieser Schlussfolgerungen festzulegen, welche Inhalte oder Anzeigen bereitgestellt werden. |
| Personalisierung einer einzelnen Identität | Eine Aktion, bei der eine einzelne Identität zu Personalisierungszwecken verwendet werden muss, anstatt Identitäten aus mehreren Quellen zu verbinden. |
