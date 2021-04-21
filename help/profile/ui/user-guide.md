---
keywords: Experience Platform;Profil;Echtzeit-Profil des Kunden;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;RTCP;Profil aktivieren;Profil aktivieren;Vereinigung Schema;VEREINIGUNG PROFIL;Vereinigung Profil
title: Handbuch zur Benutzeroberfläche des Profils in Echtzeit
topic-legacy: guide
description: Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht Ihrer einzelnen Kunden und fasst Daten aus mehreren Kanälen (einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen. Dieses Dokument dient als Leitfaden für die Interaktion mit dem Echtzeit-Kundenprofil in der Benutzeroberfläche von Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 9%

---

# [!DNL Real-time Customer Profile] UI-Handbuch

[!DNL Real-time Customer Profile] erstellt eine ganzheitliche Ansicht der einzelnen Kunden und kombiniert Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten. Dieses Dokument dient als Leitfaden für die Interaktion mit [!DNL Real-time Customer Profile]-Daten in der Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses UI-Handbuch erfordert ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste, die mit der Verwaltung von [!DNL Real-time Customer Profiles] verbunden sind. Bevor Sie dieses Handbuch lesen oder in der Benutzeroberfläche arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Real-time Customer Profile]](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Identity Service]](../../identity-service/home.md): Ermöglicht  [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die sie eingeordnet werden  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

## Übersicht

Wählen Sie in der Benutzeroberfläche &quot;Experience Platform&quot;in der linken Navigationsleiste **[!UICONTROL Profil]** aus, um die Registerkarte **[!UICONTROL Übersicht]** zu öffnen. Diese Registerkarte enthält Links zu Dokumentationen und Videos, die Ihnen helfen, Profile zu verstehen und mit ihnen zu arbeiten.

![](../images/user-guide/profiles-overview.png)

### (Alpha) Profil-Dashboard

>[!IMPORTANT]
>
>Die Dashboard-Funktion ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Bei einigen Benutzern bietet die Auswahl von **[!UICONTROL Profilen]** im linken Navigationsbereich und das Öffnen der Registerkarte **[!UICONTROL Übersicht]** ein Dashboard, in dem die Schlüsselmetriken im Zusammenhang mit Ihren Profil-Daten skizziert werden.

Weitere Informationen finden Sie im Dashboard [Profil Guide](profile-dashboard.md).

## Durchsuchen

Wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]**, um Profile nach Identität zu durchsuchen.

![](../images/user-guide/profiles-browse.png)

### Profil-Metriken {#profile-metrics}

Auf der rechten Seite des Registers **[!UICONTROL Durchsuchen]** stehen einige wichtige Metriken zu Ihren Profil-Daten, einschließlich der Gesamtzahl [Profil-Anzahl](#profile-count) sowie der Auflistung von [Profilen nach Namensraum](#profiles-by-namespace).

Diese Profil-Metriken werden mit der standardmäßigen Zusammenführungsrichtlinie Ihres Unternehmens ausgewertet. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien, einschließlich der Definition einer standardmäßigen Zusammenführungsrichtlinie, finden Sie im Benutzerhandbuch [Richtlinien zusammenführen](merge-policies.md).

Zusätzlich zu diesen Metriken bietet der Bereich &quot;Profil-Metriken&quot;auch ein Datum und eine Uhrzeit, die zuletzt aktualisiert wurden und anzeigen, wann die Metriken zuletzt bewertet wurden.

![](../images/user-guide/profiles-profile-metrics.png)

### Anzahl der Profile {#profile-count}

Die Anzahl der Profil zeigt die Gesamtzahl der Profil in Ihrem Unternehmen innerhalb von [!DNL Experience Platform] an, nachdem die standardmäßige Zusammenführungsrichtlinie Ihres Unternehmens Profil-Fragmente zusammengeführt hat, um ein einzelnes Profil für jeden einzelnen Kunden zu erstellen. Mit anderen Worten: Ihre Organisation hat möglicherweise verschiedene Profilfragmente, die sich auf einen einzelnen Kunden beziehen, der mit Ihrer Marke über unterschiedliche Kanäle interagiert. Diese Fragmente würden jedoch zusammengeführt (gemäß der standardmäßigen Zusammenführungsrichtlinie) und eine Anzahl von „1“ zurückgeben, da sie alle mit derselben Person verbunden sind.

Die Profil-Anzahl umfasst auch Profil mit Attributen (Datensatzdaten) sowie Profil, die nur Zeitreihendaten (Ereignis) enthalten, wie z. B. Adobe Analytics-Profil. Die Anzahl der Profil wird regelmäßig aktualisiert, um eine aktuelle Gesamtanzahl von Profilen innerhalb der Plattform bereitzustellen.

Wenn die Erfassung von Datensätzen in den [!DNL Profile]-Speicher die Anzahl um mehr als 5 % erhöht oder verringert, wird ein Auftrag zur Aktualisierung der Anzahl ausgelöst. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Anzahl der Profile zu aktualisieren. Bei der Stapelverarbeitung wird innerhalb von 15 Minuten nach dem erfolgreichen Einsetzen eines Stapels in den Profil Store ein Auftrag ausgeführt, um die Anzahl der Profil zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde.

### Profil nach Namensraum {#profiles-by-namespace}

Die Metrik **[!UICONTROL Profil nach Namensraum]** zeigt die Gesamtzahl und Aufschlüsselung der Namensraum für alle zusammengeführten Profil im Profil Store an. Die Gesamtanzahl der Profil nach Namensraum (d. h. das Addieren der für jeden Namensraum angezeigten Werte) ist immer höher als die Metrik für die Anzahl der Profil, da ein Profil mit mehreren Namensräumen verknüpft sein könnte. Wenn ein Kunde beispielsweise auf mehr als einem Kanal mit Ihrer Marke interagiert, werden mehrere Namensraum mit diesem Kunden verknüpft.

Ähnlich wie bei der Metrik [Profil](#profile-count) wird bei der Erfassung von Datensätzen im [!DNL Profile]-Speicher die Anzahl um mehr als 5 % erhöht oder verringert, ein Auftrag zur Aktualisierung der Namensraum-Metriken ausgelöst. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Anzahl der Profile zu aktualisieren. Bei der Stapelverarbeitung wird innerhalb von 15 Minuten nach dem erfolgreichen Einsetzen eines Stapels in den [!DNL Profile]-Speicher ein Auftrag zur Aktualisierung der Metriken ausgeführt, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde.

### Richtlinie zusammenführen

Mit der Auswahl **[!UICONTROL Richtlinie zusammenführen]** wird automatisch die standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen ausgewählt. Wenn Sie diese Richtlinie zum Zusammenführen nicht verwenden möchten, können Sie das Dialogfeld `X` neben der Standardrichtlinie zum Zusammenführen auswählen, um das Dialogfeld **[!UICONTROL Richtlinie zum Zusammenführen auswählen, in dem Sie eine andere Richtlinie zum Zusammenführen auswählen können.]**

Weitere Informationen zu Zusammenführungsrichtlinien und ihrer Rolle in der Plattform finden Sie im Handbuch [Richtlinien in der Benutzeroberfläche zusammenführen](merge-policies.md).

![](../images/user-guide/profiles-search-merge-policy.png)

### Identitäts-Namensraum

Mit der Auswahl **[!UICONTROL Identity Namensraum]** wird ein Dialogfeld geöffnet, in dem Sie den Identitäts-Namensraum auswählen können, mit dem Sie suchen möchten. Sie können die Attribute, die bei der Suche angezeigt werden, anpassen, indem Sie das Filtersymbol auswählen und festlegen, welche Attribute Sie hinzufügen oder entfernen möchten.

![](../images/user-guide/profiles-search-filter.png)

Wählen Sie im Dialogfeld **[!UICONTROL Identitätsname auswählen]** den Namensraum aus, nach dem Sie suchen möchten, oder verwenden Sie die Suchleiste im Dialogfeld, um mit der Eingabe des Namensraums zu beginnen. Sie können einen Namensraum auswählen, um weitere Details Ansicht. Sobald Sie den gewünschten Namensraum gefunden haben, können Sie das Optionsfeld auswählen und **[!UICONTROL Auswahl]** drücken, um fortzufahren.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Identitätswert

Nach Auswahl eines Identitäts-Namensraums kehren Sie zur Registerkarte **[!UICONTROL Durchsuchen]** zurück, wo Sie einen **[!UICONTROL Identitätswert]** eingeben können. Dieser Wert ist spezifisch für ein einzelnes Profil und muss ein gültiger Eintrag für den bereitgestellten Namensraum sein. Wenn Sie beispielsweise den Identitäts-Namensraum &quot;E-Mail&quot;auswählen, ist ein Identitätswert in Form einer gültigen E-Mail-Adresse erforderlich.

![](../images/user-guide/profiles-show-profile.png)

Nachdem ein Wert eingegeben wurde, wählen Sie **[!UICONTROL Profil anzeigen]** und ein Profil, das dem Wert entspricht, wird zurückgegeben. Wählen Sie die **[!UICONTROL Profil-ID]** aus, um die Details des Profils Ansicht.

![](../images/user-guide/profiles-display-profile.png)

### Profil Detail {#profile-detail}

Wenn Sie die **[!UICONTROL Profil-ID]** auswählen, wird die Registerkarte **[!UICONTROL Detail]** geöffnet. Die auf der Registerkarte **[!UICONTROL Detail]** angezeigten Informationen zum Profil wurden aus mehreren Profil-Fragmenten zusammengeführt, um eine Ansicht des jeweiligen Kunden zu bilden. Dazu gehören Kundendetails wie Basisattribute, verknüpfte Identitäten und Voreinstellungen für Kanal. Die angezeigten Standardfelder können auch auf organisatorischer Ebene geändert werden, um bevorzugte Profil-Attribute anzuzeigen. Weitere Informationen zum Anpassen dieser Felder, einschließlich schrittweiser Anleitungen zum Hinzufügen und Entfernen von Attributen und zum Ändern der Größe von Dashboard-Bedienfeldern, finden Sie im Handbuch [Profil-Detailanpassung](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

Sie können weitere Informationen zum jeweiligen Profil durch Auswahl einer anderen verfügbaren Registerkarte Ansicht werden. Zu diesen Registerkarten gehören Attribute, Ereignis und Segmentmitgliedschaften, die die Segmente anzeigen, für die das Profil derzeit qualifiziert ist.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Zusammenführungsrichtlinien

Wählen Sie im Hauptmenü **[!UICONTROL Profil]** die Registerkarte **[!UICONTROL Richtlinien zusammenführen]** aus, um eine Liste der zu Ihrem Unternehmen gehörenden Zusammenführungsrichtlinien Ansicht. Jede aufgelistete Richtlinie zeigt ihren Namen an, unabhängig davon, ob es sich um die standardmäßige Zusammenführungsrichtlinie handelt oder nicht, sowie die Schema-Klasse, für die sie gilt.

Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im Handbuch [Richtlinien in der Benutzeroberfläche zusammenführen](merge-policies.md).

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mit der Echtzeit-Kunden-Profil-API finden Sie im [Endpunkt-Handbuch Zusammenführungsrichtlinien](../api/merge-policies.md).

![](../images/user-guide/profiles-merge-policies.png)

## Vereinigungsschema {#union-schema}

Wählen Sie im Hauptmenü **[!UICONTROL Profil]** die Registerkarte **[!UICONTROL Vereinigung Schema]** aus, um die verfügbaren Schema für die Vereinigung Ihrer erfassten Daten Ansicht. Ein Vereinigung-Schema ist eine Zusammenführung aller [!DNL Experience Data Model] (XDM)-Felder derselben Klasse, deren Schema für die Verwendung in [!DNL Real-time Customer Profile] aktiviert wurden.

Weitere Informationen zu Schemas in der Vereinigung finden Sie im Handbuch [Vereinigung Schema UI guide](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Nächste Schritte

Durch Lesen dieses Handbuchs wissen Sie jetzt, wie Sie Ihre [!DNL Profile]-Daten mit der [!DNL Experience Platform]-Benutzeroberfläche Ansicht und verwalten. Informationen zum Arbeiten mit Profil-Daten mithilfe der Echtzeit-Customer Profil API finden Sie im [Profil Developer Guide](../api/overview.md).
