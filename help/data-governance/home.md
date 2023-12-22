---
keywords: Experience Platform;Startseite;beliebte Themen;DULE;dule
solution: Experience Platform
title: Data Governance – Übersicht
description: Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Die Funktion spielt in Experience Platform auf verschiedenen Ebenen eine wichtige Rolle, wie z.B. bei Katalogisierung, Ermittlung der Datenherkunft, Datennutzungsbezeichnung, Datennutzungsrichtlinien und Steuerung der Nutzung von Daten für Marketing-Aktionen.
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 2b16ecb840e63baa244d8061a0349a9e39e726b2
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 65%

---

# Data Governance – Übersicht

Eine der Kernfunktionen von Adobe Experience Platform ist es, Daten aus verschiedenen Unternehmenssystemen zusammenzuführen, damit Marketing-Experten Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher müssen Sie dafür sorgen, dass Ihre Datenoperationen in [!DNL Platform] mit den Datennutzungsrichtlinien konform sind.

Verwalten Sie Kundendaten und stellen Sie sicher, dass die für die Datenverwendung in Adobe Experience Platform Data Governance geltenden Vorschriften, Einschränkungen und Richtlinien eingehalten werden. Data Governance spielt bei der Experience Platform auf verschiedenen Ebenen eine Schlüsselrolle, einschließlich Katalogisierung, Datenherkunft, Datennutzungsbezeichnung, Datennutzungsrichtlinien und Steuerung der Nutzung von Daten für Marketing-Aktionen.

>[!NOTE]
>
>In Experience Platform betrifft Data Governance nur die Art und Weise, wie Daten verwendet oder aktiviert werden, unabhängig davon, welcher Benutzer die Aktion durchführt. Informationen zum Steuern des Zugriffs auf spezifische Datenfelder für bestimmte Platform-Benutzer in Ihrer Organisation finden Sie hingegen in der Dokumentation zur [attributbasierten Zugriffssteuerung](../access-control/abac/overview.md).

## Data Governance-Rollen {#data-governance-roles}

Als Konzept ist Data Governance weder automatisch, noch wird die Aufgabe in einem Vakuum erledigt. Was als Rolle für eine Person begann (meist als Data Steward bezeichnet), ist mit Erweiterung des Data Governance-Ökosystems erheblich gewachsen. Data Governance erfordert heute eine kontinuierliche Verwaltung und Überwachung, um erfolgreich zu sein. Eine effektive Data Governance setzt voraus, dass Data Stewards über Tools verfügen, mit denen Daten ordnungsgemäß gekennzeichnet, Nutzungsrichtlinien erstellt und die Einhaltung dieser Richtlinien durchgesetzt werden können.

Zwar sollte sich jeder Einzelne in der Organisation für Data Governance verantwortlich fühlen, doch werden im Folgenden einige der zentralen Rollen im Data Governance-Zyklus aufgeführt:

![Grafisch zur Vermittlung der vier Data Governance-Rollen mit Anführungszeichen zu den Aufgaben jeder Rolle.](./images/overview/roles.png)

### Data Steward {#data-steward}

Data Stewards stehen im Mittelpunkt von Data Governance. Diese Rolle ist zuständig für die Interpretation von Vorschriften, vertraglichen Beschränkungen und Richtlinien sowie für deren direkte Anwendung auf Daten. Unter Beachtung der Kenntnisse dieser Vorschriften, Beschränkungen und Richtlinien beinhaltet die Rolle eines Data Stewards Folgendes:

* Überprüfen von Daten, Datensätzen und Datenmustern, um die Nutzungsbezeichnung durch Metadaten anzuwenden und zu verwalten
* Erstellen von Datenrichtlinien und Anwenden der Richtlinien auf Datensätze und Felder
* Übermitteln von Datenrichtlinien an die Organisation

### Marketer {#marketer}

Marketer befinden sich am Endpunkt von Data Governance. Sie fordern Daten von der Data Governance-Infrastruktur an, die von Data Stewards, Data Scientists und Data Engineers eingerichtet wurde. Marketer decken unter dem Marketing-Schirm eine Reihe unterschiedlicher Bereiche ab, darunter:

* Marketing-Analysten fordern Daten an, um sich Informationen über Kunden sowohl einzeln als auch in Gruppen (als Segmente bezeichnet) zu verschaffen.
* Marketing-Spezialisten und Erlebnis-Designer nutzen Daten, um neue Kundenerlebnisse zu gestalten.

## Data Governance-Framework {#data-governance-framework}

Das Data Governance-Framework vereinfacht und optimiert die Kategorisierung von Daten und die Erstellung von Datennutzungsrichtlinien. Wenn Datenkennzeichnungen und Datennutzungsrichtlinien angewendet werden, können Marketing-Aktionen ausgewertet werden, um eine korrekte Verwendung von Daten sicherzustellen.

Das Data Governance-Framework beinhaltet drei Kernelemente: Kennzeichnungen, Richtlinien und Durchsetzung.

1. **Bezeichnungen:** Klassifizieren Sie Daten anhand datenschutzbezogener Aspekte und vertraglicher Bestimmungen, sodass sie Vorschriften und Richtlinien der Organisation einhalten.
1. **Richtlinien:** Beschreiben Sie, welche Arten von Marketing-Aktionen für bestimmte Daten zulässig sind oder nicht.
1. **Durchsetzung:** Nutzen Sie das Richtlinien-Framework, um Richtlinien über verschiedene Datenzugriffsmuster hinweg zu empfehlen und durchzusetzen.

## Datennutzungskennzeichnungen {#data-usage-labels}

Data Governance ermöglicht es Data Stewards, Nutzungsbezeichnungen auf Schema-Feldebene anzuwenden, um Daten nach dem anzuwendenden Richtlinientyp zu kategorisieren.

Das Data Governance-Framework beinhaltet vordefinierte Datennutzungskennzeichnungen, mit denen Daten auf vier Arten kategorisiert werden können:

![Die drei Kategorien für Datennutzungsbezeichnungen.](./images/overview/label-categories.png)

* **Datenbezeichnungen „C“ (Contract):** Kennzeichnen und kategorisieren Sie Daten, die vertragliche Bestimmungen aufweisen oder mit den Richtlinien zur Verwaltung von Kundendaten in Zusammenhang stehen.
* **Datenbezeichnungen „I“ (Identity):** Kennzeichnen und kategorisieren Sie Daten, die zum Identifizieren oder Kontaktieren einer bestimmten Person dienen können.
* **Datenbezeichnungen „S“ (Sensitive):** Kennzeichnen und kategorisieren Sie Daten, die mit vertraulichen Daten (wie geografischen Daten) verbunden sind.

>[!NOTE]
>
>Siehe Handbuch unter [unterstützte Datennutzungsbezeichnungen](labels/reference.md) für eine vollständige Liste der verfügbaren Bezeichnungen und Definitionen für jeden Bezeichnungstyp.

Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practice empfiehlt die Kennzeichnung von Daten bei der Erfassung in Experience Platform oder sobald Daten verfügbar sind in [!DNL Platform].

Siehe Übersicht unter [Datennutzungsbezeichnungen](./labels/overview.md) Weitere Informationen dazu, wie Datennutzungsbezeichnungen verwendet werden, um die Einhaltung von Data Governance durchzusetzen.

## Datennutzungsrichtlinien {#data-usage-policies}

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Datennutzungsrichtlinien implementiert werden. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in Experience Platform ausführen bzw. nicht ausführen dürfen.

Ein Beispiel für eine Marketing-Aktion könnte der Wunsch sein, einen Datensatz an den Service eines Drittanbieters zu exportieren. Gibt es eine Richtlinie, die erklärt, dass personenbezogene Daten (PII) nicht exportiert werden können, und wurde von ihrem Schema aus eine &quot;I&quot;-Beschriftung (Identitätsdaten) auf die Feldebene angewendet. Policy Service verhindert dann jede Aktion, die diesen Datensatz an ein Drittanbieterziel exportiert. Wenn Sie versuchen, eine dieser Aktionen durchzuführen, sendet der Richtlinien-Service eine Meldung, die Sie darüber informiert, dass eine Datennutzungsrichtlinie verletzt wurde.


Es sind zwei Richtlinientypen verfügbar:

* **[!UICONTROL Data Governance-Richtlinie]**: Zum Beschränken der Datenaktivierung auf Grundlage der durchgeführten Marketing-Aktion und der Datennutzungskennzeichnungen der betreffenden Daten
* **[!UICONTROL Einverständnisrichtlinie]**: Filtern Sie die Profile, für die aktiviert werden können. [Ziele](../destinations/home.md) basierend auf der Zustimmung oder den Vorlieben Ihrer Kunden.

Sobald Datennutzungsbezeichnungen angewendet wurden, können Data Stewards Richtlinien mithilfe der Policy Service-API oder der Experience Platform-Benutzeroberfläche erstellen. Weitere Informationen zu Datennutzungsrichtlinien und Marketing-Aktionen finden Sie unter [Richtlinien – Übersicht](./policies/overview.md).

>[!IMPORTANT]
>
>Alle Datennutzungsrichtlinien (einschließlich der von Adobe bereitgestellten Kernrichtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung berücksichtigt wird, müssen Sie diese Richtlinie manuell aktivieren.

## Nächste Schritte

Dieses Dokument bietet eine allgemeine Einführung in Data Governance und das Data Governance-Framework. Sie können nun mit dem [Benutzerhandbuch zu Datennutzungsbezeichnungen](labels/user-guide.md) fortfahren und Ihren Erlebnisdaten Nutzungsbezeichnungen hinzufügen.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zu Data Governance.

### Begriffe in Data Governance {#data-governance-terminology}

In der folgenden Tabelle sind Schlüsselbegriffe im Zusammenhang mit der Data Governance und dem Data Governance-Framework aufgeführt.

| Begriff | Definition |
|---|---|
| **Vertragsbezeichnungen** | Vertragliche „C“-Bezeichnungen dienen zur Kategorisierung von Daten, die vertragliche Bestimmungen aufweisen oder mit Data Governance-Richtlinien Ihrer Organisation in Zusammenhang stehen. |
| **Site-übergreifende Daten** | Site-übergreifende Daten stellen die Kombination von Daten aus verschiedenen Sites dar. Site-übergreifende Daten umfassen sowohl On-site- als auch Off-site-Daten oder eine Kombination von Daten aus verschiedenen Offsite-Quellen. |
| **Data Governance** | Data Governance umfasst die Strategien und Technologien, mit denen sichergestellt wird, dass die Daten in Bezug auf die Datennutzung den Vorschriften und Unternehmensrichtlinien entsprechen. |
| **Data Steward** | Der Data Steward ist eine Person, die für die Verwaltung, Überwachung und Durchsetzung von Daten-Assets in einer Organisation verantwortlich ist. Ein Data Steward stellt außerdem sicher, dass Data Governance-Richtlinien geschützt und gepflegt werden, um mit staatlichen Vorschriften und Unternehmensrichtlinien konform zu sein. |
| **Datennutzungsbezeichnungen** | Mit Datennutzungsbezeichnungen können Benutzer Daten kategorisieren, die datenschutzbezogene Aspekte und vertragliche Bedingungen beinhalten, um Vorschriften und Unternehmensrichtlinien einzuhalten. |
| **Datensatzbezeichnungen** | Einem Schema können Kennzeichnungen hinzugefügt werden. Alle Felder in einem Datensatz übernehmen die Kennzeichnungen des Schemas. |
| **Feldkennzeichnung** | Feldkennzeichnungen sind Data-Governance-Kennzeichnungen, die entweder von einem Schema übernommen oder direkt auf ein Feld angewendet werden. Auf ein Feld angewendete Data-Governance-Kennzeichnungen werden nicht bis auf Schemaebene übernommen. |
| **Geofence** | Eine „Geofence“ ist eine virtuelle geografische Grenze, die durch GPS- oder RFID-Technologie definiert wird und Software in die Lage versetzt, eine Antwort auszulösen, wenn ein Mobilgerät ein bestimmtes Gebiet erreicht oder verlässt. |
| **Identitätsbezeichnungen** | Identitätsbezogene „I“-Bezeichnungen dienen der Kategorisierung von Daten, mit denen sich eine bestimmte Person identifizieren oder kontaktieren lässt. |
| **Interessenbasiertes Targeting** | Eine interessensbasierte Zielgruppenbestimmung, auch Personalisierung genannt, tritt auf, wenn die folgenden drei Bedingungen erfüllt sind:<br>Die vor Ort erfassten Daten sind<br><ul><li>Dient dazu, Rückschlüsse auf das Interesse eines Benutzers zu ziehen;</li><li>Wird in einem anderen Kontext verwendet, z. B. auf einer anderen Site oder in einer anderen App (außerhalb der Site)</li><li>Wird verwendet, um anhand dieser Rückschlüsse festzulegen, welche Inhalte oder Anzeigen bereitgestellt werden.</li></ul> |
| **Marketing-Aktion** | Eine Marketing-Aktion ist im Kontext des Data Governance-Frameworks eine Aktion, die ein Datennutzer von Experience Platform ergreift und bei der geprüft werden muss, ob gegen Datennutzungsrichtlinien verstoßen wurde. |
| **Richtlinie** | Im Data Governance-Framework ist eine Richtlinie eine Regel, die beschreibt, welche Arten von Marketing-Aktionen für bestimmte Daten zulässig sind oder nicht. |
| **Schemakennzeichnungen** | Verwalten Sie die Kennzeichnungen für Data Governance, Einwilligung und Zugriffssteuerung auf Schemaebene. Dadurch werden die Beschriftungen zu jedem Datensatz übertragen, der dieses Schema verwendet. |
| **Kennzeichnungen für vertrauliche Daten** | Sensible „S“-Kennzeichnungen dienen dazu, Daten zu kategorisieren, die Sie und Ihre Organisation als sensibel betrachten. |

## Zusätzliche Ressourcen

Im folgenden Video werden die Komponenten des Data Governance-Frameworks erklärt.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

Im folgenden Video erfahren Sie, wie Sie Datennutzungsbezeichnungen auf Ihre Schemas oder die Gesamtheit eines Datensatzes in Experience Platform anwenden.

>[!VIDEO](https://video.tv.adobe.com/v/29709/?learn=on)
