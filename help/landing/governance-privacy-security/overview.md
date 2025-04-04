---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Governance, Datenschutz und Sicherheit - Übersicht
description: Adobe Experience Platform bietet verschiedene Services und Tools, mit denen Sie Ihre erfassten Erlebnisdaten gemäß Ihren Geschäftspraktiken, Ihren rechtlichen Verpflichtungen und Ihrem Entwicklungsprozess sicher steuern können.
feature: Data Governance,Privacy
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 22%

---

# Governance, Datenschutz und Sicherheit in Adobe Experience Platform

Mit Adobe Experience Platform können Sie Ihre Daten aufnehmen, analysieren, optimieren und bearbeiten, um das Kundenerlebnis deutlich zu verbessern. Diese Daten sind riesig, komplex und unglaublich wertvoll. Abhängig von der Art Ihrer Datenvorgänge, den rechtlichen Zuständigkeiten, unter denen Ihr Unternehmen tätig ist, und Ihren organisatorischen Richtlinien zur Datennutzung müssen Sie die Erfassung und Verwendung von Kundenerlebnisdaten sorgfältig kontrollieren und überwachen, um Ihre Geschäftsinteressen zu schützen.

Experience Platform bietet verschiedene Services und Tools, mit denen Sie Ihre erfassten Erlebnisdaten sicher kontrollieren können, um Ihre Geschäftspraktiken, rechtlichen Verpflichtungen und Entwicklungsprozesse einzuhalten. In den folgenden Abschnitten finden Sie eine Einführung in jeden dieser Services sowie Links zur Dokumentation, die weitere Informationen bietet.

Die Dienste können in drei Bereiche unterteilt werden:

* [Data Governance](#governance)
* [Datenschutz   ](#privacy)
* [Sicherheit](#security)

## Data Governance {#governance}

Data Governance ist ein wesentliches Konzept, das mit allen Funktionen in Experience Platform verknüpft ist. Data Governance stellt Ihre Fähigkeit dar, Ihre Daten während ihres gesamten Journey über Experience Platform zu kontrollieren und zu erfassen. Dazu gehört die Aufrechterhaltung der Datenqualität, der Datenherkunft, der Datenkatalogisierung und mehr.

### Data Governance in Adobe Experience Platform {#data-governance}

Als Experience Platform-Service können Sie mit Adobe Experience Platform Data Governance Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von relevanten Vorschriften, Einschränkungen und Richtlinien sicherstellen. Die Funktion spielt in Experience Platform auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Datennutzungskennzeichnungen, Datennutzungsrichtlinien, der Durchsetzung von Richtlinien und der Datenherkunft.

Weitere Informationen finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md).

### Katalog und Datensätze {#catalog}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Experience Platform. Alle Daten, die in Experience Platform aufgenommen werden, werden als Dateien und Ordner im Data Lake gespeichert. Der Katalog wiederum speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

Katalog organisiert aufgenommene Daten in Datensätze, wobei jeder Datensatz Metadaten enthält, die zur Kennzeichnung und Kategorisierung der darin enthaltenen Daten verwendet werden können.

Weitere Informationen zu [ Service finden Sie ](../../catalog/home.md) der Übersicht zum Katalog-Service . Informationen zum Verwalten von Datensätzen in Experience Platform finden Sie unter [Datensätze - Übersicht](../../catalog/datasets/overview.md).

## Datenschutz    {#privacy}

Datenschutz ist ein wichtiges Thema für Ihr Unternehmen, Ihre Gesetzgeber und Ihre Kunden. Da personenbezogene Daten von Ihren Kunden im Mittelpunkt fast aller Experience Platform-Workflows stehen, bietet Experience Platform Services zur Unterstützung dieser Initiativen.

### Adobe Experience Platform Privacy Service {#privacy-service}

Rechtliche Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) der Europäischen Union und der California Consumer Privacy Act (CCPA) gewähren Bürgern in ihrem Zuständigkeitsbereich das Recht, auf die von Ihnen erfassten und gespeicherten personenbezogenen Daten zuzugreifen und sie zu löschen.

Adobe Experience Platform Privacy Service bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung dieser Anfragen unterstützen. Mit Privacy Service können Sie Anfragen für den Zugriff auf oder die Löschung von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Programmen stellen, was die automatische Einhaltung gesetzlicher und unternehmensinterner Datenschutzbestimmungen erleichtert.

Weitere Informationen finden Sie in der Übersicht ](../../privacy-service/home.md) [Privacy Service .

### Einverständnisverarbeitung {#consent}

Viele gesetzliche Datenschutzbestimmungen haben Anforderungen für aktive und spezifische Einverständnisse bei der Datenerfassung, Personalisierung und anderen Marketing-Anwendungsfällen eingeführt. Um diese Anforderungen zu erfüllen, können Sie mit Experience Platform Einverständnisinformationen in individuellen Kundenprofilen erfassen und diese Voreinstellungen als bestimmenden Faktor dafür verwenden, wie die Daten jedes Kunden in nachgelagerten Experience Platform-Workflows verwendet werden.

Informationen zur Verarbeitung von Einverständnis- und Präferenzdaten von Kunden mit dem Adobe-Standard finden Sie in der Übersicht zur [Einverständnisverarbeitung in Experience Platform](./consent/adobe/overview.md).

Informationen zur Verarbeitung von Kundeneinverständnisdaten gemäß dem IAB Transparency and Consent Framework (TCF) 2.0 finden Sie in der Übersicht zur [IAB TCF 2.0-Unterstützung in Experience Platform](./consent/iab/overview.md).

## Sicherheit {#security}

Die Integrität und Sicherheit Ihrer Daten ist für Ihr Unternehmen unverzichtbar, und dieses Risiko erfordert branchenführende Sicherheitsfunktionen. Um dieser Herausforderung gerecht zu werden, bietet Experience Platform verschiedene Tools, mit denen Sie Ihre Datenvorgänge schützen können.

### Datenverschlüsselung

Alle Experience Platform-Daten werden während der Übertragung und im Ruhezustand verschlüsselt. Weitere Informationen finden Sie im Dokument über [Datenverschlüsselung in Experience Platform](./encryption.md).

### Zugangssteuerung {#access-control}

Experience Platform verwendet Adobe Admin Console, um rollenbasierte Zugriffssteuerung für verschiedene Experience Platform-Funktionen bereitzustellen. Diese Funktion nutzt Produktprofile in Admin Console, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen.

Weiterführende Informationen dazu finden Sie unter [Zugangssteuerung – Übersicht](../../access-control/home.md).

### Sandboxes {#sandboxes}

Experience Platform wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

Um dem Bedarf an Entwicklungsflexibilität gerecht zu werden, stellt Experience Platform Sandboxes bereit, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Ihre Programme für digitale Erlebnisse basierend auf Ihrem eigenen Entwicklungslebenszyklus weiterentwickeln können.

Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die verschiedenen Experience Platform-Services und -Tools, die mit Data Governance, Datenschutz und Sicherheit zusammenhängen. Weitere Informationen zu diesen Funktionen finden Sie in der Dokumentation, auf die an mehreren Stellen in diesem Handbuch verwiesen wird.
