---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Governance, Datenschutz und Sicherheitsübersicht
description: Adobe Experience Platform bietet verschiedene Dienste und Tools, mit denen Sie Ihre erfassten Erlebnisdaten sicher steuern können, um Ihre Geschäftspraktiken, rechtlichen Verpflichtungen und Ihren Entwicklungsprozess einzuhalten.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 18%

---

# Governance, Datenschutz und Sicherheit in Adobe Experience Platform

Mit Adobe Experience Platform können Sie Ihre Daten erfassen, analysieren, optimieren und einsetzen, um Kundenerlebnisse deutlich zu verbessern. Diese Daten sind riesig, komplex und unglaublich wertvoll. Je nach Art Ihres Datenbetriebs, den gesetzlichen Bestimmungen, unter denen Ihr Unternehmen tätig ist, und Ihren organisatorischen Richtlinien zur Datennutzung müssen Sie die Erfassung und Verwendung von Kundenerlebnisdaten sorgfältig kontrollieren und überwachen, um Ihre Geschäftsinteressen zu schützen.

Experience Platform bietet verschiedene Dienste und Tools, mit denen Sie Ihre erfassten Erlebnisdaten sicher steuern können, um Ihre Geschäftspraktiken, rechtlichen Verpflichtungen und Entwicklungsprozesse einzuhalten. In den folgenden Abschnitten finden Sie eine Einführung in diese Dienste sowie Links zur Dokumentation für weitere Informationen.

Die Dienste können in drei Domänen unterteilt werden:

* [Data Governance](#governance)
* [Datenschutz   ](#privacy)
* [Sicherheit](#security)

## Data Governance {#governance}

Data Governance ist ein wesentliches Konzept, das mit allen Funktionen in der Experience Platform verknüpft ist. Data Governance stellt Ihre Fähigkeit dar, Ihre Daten über Platform im gesamten Journey zu steuern und zu verstehen. Dazu gehört die Aufrechterhaltung der Datenqualität, der Datenherkunft, der Datenkatalogisierung und mehr.

### Adobe Experience Platform Data Governance {#data-governance}

Als Platform-Dienst können Sie mit Adobe Experience Platform Data Governance Kundendaten verwalten und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sicherstellen. Sie spielt in der Experience Platform auf verschiedenen Ebenen eine Schlüsselrolle, einschließlich Datennutzungsbeschriftung, Datennutzungsrichtlinien, Richtliniendurchsetzung und Datenherkunft.

Siehe [Data Governance - Übersicht](../../data-governance/home.md) für weitere Informationen.

### Katalog und Datensätze {#catalog}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Platform. Alle Daten, die in Experience Platform aufgenommen werden, werden als Dateien und Ordner im Data Lake gespeichert. Der Katalog wiederum speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

Catalog organisiert erfasste Daten in Datensätzen, wobei jeder Datensatz Metadaten enthält, die zum Beschriften und Kategorisieren der darin enthaltenen Daten verwendet werden können.

Siehe [Catalog Service - Übersicht](../../catalog/home.md) für weitere Informationen zum Dienst. Informationen zum Verwalten von Datensätzen in Experience Platform finden Sie unter [Datensätze - Übersicht](../../catalog/datasets/overview.md).

## Datenschutz    {#privacy}

Privatsphäre ist ein wichtiges Thema für Ihr Unternehmen, Ihre Gesetzgeber und Ihre Kunden. Da personenbezogene Daten, die von Ihren Kunden erfasst werden, im Mittelpunkt fast aller Experience Platform-Workflows stehen, bietet Platform Dienste zur Unterstützung dieser Initiativen.

### Adobe Experience Platform Privacy Service {#privacy-service}

Durch gesetzliche Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) der Europäischen Union und der California Consumer Privacy Act (CCPA) erhalten Bürger innerhalb ihrer Rechtsordnungen das Recht, auf die von Ihnen erfassten und darin gespeicherten personenbezogenen Daten zuzugreifen und diese zu löschen.

Adobe Experience Platform Privacy Service bietet eine RESTful-API und eine Benutzeroberfläche, die bei der Verwaltung dieser Anfragen helfen. Mit Privacy Service können Sie Anfragen zum Zugriff auf oder zum Löschen von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, um die automatische Einhaltung gesetzlicher und organisatorischer Datenschutzbestimmungen zu erleichtern.

Weiterführende Informationen dazu finden Sie unter [Übersicht zum Privacy Service](../../privacy-service/home.md).

### Verarbeitung der Zustimmung {#consent}

Viele gesetzliche Datenschutzbestimmungen haben Anforderungen an die aktive und spezifische Einwilligung in Bezug auf Datenerfassung, Personalisierung und andere Marketing-Anwendungsfälle eingeführt. Um diese Anforderungen zu erfüllen, können Sie mit Experience Platform Einwilligungsinformationen in einzelnen Kundenprofilen erfassen und diese Voreinstellungen als entscheidenden Faktor für die Verwendung der Kundendaten in nachgelagerten Platform-Workflows verwenden.

Informationen zur Verarbeitung von Einwilligungs- und Präferenzdaten von Kunden mithilfe des Adobe-Standards finden Sie in der Übersicht unter [Zustimmungsverarbeitung in Experience Platform](./consent/adobe/overview.md).

Informationen dazu, wie Kundenzustimmungsdaten gemäß dem IAB Transparency and Consent Framework (TCF) 2.0 verarbeitet werden, finden Sie in der Übersicht unter [IAB TCF 2.0-Unterstützung in Platform](./consent/iab/overview.md).

## Sicherheit {#security}

Die Integrität und Sicherheit Ihrer Daten ist für Ihr Unternehmen unverzichtbar, und dieses Risiko erfordert branchenführende Sicherheitsfunktionen. Um diese Herausforderung zu meistern, bietet Platform verschiedene Tools zum Schutz Ihrer Datenvorgänge.

### Datenverschlüsselung

Alle Platform-Daten werden im Transit und im Ruhezustand verschlüsselt. Siehe Dokument unter [Datenverschlüsselung in Platform](./encryption.md) für weitere Informationen.

### Zugangssteuerung {#access-control}

Experience Platform verwendet die Adobe Admin Console, um rollenbasierte Zugriffskontrolle für verschiedene Platform-Funktionen bereitzustellen. Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen.

Weiterführende Informationen dazu finden Sie unter [Zugangssteuerung – Übersicht](../../access-control/home.md).

### Sandboxes {#sandboxes}

Experience Platform wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

Um Entwicklungsflexibilität zu gewährleisten, bietet Experience Platform Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, damit Sie Ihre Digital Experience Apps basierend auf Ihrem eigenen Entwicklungslebenszyklus entwickeln können.

Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die verschiedenen Platform-Dienste und -Tools, die mit Data Governance, Datenschutz und Sicherheit verbunden sind. Weitere Informationen zu diesen Funktionen finden Sie in der Dokumentation zu diesen Funktionen.
