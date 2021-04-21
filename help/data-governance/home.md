---
keywords: Experience Platform;Home;beliebte Themen;DULE;Modul
solution: Experience Platform
title: Übersicht über die Datenverwaltung
topic-legacy: overview
description: Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Die Funktion spielt in Experience Platform auf verschiedenen Ebenen eine wichtige Rolle, wie z.B. bei Katalogisierung, Ermittlung der Datenherkunft, Datennutzungsbezeichnung, Datennutzungsrichtlinien und Steuerung der Nutzung von Daten für Marketing-Aktionen
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 72%

---

# Data Governance – Übersicht

Eine der Kernfunktionen von Adobe Experience Platform ist es, Daten aus verschiedenen Unternehmenssystemen zusammenzuführen, damit Marketing-Experten Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Es ist daher wichtig sicherzustellen, dass Ihre Datenoperationen innerhalb von [!DNL Platform] den Datenverwendungsrichtlinien entsprechen.

Mit Adobe Experience Platform [!DNL Data Governance] können Sie Kundendaten verwalten und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sicherstellen. Es spielt eine Schlüsselrolle innerhalb von [!DNL Experience Platform] auf verschiedenen Ebenen, einschließlich Katalogisierung, Datenbindung, Datenverwendungsbeschriftung, Datenverwendungsrichtlinien und Steuerung der Verwendung von Daten für Marketingaktionen.

## Data Governance-Rollen

Als Konzept ist Data Governance weder automatisch, noch wird die Aufgabe in einem Vakuum erledigt. Was als Rolle für eine Person begann (meist als Data Steward bezeichnet), ist mit Erweiterung des Data Governance-Ökosystems erheblich gewachsen. Data Governance erfordert heute eine kontinuierliche Verwaltung und Überwachung, um effektiv zu sein, und basiert auf Data Stewards, die über Tools verfügen, mit denen sie Daten ordnungsgemäß kennzeichnen, Nutzungsrichtlinien erstellen und die Einhaltung dieser Richtlinien erzwingen können.

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


## [!DNL Data Governance] framework

Das [!DNL Data Governance]-Framework vereinfacht und optimiert den Prozess der Kategorisierung von Daten und Erstellung von Datenverwendungsrichtlinien. Sobald Datenbezeichnungen und Datennutzungsrichtlinien angewendet werden, können Marketing-Aktionen ausgewertet werden, um eine korrekte Verwendung von Daten sicherzustellen.

Das [!DNL Data Governance]-Framework enthält drei wichtige Elemente: Bezeichnungen, Richtlinien und Durchsetzung.

1. **Bezeichnungen:** Klassifizieren Sie Daten anhand datenschutzbezogener Aspekte und vertraglicher Bestimmungen, sodass sie Vorschriften und Richtlinien der Organisation einhalten.
1. **Richtlinien:** Beschreiben Sie, welche Arten von Marketing-Aktionen für welche Daten zulässig sind oder auch nicht.
1. **Durchsetzung:** Nutzen Sie das Richtlinien-Framework, um Richtlinien über verschiedene Datenzugriffsmuster hinweg zu empfehlen und durchzusetzen.

## Datennutzungsbezeichnungen

[!DNL Data Governance] ermöglicht es Data Stewards, Nutzungsbezeichnungen auf der Datensatz- und Feldebene anzuwenden, um Daten anhand der gültigen Richtlinien zu kategorisieren.

Das [!DNL Data Governance]-Framework enthält vordefinierte Beschriftungen für die Datenverwendung, mit denen Daten auf drei Arten kategorisiert werden können:

![Kategorien an Datennutzungsbezeichnungen](./images/overview/label-categories.png)

* **Datenbezeichnungen „C“ (Contract):** Kennzeichnen und kategorisieren Sie Daten, die vertragliche Bestimmungen aufweisen oder mit den Richtlinien zur Verwaltung von Kundendaten in Zusammenhang stehen.
* **Datenbezeichnungen „I“ (Identity):** Kennzeichnen und kategorisieren Sie Daten, die zum Identifizieren oder Kontaktieren einer bestimmten Person dienen können.
* **Datenbezeichnungen „S“ (Sensitive):** Kennzeichnen und kategorisieren Sie Daten, die mit vertraulichen Daten (wie geografischen Daten) verbunden sind.

>[!NOTE]
>
>Eine vollständige Liste der verfügbaren Bezeichnungen sowie Definitionen für jeden Bezeichnungstyp finden Sie im Handbuch zu [unterstützten Datennutzungsbezeichnungen](labels/reference.md).

Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practice empfiehlt die Kennzeichnung von Daten, sobald diese in [!DNL Experience Platform] eingeschlossen sind oder sobald Daten in [!DNL Platform] verfügbar sind.

Weitere Informationen finden Sie in der Übersicht zu [Beschriftungen für die Datenverwendung](./labels/overview.md).

## Datennutzungsrichtlinien

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datenverwendungsrichtlinien sind Regeln, die die Arten von Marketingaktionen beschreiben, von denen Sie Daten innerhalb von [!DNL Experience Platform] ausführen dürfen oder von denen Sie eingeschränkt sind.

Ein Beispiel für eine Marketing-Aktion könnte der Wunsch sein, einen Datensatz an den Dienst eines Drittanbieters zu exportieren. Wenn eine Richtlinie besagt, dass bestimmte Datentypen, wie z. B. &quot;Persönliche identifizierbare Informationen&quot;(PII), nicht exportiert werden können und eine &quot;I&quot;-Beschriftung (Identitätsdaten) auf den Datensatz angewendet wurde, erhalten Sie eine Antwort von [!DNL Policy Service], in der Sie darauf hingewiesen werden, dass eine Datenverwendungsrichtlinie verletzt wurde.

Nachdem die Beschriftungen für die Datenverwendung angewendet wurden, können Datenverwaltungen Richtlinien mit der [!DNL Policy Service]-API oder der [!DNL Experience Platform]-Benutzeroberfläche erstellen.

>[!IMPORTANT]
>
>Alle Datenverwendungsrichtlinien (einschließlich der von der Adobe bereitgestellten Kernrichtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell aktivieren.

Weitere Informationen zu Datenverwendungsrichtlinien und Marketingaktionen finden Sie im [Richtlinienüberblick](./policies/overview.md).

## Nächste Schritte

Dieses Dokument bietet eine allgemeine Einführung in das [!DNL Data Governance]- und[!DNL Data Governance]-Framework. Sie können nun mit dem [Benutzerhandbuch zu Datennutzungsbezeichnungen](labels/user-guide.md) fortfahren und Ihren Erlebnisdaten Nutzungsbezeichnungen hinzufügen.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zu [!DNL Data Governance].

### [!DNL Data Governance] Terminologie

In der folgenden Tabelle sind wichtige Begriffe im Zusammenhang mit [!DNL Data Governance] und dem[!DNL Data Governance]-Framework aufgeführt.

| Begriff | Definition |
|---|---|
| **Vertragsbezeichnungen** | Vertragliche „C“-Bezeichnungen dienen zur Kategorisierung von Daten, die vertragliche Bestimmungen aufweisen oder mit Data Governance-Richtlinien Ihrer Organisation in Zusammenhang stehen. |
| **Site-übergreifende Daten** | Site-übergreifende Daten stellen eine Kombination von Daten aus verschiedenen Sites dar, einschließlich einer Kombination aus Onsite-Daten und Offsite-Daten oder einer Kombination aus Daten, die von verschiedenen Offsite-Quellen stammen. |
| **Data Governance** | Data Governance umfasst die Strategien und Technologien, die sicherstellen, dass Daten mit Vorschriften und Unternehmensrichtlinien zur Datennutzung in Einklang stehen. |
| **Data Steward** | Der Data Steward ist eine Person, die für die Verwaltung, Überwachung und Durchsetzung von Daten-Assets in einer Organisation verantwortlich ist. Außerdem stellt ein Data Steward sicher, dass Data Governance-Richtlinien so geschützt und gepflegt werden, dass staatliche Vorschriften und Unternehmensrichtlinien erfüllt werden. |
| **Datennutzungsbezeichnungen** | Mit Datennutzungsbezeichnungen können Benutzer Daten kategorisieren, die datenschutzbezogene Aspekte und vertragliche Bedingungen beinhalten, um Vorschriften und Unternehmensrichtlinien einzuhalten. |
| **Datensatzbezeichnungen** | Einem Datensatz können Bezeichnungen hinzugefügt werden. Alle Felder in einem Datensatz übernehmen die Bezeichnungen des Datensatzes. |
| **Feldtitel** | Feldtitel sind Data Governance-Bezeichnungen, die entweder von einem Datensatz übernommen oder direkt auf ein Feld angewendet werden.  Auf ein Feld angewendete Data Governance-Beschriftungen werden nicht bis zu einem Datensatz vererbt. |
| **Geofence** | Eine „Geofence“ ist eine virtuelle geografische Grenze, die durch GPS- oder RFID-Technologie definiert wird und Software in die Lage versetzt, eine Antwort auszulösen, wenn ein Mobilgerät ein bestimmtes Gebiet erreicht oder verlässt. |
| **Identitätsbezeichnungen** | Identitätsbezogene „I“-Bezeichnungen dienen der Kategorisierung von Daten, mit denen sich eine bestimmte Person identifizieren oder kontaktieren lässt. |
| **Interessenbasiertes Targeting** | Interessenbasiertes Targeting, auch Personalisierung genannt, findet statt, wenn die folgenden drei Bedingungen erfüllt sind: Daten, die vor Ort erfasst werden, dienen dazu, Rückschlüsse über das Interesse eines Benutzers zu ziehen, werden in einem anderen Kontext verwendet (z. B. in einer anderen Site oder App, also „offsite“) und dienen dazu festzulegen, welche Inhalte oder Anzeigen auf Grundlage der Rückschlüsse bereitgestellt werden. |
| **Marketing-Aktion** | Eine Marketingaktion im Kontext des Data Governance Frameworks ist eine Aktion, die ein [!DNL Experience Platform]-Datenbenutzer unternimmt, für die überprüft werden muss, ob gegen die Datenverwendungsrichtlinien verstoßen wurde |
| **Richtlinie** | Im Data Governance-Framework ist eine Richtlinie eine Regel, die beschreibt, welche Marketing-Aktionen für bestimmte Daten zulässig oder nicht. |
| **Bezeichnungen für vertrauliche Daten** | Vertrauliche „S“-Bezeichnungen (sensitive) dienen dazu, Daten zu kategorisieren, die Sie und Ihre Organisation als vertraulich betrachten. |

## Zusätzliche Ressourcen

Das folgende Video soll Ihr Verständnis des [!DNL Data Governance]-Frameworks unterstützen.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

Im folgenden Video werden verschiedene [!DNL Data Governance]-Funktionen in der Experience Platform vorgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)
