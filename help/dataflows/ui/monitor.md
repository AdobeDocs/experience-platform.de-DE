---
title: Übersicht über das Monitoring-Dashboard
description: Erfahren Sie, wie Sie das Monitoring-Dashboard in der Benutzeroberfläche von Adobe Experience Platform verwenden.
exl-id: 06ea5380-d66e-45ae-aa02-c8060667da4e
source-git-commit: 710fa6930b27f95d34539a18881c0f9d23e1debd
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 4%

---

# Übersicht über das Monitoring-Dashboard

Verwenden Sie das Monitoring-Dashboard in der Adobe Experience Platform-Benutzeroberfläche, um die Journey Ihrer Daten von der Erfassung bis zur Aktivierung anzuzeigen. Im Monitoring-Dashboard haben Sie folgende Möglichkeiten:

* Überwachen Sie die Journey Ihrer Daten aus Quellen, Identitätsdienst, Echtzeit-Kundenprofil, Zielgruppen und schließlich in Zielen.
* Je nach Phase, in der sich Ihre Daten befinden, können Sie verschiedene Metriken und Status anzeigen.
* Filtern Sie Ihre Datenüberwachungsansicht nach Datentyp.

Das Monitoring-Dashboard unterstützt die Ansicht verschiedener Datentypen:

* **Kunde und Konto**: Kundendaten beziehen sich auf die in [Real-time Customer Data Platform](../../rtcdp/home.md) verwendeten Daten, während Kontodaten auf [Kontoprofildaten](../../rtcdp/accounts/account-profile-overview.md) verweisen, auf die bei einem Abonnement für [Real-Time CDP, B2B Edition](../../rtcdp/b2b-overview.md) zugegriffen werden kann. Wenn Ihre Real-Time CDP-Lizenz nicht Real-Time CDP, B2B Edition beinhaltet, können Sie nur das Monitoring-Dashboard verwenden, um Kundendaten zu überwachen.
* **Interessent**: [Prospect profiles](../../profile/ui/prospect-profile.md) werden verwendet, um Personen zu repräsentieren, die noch nicht mit Ihrem Unternehmen interagiert haben, aber mit denen Sie Kontakt aufnehmen möchten. Mit potenziellen Profilen können Sie Ihre Kundenprofile durch Attribute vertrauenswürdiger Drittanbieter-Partner ergänzen. Sie müssen über eine Lizenz für Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate verfügen, um den potenziellen Datentyp anzeigen zu können.
* **Anreicherung des Kontoprofils**: Mit Kontoprofilen können Sie Kontoinformationen aus mehreren Quellen vereinheitlichen. Sie müssen eine Lizenz für Real-Time CDP, B2B Edition besitzen, um die Anreicherungsdaten von Kontoprofilen überwachen zu können.

In diesem Dokument erfahren Sie, wie Sie mit dem Monitoring-Dashboard die Journey Ihrer Daten über verschiedene Experience Platform-Dienste hinweg überwachen können.

## Erste Schritte

Dieses Dokument setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Datenflüsse](../home.md): Datenflüsse sind Darstellungen von Datenaufträgen, die Daten über Experience Platform verschieben. Sie können den Arbeitsbereich &quot;Quellen&quot;verwenden, um Datenflüsse zu erstellen, die Daten von einer bestimmten Quelle zu Experience Platform erfassen.
* [Quellen](../../sources/home.md): Verwenden Sie Experience Platform-Quellen, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern zu erfassen.
* [Identity Service](../../identity-service/home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kundinnen und Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
* [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Segmentierung](../../segmentation/home.md): Verwenden Sie den Segmentierungsdienst, um Segmente und Zielgruppen aus Ihren Echtzeit-Kundenprofildaten zu erstellen.
* [Ziele](../../destinations/home.md): Ziele sind vordefinierte Integrationen mit häufig verwendeten Anwendungen, die die nahtlose Aktivierung von Daten aus Platform für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle ermöglichen.

## Handbuch zum Monitoring-Dashboard

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich unter [!UICONTROL Datenverwaltung] die Option **[!UICONTROL Überwachung]** aus.

![Das Monitoring-Dashboard in der Experience Platform-Benutzeroberfläche.](../assets/ui/monitor-overview/monitoring.png)

Wählen Sie **[!UICONTROL Datentyp]** und wählen Sie dann im Dropdown-Menü den Datentyp aus, den Sie anzeigen möchten. Datentypen werden von Experience-Datenmodell (XDM)-Schemaklasse definiert, um sicherzustellen, dass ihre Daten bei der Aufnahme in Experience Platform einem Standardformat entsprechen. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [B2B-Kontodatentyp](../../rtcdp/b2b-tutorial.md)
* [voraussichtlicher Datentyp](../../rtcdp/partner-data/prospecting.md)

Sie können Ihre Ansicht nach den folgenden Datentypen filtern:

>[!BEGINTABS]

>[!TAB Alle]

Wählen Sie **[!UICONTROL Alle]** aus, um Ihr Dashboard zu aktualisieren und Metriken zu allen Daten anzuzeigen, die im Laufe eines bestimmten Zeitraums in Experience Platform erfasst wurden.

![Der Überwachungsdatentyp, der auf &quot;Alle&quot; eingestellt ist.](../assets/ui/monitor-overview/all.png)

>[!TAB Kunde und Konto]

Wählen Sie **[!UICONTROL Kunde und Konto]** aus, um Ihr Dashboard zu aktualisieren und Metriken zu Kunden- und Kontodaten anzuzeigen, die im Laufe eines bestimmten Zeitraums in Experience Platform erfasst wurden.

![Der Überwachungsdatentyp, der auf &quot;Kunde und Konto&quot;eingestellt ist.](../assets/ui/monitor-overview/customer-account.png)

>[!TAB prospect]

Wählen Sie **[!UICONTROL Prospect]** aus, um Ihr Dashboard zu aktualisieren und Metriken zur Prospektion von Daten anzuzeigen, die im Laufe eines bestimmten Zeitraums in die Experience Platform aufgenommen wurden. **Hinweis**: Sie können Aktivitäten vom Typ &quot;Prospekt&quot;nur anzeigen, wenn Sie [ berechtigt sind, Daten nachzuschlagen](../../rtcdp/partner-data/prospecting.md).

![Der Überwachungsdatentyp, der auf &quot;Prospect&quot; gesetzt ist.](../assets/ui/monitor-overview/prospect.png)

>[!TAB Anreicherung des Kontoprofils]

Wählen Sie **[!UICONTROL Anreicherung des Kontoprofils]** aus, um Ihr Dashboard zu aktualisieren und Metriken zu Profilanreicherungsdaten anzuzeigen. **Hinweis**: Sie können die Metriken zur Anreicherung von Kontoprofilen nur anzeigen, wenn Sie über die Berechtigung für [B2B-Daten](../../rtcdp/b2b-tutorial.md) verfügen.

![Der Überwachungsdatentyp, der auf &quot;Anreicherung des Kontoprofils&quot;eingestellt ist.](../assets/ui/monitor-overview/account-profile-enrichment.png)

>[!ENDTABS]

Verwenden Sie die obere Kopfzeile des Dashboards, um eine dienstübergreifende Überwachung zu ermöglichen. Sie können Ihre Metriken und Grafiken filtern, indem Sie die von Ihnen ausgewählte Funktionskarte in der Kopfzeile der Datenkategorie auswählen.

>[!BEGINTABS]

>[!TAB Quellen]

Wählen Sie **[!UICONTROL Quellen]** aus, um Metriken zur Erfassungsrate der Quellen anzuzeigen. Weitere Informationen finden Sie im Handbuch zum [Überwachen von Quelldaten](monitor-sources.md) .

![Das Monitoring-Dashboard in der Benutzeroberfläche mit der ausgewählten Quellkarte.](../assets/ui/monitor-overview/sources.png)

>[!TAB Identitäten]

Wählen Sie **[!UICONTROL Identitäten]** aus, um die Verarbeitungserfolgsrate Ihrer Identitätsdaten anzuzeigen. Weitere Informationen finden Sie im Handbuch zum [Überwachen von Identitätsdaten](monitor-identities.md) .

![Das Monitoring-Dashboard in der Benutzeroberfläche mit der ausgewählten Identitätskarte.](../assets/ui/monitor-overview/identities.png)

>[!TAB Profile]

Wählen Sie **[!UICONTROL Profile]** aus, um die Verarbeitungserfolgsrate Ihrer Profildaten anzuzeigen. Weitere Informationen finden Sie im Handbuch zum [Überwachen von Profildaten](monitor-profiles.md) .

![Das Monitoring-Dashboard in der Benutzeroberfläche mit der ausgewählten Profilkarte.](../assets/ui/monitor-overview/profiles.png)

>[!TAB Zielgruppen]

Wählen Sie **[!UICONTROL Zielgruppen]** aus, um Metriken zu Ihren Zielgruppen und Segmentierungsaufträgen anzuzeigen. Weitere Informationen finden Sie im Handbuch zum [Überwachen von Zielgruppendaten](monitor-audiences.md) .

![Das Monitoring-Dashboard in der Benutzeroberfläche mit ausgewählter Zielgruppenkarte.](../assets/ui/monitor-overview/audiences.png)

>[!TAB Ziele]

Wählen Sie **[!UICONTROL Ziele]** aus, um Metriken für Ihre [!UICONTROL Streaming-Aktivierungsrate] und die [!UICONTROL Ausführung des fehlgeschlagenen Batch-Datenflusses] anzuzeigen. Weitere Informationen finden Sie im Handbuch zum [Überwachen von Zieldaten](monitor-destinations.md) .

![Das Monitoring-Dashboard in der Benutzeroberfläche mit der ausgewählten Zielkarte.](../assets/ui/monitor-overview/destinations.png)

>[!ENDTABS]

### Überwachungszeitrahmen konfigurieren {#configure-monitoring-time-frame}

Standardmäßig zeigt das Monitoring-Dashboard Metriken zu Daten an, die in den letzten 24 Stunden erfasst wurden. Um den Zeitrahmen zu aktualisieren, wählen Sie **[!UICONTROL Letzte 24 Stunden]** aus.

![Das Monitoring-Dashboard in der Benutzeroberfläche mit der ausgewählten Zeitkonfiguration.](../assets/ui/monitor-overview/select-time.png)

Sie können im angezeigten Dialogfeld einen neuen Zeitrahmen für Ihre Datenüberwachungsansicht konfigurieren. Sie haben die Möglichkeit, einen benutzerdefinierten Zeitrahmen zu erstellen oder aus der Liste der vorkonfigurierten Optionen auszuwählen:

* [!UICONTROL Letzte 24 Stunden]
* [!UICONTROL Letzte 7 Tage]
* [!UICONTROL Letzte 30 Tage]

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![Das Popup-Fenster für die Zeitrahmen-Konfiguration im Monitoring-Dashboard.](../assets/ui/monitor-overview/update-time.png)

## Nächste Schritte

Durch Lesen dieses Dokuments können Sie jetzt in der Benutzeroberfläche durch das Monitoring-Dashboard navigieren. Informationen zum Überwachen von Daten für einen bestimmten Experience Platform-Dienst finden Sie in der folgenden Dokumentation:

* [Überwachen Sie die Quelldaten](monitor-sources.md).
* [Überwachen von Identitätsdaten](monitor-identities.md).
* [Überwachen von Profildaten](monitor-profiles.md).
* [Überwachen von Zielgruppendaten](monitor-audiences.md).
* [Überwachen von Zieldaten](monitor-destinations.md).
