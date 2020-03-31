---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Data Governance
topic: overview
translation-type: tm+mt
source-git-commit: 4a60956ade2d742ac83e138a2921a6a4893e06ef

---


# Data Governance – Übersicht

Eine der Kernfunktionen der Adobe Experience Platform besteht darin, Daten aus mehreren Unternehmenssystemen zusammenzuführen, damit Marketingexperten Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Es ist daher wichtig sicherzustellen, dass Ihre Datenoperationen innerhalb der Plattform mit den Datenverwendungsrichtlinien konform sind.

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Es spielt eine Schlüsselrolle in der Experience Platform auf verschiedenen Ebenen, wie z.B. Katalogisierung, Datennutzungsbeschriftung, Datenverwendungsrichtlinien und Steuerung der Nutzung von Daten für Marketingaktionen.

## Datenverwaltungsfunktionen

Das Konzept der Datenverwaltung ist weder automatisch, noch tritt sie in einem Vakuum auf. Was als eine Rolle für eine Einzelperson begann, die normalerweise als **Datenverwalter** anerkannt wird, ist mit der Erweiterung des Ökosystems zur Datenverwaltung erheblich gewachsen. Die Datenverwaltung erfordert eine kontinuierliche Verwaltung und Überwachung, um erfolgreich zu sein, und setzt darauf, dass Datenmanager über Werkzeuge verfügen, mit denen Daten ordnungsgemäß gekennzeichnet werden können, Nutzungsrichtlinien erstellt werden können und die Einhaltung dieser Richtlinien erzwungen werden kann.

Während die Datenverwaltung in die Verantwortung jedes Einzelnen in der Organisation fallen sollte, sind hier einige der wesentlichen Rollen innerhalb des Datenmanagementzyklus:

![Datenverwaltungsrollen](./images/overview/roles.png)

### Datenstatus

Datenmanager sind das Herzstück der Datenverwaltung. Diese Rolle ist verantwortlich für die Interpretation von Regulierungen, vertraglichen Beschränkungen und Richtlinien und deren direkte Anwendung auf die Daten. Indem sie diese Regeln, Einschränkungen und Richtlinien verstehen, beinhaltet die Rolle eines Datenführers Folgendes:

* Überprüfen von Daten, Datensätzen und Datenmustern, um die Beschriftung zur Verwendung von Metadaten anzuwenden und zu verwalten.
* Erstellen von Datenrichtlinien und Anwenden auf Datensätze und Felder.
* Übermittlung von Datenrichtlinien an das Unternehmen.

### Marketer

Marketingexperten sind der Endpunkt der Datenverwaltung. Sie fordern Daten von der Infrastruktur zur Datenverwaltung an, die von Datenführern, Wissenschaftlern und Ingenieuren geschaffen wurde. Marketingexperten bieten unter dem Marketing-Schirm eine Reihe unterschiedlicher Spezialitäten, darunter:

* Marketing-Analysten fordern Daten an, um ein Verständnis der Kunden sowohl als Einzelpersonen als auch in Gruppen (auch als Segmente bezeichnet) zu ermöglichen.
* Marketing-Spezialisten und Experience Designer verwenden Daten, um neue Kundenerlebnisse zu entwerfen.


## DULE-Framework

Datennutzungskennzeichnung und -durchsetzung (DULE) ist das Kernframework für die Datenverwaltung in der Experience Platform. DULE vereinfacht und optimiert den Prozess der Kategorisierung von Daten und Erstellung von Datenverwendungsrichtlinien. Sobald Datenbeschriftungen angewendet und Datenverwendungsrichtlinien eingeführt wurden, können Marketingaktionen ausgewertet werden, um die korrekte Verwendung der Daten sicherzustellen.

Das DUL-Framework umfasst drei Kernelemente: Bezeichnungen, Richtlinien und Durchsetzung.

1. **Beschriftungen:** Klassifizieren Sie Daten, die datenschutzbezogene Erwägungen und Vertragsbedingungen widerspiegeln, entsprechend den Vorschriften und den Richtlinien der Organisation.
1. **Richtlinien:** Beschreiben Sie, welche Art(en) von Marketingaktionen für bestimmte Daten zulässig oder nicht zulässig sind.
1. **Durchsetzung:** Verwendet den Richtlinienrahmen, um Richtlinien über verschiedene Datenzugriffsmuster hinweg zu beraten und durchzusetzen.

## Datenverwendungsbeschriftungen

Die Datenverwaltung ermöglicht es Datenführern, Nutzungsbezeichnungen auf der Dataset- und Feldebene anzuwenden, um Daten entsprechend den jeweiligen Richtlinien zu kategorisieren.

Das DULE-Framework enthält vordefinierte Datenverwendungsbeschriftungen, mit denen Daten auf vier Arten kategorisiert werden können:

![Kategorien zur Bezeichnung der Datenverwendung](./images/overview/label-categories.png)

* **Vertragsdatenbezeichnungen &quot;C&quot;:** Kennzeichnen und Kategorisieren von Daten, die vertragliche Verpflichtungen haben oder mit den Richtlinien zur Verwaltung von Kundendaten in Zusammenhang stehen.
* **Identitäts-&quot;I&quot;-Datenbezeichnungen:** Kennzeichnen und Kategorisieren von Daten, die eine bestimmte Person identifizieren oder kontaktieren können.
* **Sensible &quot;S&quot;-Datenbezeichnungen:** Beschriften und Kategorisieren von Daten, die mit sensiblen Daten wie geografischen Daten zusammenhängen.
* **GDPR-Datenbeschriftungen:** Kennzeichnen und Kategorisieren von Daten, die persönliche IDs für den Zugriff auf GDPR und/oder Löschanforderungen enthalten können.

>[!NOTE] Eine vollständige Liste der verfügbaren Beschriftungen sowie Definitionen für jeden Beschriftungstyp finden Sie im Handbuch zu den [unterstützten Datenverwendungsbezeichnungen](labels/reference.md) .

Bezeichnungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practice empfiehlt die Kennzeichnung von Daten, sobald diese in die Experience Platform integriert werden oder sobald Daten in Platform verfügbar sind.

Eine schrittweise Anleitung zum Anwenden von Beschriftungen auf Datasets und Felder mithilfe der Benutzeroberfläche finden Sie in der Übersicht über die [Datenverwendungsbeschriftungen](./labels/overview.md) .

## Datenverwendungsrichtlinien

Damit Datenverwendungsbeschriftungen die Datenkonformität effektiv unterstützen können, müssen Datenverwendungsrichtlinien implementiert werden. Datenverwendungs-Richtlinien sind Regeln, die die Arten von Marketingaktionen beschreiben, die Sie für Daten in Experience Platform ausführen dürfen oder von denen Sie eingeschränkt sind.

Ein Beispiel für eine Marketingaktion könnte der Wunsch sein, einen Datensatz in einen Drittanbieter-Service zu exportieren. Wenn eine Richtlinie besagt, dass bestimmte Datentypen, wie z. B. persönliche identifizierbare Informationen (PII), nicht exportiert werden können und eine &quot;I&quot;-Beschriftung (Identitätsdaten) auf den Datensatz angewendet wurde, erhalten Sie eine Antwort des Policy Service, in der Sie darauf hingewiesen werden, dass eine Datenverwendungsrichtlinie verletzt wurde.

### So erstellen und arbeiten Sie mit Datenverwendungsrichtlinien

Nachdem die Datenverwendungsbeschriftungen angewendet wurden, können Datenverwaltungen Richtlinien mit der API des DULE Policy Service erstellen.

Als Datenmanager können Sie die Policy Service API verwenden, um Richtlinien im Zusammenhang mit Marketingaktionen zu verwalten und auszuwerten, die für Daten mit DULE-Beschriftungen durchgeführt werden. Mithilfe der API können Sie Richtlinien erstellen und aktualisieren, den Status einer Richtlinie ermitteln und mit Marketingaktionen bewerten, ob eine bestimmte Aktion eine Datenverwendungsrichtlinie verletzt.

Innerhalb der Policy Service-API werden alle Richtlinien und Marketingaktionen als entweder `core` oder `custom` Ressourcen bezeichnet. `core` Ressourcen werden von Adobe definiert und verwaltet, während `custom` Ressourcen von einzelnen Kunden erstellt und gepflegt werden. Die `custom` Ressourcen sind daher einzigartig und nur für die Organisation sichtbar, die sie geschaffen hat.

Weitere Informationen zum Ausführen der von der DUL Policy Service API bereitgestellten wichtigen Vorgänge finden Sie im Entwicklerhandbuch für den [Policy Service](api/getting-started.md). Eine schrittweise Anleitung zum Arbeiten mit DULE-Richtlinien finden Sie im Lernprogramm zum [Erstellen und Evaluieren von DULE-Richtlinien](policies/create.md).

## Zukünftige Versionen

Die Datenverwaltung unterstützt derzeit die DULE-Kennzeichnung auf zwei Ebenen (Datensatz und Feld). Die Datenverwaltung unterstützt auch die Erstellung und Verwaltung von Datenverwendungsrichtlinien und Marketingaktionen über die DUL Policy Service API.

Nachfolgende Versionen bieten die folgenden Funktionen:

* Benutzerdefinierte Datenverwendungsbeschriftungen: Erstellen Sie neue Beschriftungen und Definitionen entsprechend den Anforderungen Ihres Unternehmens.
* Durchsetzung der Politik: Verwenden Sie den Richtlinienrahmen, um Richtlinien über verschiedene Datenzugriffsmuster hinweg zu beraten und durchzusetzen.
* Prüfung: Überwachen Sie die Aktivitäten des Datenzugriffs und identifizieren Sie Compliance-Probleme und erstellen Sie Berichte zu diesen Problemen.

## Nächste Schritte

Dieses Dokument bot eine Einführung in die Datenverwaltung und das DUL-Framework auf hoher Ebene. Sie können nun mit dem Benutzerhandbuch [zur](labels/user-guide.md) Datenverwendung fortfahren und Ihren Erlebnisdaten Gebrauchsbeschriftungen hinzufügen.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zur Datenverwaltung.

### Terminologie der Datenverwaltung

In der folgenden Tabelle sind die Schlüsselbegriffe im Zusammenhang mit der Datenverwaltung und dem DUL-Rahmen aufgeführt.

| Begriff | Definition |
|---|---|
| **Vertragsbezeichnungen** | Die &quot;C&quot;-Beschriftungen des Vertrags werden zur Kategorisierung von Daten verwendet, die vertragliche Verpflichtungen haben oder mit den Datenschutzrichtlinien Ihres Unternehmens in Zusammenhang stehen. |
| **Site-übergreifende Daten** | Site-übergreifende Daten sind die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Vor-Ort-Daten und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen. |
| **Datenverwaltung** | Die Datenverwaltung umfasst die Strategien und Technologien, mit denen sichergestellt werden soll, dass die Daten in Übereinstimmung mit den Vorschriften und Unternehmensrichtlinien zur Datenverwendung stehen. |
| **Datenstatus** | Der Datenverwalter ist die Person, die für die Verwaltung, Überwachung und Durchsetzung der Datenbestände einer Organisation verantwortlich ist. Ein Datenmanager stellt außerdem sicher, dass die Datenschutzrichtlinien geschützt und so aufrechterhalten werden, dass sie mit den Regierungs- und Organisationspolitiken im Einklang stehen. |
| **Datenverwendungsbeschriftungen** | Datenverwendungsbeschriftungen bieten Benutzern die Möglichkeit, Daten zu kategorisieren, die datenschutzbezogene Erwägungen und Vertragsbedingungen widerspiegeln, damit sie mit Vorschriften und Unternehmensrichtlinien übereinstimmen. |
| **Datenbeschriftungen** | Bezeichnungen können einem Datensatz hinzugefügt werden. Alle Felder in einem Datensatz übernehmen die Beschriftungen des Datensatzes. |
| **DULE** | DULE ist ein Akronym für &quot;Datenverwendung - Kennzeichnung und Durchsetzung&quot;. DULE ist ein wichtiger Bestandteil der Datenverwaltung und bietet Funktionen, die eine Datenverwendungskennzeichnung und die Anwendung von Datenzugriffsrichtlinien für Governance-Anforderungen in einem Unternehmen ermöglichen. |
| **Feldbeschriftungen** | Feldbezeichnungen sind Bezeichnungen zur Datenverwaltung, die entweder von einem Datensatz übernommen oder direkt auf ein Feld angewendet werden.  Auf ein Feld angewendete Datenverwaltungs-Beschriftungen werden nicht bis zu einem Datensatz geerbt. |
| **Geofence** | Eine Geofence ist eine virtuelle geografische Grenze, die durch GPS- oder RFID-Technologie definiert wird und die Software in die Lage versetzt, eine Antwort auszulösen, wenn ein Mobilgerät ein bestimmtes Gebiet betritt oder verlässt. |
| **Beschriftungen** | Identitäts-&quot;I&quot;-Beschriftungen werden zur Kategorisierung von Daten verwendet, die eine bestimmte Person identifizieren oder kontaktieren können. |
| **Interessensbasiertes Targeting** | Interessensbasiertes Targeting, auch Personalisierung genannt, tritt auf, wenn die folgenden drei Bedingungen erfüllt sind: Daten, die vor Ort gesammelt werden, werden verwendet, um Rückschlüsse auf das Interesse eines Benutzers zu ziehen, werden in einem anderen Kontext verwendet, z. B. auf einer anderen Site oder App (außerhalb der Site), und werden verwendet, um festzulegen, welche Inhalte oder Anzeigen auf der Grundlage dieser Schlussfolgerungen bereitgestellt werden. |
| **Marketingaktion** | Eine Marketingaktion im Kontext des Data Governance-Rahmens ist eine Aktion, die ein Datennutzer von Experience Platform durchführt und bei der überprüft werden muss, ob gegen die Datenverwendungsrichtlinien verstoßen wurde |
| **Politik** | Im Rahmen der Datenverwaltung ist eine Richtlinie eine Regel, die beschreibt, welche Marketingaktionen für bestimmte Daten zulässig oder nicht zulässig sind. |
| **Sensible Beschriftungen** | Sensible &quot;S&quot;-Beschriftungen werden verwendet, um Daten zu kategorisieren, die Sie und Ihr Unternehmen als vertraulich betrachten. |

## Zusätzliche Ressourcen   

Das folgende Video soll Ihnen dabei helfen, die Datenverwaltung zu verstehen, und zeigt die wichtigsten Aspekte des Rahmenwerks zur Datenbenennung und -durchsetzung (DULE) auf.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)
