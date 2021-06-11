---
keywords: Experience Platform;Home;beliebte Themen;Daten;DULE
solution: Experience Platform
title: Datennutzungsrichtlinien – Übersicht
topic-legacy: policies
description: Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in Experience Platform ausführen bzw. nicht ausführen dürfen.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 4aeb12aec026ab2dc29133dd44e54b453fb71fe3
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 93%

---

# Datennutzungsrichtlinien – Übersicht

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in [!DNL Experience Platform] ausführen bzw. nicht ausführen dürfen.

Dieses Dokument bietet eine allgemeine Übersicht über die Richtlinien zur Datennutzung und enthält Links zu weiteren Dokumentationen zum Arbeiten mit Richtlinien in der Benutzeroberfläche oder API.

## Marketing-Aktionen {#marketing-actions}

Marketing-Aktionen (auch als Marketing-Nutzungsszenarien bezeichnet) im Rahmen des Data Governance-Frameworks sind Aktionen, die ein [!DNL Experience Platform]-Benutzer ausführen kann und für die Ihr Unternehmen die Datennutzung einschränken möchte. Daher wird eine Datennutzungsrichtlinie wie folgt definiert:

1. Eine bestimmte Marketing-Aktion
2. Die Datennutzungsbeschriftung(en), für die diese Aktion nicht ausgeführt werden darf

Ein Beispiel für eine Marketing-Aktion könnte der Wunsch sein, einen Datensatz an den Dienst eines Drittanbieters zu exportieren. Wenn es eine Richtlinie gibt, die besagt, dass bestimmte Datentypen (z. B. persönliche identifizierbare Informationen (PII)) nicht exportiert werden können, und Sie versuchen, einen Datensatz zu exportieren, der eine Kennzeichnung „I“ (Identitätsdaten) enthält, erhalten Sie eine Antwort von [!DNL Policy Service], in der Sie darauf hingewiesen werden, dass eine Datennutzungsrichtlinie verletzt wurde.

>[!NOTE]
>
>Marketing-Aktionen allein schränken die Datennutzung nicht ein. Sie müssen in aktivierten Datennutzungsrichtlinien eingeschlossen sein, damit diese Aktionen auf Richtlinienverletzungen hin bewertet werden können.

Wenn die Nutzung von Daten im Dienst Ihres Unternehmens stattfindet, sollten relevante Marketing-Aktionen angezeigt werden, damit etwaige Richtlinienverletzungen festgestellt werden können. Anschließend können Sie die [Policy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) verwenden, um Richtlinienverletzungen in Ihrer Integration zu prüfen.

>[!NOTE]
>
>Wenn Sie [!DNL Real-time Customer Data Platform] verwenden, können Sie Anwendungsfälle des Marketings für Ziele einrichten, um die Durchsetzung der Richtlinie zu automatisieren. Weitere Informationen finden Sie im Dokument [Datenverwaltung in der Echtzeit-CDP](../../rtcdp/privacy/data-governance-overview.md).

Eine Liste der [von Adobe definierten verfügbaren Marketing-Aktionen](#core-actions) finden Sie im Anhang zu diesem Dokument. Sie können Ihre eigenen benutzerspezifischen Marketing-Aktionen auch mit der [!DNL Policy Service]-API oder über die [!DNL Experience Platform ]-Benutzeroberfläche definieren. Weitere Informationen zum Arbeiten mit Marketing-Aktionen und Richtlinien finden Sie im nächsten Abschnitt.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Datennutzungsrichtlinien verwalten {#manage}

Sobald die Datennutzungsbeschriftungen angewendet wurden, können Datenverwalter die [!DNL Policy Service]-API oder die [!DNL Experience Platform]-Benutzeroberfläche verwenden, um Richtlinien zu verwalten und auszuwerten, die mit Marketing-Aktionen in Verbindung stehen, welche Daten mit Datennutzungsbeschriftungen betreffen. Sie können Richtlinien erstellen und aktualisieren, den Status einer Richtlinie bestimmen und mit Marketing-Aktionen arbeiten, um zu bewerten, ob eine bestimmte Aktion eine Datennutzungsrichtlinie verletzt.

>[!IMPORTANT]
>
>Alle Datennutzungsrichtlinien (einschließlich der von Adobe bereitgestellten Kernrichtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell über die API oder die Benutzeroberfläche aktivieren.

Eine schrittweise Anleitung zum Arbeiten mit Marketing-Aktionen und Datennutzungsrichtlinien in der API finden Sie im Tutorial [Erstellen und Auswerten von Datennutzungsrichtlinien](create.md). Weiterführende Informationen zum Ausführen der wichtigsten von der [!DNL Policy Service]-API unterstützten Vorgänge finden Sie im [Policy Service-Entwicklerhandbuch](../api/getting-started.md).

Informationen zum Arbeiten mit Marketing-Aktionen und Richtlinien in der [!DNL Platform]-Benutzeroberfläche finden Sie im [Benutzerhandbuch zu den Datennutzungsrichtlinien](./user-guide.md).

## Nächste Schritte

In diesem Dokument wurde eine Einführung in die Datennutzungsrichtlinien im [!DNL Data Governance]-Framework gegeben. Sie können nun mit dem Lesen der Prozessdokumentation fortfahren, auf die in diesem Handbuch mehrfach verwiesen wurde, um mehr darüber zu erfahren, wie Sie in der API und der Benutzeroberfläche mit Richtlinien arbeiten.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zu Datennutzungsrichtlinien.

### Von Adobe definierte Marketing-Aktionen {#core-actions}

Die folgende Tabelle beschreibt die wichtigsten Marketing-Aktionen, die von Adobe vorkonfiguriert bereitgestellt werden.

>[!NOTE]
>
>Die wichtigsten Marketing-Aktionen sollten als Ausgangspunkt betrachtet werden, um zu ermitteln, welche Nutzungsrichtlinien erstellt und auf Verstöße überprüft werden müssen. Die Definitionen und ihre Interpretationen hängen von den Anforderungen und Richtlinien Ihres Unternehmens ab.

| Marketing-Aktion | Beschreibung |
| --- | --- |
| Analytics | Eine Aktion, die Daten zu Analysezwecken verwendet, z. B. zum Messen, Analysieren und Erstellen von Berichten über die Nutzung der Websites oder Programmen Ihres Unternehmens durch Kunden. |
| Kombinieren mit direkt identifizierbaren Daten | Eine Aktion, die alle persönlichen identifizierbaren Informationen (PII) mit anonymen Daten kombiniert. Verträge über Daten, die aus Werbenetzwerken, Werbe-Servern und Drittanbietern von Daten bezogen werden, beinhalten häufig spezifische vertragliche Verbote der Verwendung solcher Daten mit direkt identifizierbaren Daten. |
| Site-übergreifendes Targeting | Eine Aktion, die Daten für Site-übergreifendes Targeting von Anzeigen verwendet. Die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Daten in einer Site und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen, wird als „Site-übergreifende Daten“ bezeichnet. Site-übergreifende Daten werden in der Regel gesammelt und verarbeitet, um Rückschlüsse auf die Interessen der Benutzer zu ziehen. |
| Data Science | Eine Aktion, die Daten für datenwissenschaftliche Workflows verwendet. Einige Verträge beinhalten ein explizites Verbot der Datennutzung für datenwissenschaftliche Zwecke. Manchmal wird dies so ausgedrückt, dass die Verwendung von Daten für künstliche Intelligenz (KI), maschinelles Lernen (ML) oder Modellierung verboten ist. |
| E-Mail-Targeting | Eine Aktion, die Daten in E-Mail-Targeting-Kampagnen verwendet. |
| Exportieren an Dritte | Eine Aktion, die Daten an Prozessoren und Entitäten exportiert, die keine direkten Beziehungen zu Kunden haben. Viele Datenanbieter haben Vertragsbedingungen, die den Export von Daten von dort, wo sie ursprünglich erfasst wurden, verbieten. So wird beispielsweise die Übertragung von Daten, die Sie von sozialen Netzwerken erhalten, oft durch deren Verträge eingeschränkt. |
| Onsite-Werbung | Eine Aktion, die Daten für Anzeigen auf Websites verwendet, einschließlich der Auswahl und des Versands von Anzeigen auf den Websites oder in Programmen Ihres Unternehmens, oder zur Messung des Versands und der Effektivität solcher Anzeigen dient. |
| Onsite-Personalisierung | Eine Aktion, die Daten zur Personalisierung von Inhalten in einer Website verwendet. Bei der Onsite-Personalisierung geht es um alle Daten, die verwendet werden, um Rückschlüsse auf die Interessen der Benutzer zu ziehen, und darum, auszuwählen, welche Inhalte oder Anzeigen auf der Grundlage dieser Rückschlüsse bereitgestellt werden. |
| Segmentübereinstimmung | Eine Aktion, bei der Daten für die Adobe Experience Platform-Segmentübereinstimmung verwendet werden, mit der zwei oder mehr Platform-Benutzer Segmentdaten austauschen können. Durch Aktivierung von Richtlinien, die auf diese Aktion verweisen, können Sie einschränken, welche Daten für die Segmentübereinstimmung verwendet werden. Wenn beispielsweise die Kernrichtlinie &quot;Datenfreigabe beschränken&quot;aktiviert ist, können keine Daten mit der Beschriftung [C11](../labels/reference.md#c11) für die Segmentübereinstimmung verwendet werden. |
| Personalisierung für eine einzelne Identität | Eine Aktion, bei der eine einzelne Identität zu Personalisierungszwecken verwendet werden muss, anstatt Identitäten aus mehreren Quellen identische Inhalte zu bieten. |
