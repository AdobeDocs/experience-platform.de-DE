---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Data Governance
topic: overview
translation-type: tm+mt
source-git-commit: 53225525feb1878aae58939338c1a94f98ec1607
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 73%

---


# [!DNL Data Governance]Übersicht

Eine der Kernfunktionen von Adobe Experience Platform ist es, Daten aus verschiedenen Unternehmenssystemen zusammenzuführen, damit Marketing-Experten Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen definiert werden. It is therefore important to ensure that your data operations within [!DNL Platform] are compliant with data usage policies.

Adobe Experience Platform [!DNL Data Governance] allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data usage policies, and controlling usage of data for marketing actions.

## Data Governance-Rollen

Als Konzept ist Data Governance weder automatisch, noch wird die Aufgabe in einem Vakuum erledigt. Was als Rolle für eine Person begann (meist als **Data Steward** bezeichnet), ist mit Erweiterung des Data Governance-Ökosystems erheblich gewachsen. Data Governance erfordert heute eine kontinuierliche Verwaltung und Überwachung, um effektiv zu sein, und basiert auf Data Stewards, die über Tools verfügen, mit denen sie Daten ordnungsgemäß kennzeichnen, Nutzungsrichtlinien erstellen und die Einhaltung dieser Richtlinien erzwingen können.

Zwar sollte sich jeder Einzelne in der Organisation für Data Governance verantwortlich fühlen, doch werden im Folgenden einige der zentralen Rollen im Data Governance-Zyklus aufgeführt:

![Data Governance-Rollen](./images/overview/roles.png)

### Data Steward

Data Stewards stehen im Mittelpunkt von Data Governance. Diese Rolle ist zuständig für die Interpretation von Vorschriften, vertraglichen Beschränkungen und Richtlinien sowie für deren direkte Anwendung auf Daten. Unter Beachtung der Kenntnisse dieser Vorschriften, Beschränkungen und Richtlinien beinhaltet die Rolle eines Data Stewards Folgendes:

* Überprüfen von Daten, Datensätzen und Datenmustern, um die Nutzungsbezeichnung durch Metadaten anzuwenden und zu verwalten
* Erstellen von Datenrichtlinien und Anwenden der Richtlinien auf Datensätze und Felder
* Übermitteln von Datenrichtlinien an die Organisation

### Marketer

Marketer befinden sich am Endpunkt von Data Governance. Sie fordern Daten von der Data Governance-Infrastruktur an, die von Data Stewards, Data Scientists und Data Engineers eingerichtet wurde. Marketer decken unter dem Marketing-Schirm eine Reihe unterschiedlicher Bereiche ab, darunter:

* Marketing-Analysten fordern Daten an, um sich Informationen über Kunden sowohl einzeln als auch in Gruppen (als Segmente bezeichnet) zu verschaffen.
* Marketing-Spezialisten und Erlebnis-Designer nutzen Daten, um neue Kundenerlebnisse zu gestalten.


## DULE-Framework

Data Usage Labeling and Enforcement (DULE) is the core framework for [!DNL Experience Platform] [!DNL Data Governance]. DULE vereinfacht und optimiert die Kategorisierung von Daten und Erstellung von Datennutzungsrichtlinien. Sobald Datenbezeichnungen und Datennutzungsrichtlinien angewendet werden, können Marketing-Aktionen ausgewertet werden, um eine korrekte Verwendung von Daten sicherzustellen.

Das DULE-Framework beinhaltet drei Kernelemente: Bezeichnungen, Richtlinien und Durchsetzung.

1. **Bezeichnungen:** Klassifizieren Sie Daten anhand datenschutzbezogener Aspekte und vertraglicher Bestimmungen, sodass sie Vorschriften und Richtlinien der Organisation einhalten.
1. **Richtlinien:** Beschreiben Sie, welche Arten von Marketing-Aktionen für welche Daten zulässig sind oder auch nicht.
1. **Durchsetzung:** Nutzen Sie das Richtlinien-Framework, um Richtlinien über verschiedene Datenzugriffsmuster hinweg zu empfehlen und durchzusetzen.

## Datennutzungsbezeichnungen

[!DNL Data Governance] ermöglicht es Data Stewards, Nutzungsbezeichnungen auf der Datensatz- und Feldebene anzuwenden, um Daten anhand der gültigen Richtlinien zu kategorisieren.

Das DULE-Framework enthält vordefinierte Datenverwendungsbeschriftungen, mit denen Daten auf drei Arten kategorisiert werden können:

![Kategorien an Datennutzungsbezeichnungen](./images/overview/label-categories.png)

* **Datenbezeichnungen „C“ (Contract):** Kennzeichnen und kategorisieren Sie Daten, die vertragliche Bestimmungen aufweisen oder mit den Richtlinien zur Verwaltung von Kundendaten in Zusammenhang stehen.
* **Datenbezeichnungen „I“ (Identity):** Kennzeichnen und kategorisieren Sie Daten, die zum Identifizieren oder Kontaktieren einer bestimmten Person dienen können.
* **Datenbezeichnungen „S“ (Sensitive):** Kennzeichnen und kategorisieren Sie Daten, die mit vertraulichen Daten (wie geografischen Daten) verbunden sind.

>[!NOTE]
>
>Eine vollständige Liste der verfügbaren Bezeichnungen sowie Definitionen für jeden Bezeichnungstyp finden Sie im Handbuch zu [unterstützten Datennutzungsbezeichnungen](labels/reference.md).

Bezeichnungen können jederzeit angewendet werden, was eine flexible Datenverwaltung ermöglicht. Best practice encourages labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available in [!DNL Platform].

Weitere Informationen finden Sie in der Übersicht über die Beschriftungen [zur](./labels/overview.md) Datenverwendung.

## Datennutzungsrichtlinien

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Data usage policies are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform].

Ein Beispiel für eine Marketing-Aktion könnte der Wunsch sein, einen Datensatz an den Dienst eines Drittanbieters zu exportieren. If there is a policy in place saying that specific types of data, such as Personally Identifiable Information (PII), cannot be exported and an &quot;I&quot; label (Identity data) has been applied to the dataset, you will receive a response from the [!DNL Policy Service] telling you that a data usage policy has been violated.

Once data usage labels have been applied, data stewards can create policies using the DULE [!DNL Policy Service] API or the [!DNL Experience Platform] user interface.

>[!IMPORTANT]
>
>Alle Datenverwendungsrichtlinien (einschließlich der von Adobe bereitgestellten Core-Richtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell aktivieren.

Weitere Informationen zu Datenverwendungsrichtlinien und Marketingaktionen finden Sie in der [Richtlinienübersicht](./policies/overview.md).

## Nächste Schritte

This document provided a high-level introduction to [!DNL Data Governance] and the DULE framework. Sie können nun mit dem [Benutzerhandbuch zu Datennutzungsbezeichnungen](labels/user-guide.md) fortfahren und Ihren Erlebnisdaten Nutzungsbezeichnungen hinzufügen.

## Anhang

The following section provides additional information regarding [!DNL Data Governance].

### [!DNL Data Governance] Terminologie

The following table outlines key terms related to [!DNL Data Governance] and the DULE framework.

| Begriff | Definition |
|---|---|
| **Vertragsbezeichnungen** | Vertragliche „C“-Bezeichnungen dienen zur Kategorisierung von Daten, die vertragliche Bestimmungen aufweisen oder mit Data Governance-Richtlinien Ihrer Organisation in Zusammenhang stehen. |
| **Site-übergreifende Daten** | Site-übergreifende Daten stellen eine Kombination von Daten aus verschiedenen Sites dar, einschließlich einer Kombination aus Onsite-Daten und Offsite-Daten oder einer Kombination aus Daten, die von verschiedenen Offsite-Quellen stammen. |
| **Data Governance** | Data Governance umfasst die Strategien und Technologien, die sicherstellen, dass Daten mit Vorschriften und Unternehmensrichtlinien zur Datennutzung in Einklang stehen. |
| **Data Steward** | Der Data Steward ist eine Person, die für die Verwaltung, Überwachung und Durchsetzung von Daten-Assets in einer Organisation verantwortlich ist. Außerdem stellt ein Data Steward sicher, dass Data Governance-Richtlinien so geschützt und gepflegt werden, dass staatliche Vorschriften und Unternehmensrichtlinien erfüllt werden. |
| **Datennutzungsbezeichnungen** | Mit Datennutzungsbezeichnungen können Benutzer Daten kategorisieren, die datenschutzbezogene Aspekte und vertragliche Bedingungen beinhalten, um Vorschriften und Unternehmensrichtlinien einzuhalten. |
| **Datensatzbezeichnungen** | Einem Datensatz können Bezeichnungen hinzugefügt werden. Alle Felder in einem Datensatz übernehmen die Bezeichnungen des Datensatzes. |
| **DULE** | DULE ist eine Abkürzung für „Data Usage Labeling and Enforcement“. DULE ist ein wichtiger Bestandteil von Data Governance und bietet verschiedene Funktionen, die in einer Organisation eine Datennutzungsbezeichnung und Anwendung von Datenzugriffsrichtlinien für Governance-Anforderungen ermöglichen. |
| **Feldtitel** | Feldtitel sind Data Governance-Bezeichnungen, die entweder von einem Datensatz übernommen oder direkt auf ein Feld angewendet werden.  Auf ein Feld angewendete Data Governance-Beschriftungen werden nicht bis zu einem Datensatz vererbt. |
| **Geofence** | Eine „Geofence“ ist eine virtuelle geografische Grenze, die durch GPS- oder RFID-Technologie definiert wird und Software in die Lage versetzt, eine Antwort auszulösen, wenn ein Mobilgerät ein bestimmtes Gebiet erreicht oder verlässt. |
| **Identitätsbezeichnungen** | Identitätsbezogene „I“-Bezeichnungen dienen der Kategorisierung von Daten, mit denen sich eine bestimmte Person identifizieren oder kontaktieren lässt. |
| **Interessenbasiertes Targeting** | Interessenbasiertes Targeting, auch Personalisierung genannt, findet statt, wenn die folgenden drei Bedingungen erfüllt sind: Daten, die vor Ort erfasst werden, dienen dazu, Rückschlüsse über das Interesse eines Benutzers zu ziehen, werden in einem anderen Kontext verwendet (z. B. in einer anderen Site oder App, also „offsite“) und dienen dazu festzulegen, welche Inhalte oder Anzeigen auf Grundlage der Rückschlüsse bereitgestellt werden. |
| **Marketing-Aktion** | A marketing action, in the context of the data governance framework, is an action that an [!DNL Experience Platform] data consumer takes, for which there is a need to check for violations of data usage policies |
| **Richtlinie** | Im Data Governance-Framework ist eine Richtlinie eine Regel, die beschreibt, welche Marketing-Aktionen für bestimmte Daten zulässig oder nicht. |
| **Bezeichnungen für vertrauliche Daten** | Vertrauliche „S“-Bezeichnungen (sensitive) dienen dazu, Daten zu kategorisieren, die Sie und Ihre Organisation als vertraulich betrachten. |

## Zusätzliche Ressourcen

The following video is intended to support your understanding of [!DNL Data Governance], and outlines the key aspects of the Data Usage Labeling and Enforcement (DULE) framework.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)
