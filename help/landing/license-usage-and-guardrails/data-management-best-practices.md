---
keywords: Experience Platform; Startseite; beliebte Themen; Datenmanagement; Lizenzberechtigungen; Lizenzierung; Best Practices
title: Best Practices für Data Management-Lizenzberechtigungen
description: In diesem Dokument werden Best Practices und Tools beschrieben, mit denen Sie Ihre Lizenzberechtigungen mit Adobe Experience Platform besser verwalten können.
source-git-commit: 3bac35ba5f6e9cde6c1324b11220c523daa1f8cb
workflow-type: tm+mt
source-wordcount: '2603'
ht-degree: 1%

---

# Best Practices für die Zuweisung von Datenverwaltungslizenzen

Adobe Experience Platform ist ein offenes System, das Ihre Daten in robuste Kundenprofile umwandelt, die in Echtzeit aktualisiert werden und mithilfe von KI-gestützten Einblicken die richtigen Erlebnisse für jeden Kanal bereitstellt. Sie können Daten unterschiedlicher Typen, Volumen und Historien mithilfe von Quellen in die Experience Platform aufnehmen und diese Daten dann für Anwendungsfälle von der Segmentierung und Personalisierung bis hin zu Analysen und maschinellem Lernen nutzen.

Platform bietet Lizenzen, die die Anzahl der Profile, die Sie erstellen können, und die Menge der Daten festlegen, die Sie einbringen können. Aufgrund der Fähigkeit, Daten aus beliebigen Quellen, Volumen oder der Datengeschichte einzubringen, ist es möglich, Ihre Lizenzberechtigungen zu überschreiten, wenn Ihr Datenvolumen wächst.

In diesem Dokument werden Best Practices und Tools beschrieben, mit denen Sie Ihre Lizenzberechtigungen mit Adobe Experience Platform besser verwalten können.

## Grundlagen zur Datenspeicherung in Adobe Experience Platform

Experience Platform besteht hauptsächlich aus zwei Datenrepository: die [!DNL Data Lake] und den Profilspeicher.

Die **[!DNL Data Lake]** dient hauptsächlich folgenden Zwecken:

* fungiert als Staging-Bereich für das Onboarding von Daten in die Experience Platform;
* fungiert als langfristige Datenspeicherung für alle Daten der Experience Platform;
* Aktiviert Anwendungsfälle wie Datenanalyse und Datenwissenschaft.

Die **Profilspeicher** ist der Ort, an dem Kundenprofile erstellt werden und in erster Linie die folgenden Zwecke erfüllt:

* fungiert als Datenspeicher für Profile, die zur Unterstützung von Echtzeit-Erlebnissen verwendet werden;
* Aktiviert Anwendungsfälle wie Segmentierung, Aktivierung und Personalisierung.

>[!NOTE]
>
>Ihr Zugriff auf [!DNL Data Lake] kann von der von Ihnen erworbenen Produkt-SKU abhängen. Weitere Informationen zu Produkt-SKUs erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

## Lizenznutzung {#license-usage}

Wenn Sie Experience Platform lizenzieren, erhalten Sie Lizenznutzungsberechtigungen, die je nach SKU variieren:

**[!DNL Addressable Audience]** - die Gesamtzahl der Kundenprofile, die vertraglich für die Experience Platform zugelassen sind, einschließlich bekannter und pseudonymer Profile.

**[!DNL Profile Richness]** - die durchschnittliche Größe Ihrer Profildaten in Experience Platform. Sie können Ihre [!DNL Profile Richness] Anspruch durch Kauf eines Reichtums.

Die [!DNL Profile Richness] -Metrik variiert je nach der von Ihnen erworbenen Lizenz. Es gibt zwei Berechnungen für [!DNL Profile Richness] verfügbar:

* Die Summe aller in Real-time Customer Data Platform gespeicherten Produktionsdaten (d. h. Profildienst und Identitätsdienst) zu einem beliebigen Zeitpunkt dividiert durch die [!DNL Addressable Audience];
* Die Summe aller in Platform gespeicherten Daten (einschließlich, aber nicht beschränkt auf die Variable [!DNL Data Lake], Profile Service und Identity Service) zu einem beliebigen Zeitpunkt und Daten, die Sie in den letzten 12 Monaten über die Plattform streamen (anstatt darin zu speichern), geteilt durch die [!DNL Addressable Audience].

Die Verfügbarkeit dieser Metriken und die spezifische Definition dieser Metriken hängen von der von Ihrem Unternehmen erworbenen Lizenz ab.

## Dashboard zur Lizenzverwendung

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie eine Momentaufnahme der lizenzbezogenen Daten Ihres Unternehmens für Platform anzeigen können. Die Daten im Dashboard werden exakt so angezeigt, wie sie zum Zeitpunkt der Momentaufnahme angezeigt werden. Der Schnappschuss ist weder eine Annäherung noch ein Beispiel von Daten, und das Dashboard wird nicht in Echtzeit aktualisiert.

Weitere Informationen finden Sie im Handbuch unter [Verwenden des Dashboards zur Lizenznutzung in der Platform-Benutzeroberfläche](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Best Practices für das Datenmanagement

In den folgenden Abschnitten werden Best Practices für eine bessere Verwaltung Ihrer Daten beschrieben.

### Grundlegendes zu Daten

Nicht alle Daten sind in Adobe Experience Platform identisch. Einige Daten sind zwar dicht, aber wertmäßig niedrig, während andere zwar sparsam, aber wertmäßig sind. Manche Daten können nach ihrer Erstellung an Wert verlieren, während andere für Monate, wenn nicht sogar für Jahre wertvoll sein können.

Beim Verständnis des Werts Ihrer Daten sind drei Dimensionen zu beachten:

| Dimension | Beschreibung | Beispiel |
| --- | --- | --- |
| Volumen | Stellt die Menge und Gesamtsumme der erfassten Daten dar. | Web-Klicks - hohe Volumen und mäßige Treue. Der Wert kann schnell abnehmen. |
| Zeitbereich | Stellt die Zeitdauer dar, die erfasste Daten weiterhin wertvoll bleiben. | Offline-Käufe - moderates Volumen und Treue, können aber über lange Zeiträume wertvoll sein. |
| Treue | Stellt dar, wie reich die Daten an Informationen sind. | Kundenkonten - geringe Menge, aber hohe Treue. Kann über die Lebensdauer eines Kunden hinaus nützlich sein. |

### Data-Management-Tools {#data-management-tools}

Es gibt zwei zentrale Szenarien, in denen Sie sicherstellen müssen, dass Ihre Datennutzung innerhalb Ihrer Lizenzberechtigungsbeschränkungen bleibt:

### Welche Daten müssen in Platform integriert werden?

Daten können in Platform in ein oder mehrere Systeme aufgenommen werden, nämlich die [!DNL Data Lake] und/oder den Profilspeicher. Dies bedeutet, dass in beiden Systemen für eine Vielzahl verschiedener Anwendungsfälle unterschiedliche Daten vorhanden sein können. Beispielsweise können Sie historische Daten im [!DNL Data Lake], jedoch nicht im Profilspeicher. Sie können auswählen, welche Daten an den Profilspeicher gesendet werden sollen, indem Sie einen Datensatz für die Profilaufnahme aktivieren.

>[!NOTE]
>
>Ihr Zugriff auf [!DNL Data Lake] kann von der von Ihnen erworbenen Produkt-SKU abhängen. Weitere Informationen zu Produkt-SKUs erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

### Welche Daten müssen aufbewahrt werden?

Sie können sowohl Datenerfassungsfilter als auch Ablaufregeln (auch TTL-Zeit genannt) anwenden, um Daten zu entfernen, die für Ihre Anwendungsfälle mittlerweile veraltet sind. In der Regel verbrauchen Verhaltensdaten (z. B. Analytics-Daten) wesentlich mehr Speicher als Datensatzdaten (z. B. CRM-Daten). So haben viele Platform-Benutzer beispielsweise bis zu 90 % der Profile, die allein durch Verhaltensdaten befüllt werden, im Vergleich zu Datensatzdaten. Daher ist die Verwaltung Ihrer Verhaltensdaten von entscheidender Bedeutung, um die Einhaltung Ihrer Lizenzberechtigungen sicherzustellen.

Es gibt eine Reihe von Tools, die Sie nutzen können, um in Ihren Lizenznutzungsberechtigungen zu bleiben:

* [Aufnahmefilter](#ingestion-filters)
* [Profil-Service-TTL](#profile-service)

### Aufnahmefilter {#ingestion-filters}

Mit Aufnahmefiltern können Sie nur die für Ihre Anwendungsfälle erforderlichen Daten einbringen und alle nicht erforderlichen Ereignisse herausfiltern.

| Aufnahmefilter | Beschreibung |
| --- | --- |
| Adobe Audience Manager-Quellfilter | Wenn Sie eine Adobe Audience Manager-Quellverbindung erstellen, können Sie auswählen, welche Segmente und Eigenschaften in die [!DNL Data Lake] und Profildienst verwenden, anstatt die Daten des Audience Managers vollständig zu erfassen. Siehe Handbuch unter [Erstellen einer Audience Manager-Quellverbindung](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) für weitere Informationen. |
| Adobe Analytics-Datenvorbereitung | Sie können [!DNL Data Prep] Funktionen beim Erstellen einer Analytics-Quellverbindung zum Filtern von Daten, die für Ihre Anwendungsfälle nicht erforderlich sind. bis [!DNL Data Prep]können Sie festlegen, welche Attribute/Spalten in Profile veröffentlicht werden sollen. Sie können auch bedingte Anweisungen bereitstellen, um Platform darüber zu informieren, ob Daten voraussichtlich im Profil oder nur im [!DNL Data Lake]. Siehe Handbuch unter [Erstellen einer Analytics-Quellverbindung](../../sources/tutorials/ui/create/adobe-applications/analytics.md) für weitere Informationen. |
| Unterstützung für das Aktivieren/Deaktivieren von Datensätzen für Profile | Um Daten in den Profildienst zu erfassen, müssen Sie einen Datensatz für die Verwendung im Profilspeicher aktivieren. Dadurch erhöht sich die [!DNL Addressable Audience] und [!DNL Profile Richness] Berechtigungen. Sobald ein Datensatz für Anwendungsfälle von Kundenprofilen nicht mehr erforderlich ist, können Sie die Integration dieses Datensatzes in das Profil deaktivieren, um sicherzustellen, dass Ihre Daten weiterhin lizenzkonform sind. Siehe Handbuch unter [Aktivieren und Deaktivieren von Datensätzen für Profile](../../catalog/datasets/enable-for-profile.md) für weitere Informationen. |
| Ausschließen von Web SDK- und Mobile SDK-Daten | Es gibt zwei Arten von Daten, die vom Web- und Mobile-SDK erfasst werden: automatisch erfasste Daten und explizit von Ihrem Entwickler erfasste Daten. Um die Lizenzkonformität besser zu verwalten, können Sie die automatische Datenerfassung in der SDK-Konfiguration über die Kontexteinstellung deaktivieren. Benutzerdefinierte Daten können auch von Ihrem Entwickler entfernt oder nicht festgelegt werden. Siehe Handbuch unter [Konfigurieren der SDK-Grundlagen](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) für weitere Informationen. |
| Datenausschluss der serverseitigen Weiterleitung | Wenn Sie Daten mithilfe der serverseitigen Weiterleitung an Platform senden, können Sie ausschließen, welche Daten gesendet werden, indem Sie entweder das Mapping in einer Regelaktion entfernen und es über alle Ereignisse hinweg ausschließen oder Bedingungen zur Regel hinzufügen, sodass Daten nur für bestimmte Ereignisse ausgelöst werden. Weitere Informationen finden Sie in der Dokumentation unter [Ereignisse und Bedingungen](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

### Profildienst {#profile-service}

Mit der TTL-Funktion (Time-to-Live) des Profildienstes können Sie TTL auf Daten im Profilspeicher anwenden. Dadurch kann das System automatisch Daten entfernen, die im Laufe der Zeit an Wert verloren haben.

Der Profilspeicher besteht aus den folgenden Komponenten:

| Profilspeicherkomponente | Beschreibung |
| --- | --- |
| Profilfragmente | Jedes Kundenprofil besteht aus mehreren **Profilfragmente** die zusammengeführt wurden, um eine einzige Ansicht dieses Kunden zu bilden. Wenn beispielsweise ein Kunde über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen über mehrere **Profilfragmente** im Zusammenhang mit diesem einzelnen Kunden stehen, der in mehreren Datensätzen angezeigt wird. Wenn diese Fragmente in Platform erfasst werden, werden sie mithilfe des Identitätsdiagramms zusammengeführt, um ein einzelnes Profil für diesen Kunden zu erstellen. **Profilfragmente** besteht aus einem Identitäts-Namespace als Kennung mit zugehörigen Datensatzdaten und/oder Zeitreihendaten. |
| Daten aufzeichnen (Attribute) | Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson, die aus vielen **Attribute** (auch bekannt als **Datensatzdaten**). So kann etwa ein Produktprofil eine SKU und eine Beschreibung enthalten, während in einem Personenprofil Informationen wie Vorname, Nachname und E-Mail-Adresse erfasst sind. **Daten aufzeichnen** ist in der Regel gering/mäßig in der Menge, aber für lange Zeiträume wertvoll. |
| Zeitreihendaten (Verhalten) | **Zeitreihendaten** liefert Informationen zum Benutzerverhalten. Wird durch die Experience-Datenmodell (XDM)-Standardschemaklasse dargestellt [!DNL ExperienceEvent]können Zeitreihendaten Ereignisse beschreiben, z. B. das Hinzufügen von Artikeln zu einem Warenkorb, das Klicken auf Links und das Ansehen von Videos. Der Wert des Verhaltens kann mit der Zeit abnehmen. |
| Identitäts-Namespace (identities) | Wenn Kundendaten zusammenkommen, werden sie mithilfe von **Identitäts-Namespaces** und die Möglichkeit, diese Identitäten miteinander zu verknüpfen, sobald weitere Informationen über den Benutzer bekannt werden. Siehe [Übersicht über Identitäts-Namespaces](../../identity-service/namespaces.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

#### Berichte zur Komposition im Profilspeicher

Es stehen verschiedene Berichte zur Verfügung, die Ihnen helfen, die Zusammensetzung des Profilspeichers zu verstehen. Diese Berichte helfen Ihnen dabei, fundierte Entscheidungen darüber zu treffen, wie und wo Sie Ihre Profil-TTLs einrichten, um Ihre Lizenznutzung besser zu optimieren:

* **Datensatz-Overlap Report API**: Stellt die Datensätze bereit, die am meisten zu Ihrer ansprechbaren Zielgruppe beitragen. Mit diesem Bericht können Sie ermitteln, welche [!DNL ExperienceEvent] -Datensätze, für die eine TTL festgelegt werden soll. Siehe Tutorial zu [Generieren des Berichts zur Datensatzüberschneidung](../../profile/tutorials/dataset-overlap-report.md) für weitere Informationen.
* **Identity Overlap Report API**: Stellt die Identitäts-Namespaces bereit, die am meisten zu Ihrer ansprechbaren Zielgruppe beitragen. Siehe Tutorial zu [Erstellen des Berichts zur Identitätsüberschneidung](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) für weitere Informationen.
* **Unbekannte Profiles Report API**: Zeigt die Auswirkungen der Anwendung von pseudonymen TTL für verschiedene Zeitschwellen an. Mit diesem Bericht können Sie ermitteln, welcher pseudonyme TTL-Schwellenwert angewendet werden soll. Siehe Tutorial zu [Erstellung des Berichts über unbekannte Profile](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) für weitere Informationen.

#### [!DNL ExperienceEvent] Datensatz-TTL {#dataset-ttl}

Sie können TTL auf profilaktivierte Datensätze anwenden, um Verhaltensdaten aus dem Profilspeicher zu entfernen, die für Ihre Anwendungsfälle nicht mehr nützlich sind. Sobald TTL auf einen profilaktivierten Datensatz angewendet wird, entfernt Platform automatisch Daten, die nicht mehr durch einen zweiteiligen Prozess benötigt werden:

* Bei allen neuen Daten wird der TTL-Ablaufwert zum Zeitpunkt der Aufnahme angewendet.
* Bei allen vorhandenen Daten wird der TTL-Ablaufwert im Rahmen eines einmaligen Aufstockungssystemauftrags angewendet.

Sie können erwarten, dass der TTL-Wert für jedes Ereignis aus dem Ereignis-Zeitstempel stammt. Alle Ereignisse, die älter als der TTL-Ablaufwert sind, werden bei Ausführung des Systemauftrags sofort gelöscht. Alle anderen Ereignisse werden entfernt, wenn sie sich dem im Ereigniszeitstempel angegebenen TTL-Ablaufwert nähern.

Im folgenden Beispiel erfahren Sie, wie Sie [!DNL ExperienceEvent] Datensatz-TTL.

Wenn Sie am 15. Mai einen TTL-Wert von 30 Tagen anwenden, dann:

* Für alle neuen Ereignisse wird eine TTL von 30 Tagen angewendet, sobald sie eintreten.
* Alle vorhandenen Ereignisse mit einem Zeitstempel, der älter als der 15. April ist, werden durch einen Systemauftrag sofort gelöscht.;
* Ereignisse, die nach dem 15. April einen Zeitstempel aufweisen, laufen mit ihrem Ereigniszeitstempel und TTL-Tagen ab. Ein Ereignis mit einem Zeitstempel vom 18. April wird also drei Tage nach dem 15. Mai fallen.

>[!IMPORTANT]
>
>Sobald eine TTL angewendet wird, werden alle Daten, die älter als die ausgewählte TTL-Anzahl von Tagen sind, **dauerhaft** gelöscht und kann nicht wiederhergestellt werden.

Bevor Sie TTL anwenden, müssen Sie sicherstellen, dass ein Lookback-Fenster aller Segmente innerhalb der TTL-Grenze bleibt. Andernfalls können die Segmentergebnisse nach der Anwendung von TTL falsch werden. Wenn Sie beispielsweise für Adobe Analytics-Daten eine TTL von 30 Tagen und für In-Store-Transaktionsdaten eine TTL von 365 Tagen angewendet haben, führt das folgende Segment zu falschen Ergebnissen:

* Produktseite in den letzten 60 Tagen angezeigt, gefolgt von einem Kauf im Geschäft;
* In den Warenkorb legen und in den letzten 60 Tagen keinen Kauf tätigen.

Umgekehrt führt Folgendes weiterhin zu korrekten Ergebnissen:

* Produktseite in den letzten 14 Tagen angezeigt, gefolgt von einem Kauf im Geschäft;
* Anzeige einer speziellen Hilfeseite in den letzten 30 Tagen online;
* Ein Produkt wurde in den letzten 120 Tagen offline gekauft.
* Zum Warenkorb hinzugefügt, gefolgt vom Kauf in den letzten 14 Tagen.

>[!TIP]
>
>Aus Gründen der Einfachheit können Sie dieselbe TTL für alle Datensätze beibehalten, sodass Sie sich über die TTL-Auswirkungen für alle Datensätze in der Segmentierungslogik keine Gedanken machen müssen.

Weitere Informationen zum Anwenden von TTL auf Profildaten finden Sie in der Dokumentation unter [Profil-Service-TTL](../../profile/apply-ttl.md).

## Zusammenfassung der Best Practices für die Kompatibilität der Lizenznutzung {#best-practices}

Im Folgenden finden Sie eine Liste empfohlener Best Practices, die Sie befolgen können, um eine bessere Einhaltung Ihrer Lizenz zur Lizenznutzung sicherzustellen:

* Verwenden Sie die [Nutzungs-Dashboard für Lizenzen](../../dashboards/guides/license-usage.md) , um Nutzungstrends der Kunden zu verfolgen und zu überwachen. Dadurch können Sie potenzielle Überschüsse, die auftreten könnten, vorausschauend nutzen.
* Konfigurieren [Aufnahmefilter](#ingestion-filters) durch Identifizierung der Ereignisse, die für Ihre Anwendungsfälle der Segmentierung und Personalisierung erforderlich sind. Auf diese Weise können Sie nur wichtige Ereignisse senden, die für Ihre Anwendungsfälle erforderlich sind.
* Stellen Sie sicher, dass Sie nur [aktivierte Datensätze für Profile](#ingestion-filters) die für Ihre Segmentierung und Personalisierung-Anwendungsfälle erforderlich sind.
* Konfigurieren Sie eine [[!DNL ExperienceEvent] Datensatz-TTL](#dataset-ttl) für hochfrequente Daten wie Webdaten.
* Prüfen Sie regelmäßig die [Berichte zur Profilgruppierung](#profile-store-composition-reports) , um die Komposition im Profilspeicher zu verstehen. Auf diese Weise können Sie die Datenquellen nachvollziehen, die am meisten zu Ihrer Lizenznutzung beitragen.

## Funktionszusammenfassung und -verfügbarkeit {#feature-summary}

Die in diesem Dokument beschriebenen Best Practices und Tools helfen Ihnen bei der besseren Verwaltung der Nutzung Ihrer Lizenzberechtigungen in Adobe Experience Platform. Dieses Dokument wird aktualisiert, sobald zusätzliche Funktionen veröffentlicht werden, um allen Experience Platform-Kunden Sichtbarkeit und Kontrolle zu bieten.

In der folgenden Tabelle finden Sie eine Liste der derzeit verfügbaren Funktionen, mit denen Sie Ihre Lizenz für die Lizenznutzung besser verwalten können.

| Funktion | Beschreibung |
| --- | --- |
| [Datensätze für Profil aktivieren/deaktivieren](../../catalog/datasets/user-guide.md) | Aktivieren oder Deaktivieren der Datensatzaufnahme in den Profildienst |
| [!DNL ExperienceEvent] Datensatz-TTL | Wenden Sie für Verhaltens-Datensätze im Profilspeicher einen TTL-Ablauf an. Wenden Sie sich an Ihren Support-Mitarbeiter für Adoben. |
| [Adobe Analytics-Datenvorbereitung-Filter](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Anwenden [!DNL Kafka] Filter zum Ausschließen unnötiger Daten von der Erfassung |
| [Adobe Audience Manager-Quell-Connector-Filter](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Anwenden von Audience Manager-Quellverbindungsfiltern, um unnötige Daten von der Erfassung auszuschließen |
| [Zulassen von SDK-Datenfiltern](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | Alloy-Filter anwenden, um unnötige Daten von der Erfassung auszuschließen |
| [Serverseitige Datenfilter](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html?lang=en-better-data-governance) | Anwenden [!DNL Kafka] -Filter, um unnötige Daten von der Erfassung auszuschließen.  Weitere Informationen finden Sie in der Dokumentation unter [Ereignisse und Bedingungen](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) für weitere Informationen. |
| [Benutzeroberfläche des Lizenznutzungs-Dashboards](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Zeigen Sie eine Momentaufnahme der lizenzbezogenen Daten Ihres Unternehmens für die Experience Platform an. |
| [Datensatz-Overlap Report API](../../profile/tutorials/dataset-overlap-report.md) | Gibt die Datensätze aus, die am meisten zu Ihrer ansprechbaren Zielgruppe beitragen |
| [Unbekannte Profiles Report API](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) | Gibt die Auswirkungen der Anwendung der pseudonymen TTL für verschiedene Zeitschwellen aus |
| [Identity Overlap Report API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Gibt die Identitäts-Namespaces aus, die am meisten zu Ihrer ansprechbaren Zielgruppe beitragen |

{style=&quot;table-layout:auto&quot;}