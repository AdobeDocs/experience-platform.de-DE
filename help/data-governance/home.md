---
keywords: Experience Platform;Startseite;beliebte Themen;DULE;dule
solution: Experience Platform
title: Data Governance – Übersicht
description: Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Die Funktion spielt in Experience Platform auf verschiedenen Ebenen eine wichtige Rolle, wie z.B. bei Katalogisierung, Ermittlung der Datenherkunft, Datennutzungsbezeichnung, Datennutzungsrichtlinien und Steuerung der Nutzung von Daten für Marketing-Aktionen
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: e6f003a058f50454a6fd4923510976973c6946fb
workflow-type: ht
source-wordcount: '1518'
ht-degree: 100%

---

# Data Governance – Übersicht

Eine der Kernfunktionen von Adobe Experience Platform ist es, Daten aus verschiedenen Unternehmenssystemen zusammenzuführen, damit Marketing-Experten Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher müssen Sie dafür sorgen, dass Ihre Datenoperationen in [!DNL Platform] mit den Datennutzungsrichtlinien konform sind.

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, beispielsweise bei der Katalogisierung, bei der Ermittlung der Datenherkunft, bei Datennutzungskennzeichnungen, bei Datennutzungsrichtlinien und bei der Steuerung der Nutzung von Daten für Marketing-Aktionen.

>[!NOTE]
>
>In Experience Platform betrifft Data Governance nur die Art und Weise, wie Daten verwendet oder aktiviert werden, unabhängig davon, welcher Benutzer die Aktion durchführt. Informationen zum Steuern des Zugriffs auf spezifische Datenfelder für bestimmte Platform-Benutzer in Ihrer Organisation finden Sie hingegen in der Dokumentation zur [attributbasierten Zugriffssteuerung](../access-control/abac/overview.md).

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


## Data Governance-Framework

Das Data Governance-Framework vereinfacht und optimiert die Kategorisierung von Daten und die Erstellung von Datennutzungsrichtlinien. Wenn Datenkennzeichnungen und Datennutzungsrichtlinien angewendet werden, können Marketing-Aktionen evaluiert werden, um eine korrekte Verwendung von Daten sicherzustellen.

Das Data Governance-Framework beinhaltet drei Kernelemente: Kennzeichnungen, Richtlinien und Durchsetzung.

1. **Bezeichnungen:** Klassifizieren Sie Daten anhand datenschutzbezogener Aspekte und vertraglicher Bestimmungen, sodass sie Vorschriften und Richtlinien der Organisation einhalten.
1. **Richtlinien:** Beschreiben Sie, welche Arten von Marketing-Aktionen für welche Daten zulässig sind oder auch nicht.
1. **Durchsetzung:** Nutzen Sie das Richtlinien-Framework, um Richtlinien über verschiedene Datenzugriffsmuster hinweg zu empfehlen und durchzusetzen.

## Datennutzungskennzeichnungen

Data Governance ermöglicht es Data Stewards, Nutzungskennzeichnungen auf Schemafeld- und Datensatzebene anzuwenden, um Daten anhand der gültigen Richtlinien zu kategorisieren.

Das Data Governance-Framework beinhaltet vordefinierte Datennutzungskennzeichnungen, mit denen Daten auf vier Arten kategorisiert werden können:

![Kategorien an Datennutzungsbezeichnungen](./images/overview/label-categories.png)

* **Datenbezeichnungen „C“ (Contract):** Kennzeichnen und kategorisieren Sie Daten, die vertragliche Bestimmungen aufweisen oder mit den Richtlinien zur Verwaltung von Kundendaten in Zusammenhang stehen.
* **Datenbezeichnungen „I“ (Identity):** Kennzeichnen und kategorisieren Sie Daten, die zum Identifizieren oder Kontaktieren einer bestimmten Person dienen können.
* **Datenbezeichnungen „S“ (Sensitive):** Kennzeichnen und kategorisieren Sie Daten, die mit vertraulichen Daten (wie geografischen Daten) verbunden sind.

>[!NOTE]
>
>Eine vollständige Liste der verfügbaren Bezeichnungen sowie Definitionen für jeden Bezeichnungstyp finden Sie im Handbuch zu [unterstützten Datennutzungsbezeichnungen](labels/reference.md).

Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Als Best Practice empfiehlt sich eine Kennzeichnung von Daten, sobald diese in [!DNL Experience Platform] erfasst oder in [!DNL Platform] verfügbar werden.

Weitere Informationen finden Sie in der Übersicht zu [Datennutzungskennzeichnungen](./labels/overview.md).

## Datennutzungsrichtlinien {#data-usage-policies}

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in [!DNL Experience Platform] ausführen bzw. nicht ausführen dürfen.

Ein Beispiel für eine Marketing-Aktion könnte der Wunsch sein, einen Datensatz an den Service eines Drittanbieters zu exportieren. Wenn gemäß einer Richtlinie personenbezogene Daten (Personally Identifiable Information, PII) nicht exportiert werden können und auf Feldebene oder auf den Datensatz eine „I“-Kennzeichnung (Identitätsdaten) angewendet wurde, verhindert [!DNL Policy Service] jede Aktion, die diesen Datensatz an ein Drittanbieterziel exportieren würde. Wenn Sie versuchen, eine dieser Aktionen durchzuführen, sendet der Richtlinien-Service eine Meldung, die Sie darüber informiert, dass eine Datennutzungsrichtlinie verletzt wurde.

Es sind zwei Richtlinientypen verfügbar:

* **[!UICONTROL Data Governance-Richtlinie]**: Zum Beschränken der Datenaktivierung auf Grundlage der durchgeführten Marketing-Aktion und der Datennutzungskennzeichnungen der betreffenden Daten
* **[!UICONTROL Einverständnisrichtlinie]**: Zum Filtern der Profile, die für [Ziele](../destinations/home.md) auf Grundlage der Zustimmung oder Voreinstellungen Ihrer Kunden aktiviert werden können.

Sobald Datennutzungskennzeichnungen angewendet wurden, können Datenverwalter mithilfe der [!DNL Policy Service]-API oder der Benutzeroberfläche von [!DNL Experience Platform] Richtlinien erstellen. Weitere Informationen zu Datennutzungsrichtlinien und Marketing-Aktionen finden Sie unter [Richtlinien – Übersicht](./policies/overview.md).

>[!IMPORTANT]
>
>Alle Datennutzungsrichtlinien (einschließlich der von Adobe bereitgestellten Kernrichtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell aktivieren.

## Nächste Schritte

Dieses Dokument liefert eine Einführung in die Data Governance und das Data Governance-Framework. Sie können nun mit dem [Benutzerhandbuch zu Datennutzungsbezeichnungen](labels/user-guide.md) fortfahren und Ihren Erlebnisdaten Nutzungsbezeichnungen hinzufügen.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zu Data Governance.

### Begriffe in Data Governance {#data-governance-terminology}

In der folgenden Tabelle sind Schlüsselbegriffe im Zusammenhang mit der Data Governance und dem Data Governance-Framework aufgeführt.

| Begriff | Definition |
|---|---|
| **Vertragsbezeichnungen** | Vertragliche „C“-Bezeichnungen dienen zur Kategorisierung von Daten, die vertragliche Bestimmungen aufweisen oder mit Data Governance-Richtlinien Ihrer Organisation in Zusammenhang stehen. |
| **Site-übergreifende Daten** | Site-übergreifende Daten stellen eine Kombination von Daten aus verschiedenen Sites dar, einschließlich einer Kombination aus Onsite-Daten und Offsite-Daten oder einer Kombination aus Daten, die von verschiedenen Offsite-Quellen stammen. |
| **Data Governance** | Data Governance umfasst die Strategien und Technologien, die sicherstellen, dass Daten mit Vorschriften und Unternehmensrichtlinien zur Datennutzung in Einklang stehen. |
| **Data Steward** | Der Data Steward ist eine Person, die für die Verwaltung, Überwachung und Durchsetzung von Daten-Assets in einer Organisation verantwortlich ist. Außerdem stellt ein Data Steward sicher, dass Data Governance-Richtlinien so geschützt und gepflegt werden, dass staatliche Vorschriften und Unternehmensrichtlinien erfüllt werden. |
| **Datennutzungsbezeichnungen** | Mit Datennutzungsbezeichnungen können Benutzer Daten kategorisieren, die datenschutzbezogene Aspekte und vertragliche Bedingungen beinhalten, um Vorschriften und Unternehmensrichtlinien einzuhalten. |
| **Datensatzbezeichnungen** | Einem Schema können Kennzeichnungen hinzugefügt werden. Alle Felder in einem Datensatz übernehmen die Kennzeichnungen des Schemas. |
| **Feldkennzeichnung** | Feldkennzeichnungen sind Data-Governance-Kennzeichnungen, die entweder von einem Schema übernommen oder direkt auf ein Feld angewendet werden. Auf ein Feld angewendete Data-Governance-Kennzeichnungen werden nicht bis auf Schemaebene übernommen. |
| **Geofence** | Eine „Geofence“ ist eine virtuelle geografische Grenze, die durch GPS- oder RFID-Technologie definiert wird und Software in die Lage versetzt, eine Antwort auszulösen, wenn ein Mobilgerät ein bestimmtes Gebiet erreicht oder verlässt. |
| **Identitätsbezeichnungen** | Identitätsbezogene „I“-Bezeichnungen dienen der Kategorisierung von Daten, mit denen sich eine bestimmte Person identifizieren oder kontaktieren lässt. |
| **Interessenbasiertes Targeting** | Interessenbasiertes Targeting, auch Personalisierung genannt, findet statt, wenn die auf einer Website erhobenen Daten für folgende drei Zwecke verwendet werden: zum Ziehen von Rückschlüssen über das Interesse eines Benutzers; zur Nutzung in einem anderen Kontext (z. B. auf einer anderen Website oder in einer App, also „offsite“); zum Festlegen, welche Inhalte oder Anzeigen auf Grundlage der Rückschlüsse bereitgestellt werden. |
| **Marketing-Aktion** | Eine Marketing-Aktion ist im Kontext von Data Governance eine Aktion, die ein Datennutzer von [!DNL Experience Platform] ergreift und bei der geprüft werden muss, ob gegen Datennutzungsrichtlinien verstoßen wurde. |
| **Richtlinie** | Im Data Governance-Framework ist eine Richtlinie eine Regel, die beschreibt, welche Marketing-Aktionen für bestimmte Daten zulässig oder nicht. |
| **Schemakennzeichnungen** | Verwalten Sie die Kennzeichnungen für Data Governance, Einwilligung und Zugriffssteuerung auf Schemaebene. Dadurch werden die Kennzeichnungen zu jedem Datensatz weitergegeben, der dieses Schema verwendet. |
| **Kennzeichnungen für vertrauliche Daten** | Sensible „S“-Kennzeichnungen dienen dazu, Daten zu kategorisieren, die Sie und Ihre Organisation als sensibel betrachten. |

## Zusätzliche Ressourcen

Im folgenden Video werden die Komponenten des Data Governance-Frameworks erklärt.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

Das folgende Video enthält Anleitungen zum Anwenden von Datennutzungskennzeichnungen auf Ihre Schemata und Datensätze in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29709/?learn=on)
