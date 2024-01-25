---
title: Best Practices für die Verwaltung von Daten im Rahmen von Lizenzberechtigungen
description: Erfahren Sie mehr über Best Practices und Werkzeuge, die Sie zur besseren Verwaltung Ihrer Lizenzberechtigungen mit Adobe Experience Platform einsetzen können.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2264'
ht-degree: 73%

---

# Best Practices für die Verwaltung von Daten im Rahmen von Lizenzberechtigungen

Adobe Experience Platform ist ein offenes System, das Ihre Daten in Kundenprofile umwandelt, die in Echtzeit aktualisiert werden. Darüber hinaus nutzt Adobe Experience Platform KI-gestützte Einblicken, mithilfe derer Sie auf allen Kanälen ansprechende Erlebnisse bereitstellen können. Sie können Daten unterschiedlicher Art, Menge und Historie mit Hilfe von Quellen in Experience Platform einspeisen und diese Daten dann für Anwendungsfälle nutzen – von der Segmentierung und Personalisierung bis hin zu Analysen und maschinellem Lernen.

Platform bietet Lizenzen an, die die Anzahl der Profile, die Sie erstellen können, und die Menge der Daten, die Sie einbringen können, festlegen. Da Sie Daten aus beliebigen Quellen, mit beliebigem Volumen und beliebiger Historie einbringen können, kann es vorkommen, dass Sie das Limit Ihrer Lizenzberechtigungen überschreiten, wenn Ihr Datenvolumen wächst.

In diesem Dokument werden Best Practices und Tools beschrieben, mit denen Sie Ihre Lizenzberechtigungen mit Adobe Experience Platform besser verwalten können.

## Grundlagen zur Datenspeicherung in Adobe Experience Platform

Experience Platform besteht hauptsächlich aus zwei Datenspeichern: dem [!DNL data lake] und den Profilspeicher.

Der **[!DNL data lake]** dient hauptsächlich folgenden Zwecken:

* Fungiert als Staging-Bereich für das Onboarding von Daten in Experience Platform;
* Fungiert als langfristiger Datenspeicher für alle Daten in Experience Platform;
* Ermöglicht Anwendungsfälle wie die Datenanalyse und Datenwissenschaft.

Die **Profilspeicher** ist der Ort, an dem Kundenprofile erstellt werden und in erster Linie die folgenden Zwecke erfüllt:

* Fungiert als Datenspeicher für Profile, die zur Bereitstellung von Echtzeit-Erlebnissen verwendet werden;
* Aktiviert Anwendungsfälle wie die Segmentierung, Aktivierung und Personalisierung.

>[!NOTE]
>
>Ihr Zugriff auf den [!DNL data lake] kann von der von Ihnen erworbenen Produkt-SKU abhängen. Weitere Informationen zu Produkt-SKUs erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

## Lizenznutzung {#license-usage}

Wenn Sie eine Lizenz für Experience Platform erwerben, erhalten Sie Lizenznutzungsberechtigungen, die je nach SKU variieren:

**[!DNL Addressable Audience]** – die Gesamtzahl der Kundenprofile, die vertraglich für Experience Platform zugelassen sind, einschließlich bekannter und pseudonymer Profile.

**[!DNL Profile Richness]** – die durchschnittliche Größe Ihrer Profildaten in Experience Platform. Sie können die Obergrenze Ihrer [!DNL Profile Richness]-Berechtigung durch den Kauf eines Anreicherungspakets erhöhen.

Die [!DNL Profile Richness]-Metrik variiert je nach der von Ihnen erworbenen Lizenz. Die [!DNL Profile Richness] kann durch zwei Berechnungen festgestellt werden:

* Die Summe aller in Adobe Real-time Customer Data Platform gespeicherten Produktionsdaten (d. h. Echtzeit-Kundenprofil und Identitätsdienst) zu einem beliebigen Zeitpunkt dividiert durch die Variable [!DNL Addressable Audience];
* Die Summe aller in Platform gespeicherten Daten (einschließlich, aber nicht beschränkt auf die Variable [!DNL data lake], Echtzeit-Kundenprofil und Identity Service) zu einem beliebigen Zeitpunkt und beliebigen Daten, die Sie in der Plattform in den letzten 12 Monaten streamen (anstatt darin zu speichern), geteilt durch die [!DNL Addressable Audience].

Die Verfügbarkeit und spezifische Definition dieser Metriken hängen von der von Ihrem Unternehmen erworbenen Lizenz ab.

## Lizenznutzungs-Dashboard

Die Benutzeroberfläche von Adobe Experience Platform verfügt über ein Dashboard, in dem Sie eine Momentaufnahme der Lizenzdaten Ihres Unternehmens für Platform anzeigen können. Die Daten im Dashboard werden genau so angezeigt, wie sie zu dem Zeitpunkt erscheinen, an dem der Snapshot erstellt wurde. Der Snapshot ist weder ein Näherungswert noch eine Stichprobe von Daten, und das Dashboard wird nicht in Echtzeit aktualisiert.

Weitere Informationen finden Sie in der Anleitung zum [Verwenden des Lizenznutzungs-Dashboards in der Platform-Benutzeroberfläche](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

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

### Welche Daten integrieren Sie in Platform?

Daten können in Platform in ein oder mehrere Systeme aufgenommen werden, nämlich die [!DNL data lake] und/oder den Profilspeicher. Dies bedeutet, dass in beiden Systemen für eine Vielzahl verschiedener Anwendungsfälle unterschiedliche Daten vorhanden sein können. Beispielsweise können Sie historische Daten im [!DNL data lake], jedoch nicht im Profilspeicher. Sie können auswählen, welche Daten an den Profilspeicher gesendet werden sollen, indem Sie einen Datensatz für die Profilaufnahme aktivieren.

>[!NOTE]
>
>Ihr Zugriff auf den [!DNL data lake] kann von der von Ihnen erworbenen Produkt-SKU abhängen. Weitere Informationen zu Produkt-SKUs erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

### Welche Daten behalten Sie?

Sie können sowohl Datenerfassungsfilter als auch Ablaufregeln anwenden, um Daten zu entfernen, die für Ihre Anwendungsfälle veraltet sind. In der Regel verbrauchen Verhaltensdaten (z. B. Analytics-Daten) wesentlich mehr Speicher als Datensatzdaten (z. B. CRM-Daten). Viele Platform-Benutzer haben bis zu 90 % Profile, die ausschließlich Verhaltensdaten enthalten, und vergleichsweise wenige Datensatzdaten. Daher ist die Verwaltung Ihrer Verhaltensdaten von entscheidender Bedeutung, um die Einhaltung Ihrer Lizenzberechtigungen sicherzustellen.

Es gibt eine Reihe von Tools, die Ihnen helfen, Ihre Lizenznutzungsberechtigungen einzuhalten:

* [Aufnahmefilter](#ingestion-filters)
* [Profilspeicher](#profile-service)

### Identity Service und adressierbare Zielgruppe {#identity-service}

Identitätsdiagramme werden nicht mit Ihrer gesamten adressierbaren Zielgruppenberechtigungen angerechnet, da adressierbare Zielgruppen auf Ihre Gesamtzahl an Kundenprofilen verweisen.

Beschränkungen für Identitätsdiagramme können sich jedoch auf Ihre adressierbare Zielgruppe auswirken, da Identitäten geteilt werden. Wenn beispielsweise die älteste ECID aus dem Diagramm entfernt wird, existiert die ECID weiterhin im Echtzeit-Kundenprofil als pseudonymes Profil. Sie können [Pseudonyme Profildatenabläufe](../../profile/pseudonymous-profiles.md) um dieses Verhalten zu umgehen. Weitere Informationen finden Sie im Abschnitt [Limits für Identity Service-Daten](../../identity-service/guardrails.md).

### Aufnahmefilter {#ingestion-filters}

Aufnahmefilter ermöglichen Ihnen, nur die für Ihre Anwendungsfälle erforderlichen Daten aufzunehmen und alle nicht erforderlichen Ereignisse herauszufiltern.

| Aufnahmefilter | Beschreibung |
| --- | --- |
| Adobe Audience Manager-Quellfilter | Wenn Sie eine Adobe Audience Manager-Quellverbindung erstellen, können Sie auswählen, welche Segmente und Eigenschaften in die [!DNL data lake] und Echtzeit-Kundenprofil verwenden, anstatt die Daten des Audience Managers vollständig zu erfassen. Weitere Informationen finden Sie in der Anleitung zum [Erstellen einer Audience Manager-Quellverbindung](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Adobe Analytics Data Prep | Sie können beim Erstellen einer Analytics-Quellverbindung mit [!DNL Data Prep]-Funktionen Daten herausfiltern, die für Ihre Anwendungsfälle nicht erforderlich sind. Mit [!DNL Data Prep] können Sie festlegen, welche Attribute/Spalten für das jeweilige Profil veröffentlicht werden sollen. Sie können auch bedingte Anweisungen erstellen, um Platform darüber zu informieren, ob Daten für das Profil oder nur für den [!DNL data lake] veröffentlicht werden sollen. Weitere Informationen finden Sie in der Anleitung zum [Erstellen einer Analytics-Quellverbindung](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Unterstützung für das Aktivieren/Deaktivieren von Datensätzen für ein Profil | Um Daten in das Echtzeit-Kundenprofil zu erfassen, müssen Sie einen Datensatz für die Verwendung im Profilspeicher aktivieren. Dadurch wird ein höherer Anteil Ihrer [!DNL Addressable Audience]- und [!DNL Profile Richness]-Berechtigungen verbraucht. Sobald ein Datensatz für Anwendungsfälle von Kundenprofilen nicht mehr erforderlich ist, können Sie die Integration dieses Datensatzes in das Profil deaktivieren, um sicherzustellen, dass Ihre Daten weiterhin lizenzkonform sind. Weitere Informationen dazu finden Sie in der Anleitung zum [Aktivieren und Deaktivieren von Datensätzen für ein Profil](../../catalog/datasets/enable-for-profile.md). |
| Ausschließen von Web SDK- und Mobile SDK-Daten | Es gibt zwei Arten von Daten, die vom Web- und Mobile-SDK erfasst werden: automatisch erfasste Daten und explizit von Ihrem Entwickler erfasste Daten. Um die Einhaltung Ihrer Lizenz zu gewährleisten, können Sie die automatische Datenerfassung in der SDK-Konfiguration über die Kontexteinstellung deaktivieren. Benutzerdefinierte Daten können auch von Ihrem Entwickler entfernt oder nicht eingerichtet werden. Weitere Informationen finden Sie in der Anleitung zu den [Grundlagen der SDK-Konfiguration](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#fundamentals). |
| Datenausschluss bei Server-seitiger Weiterleitung | Wenn Sie Daten mithilfe der Server-seitigen Weiterleitung an Platform senden, können Sie festlegen, welche Daten beim Versand ausgeschlossen werden, indem Sie entweder in einer Regel das Mapping entfernen und es für alle Ereignisse ausschließen oder Bedingungen zur Regel hinzufügen, sodass Daten nur für bestimmte Ereignisse ausgelöst werden. Siehe die Dokumentation unter [Ereignisse und Bedingungen](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if) für weitere Informationen. |
| Filtern von Daten auf Quellebene | Sie können logische Operatoren und Vergleichsoperatoren verwenden, um Daten auf Zeilenebene aus Ihren Quellen zu filtern, bevor Sie eine Verbindung herstellen und Daten auf Experience Platform erfassen. Weitere Informationen finden Sie im Handbuch unter [Filtern von Daten auf Zeilenebene für eine Quelle mithilfe der [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Profilspeicher {#profile-service}

Der Profilspeicher besteht aus den folgenden Komponenten:

| Profilspeicherkomponente | Beschreibung |
| --- | --- |
| Profilfragmente | Jedes Kundenprofil besteht aus mehreren **Profilfragmenten**, die zu einer einzigen Ansicht dieses Kunden zusammengefügt werden. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen über mehrere **Profilfragmente**, die sich auf diesen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Platform aufgenommen werden, werden sie mithilfe des Identitätsdiagramms zusammengeführt, sodass ein einziges Profil für diesen Kunden entsteht. **Profilfragmente** bestehen aus einem Identity-Namespace als Kennung sowie den zugehörigen Datensatzdaten und/oder Zeitreihedaten. |
| Datensatzdaten (Attribute) | Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson, die aus vielen **Attributen** besteht (auch als **Datensatzdaten** bezeichnet). So kann etwa ein Produktprofil eine SKU und eine Beschreibung enthalten, während in einem Personenprofil Informationen wie Vorname, Nachname und E-Mail-Adresse erfasst sind. **Datensatzdaten** haben normalerweise geringes/mäßiges Volumen, sind aber über einen langen Zeitraum hinweg wertvoll. |
| Zeitreihedaten (Verhalten) | **Zeitreihedaten** liefern Informationen zum Benutzerverhalten. Zeitreihedaten werden durch die Standard-Schemaklasse Experience-Datenmodell (XDM) [!DNL ExperienceEvent] dargestellt. Sie beschreiben Ereignisse wie etwa das Hinzufügen eines Artikels zu einem Warenkorb, das Klicken auf einen Link, das Abspielen eines Videos usw. Der Wert der Verhaltensdaten kann mit der Zeit abnehmen. |
| Identity-Namespace (Identitäten) | Wenn Kundendaten erfasst werden, werden sie mithilfe von **Identity-Namespaces** zu einem einzigen Profil zusammengeführt. Zudem besteht die Möglichkeit, solche Identitäten zu verknüpfen, sobald mehr Informationen über den jeweiligen Kunden bekannt werden. Weiterführende Informationen dazu finden Sie unter [Übersicht zu Identity-Namespaces](../../identity-service/features/namespaces.md). |

{style="table-layout:auto"}

#### Komprimierungsberichte aus dem Profilspeicher

Es stehen verschiedene Berichte zur Verfügung, die Ihnen helfen, die Zusammensetzung des Profilspeichers zu verstehen. Diese Berichte helfen Ihnen dabei, fundierte Entscheidungen darüber zu treffen, wie und wo Sie Ihre Erlebnisereignis-Abläufe festlegen können, um Ihre Lizenznutzung besser zu optimieren:

* **Dataset Overlap Report API**: Zeigt die Datensätze, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen. Mit diesem Bericht können Sie ermitteln, welche [!DNL ExperienceEvent] -Datensätze, für die ein Ablaufdatum festgelegt wird. Weitere Informationen dazu finden Sie im Tutorial zum [Erstellen des Dataset Overlap Reports](../../profile/tutorials/dataset-overlap-report.md).
* **Identity Overlap Report API**: Zeigt die Identity-Namespaces, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen. Weitere Informationen dazu finden Sie im Tutorial zum [Erstellen des Identity Overlap Reports](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report).
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Pseudonyme Profildatenabläufe {#pseudonymous-profile-expirations}

Mit dieser Funktion können Sie alte Pseudonyme Profile automatisch aus dem Profilspeicher entfernen. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Übersicht über den Ablauf der pseudonymen Profildaten](../../profile/pseudonymous-profiles.md).

#### Gültigkeitsdauern von Erlebnisereignissen {#event-expirations}

Mit dieser Funktion können Sie Verhaltensdaten automatisch aus einem für Profile aktivierten Datensatz entfernen, der für Ihre Anwendungsfälle nicht mehr nützlich ist. Siehe Übersicht unter [Ablauf von Erlebnisereignissen](../../profile/event-expirations.md) für Details darüber, wie dieser Prozess funktioniert, nachdem er für einen Datensatz aktiviert wurde.

## Zusammenfassung der Best Practices für die Lizenznutzung {#best-practices}

Im Folgenden finden Sie eine Liste empfohlener Best Practices, die Sie befolgen können, um die optimale Nutzung Ihrer Lizenz sicherzustellen:

* Verwenden Sie das [Lizenznutzungs-Dashboard](../../dashboards/guides/license-usage.md), um die Nutzung durch Kunden zu verfolgen und zu überwachen. Dadurch können Sie potenziellen Überschreitungen rechtzeitig gegensteuern.
* Konfigurieren Sie [Aufnahmefilter](#ingestion-filters), indem Sie die Ereignisse bestimmen, die für Ihre Segmentierungs- und Personalisierungs-Anwendungsfälle erforderlich sind. Dies ermöglicht Ihnen, nur wichtige Ereignisse zu senden, die für Ihre Anwendungsfälle nötig sind.
* Stellen Sie sicher, dass Sie nur [Datensätze für Profile aktiviert haben](#ingestion-filters), die für Ihre Segmentierungs- und Personalisierungs-Anwendungsfälle erforderlich sind.
* Konfigurieren [Ablauf von Erlebnisereignissen](#event-expirations) und [Pseudonyme Profildatenabläufe](#pseudonymous-profile-expirations) für hochfrequente Daten wie Webdaten.
* Prüfen Sie regelmäßig die [Berichte zur Profilgruppierung](#profile-store-composition-reports) , um die Komposition im Profilspeicher zu verstehen. Auf diese Weise können Sie die Datenquellen ermitteln, die im Rahmen Ihrer Lizenzberechtigung die meisten Daten nutzen.

## Funktionsüberblick und -verfügbarkeit {#feature-summary}

Die in diesem Dokument beschriebenen Best Practices und Tools helfen Ihnen bei der besseren Verwaltung der Nutzung Ihrer Lizenzberechtigungen in Adobe Experience Platform. Dieses Dokument wird aktualisiert, sobald zusätzliche Funktionen veröffentlicht werden, um allen Experience Platform-Kunden Transparenz und Kontrolle zu bieten.

In der folgenden Tabelle finden Sie eine Liste der derzeit verfügbaren Funktionen, mit denen Sie Ihre Lizenznutzungsberechtigung besser verwalten können.

| Funktion | Beschreibung |
| --- | --- |
| [Datensätze für ein Profil aktivieren/deaktivieren](../../catalog/datasets/user-guide.md) | Aktivieren oder deaktivieren Sie die Erfassung von Datensätzen in Echtzeit-Kundenprofil. |
| [Ablauf von Erlebnisereignissen](../../profile/event-expirations.md) | Wenden Sie eine Ablaufzeit für alle Ereignisse an, die in einen Profil-aktivierten Datensatz aufgenommen werden. Wenden Sie sich an Ihr Adobe-Account-Team oder an die Kundenunterstützung, um diese Funktion zu aktivieren. |
| [Adobe Analytics-Datenvorbereitungsfilter](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Anwenden von [!DNL Kafka]-Filtern zum Ausschließen unnötiger Daten von der Aufnahme |
| [Quell-Connector-Filter von Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Anwenden von Audience Manager-Quellverbindungsfiltern, um unnötige Daten von der Aufnahme auszuschließen |
| [Alloy-SDK-Datenfilter](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#fundamentals) | Anwenden von Alloy-Filtern, um unnötige Daten von der Aufnahme auszuschließen |
| [Datenfilter für die Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) | Anwenden von Server-seitigen [!DNL Kafka]-Filtern, um unnötige Daten von der Aufnahme auszuschließen.  Weitere Informationen finden Sie in der Dokumentation unter [Tag-Regeln](../../tags/ui/managing-resources/rules.md). |
| [Lizenznutzungs-Dashboard](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Ansicht eines Snapshots der lizenzbezogenen Daten Ihres Unternehmens für Experience Platform. |
| [Dataset Overlap Report API](../../profile/tutorials/dataset-overlap-report.md) | Gibt die Datensätze an, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen. |
| [Identity Overlap Report API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Gibt die Identity-Namespaces an, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen |

{style="table-layout:auto"}
