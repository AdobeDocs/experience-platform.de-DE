---
title: Best Practices für die Verwaltung von Daten im Rahmen von Lizenzberechtigungen
description: Erfahren Sie mehr über Best Practices und Werkzeuge, die Sie zur besseren Verwaltung Ihrer Lizenzberechtigungen mit Adobe Experience Platform einsetzen können.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 65%

---

# Best Practices für die Verwaltung von Daten im Rahmen von Lizenzberechtigungen

Adobe Experience Platform ist ein offenes System, das Ihre Daten in Kundenprofile umwandelt, die in Echtzeit aktualisiert werden. Darüber hinaus nutzt Adobe Experience Platform KI-gestützte Einblicken, mithilfe derer Sie auf allen Kanälen ansprechende Erlebnisse bereitstellen können. Sie können Daten unterschiedlicher Art, Menge und Historie mit Hilfe von Quellen in Experience Platform einspeisen und diese Daten dann für Anwendungsfälle nutzen – von der Segmentierung und Personalisierung bis hin zu Analysen und maschinellem Lernen.

Experience Platform bietet Lizenzen an, die die Anzahl der Profile, die Sie erstellen können, und die Menge der Daten, die Sie einbringen können, festlegen. Da Sie Daten aus beliebigen Quellen, mit beliebigem Volumen und beliebiger Historie einbringen können, kann es vorkommen, dass Sie das Limit Ihrer Lizenzberechtigungen überschreiten, wenn Ihr Datenvolumen wächst.

In diesem Dokument werden Best Practices und Tools beschrieben, mit denen Sie Ihre Lizenzberechtigungen mit Adobe Experience Platform besser verwalten können.

## Grundlagen zur Datenspeicherung in Adobe Experience Platform

Experience Platform besteht im Wesentlichen aus zwei Datenspeichern: dem [!DNL data lake] und dem Profilspeicher.

Der **[!DNL data lake]** dient hauptsächlich folgenden Zwecken:

* Fungiert als Staging-Bereich für das Onboarding von Daten in Experience Platform;
* Fungiert als langfristiger Datenspeicher für alle Daten in Experience Platform;
* Ermöglicht Anwendungsfälle wie die Datenanalyse und Datenwissenschaft.

Der **Profilspeicher** ist der Ort, an dem Kundenprofile erstellt werden. Er hat vor allem folgende Aufgaben:

* Fungiert als Datenspeicher für Profile, die zur Bereitstellung von Echtzeit-Erlebnissen verwendet werden;
* Aktiviert Anwendungsfälle wie die Segmentierung, Aktivierung und Personalisierung.

>[!NOTE]
>
>Ihr Zugriff auf den [!DNL data lake] kann von der von Ihnen erworbenen Produkt-SKU abhängen. Weitere Informationen zu Produkt-SKUs erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

## Lizenznutzung {#license-usage}

Wenn Sie eine Lizenz für Experience Platform erwerben, erhalten Sie Lizenznutzungsberechtigungen, die je nach SKU variieren:

**[!DNL Addressable Audience]** – die Gesamtzahl der Kundenprofile, die vertraglich für Experience Platform zugelassen sind, einschließlich bekannter und pseudonymer Profile.

**[!DNL Total Data Volume]** : Die Gesamtmenge der für den Adobe Experience Platform-Profil-Service verfügbaren Daten, die in Interaktions-Workflows verwendet werden können.

Die Verfügbarkeit und spezifische Definition dieser Metriken hängen von der von Ihrem Unternehmen erworbenen Lizenz ab.

## Lizenznutzungs-Dashboard

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie einen Schnappschuss der Lizenzdaten Ihres Unternehmens für Experience Platform anzeigen können. Die Daten im Dashboard werden genau so angezeigt, wie sie zu dem Zeitpunkt erscheinen, an dem der Snapshot erstellt wurde. Der Snapshot ist weder ein Näherungswert noch eine Stichprobe von Daten, und das Dashboard wird nicht in Echtzeit aktualisiert.

Weitere Informationen finden Sie im Handbuch unter [Verwenden des Lizenznutzungs-Dashboards in der Experience Platform-Benutzeroberfläche](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Best Practices für das Daten-Management

In den folgenden Abschnitten finden Sie Best Practices für eine bessere Verwaltung Ihrer Daten.

### Grundlegendes zu Daten

Nicht alle Daten in Adobe Experience Platform sind gleich. Einige Daten mögen zwar reichlich vorhanden, aber von geringem Wert sein, während andere spärlich, aber von hohem Wert sind. Manche Daten können unmittelbar nach ihrer Erstellung an Wert verlieren, während andere monatelang, wenn nicht sogar jahrelang ihren Wert behalten.

Bei der Einschätzung des Werts Ihrer Daten sind drei Dimensionen zu beachten:

| Dimension | Beschreibung | Beispiel |
| --- | --- | --- |
| Volumen | Stellt die Menge und Gesamtheit der erfassten Daten dar. | Web-Klicks – hohes Volumen und mäßige Aussagekraft. Der Wert kann schnell abnehmen. |
| Zeitpanne | Stellt die Zeitdauer dar, während der die erfassten Daten nützlich sind. | Offline-Käufe – moderates Volumen und Aussagekraft, können aber über lange Zeit nützlich sein. |
| Aussagekraft | Gibt an, wie reich die Daten an Informationen sind. | Kundenkonten – geringes Datenvolumen, aber große Aussagekraft. Kann über die Kundenlebensdauer hinaus nützlich sein. |

### Daten-Management-Tools {#data-management-tools}

Es gibt zwei zentrale Überlegungen, die Sie berücksichtigen sollten, wenn Sie sicherstellen möchten, dass Ihre Datennutzung innerhalb der Limits Ihrer Lizenzberechtigung bleibt:

### Welche Daten integrieren Sie in Experience Platform?

Daten können in Experience Platform in ein oder mehrere Systeme aufgenommen werden, nämlich den [!DNL data lake] und/oder den Profilspeicher. Dies bedeutet, dass in beiden Systemen für eine Vielzahl verschiedener Anwendungsfälle unterschiedliche Daten vorhanden sein können. Beispielsweise können Sie historische Daten im [!DNL data lake] speichern, jedoch nicht im Profilspeicher. Sie können auswählen, welche Daten an den Profilspeicher gesendet werden sollen, indem Sie einen Datensatz für die Profilaufnahme aktivieren.

>[!NOTE]
>
>Ihr Zugriff auf den [!DNL data lake] kann von der von Ihnen erworbenen Produkt-SKU abhängen. Weitere Informationen zu Produkt-SKUs erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

### Welche Daten behalten Sie?

Sie können sowohl Datenaufnahme-Filter als auch Ablaufregeln anwenden, um Daten zu entfernen, die für Ihre Anwendungsfälle veraltet sind. In der Regel verbrauchen Verhaltensdaten (z. B. Analytics-Daten) wesentlich mehr Speicher als Datensatzdaten (z. B. CRM-Daten). Viele Experience Platform-Benutzer weisen beispielsweise bis zu 90 % Profile auf, die ausschließlich Verhaltensdaten enthalten, verglichen mit Datensatzdaten. Daher ist die Verwaltung Ihrer Verhaltensdaten von entscheidender Bedeutung, um die Einhaltung Ihrer Lizenzberechtigungen sicherzustellen.

Es gibt eine Reihe von Tools, die Ihnen helfen, Ihre Lizenznutzungsberechtigungen einzuhalten:

* [Aufnahmefilter](#ingestion-filters)
* [Profilspeicher](#profile-service)

### Identity Service und adressierbare Zielgruppe {#identity-service}

Identitätsdiagramme werden nicht auf Ihre gesamte adressierbare Zielgruppenberechtigung angerechnet, da sich adressierbare Zielgruppe auf Ihre Gesamtzahl an Kundenprofilen bezieht.

Aufgrund der Aufteilung von Identitäten können sich jedoch Beschränkungen des Identitätsdiagramms auf Ihre adressierbare Zielgruppe auswirken. Wenn beispielsweise die älteste ECID aus dem Diagramm entfernt wird, bleibt die ECID im Echtzeit-Kundenprofil als pseudonymes Profil bestehen. Sie können [Ablauf von Daten pseudonymer Profile](../../profile/pseudonymous-profiles.md) festlegen, um dieses Verhalten zu umgehen. Weitere Informationen finden Sie unter [ für Identity Service-Daten](../../identity-service/guardrails.md).

### Aufnahmefilter {#ingestion-filters}

Aufnahmefilter ermöglichen Ihnen, nur die für Ihre Anwendungsfälle erforderlichen Daten aufzunehmen und alle nicht erforderlichen Ereignisse herauszufiltern.

| Aufnahmefilter | Beschreibung |
| --- | --- |
| Adobe Audience Manager-Quellfilter | Wenn Sie eine Adobe Audience Manager-Quellverbindung erstellen, können Sie auswählen, welche Segmente und Merkmale in das [!DNL data lake]- und Echtzeit-Kundenprofil eingebracht werden sollen, anstatt alle Audience Manager-Daten zu erfassen. Weitere Informationen finden Sie in der Anleitung zum [Erstellen einer Audience Manager-Quellverbindung](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Adobe Analytics Data Prep | Sie können beim Erstellen einer Analytics-Quellverbindung mit [!DNL Data Prep]-Funktionen Daten herausfiltern, die für Ihre Anwendungsfälle nicht erforderlich sind. Mit [!DNL Data Prep] können Sie festlegen, welche Attribute/Spalten für das jeweilige Profil veröffentlicht werden sollen. Sie können auch bedingte Anweisungen erstellen, um Experience Platform darüber zu informieren, ob Daten für das Profil oder nur für den [!DNL data lake] veröffentlicht werden sollen. Weitere Informationen finden Sie in der Anleitung zum [Erstellen einer Analytics-Quellverbindung](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Unterstützung für das Aktivieren/Deaktivieren von Datensätzen für ein Profil | Um Daten in das Echtzeit-Kundenprofil aufzunehmen, müssen Sie einen Datensatz für die Verwendung im Profilspeicher aktivieren. Dadurch wird ein höherer Anteil Ihrer [!DNL Addressable Audience]- und [!DNL Total Data Volume]-Berechtigungen verbraucht. Sobald ein Datensatz für Anwendungsfälle von Kundenprofilen nicht mehr erforderlich ist, können Sie die Integration dieses Datensatzes in das Profil deaktivieren, um sicherzustellen, dass Ihre Daten weiterhin lizenzkonform sind. Weitere Informationen dazu finden Sie in der Anleitung zum [Aktivieren und Deaktivieren von Datensätzen für ein Profil](../../catalog/datasets/enable-for-profile.md). |
| Ausschließen von Web SDK- und Mobile SDK-Daten | Es gibt zwei Arten von Daten, die vom Web- und Mobile-SDK erfasst werden: automatisch erfasste Daten und explizit von Ihrem Entwickler erfasste Daten. Um die Einhaltung Ihrer Lizenz zu gewährleisten, können Sie die automatische Datenerfassung in der SDK-Konfiguration über die Kontexteinstellung deaktivieren. Benutzerdefinierte Daten können auch von Ihrem Entwickler entfernt oder nicht festgelegt werden. |
| Datenausschluss bei Server-seitiger Weiterleitung | Wenn Sie Daten mithilfe der Server-seitigen Weiterleitung an Experience Platform senden, können Sie festlegen, welche Daten nicht gesendet werden sollen, indem Sie entweder die Zuordnung in einer Regelaktion entfernen, um sie für alle Ereignisse auszuschließen, oder Bedingungen zur Regel hinzufügen, sodass Daten nur für bestimmte Ereignisse ausgelöst werden. Weitere Informationen finden Sie in der Dokumentation unter [Ereignisse und Bedingungen](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if). |
| Filtern von Daten auf Quellebene | Sie können logische Operatoren und Vergleichsoperatoren verwenden, um Daten auf Zeilenebene aus Ihren Quellen zu filtern, bevor Sie eine Verbindung erstellen und Daten in Experience Platform aufnehmen. Weitere Informationen finden Sie im Handbuch unter [Filtern von Daten auf Zeilenebene für eine Quelle mithilfe der  [!DNL Flow Service] -API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Profilspeicher {#profile-service}

Der Profilspeicher besteht aus den folgenden Komponenten:

| Profilspeicherkomponente | Beschreibung |
| --- | --- |
| Profilfragmente | Jedes Kundenprofil besteht aus mehreren **Profilfragmenten**, die zu einer einzigen Ansicht dieses Kunden zusammengefügt werden. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen über mehrere **Profilfragmente**, die sich auf diesen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Experience Platform aufgenommen werden, werden sie mithilfe des Identitätsdiagramms zusammengeführt, sodass ein einziges Profil für diesen Kunden entsteht. **Profilfragmente** bestehen aus einem Identity-Namespace als Kennung sowie den zugehörigen Datensatzdaten und/oder Zeitreihedaten. |
| Datensatzdaten (Attribute) | Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson, die aus vielen **Attributen** besteht (auch als **Datensatzdaten** bezeichnet). So kann etwa ein Produktprofil eine SKU und eine Beschreibung enthalten, während in einem Personenprofil Informationen wie Vorname, Nachname und E-Mail-Adresse erfasst sind. **Datensatzdaten** haben normalerweise geringes/mäßiges Volumen, sind aber über einen langen Zeitraum hinweg wertvoll. |
| Zeitreihedaten (Verhalten) | **Zeitreihedaten** liefern Informationen zum Benutzerverhalten. Zeitreihedaten werden durch die Standard-Schemaklasse Experience-Datenmodell (XDM) [!DNL ExperienceEvent] dargestellt. Sie beschreiben Ereignisse wie etwa das Hinzufügen eines Artikels zu einem Warenkorb, das Klicken auf einen Link, das Abspielen eines Videos usw. Der Wert der Verhaltensdaten kann mit der Zeit abnehmen. |
| Identity-Namespace (Identitäten) | Wenn Kundendaten erfasst werden, werden sie mithilfe von **Identity-Namespaces** zu einem einzigen Profil zusammengeführt. Zudem besteht die Möglichkeit, solche Identitäten zu verknüpfen, sobald mehr Informationen über den jeweiligen Kunden bekannt werden. Weiterführende Informationen dazu finden Sie unter [Übersicht zu Identity-Namespaces](../../identity-service/features/namespaces.md). |

{style="table-layout:auto"}

#### Berichte zur Zusammensetzung des Profilspeichers

Es stehen eine Reihe von Berichten zur Verfügung, die Ihnen dabei helfen, die Zusammensetzung des Profilspeichers zu verstehen. Diese Berichte helfen Ihnen dabei, fundierte Entscheidungen darüber zu treffen, wie und wo Sie Ihren Ablauf von Erlebnisereignissen festlegen können, um Ihre Lizenznutzung zu optimieren:

* **Dataset Overlap Report API**: Zeigt die Datensätze, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen. Sie können diesen Bericht verwenden, um zu ermitteln, für welche [!DNL ExperienceEvent] Datensätze eine Gültigkeit festgelegt werden soll. Weitere Informationen dazu finden Sie im Tutorial zum [Erstellen des Dataset Overlap Reports](../../profile/tutorials/dataset-overlap-report.md).
* **Identity Overlap Report API**: Zeigt die Identity-Namespaces, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen. Weitere Informationen dazu finden Sie im Tutorial zum [Erstellen des Identity Overlap Reports](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report).
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Ablauf von Daten pseudonymer Profile {#pseudonymous-profile-expirations}

Mit dieser Funktion können Sie veraltete pseudonyme Profile automatisch aus dem Profilspeicher entfernen. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Ablauf von Daten pseudonymer Profile - Übersicht](../../profile/pseudonymous-profiles.md).

#### Gültigkeitsdauern von Erlebnisereignissen {#event-expirations}

Mit dieser Funktion können Sie Verhaltensdaten automatisch aus einem profilaktivierten Datensatz entfernen, der für Ihre Anwendungsfälle nicht mehr nützlich ist. In der Übersicht zu [Gültigkeitsdauern von Erlebnisereignissen](../../profile/event-expirations.md) finden Sie Details dazu, wie dieser Prozess funktioniert, sobald er für einen Datensatz aktiviert ist.

## Zusammenfassung der Best Practices für die Lizenznutzung {#best-practices}

Im Folgenden finden Sie eine Liste empfohlener Best Practices, die Sie befolgen können, um die optimale Nutzung Ihrer Lizenz sicherzustellen:

* Verwenden Sie das [Lizenznutzungs-Dashboard](../../dashboards/guides/license-usage.md), um die Nutzung durch Kunden zu verfolgen und zu überwachen. Dadurch können Sie potenziellen Überschreitungen rechtzeitig gegensteuern.
* Konfigurieren Sie [Aufnahmefilter](#ingestion-filters), indem Sie die Ereignisse bestimmen, die für Ihre Segmentierungs- und Personalisierungs-Anwendungsfälle erforderlich sind. Dies ermöglicht Ihnen, nur wichtige Ereignisse zu senden, die für Ihre Anwendungsfälle nötig sind.
* Stellen Sie sicher, dass Sie nur [Datensätze für Profile aktiviert haben](#ingestion-filters), die für Ihre Segmentierungs- und Personalisierungs-Anwendungsfälle erforderlich sind.
* Konfigurieren Sie [Ablauf von Erlebnisereignissen](#event-expirations) und [Ablauf von Daten pseudonymer Profile](#pseudonymous-profile-expirations) für sehr häufige Daten wie Web-Daten.
* Überprüfen Sie regelmäßig die [Berichte zur Profilzusammensetzung](#profile-store-composition-reports), um sich ein Bild über die Zusammensetzung des Profilspeichers zu machen. Auf diese Weise können Sie die Datenquellen ermitteln, die im Rahmen Ihrer Lizenzberechtigung die meisten Daten nutzen.

## Funktionsüberblick und -verfügbarkeit {#feature-summary}

Die in diesem Dokument beschriebenen Best Practices und Tools helfen Ihnen bei der besseren Nutzung Ihrer Lizenzberechtigungen in Adobe Experience Platform. Dieses Dokument wird aktualisiert, sobald zusätzliche Funktionen veröffentlicht werden, um allen Experience Platform-Kunden Transparenz und Kontrolle zu bieten.

In der folgenden Tabelle finden Sie eine Liste der derzeit verfügbaren Funktionen, mit denen Sie Ihre Lizenznutzungsberechtigung besser verwalten können.

| Funktion | Beschreibung |
| --- | --- |
| [Datensätze für ein Profil aktivieren/deaktivieren](../../catalog/datasets/user-guide.md) | Aktivieren oder Deaktivieren der Datensatzaufnahme in das Echtzeit-Kundenprofil. |
| [Gültigkeitsdauern von Erlebnisereignissen](../../profile/event-expirations.md) | Wenden Sie eine Ablaufzeit auf alle Ereignisse an, die in einen profilaktivierten Datensatz aufgenommen werden. Wenden Sie sich an Ihr Adobe-Accountteam oder die Kundenunterstützung, um diese Funktion zu aktivieren. |
| [Adobe Analytics-Datenvorbereitungsfilter](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Anwenden von [!DNL Kafka]-Filtern zum Ausschließen unnötiger Daten von der Aufnahme |
| [Quell-Connector-Filter von Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Anwenden von Audience Manager-Quellverbindungsfiltern, um unnötige Daten von der Aufnahme auszuschließen |
| [Datenfilter für die Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) | Anwenden von Server-seitigen [!DNL Kafka]-Filtern, um unnötige Daten von der Aufnahme auszuschließen.  Weitere Informationen finden Sie in der Dokumentation unter [Tag-Regeln](../../tags/ui/managing-resources/rules.md). |
| [Lizenznutzungs-Dashboard](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Ansicht eines Snapshots der lizenzbezogenen Daten Ihres Unternehmens für Experience Platform. |
| [Dataset Overlap Report API](../../profile/tutorials/dataset-overlap-report.md) | Gibt die Datensätze an, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen. |
| [Identity Overlap Report API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Gibt die Identity-Namespaces an, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen |

{style="table-layout:auto"}
