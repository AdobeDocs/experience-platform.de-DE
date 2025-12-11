---
keywords: Experience Platform;Startseite;beliebte Themen;DULE;dule
solution: Experience Platform
title: Data Governance – Übersicht
description: Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Die Funktion spielt in Experience Platform auf verschiedenen Ebenen eine wichtige Rolle, wie z.B. bei Katalogisierung, Ermittlung der Datenherkunft, Datennutzungsbezeichnung, Datennutzungsrichtlinien und Steuerung der Nutzung von Daten für Marketing-Aktionen.
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 9b1630a4876c0bcd7331f8da264e4f19ce00b59a
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 62%

---

# Data Governance – Übersicht {#data-governance-overview}

>[!CONTEXTUALHELP]
>id="platform_datagovernance_framework"
>title="Data-Governance-Verpflichtung"
>abstract="Bitte beachten Sie, dass es in Ihrer alleinigen Verantwortung liegt, die Data-Governance-Richtlinien Ihres Unternehmens einzuhalten und Ihre gesetzlichen Anforderungen zu erfüllen. Experience Platform bietet Data-Governance-Tools, mit denen Sie Ihre Datennutzungsverpflichtungen verwalten können. Wenden Sie die entsprechenden Datennutzungskennzeichnungen an, bevor Sie Daten abfragen oder verarbeiten. Weitere Informationen zu Tools und Best Practices für Data Governance finden Sie in der Dokumentation."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de" text="Data Governance – Übersicht"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=de" text="Überblick über Data-Governance-Beschriftungen"

Eine der Kernfunktionen von Adobe Experience Platform ist es, Daten aus verschiedenen Unternehmenssystemen zusammenzuführen, damit Marketing-Experten Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher müssen Sie dafür sorgen, dass Ihre Datenoperationen in [!DNL Experience Platform] mit den Datennutzungsrichtlinien konform sind.

Verwalten Sie Kundendaten und stellen Sie die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicher, die für die Verwendung von Daten mit Adobe Experience Platform Data Governance gelten. Data Governance spielt in Experience Platform auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Ermittlung der Datenherkunft, Datennutzungsbezeichnung, Datennutzungsrichtlinien und Steuerung der Nutzung von Daten für Marketing-Aktionen.

>[!NOTE]
>
>In Experience Platform betrifft Data Governance nur die Art und Weise, wie Daten verwendet oder aktiviert werden, unabhängig davon, welcher Benutzer die Aktion durchführt. Informationen zum Steuern des Zugriffs auf bestimmte Datenfelder für bestimmte Experience Platform-Benutzende in Ihrem Unternehmen finden Sie stattdessen in der Dokumentation [attributbasierten Zugriffssteuerung](../access-control/abac/overview.md).

## Data Governance-Rollen {#data-governance-roles}

Als Konzept ist Data Governance weder automatisch, noch wird die Aufgabe in einem Vakuum erledigt. Was als Rolle für eine Person begann (meist als Data Steward bezeichnet), ist mit Erweiterung des Data Governance-Ökosystems erheblich gewachsen. Data Governance erfordert heutzutage eine kontinuierliche Verwaltung und Überwachung, um erfolgreich zu sein. Eine effektive Data Governance beruht darauf, dass Datenverwalter über Tools verfügen, mit denen Daten ordnungsgemäß gekennzeichnet, Nutzungsrichtlinien erstellt und die Einhaltung dieser Richtlinien durchgesetzt werden können.

Zwar sollte sich jeder Einzelne in der Organisation für Data Governance verantwortlich fühlen, doch werden im Folgenden einige der zentralen Rollen im Data Governance-Zyklus aufgeführt:

![Grafik zur Vermittlung der vier Data-Governance-Rollen mit Zitaten zu den Aufgaben der einzelnen Rollen.](./images/overview/roles.png)

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

Das Data Governance-Framework vereinfacht und optimiert die Kategorisierung von Daten und die Erstellung von Datennutzungsrichtlinien. Wenn Daten-Labels und Datennutzungsrichtlinien angewendet werden, können Marketing-Aktionen ausgewertet werden, um eine korrekte Verwendung von Daten sicherzustellen.

Das Data Governance-Framework beinhaltet drei Kernelemente: Kennzeichnungen, Richtlinien und Durchsetzung.

1. **Labels:** Klassifizieren Sie Daten anhand datenschutzbezogener Aspekte und vertraglicher Bestimmungen, sodass sie Vorschriften und Richtlinien der Organisation einhalten.
1. **Richtlinien:** Beschreiben Sie, welche Arten von Marketing-Aktionen für bestimmte Daten zulässig bzw. nicht zulässig sind.
1. **Durchsetzung:** Nutzen Sie das Richtlinien-Framework, um Richtlinien über verschiedene Datenzugriffsmuster hinweg zu empfehlen und durchzusetzen.

## Datennutzungs-Labels {#data-usage-labels}

Data Governance ermöglicht es Data Stewards, Nutzungsbezeichnungen auf der Ebene der Schemafelder anzuwenden, um Daten anhand der gültigen Richtlinien zu kategorisieren.

Das Data Governance-Framework beinhaltet vordefinierte Datennutzungskennzeichnungen, mit denen Daten auf vier Arten kategorisiert werden können:

![Die drei Kategorien von Datennutzungskennzeichnungen.](./images/overview/label-categories.png)

* **Daten-Labels „C“ (Contract):** Kennzeichnen und kategorisieren Sie Daten, die vertragliche Bestimmungen aufweisen oder mit den Richtlinien zur Verwaltung von Kundendaten in Zusammenhang stehen.
* **Daten-Labels „I“ (Identity):** Kennzeichnen und kategorisieren Sie Daten, die zum Identifizieren oder Kontaktieren einer bestimmten Person dienen können.
* **Daten-Labels „S“ (Sensitive):** Kennzeichnen und kategorisieren Sie Daten, die mit vertraulichen Daten (wie geografischen Daten) verbunden sind.

>[!NOTE]
>
>Eine vollständige Liste [&#x200B; verfügbaren Bezeichnungen und Definitionen für &#x200B;](labels/reference.md) Bezeichnungstyp finden Sie im Handbuch zu „Unterstützte Datennutzungsbezeichnungen“.

Labels können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Als Best Practice empfiehlt sich eine Kennzeichnung von Daten, wenn diese in Experience Platform aufgenommen oder in [!DNL Experience Platform] verfügbar werden.

Weitere Informationen dazu, wie [&#x200B; Datennutzungskennzeichnungen zur Durchsetzung der Data-Governance](./labels/overview.md)Compliance verwendet werden, finden Sie in der Übersicht zu Datennutzungskennzeichnungen .

## Datennutzungsrichtlinien {#data-usage-policies}

Damit Datennutzungskennzeichnungen die Datenkonformität effektiv unterstützen können, müssen Datennutzungsrichtlinien implementiert werden. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in Experience Platform ausführen bzw. nicht ausführen dürfen.

Ein Beispiel für eine Marketing-Aktion könnte der Wunsch sein, einen Datensatz an den Service eines Drittanbieters zu exportieren. Wenn es eine Richtlinie gibt, die erklärt, dass personenbezogene Daten (PII) nicht exportiert werden können, und eine Kennzeichnung „I“ (Identitätsdaten) auf Feldebene aus ihrem Schema angewendet wurde. Der Richtlinien-Service verhindert dann jede Aktion, die diesen Datensatz an ein Drittanbieterziel exportieren würde. Wenn Sie versuchen, eine dieser Aktionen durchzuführen, sendet der Richtlinien-Service eine Meldung, die Sie darüber informiert, dass eine Datennutzungsrichtlinie verletzt wurde.


Es sind zwei Richtlinientypen verfügbar:

* **[!UICONTROL Data governance policy]**: Beschränken Sie die Datenaktivierung auf der Grundlage der durchgeführten Marketing-Aktion und der von den betreffenden Daten getragenen Datennutzungskennzeichnungen.
* **[!UICONTROL Consent policy]**: Filtern Sie die Profile, die für ([) &#x200B;](../destinations/home.md) aktiviert werden können, basierend auf dem Einverständnis oder den Voreinstellungen Ihrer Kunden.

Sobald Datennutzungskennzeichnungen angewendet wurden, können Datenverwalter mithilfe der Richtlinien-Service-API oder der Benutzeroberfläche von Experience Platform Richtlinien erstellen. Weitere Informationen zu Datennutzungsrichtlinien und Marketing-Aktionen finden Sie unter [Richtlinien – Übersicht](./policies/overview.md).

>[!IMPORTANT]
>
>Alle Datennutzungsrichtlinien (einschließlich der von Adobe bereitgestellten Kernrichtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell aktivieren.

## Nächste Schritte

Dieses Dokument bietet eine allgemeine Einführung in die Data Governance und das Data Governance-Framework. Sie können nun mit dem [Benutzerhandbuch zu Datennutzungs-Labels](labels/user-guide.md) fortfahren und Ihren Erlebnisdaten Nutzungs-Labels hinzufügen.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zu Data Governance.

### Begriffe in Data Governance {#data-governance-terminology}

In der folgenden Tabelle sind Schlüsselbegriffe im Zusammenhang mit der Data Governance und dem Data Governance-Framework aufgeführt.

| Begriff | Definition |
|---|---|
| **Vertragsbezeichnungen** | Vertragliche „C“-Labels dienen zur Kategorisierung von Daten, die vertragliche Bestimmungen aufweisen oder mit Data Governance-Richtlinien Ihrer Organisation in Zusammenhang stehen. |
| **Site-übergreifende Daten** | Site-übergreifende Daten sind die Kombination von Daten aus mehreren Sites. Site-übergreifende Daten umfassen sowohl Onsite- als auch Offsite-Daten oder eine Kombination aus Daten aus verschiedenen Offsite-Quellen. |
| **Data Governance** | Data Governance umfasst die Strategien und Technologien, mit denen sichergestellt werden soll, dass die Daten den Vorschriften und Unternehmensrichtlinien in Bezug auf die Datennutzung entsprechen. |
| **Data Steward** | Der Data Steward ist eine Person, die für die Verwaltung, Überwachung und Durchsetzung von Daten-Assets in einer Organisation verantwortlich ist. Ein Data Steward stellt außerdem sicher, dass die Data Governance-Richtlinien geschützt und gepflegt werden, sodass sie den gesetzlichen Vorschriften und den Richtlinien der Organisation entsprechen. |
| **Datennutzungs-Labels** | Mit Datennutzungs-Labels können Benutzer Daten kategorisieren, die datenschutzbezogene Aspekte und vertragliche Bedingungen beinhalten, um Vorschriften und Unternehmensrichtlinien einzuhalten. |
| **Datensatz-Labels** | Einem Schema können Labels hinzugefügt werden. Alle Felder in einem Datensatz übernehmen die Labels des Schemas. |
| **Feldkennzeichnung** | Feldkennzeichnungen sind Data-Governance-Labels, die entweder von einem Schema übernommen oder direkt auf ein Feld angewendet werden. Auf ein Feld angewendete Data-Governance-Labels werden nicht bis auf Schemaebene übernommen. |
| **Geofence** | Eine „Geofence“ ist eine virtuelle geografische Grenze, die durch GPS- oder RFID-Technologie definiert wird und Software in die Lage versetzt, eine Antwort auszulösen, wenn ein Mobilgerät ein bestimmtes Gebiet erreicht oder verlässt. |
| **Identitäts-Labels** | Identitätsbezogene „I“-Labels dienen der Kategorisierung von Daten, mit denen sich eine bestimmte Person identifizieren oder kontaktieren lässt. |
| **Interessenbasiertes Targeting** | Ein interessenbasiertes Targeting, auch Personalisierung genannt, findet statt, wenn die folgenden drei Bedingungen erfüllt sind<br>Die auf der Site erhobenen Daten sind<br><ul><li>Wird verwendet, um Rückschlüsse auf das Interesse eines Benutzers zu ziehen,</li><li>Wird in einem anderen Kontext verwendet, z. B. auf einer anderen Site oder in einer App (extern)</li><li>Wird verwendet, um auszuwählen, welche Inhalte oder Anzeigen basierend auf diesen Rückschlüssen bereitgestellt werden sollen.</li></ul> |
| **Marketing-Aktion** | Eine Marketing-Aktion ist im Kontext des Data Governance-Frameworks eine Aktion, die ein Datennutzer von Experience Platform ergreift und bei der geprüft werden muss, ob gegen Datennutzungsrichtlinien verstoßen wurde. |
| **Richtlinie** | Im Data Governance-Framework ist eine Richtlinie eine Regel, die beschreibt, welche Arten von Marketing-Aktionen für bestimmte Daten zulässig bzw. nicht zulässig sind. |
| **Schema-Labels** | Verwalten Sie die Labels für Data Governance, Einwilligung und Zugriffssteuerung auf Schemaebene. Dadurch werden die Kennzeichnungen an jeden Datensatz weitergegeben, der dieses Schema verwendet. |
| **Labels für vertrauliche Daten** | Sensible „S“-Labels dienen dazu, Daten zu kategorisieren, die Sie und Ihre Organisation als sensibel betrachten. |

## Zusätzliche Ressourcen

Im folgenden Video werden die Komponenten des Data Governance-Frameworks erklärt.

>[!IMPORTANT]
>
>Das Video verweist auf das Anwenden von Kennzeichnungen auf einzelne Datensatzfelder. Dieser Workflow wird nicht mehr unterstützt. [Kennzeichnungen müssen jetzt auf Schemafeldebene angewendet werden](./e2e.md#labels). Die Konzepte im Video bleiben korrekt, aber der Workflow für die Beschriftung wurde geändert.

>[!VIDEO](https://video.tv.adobe.com/v/33153?captions=ger&quality=12&enable10seconds=on&speedcontrol=on)

Im folgenden Video erfahren Sie, wie Sie Datennutzungskennzeichnungen auf Ihre Schemata oder auf einen Datensatz in Experience Platform insgesamt anwenden können.

>[!VIDEO](https://video.tv.adobe.com/v/3422789/?captions=ger&learn=on)
