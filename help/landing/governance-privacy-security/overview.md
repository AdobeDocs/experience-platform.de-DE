---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Governance, Datenschutz und Sicherheitsübersicht
topic: Übersicht
description: Adobe Experience Platform bietet verschiedene Services und Tools, mit denen Sie Ihre erfassten Erlebnisdaten vertraulich steuern können, um Ihren Geschäftspraktiken, rechtlichen Verpflichtungen und Entwicklungsprozessen zu entsprechen.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
translation-type: tm+mt
source-git-commit: 3f7808a08d033c5940d2115006c269b8c4079822
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 18%

---

# Governance, Datenschutz und Sicherheit in Adobe Experience Platform

Mit Adobe Experience Platform können Sie Ihre Daten erfassen, analysieren, optimieren und handeln, um die Kundenerfahrung deutlich zu verbessern. Diese Daten sind riesig, komplex und unglaublich wertvoll. Abhängig von der Art Ihres Datenbetriebs, den gesetzlichen Bestimmungen, unter denen Ihr Unternehmen tätig ist, und Ihren organisatorischen Richtlinien zur Datenverwendung müssen Sie die Erfassung und Verwendung von Kundenerlebnisdaten sorgfältig kontrollieren und überwachen, um Ihre Geschäftsinteressen zu schützen.

Experience Platform bietet verschiedene Services und Tools, mit denen Sie Ihre erfassten Erlebnisdaten vertraulich steuern können, um Ihren Geschäftspraktiken, rechtlichen Verpflichtungen und Entwicklungsprozessen zu entsprechen. Die folgenden Abschnitte enthalten eine Einführung zu jedem dieser Dienste sowie Links zur Dokumentation für weitere Informationen.

Die Dienste können in drei Domänen kategorisiert werden:

* [Data Governance](#governance)
* [Datenschutz](#privacy)
* [Sicherheit](#security)

## Data Governance {#governance}

Die Datenverwaltung ist ein unverzichtbares Konzept, das mit jeder Fähigkeit in der Experience Platform verknüpft ist. Die Datenverwaltung stellt Ihre Fähigkeit dar, Ihre Daten über die gesamte Journey-Plattform zu steuern und zu verstehen. Dazu gehören die Erhaltung der Datenqualität, der Datenreihenfolge, der Datenkatalogisierung und mehr.

### Adobe Experience Platform Data Governance {#data-governance}

Als Plattformdienst ermöglicht Ihnen die Adobe Experience Platform Data Governance die Verwaltung von Kundendaten und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung. Es spielt eine Schlüsselrolle in der Experience Platform auf verschiedenen Ebenen, wie z.B. die Kennzeichnung der Datenverwendung, Datenverwendungsrichtlinien, die Durchsetzung von Richtlinien und die Datenleitung.

Weitere Informationen finden Sie unter [Übersicht über die Datenverwaltung](../../data-governance/home.md).

### Katalog und Datensätze {#catalog}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Platform. Alle Daten, die in Experience Platform aufgenommen werden, werden als Dateien und Ordner im Data Lake gespeichert. Der Katalog wiederum speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

Der Katalog ordnet die erfassten Daten in Datensätze zusammen, wobei jeder Datensatz Metadaten enthält, mit denen die darin enthaltenen Daten beschriftet und kategorisiert werden können.

Weitere Informationen zum Dienst finden Sie unter [Übersicht über den Katalogdienst](../../catalog/home.md). Informationen zum Verwalten von Datensätzen in Experience Platform finden Sie unter [Übersicht über Datensätze](../../catalog/datasets/overview.md).

## Datenschutz {#privacy}

Privatsphäre ist ein kritisches Problem für Ihr Unternehmen, Ihre Gesetzgeber und Ihre Kunden. Da personenbezogene Daten, die von Ihren Kunden gesammelt werden, im Mittelpunkt nahezu aller Workflows Experience Platformen stehen, bietet Platform Dienstleistungen zur Unterstützung dieser Initiativen.

### Adobe Experience Platform Privacy Service {#privacy-service}

Rechtliche Datenschutzbestimmungen wie die Datenschutzverordnung der Europäischen Vereinigung (GDPR) und das kalifornische Verbraucherschutzgesetz (CCPA) gewähren den Bürgern in ihrem Hoheitsgebiet das Recht, auf die von Ihnen erfassten und gespeicherten personenbezogenen Daten zuzugreifen und sie zu löschen.

Adobe Experience Platform Privacy Service stellt eine RESTful-API und eine Benutzeroberfläche zur Verfügung, die bei der Verwaltung dieser Anforderungen helfen. Mit Privacy Service können Sie Anfragen zum Zugriff auf oder Löschen von persönlichen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

Weiterführende Informationen dazu finden Sie unter [Übersicht zum Privacy Service](../../privacy-service/home.md).

### Verarbeitung der Zustimmung {#consent}

In vielen gesetzlichen Datenschutzbestimmungen wurden Anforderungen an die aktive und spezifische Zustimmung bei der Datenerfassung, Personalisierung und anderen Marketingzwecken eingeführt. Um diese Anforderungen zu erfüllen, ermöglicht Ihnen die Experience Platform die Erfassung von Informationen zur Einwilligung in einzelnen Profilen und die Verwendung dieser Präferenzen als entscheidenden Faktor für die Verwendung der Daten der einzelnen Kunden in den nachgelagerten Plattform-Workflows.

Informationen zur Verarbeitung von Daten zur Kundeneinwilligung und zu Kundenpräferenzen mithilfe des Standards für Adoben finden Sie in der Übersicht zur [Verarbeitung der Einwilligung in Experience Platform](./consent/adobe/overview.md).

Informationen darüber, wie Daten zur Kundeneinwilligung gemäß dem IAB-Transparenz- und -Zustimmung-Framework (TCF) 2.0 verarbeitet werden, finden Sie in der Übersicht über die Unterstützung für die IAB-TCF 2.0 in Platform](./consent/iab/overview.md).[

## Sicherheit {#security}

Die Integrität und Sicherheit Ihrer Daten ist unverzichtbar für Ihr Unternehmen, und dieses Risiko erfordert branchenführende Sicherheitsfunktionen. Um diese Herausforderung zu meistern, bietet Platform verschiedene Tools zum Schutz Ihrer Datenvorgänge.

### Zugriffskontrolle {#access-control}

Experience Platform nutzt das Adobe Admin Console, um verschiedene Plattformfunktionen rollenbasierter Zugriffskontrolle zu bieten. Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen.

Weiterführende Informationen dazu finden Sie unter [Zugriffskontrolle – Übersicht](../../access-control/home.md).

### Sandboxes {#sandboxes}

Experience Platform wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

Um die erforderliche Entwicklungsflexibilität zu gewährleisten, bietet Experience Platform Sandboxen, die eine einzelne Plattforminstanz in separate virtuelle Umgebung aufteilen, damit Sie Ihre digitalen Erlebnisanwendungen auf Grundlage Ihres eigenen Entwicklungszyklus entwickeln können.

Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die verschiedenen Plattformdienste und -werkzeuge, die mit der Datenverwaltung, dem Datenschutz und der Datensicherheit verbunden sind. Weitere Informationen zu diesen Funktionen finden Sie in der Dokumentation zu diesem Handbuch.
