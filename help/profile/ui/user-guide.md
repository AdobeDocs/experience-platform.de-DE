---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; einheitliches Profil; Einheitliches Profil; einheitliches Profil; Profil; rtcp; Profil aktivieren; Profil aktivieren; Vereinigungsschema; UNION PROFILE; Vereinigungsprofil
title: Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils
topic-legacy: guide
description: Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht Ihrer einzelnen Kunden und fasst Daten aus mehreren Kanälen (einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen. Dieses Dokument dient als Leitfaden für die Interaktion mit dem Echtzeit-Kundenprofil in der Benutzeroberfläche von Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 10%

---

# Handbuch für die [!DNL Real-time Customer Profile]-Benutzeroberfläche

[!DNL Real-time Customer Profile] erstellt eine ganzheitliche Ansicht Ihrer einzelnen Kunden, wobei Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten, kombiniert werden. Dieses Dokument dient als Leitfaden für die Interaktion mit [!DNL Real-time Customer Profile]-Daten in der Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses UI-Handbuch setzt ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste voraus, die mit der Verwaltung von [!DNL Real-time Customer Profiles] verbunden sind. Bevor Sie dieses Handbuch lesen oder in der Benutzeroberfläche arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Real-time Customer Profile]](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Identity Service]](../../identity-service/home.md): Ermöglicht  [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen bei der Erfassung in  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

## Übersicht

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Profile]** aus, um die Registerkarte **[!UICONTROL Übersicht]** mit dem Dashboard  zu öffnen.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, ist das Dashboard [!UICONTROL Profile] nicht sichtbar. Stattdessen werden auf der Registerkarte [!UICONTROL Übersicht] Links und Dokumentation angezeigt, die Ihnen bei den ersten Schritten mit dem Echtzeit-Kundenprofil helfen.

###  Profilesdashboard  {#profile-dashboard}

Das Dashboard **[!UICONTROL Profile]** enthält Schlüsselmetriken, die sich auf die Profildaten Ihres Unternehmens beziehen.

Weitere Informationen finden Sie im [Profil-Dashboard-Handbuch](../../dashboards/guides/profiles.md).

![](../../dashboards/images/profiles/dashboard-overview.png)

## Durchsuchen

Wählen Sie den Tab **[!UICONTROL Durchsuchen]** aus, um Profile nach Identität zu durchsuchen.

![](../images/user-guide/profiles-browse.png)

### Profilmetriken {#profile-metrics}

Auf der rechten Seite des Tabs **[!UICONTROL Durchsuchen]** befinden sich verschiedene wichtige Metriken, die mit Ihren Profildaten verbunden sind, darunter die Gesamtzahl der Profile [](#profile-count) sowie die Auflistung der Profile [nach Namespace](#profiles-by-namespace).

Diese Profilmetriken werden mit der standardmäßigen Zusammenführungsrichtlinie Ihres Unternehmens ausgewertet. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien, einschließlich der Definition einer standardmäßigen Zusammenführungsrichtlinie, finden Sie unter [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

Zusätzlich zu diesen Metriken bietet der Abschnitt Profilmetriken auch ein Datum und eine Uhrzeit der letzten Aktualisierung, die anzeigt, wann die Metriken zuletzt ausgewertet wurden.

![](../images/user-guide/profiles-profile-metrics.png)

### Anzahl der Profile {#profile-count}

Die Anzahl der Profile zeigt die Gesamtzahl der Profile an, die Ihr Unternehmen innerhalb von [!DNL Experience Platform] hat, nachdem die standardmäßige Zusammenführungsrichtlinie Ihres Unternehmens Profilfragmente zusammengeführt hat, um für jeden einzelnen Kunden ein einzelnes Profil zu erstellen. Mit anderen Worten: Ihre Organisation hat möglicherweise verschiedene Profilfragmente, die sich auf einen einzelnen Kunden beziehen, der mit Ihrer Marke über unterschiedliche Kanäle interagiert. Diese Fragmente würden jedoch zusammengeführt (gemäß der standardmäßigen Zusammenführungsrichtlinie) und eine Anzahl von „1“ zurückgeben, da sie alle mit derselben Person verbunden sind.

Die Profilanzahl umfasst auch Profile mit Attributen (Datensatzdaten) sowie Profile, die nur Zeitreihendaten (Ereignisdaten) enthalten, z. B. Adobe Analytics-Profile. Die Profilanzahl wird regelmäßig aktualisiert, um eine aktuelle Gesamtanzahl von Profilen in Platform bereitzustellen.

Wenn die Aufnahme von Datensätzen in den Speicher [!DNL Profile] die Anzahl um mehr als 5 % erhöht oder verringert, wird ein Auftrag ausgelöst, der die Anzahl aktualisiert. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für eine Zu- oder Abnahme um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Profilanzahl zu aktualisieren. Bei der Batch-Erfassung wird innerhalb von 15 Minuten nach erfolgreicher Aufnahme eines Batches in den Profilspeicher ein Auftrag ausgeführt, um die Profilanzahl zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht ist.

### Profile nach Namespace {#profiles-by-namespace}

Die Metrik **[!UICONTROL Profile nach Namespace]** zeigt die Gesamtanzahl und Aufschlüsselung der Namespaces für alle zusammengeführten Profile in Ihrem Profilspeicher an. Die Gesamtzahl der Profile nach Namespace (d. h. das Addieren der für jeden Namespace angezeigten Werte) ist immer höher als die Metrik für die Profilanzahl, da einem Profil mehrere Namespaces zugeordnet sein können. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

Ähnlich wie bei der Metrik [Profilanzahl](#profile-count) wird ein Auftrag ausgelöst, um die Namespace-Metriken zu aktualisieren, wenn durch die Aufnahme von Datensätzen in den [!DNL Profile]-Speicher die Anzahl um mehr als 5 % erhöht oder verringert wird. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für eine Zu- oder Abnahme um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Profilanzahl zu aktualisieren. Bei der Batch-Erfassung wird innerhalb von 15 Minuten nach erfolgreicher Aufnahme eines Batches in den [!DNL Profile]-Speicher ein Auftrag ausgeführt, um die Metriken zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht ist.

### Zusammenführungsrichtlinie

Der Selektor **[!UICONTROL Zusammenführungsrichtlinie]** wählt automatisch die standardmäßige Zusammenführungsrichtlinie für Ihre Organisation aus. Wenn Sie diese Zusammenführungsrichtlinie nicht verwenden möchten, können Sie `X` neben der standardmäßigen Zusammenführungsrichtlinie auswählen, um das Dialogfeld **[!UICONTROL Zusammenführungsrichtlinie]** zu öffnen, in dem Sie eine andere Zusammenführungsrichtlinie auswählen können.

Weitere Informationen zu Zusammenführungsrichtlinien und ihrer Rolle in Platform finden Sie unter [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

![](../images/user-guide/profiles-search-merge-policy.png)

### Identitäts-Namespace

Der Selektor **[!UICONTROL Identitäts-Namespace]** öffnet ein Dialogfeld, in dem Sie den Identitäts-Namespace auswählen können, mit dem Sie suchen möchten. Außerdem können Sie die Attribute, die bei Ihrer Suche angezeigt werden, anpassen, indem Sie das Filtersymbol auswählen und auswählen, welche Attribute Sie hinzufügen oder entfernen möchten.

![](../images/user-guide/profiles-search-filter.png)

Wählen Sie im Dialogfeld **[!UICONTROL Identitäts-Namespace]** aus, wählen Sie den Namespace aus, nach dem Sie suchen möchten, oder verwenden Sie die Suchleiste im Dialogfeld, um mit der Eingabe des Namens eines Namespace zu beginnen. Sie können einen Namespace auswählen, um weitere Details anzuzeigen. Sobald Sie den Namespace gefunden haben, den Sie verwenden möchten, können Sie das Optionsfeld auswählen und auf **[!UICONTROL Auswählen]** klicken, um fortzufahren.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Identitätswert

Nachdem Sie einen Identitäts-Namespace ausgewählt haben, kehren Sie zur Registerkarte **[!UICONTROL Durchsuchen]** zurück, auf der Sie einen **[!UICONTROL Identitätswert]** eingeben können. Dieser Wert ist spezifisch für ein einzelnes Kundenprofil und muss ein gültiger Eintrag für den angegebenen Namespace sein. Beispielsweise würde die Auswahl des Identitäts-Namespace &quot;E-Mail&quot;einen Identitätswert in Form einer gültigen E-Mail-Adresse erfordern.

![](../images/user-guide/profiles-show-profile.png)

Nachdem ein Wert eingegeben wurde, wählen Sie **[!UICONTROL Profil anzeigen]** und ein einzelnes Profil, das dem Wert entspricht, wird zurückgegeben. Wählen Sie **[!UICONTROL Profil-ID]** aus, um die Profildetails anzuzeigen.

![](../images/user-guide/profiles-display-profile.png)

### Profildetail {#profile-detail}

Nach Auswahl der **[!UICONTROL Profil-ID]** wird die Registerkarte **[!UICONTROL Detail]** geöffnet. Die auf der Registerkarte **[!UICONTROL Detail]** angezeigten Profilinformationen wurden aus mehreren Profilfragmenten zusammengeführt, um eine einzige Ansicht des einzelnen Kunden zu bilden. Dazu gehören Kundendetails wie grundlegende Attribute, verknüpfte Identitäten und Kanalpräferenzen. Die angezeigten Standardfelder können auch auf Organisationsebene geändert werden, um die bevorzugten Profilattribute anzuzeigen. Weitere Informationen zum Anpassen dieser Felder, einschließlich einer schrittweisen Anleitung zum Hinzufügen und Entfernen von Attributen und zum Ändern der Größe von Dashboard-Bedienfeldern, finden Sie im [Handbuch zur Profildetailanpassung](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

Sie können zusätzliche Informationen zum jeweiligen Profil anzeigen, indem Sie eine andere der verfügbaren Registerkarten auswählen. Diese Registerkarten umfassen Attribute, Ereignisse und Segmentzugehörigkeiten, die die Segmente anzeigen, für die das Profil derzeit qualifiziert ist.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Zusammenführungsrichtlinien

Wählen Sie im Hauptmenü **[!UICONTROL Profile]** die Registerkarte **[!UICONTROL Zusammenführungsrichtlinien]** aus, um eine Liste der zu Ihrer Organisation gehörenden Zusammenführungsrichtlinien anzuzeigen. Jede aufgelistete Richtlinie zeigt ihren Namen an, unabhängig davon, ob es sich um die standardmäßige Zusammenführungsrichtlinie handelt oder nicht, und die Schemaklasse, für die sie gilt.

Weiterführende Informationen zu Zusammenführungsrichtlinien finden Sie unter [Zusammenführungsrichtlinien – Übersicht](../merge-policies/overview.md).

![](../images/user-guide/profiles-merge-policies.png)

## Vereinigungsschema {#union-schema}

Wählen Sie im Hauptmenü **[!UICONTROL Profile]** die Registerkarte **[!UICONTROL Vereinigungsschema]** aus, um verfügbare Vereinigungsschemas für die erfassten Daten anzuzeigen. Ein Vereinigungsschema ist eine Kombination aller [!DNL Experience Data Model] (XDM)-Felder derselben Klasse, deren Schemas für die Verwendung in [!DNL Real-time Customer Profile] aktiviert wurden.

Weitere Informationen zu Vereinigungsschemas finden Sie im [UI-Handbuch für Vereinigungsschemas](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Nächste Schritte

Durch Lesen dieses Handbuchs wissen Sie jetzt, wie Sie Ihre [!DNL Profile]-Daten mithilfe der [!DNL Experience Platform]-Benutzeroberfläche anzeigen und verwalten können. Informationen zum Arbeiten mit Profildaten mithilfe der Echtzeit-Kundenprofil-API finden Sie im [Profil-Entwicklerhandbuch](../api/overview.md).
