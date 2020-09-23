---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile;Union schema;UNION PROFILE;union profile
title: Benutzerhandbuch zum Echtzeit-Kundenprofil
topic: guide
description: Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht Ihrer einzelnen Kunden und fasst Daten aus mehreren Kanälen (einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen. Dieses Dokument dient als Leitfaden für die Interaktion mit dem Echtzeit-Kundenprofil in der Benutzeroberfläche von Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 11%

---


# [!DNL Real-time Customer Profile] Benutzerhandbuch

[!DNL Real-time Customer Profile] erstellt eine ganzheitliche Ansicht der einzelnen Kunden und kombiniert Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten.

This document serves as a guide for interacting with [!DNL Real-time Customer Profile] data in the Adobe Experience Platform user interface.

## Erste Schritte

Dieses Benutzerhandbuch erfordert ein Verständnis der verschiedenen mit der Verwaltung verbundenen [!DNL Experience Platform] Dienste [!DNL Real-time Customer Profiles]. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Dienste:

* [[!DNL Echtzeit-Profil]](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL-Identitätsdienst]](../../identity-service/home.md): Ermöglicht die [!DNL Real-time Customer Profile] Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die sie eingeordnet werden [!DNL Platform].
* [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

## Übersicht

Wählen Sie in der [[!DNL Experience Platform] Benutzeroberfläche](http://platform.adobe.com)im linken Navigationsbereich die Option &quot; **[!UICONTROL Profil]** &quot;, um die Registerkarte &quot; **[!UICONTROL Übersicht]** &quot;zu öffnen. Diese Registerkarte enthält Links zu Dokumentationen und Videos, die Ihnen helfen, Profile zu verstehen und mit ihnen zu arbeiten.

![](../images/user-guide/profiles-overview.png)

## Durchsuchen

Wählen Sie die Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;aus, um nach Profilen anhand ihrer Identität zu suchen.

![](../images/user-guide/profiles-browse.png)

### Profil-Metriken {#profile-metrics}

Auf der rechten Seite der Registerkarte &quot; [!UICONTROL Durchsuchen] &quot;finden Sie eine Reihe wichtiger Metriken zu Ihren Profil-Daten, darunter die Gesamtzahl der [Profil](#profile-count) sowie eine Auflistung der [Profil nach Namensraum](#profiles-by-namespace).

Diese Profil-Metriken werden mit der standardmäßigen Zusammenführungsrichtlinie Ihres Unternehmens ausgewertet. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien, einschließlich der Definition einer standardmäßigen Zusammenführungsrichtlinie, finden Sie im [Benutzerhandbuch](merge-policies.md)&quot;Richtlinien zusammenführen&quot;.

Zusätzlich zu diesen Metriken bietet der Bereich &quot;Profil-Metriken&quot;auch das Datum und die Uhrzeit der [!UICONTROL letzten Aktualisierung] , die anzeigen, wann die Metriken zuletzt ausgewertet wurden.

![](../images/user-guide/profiles-profile-metrics.png)

### Anzahl der Profile {#profile-count}

The profile count displays the total number of profiles your organization has within [!DNL Experience Platform], after your organization&#39;s default merge policy has merged together profile fragments to form a single profile for each individual customer. Mit anderen Worten: Ihre Organisation hat möglicherweise verschiedene Profilfragmente, die sich auf einen einzelnen Kunden beziehen, der mit Ihrer Marke über unterschiedliche Kanäle interagiert. Diese Fragmente würden jedoch zusammengeführt (gemäß der standardmäßigen Zusammenführungsrichtlinie) und eine Anzahl von „1“ zurückgeben, da sie alle mit derselben Person verbunden sind.

Die Profil-Anzahl umfasst auch Profil mit Attributen (Datensatzdaten) sowie Profil, die nur Zeitreihendaten (Ereignis) enthalten, wie z. B. Adobe Analytics-Profil. Die Anzahl der Profil wird regelmäßig aktualisiert, um eine aktuelle Gesamtanzahl von Profilen innerhalb der Plattform bereitzustellen.

Wenn die Erfassung von Datensätzen im [!DNL Profile] Store die Anzahl um mehr als 5 % erhöht oder verringert, wird ein Auftrag zur Aktualisierung der Anzahl ausgelöst. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Anzahl der Profile zu aktualisieren. Bei der Stapelverarbeitung wird innerhalb von 15 Minuten nach dem erfolgreichen Einsetzen eines Stapels in den Profil Store ein Auftrag ausgeführt, um die Anzahl der Profil zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde.

### Profile nach Namensraum {#profiles-by-namespace}

Die Metrik &quot; **[!UICONTROL Profil nach Namensraum]** &quot;zeigt die Gesamtanzahl und Unterteilung der Namensraum für alle zusammengeführten Profil im Profil Store an. Die Gesamtanzahl der Profil nach Namensraum (d. h. das Addieren der für jeden Namensraum angezeigten Werte) ist immer höher als die Metrik für die Anzahl der Profil, da ein Profil mit mehreren Namensräumen verknüpft sein könnte. Wenn ein Kunde beispielsweise auf mehr als einem Kanal mit Ihrer Marke interagiert, werden mehrere Namensraum mit diesem Kunden verknüpft.

Ähnlich wie bei der Metrik für die [Profil-Zählung](#profile-count) wird ein Auftrag zur Aktualisierung der Namensraum-Metriken ausgelöst, wenn die Erfassung von Datensätzen in den [!DNL Profile] Store um mehr als 5 % erhöht oder verringert wird. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Anzahl der Profile zu aktualisieren. Bei der Stapelverarbeitung wird innerhalb von 15 Minuten nach dem erfolgreichen Einsetzen eines Stapels in den [!DNL Profile] Store ein Auftrag zur Aktualisierung der Metriken ausgeführt, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde.

### Richtlinie zusammenführen

Mit der **[!UICONTROL Auswahl der Richtlinie]** zusammenführen wird automatisch die standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen ausgewählt. Wenn Sie diese Richtlinie nicht verwenden möchten, können Sie das `X` Kontrollkästchen neben der standardmäßigen Zusammenführungsrichtlinie auswählen, um das Dialogfeld &quot; **[!UICONTROL Zusammenführungsrichtlinie]** auswählen&quot;zu öffnen, in dem Sie eine andere Richtlinie für die Zusammenführung auswählen können. Weitere Informationen zu Zusammenführungsrichtlinien und ihrer Rolle innerhalb der Plattform finden Sie im Benutzerhandbuch zu [Zusammenführungsrichtlinien](merge-policies.md).

![](../images/user-guide/profiles-search-merge-policy.png)

### Identitäts-Namensraum

Mit der **[!UICONTROL Identitäts-Namensraum]** -Auswahl wird ein Dialogfeld geöffnet, in dem Sie den Identitäts-Namensraum auswählen können, mit dem Sie suchen möchten, und die Attribute anpassen können, die bei der Suche angezeigt werden, indem Sie das Filtersymbol auswählen und festlegen, welche Attribute Sie hinzufügen oder entfernen möchten.

![](../images/user-guide/profiles-search-filter.png)

Wählen Sie im Dialogfeld &quot;Identitätsnamen **** auswählen&quot;den Namensraum aus, nach dem Sie suchen möchten, oder verwenden Sie die Suchleiste im Dialogfeld, um den Namensraum einzugeben. Sie können einen Namensraum auswählen, um weitere Details Ansicht. Sobald Sie den gewünschten Namensraum gefunden haben, können Sie das Optionsfeld auswählen und auf **[!UICONTROL Auswählen]** klicken, um fortzufahren.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Identitätswert

Nach Auswahl eines [!UICONTROL Identitäts-Namensraums]kehren Sie zur Registerkarte &quot; [!UICONTROL Durchsuchen] &quot;zurück, auf der Sie einen **[!UICONTROL Identitätswert]** eingeben können. Dieser Wert ist spezifisch für ein einzelnes Profil und muss ein gültiger Eintrag für den bereitgestellten Namensraum sein. Wenn Sie beispielsweise den [!UICONTROL Identitäts-Namensraum] &quot;E-Mail&quot;auswählen, ist ein [!UICONTROL Identitätswert] in Form einer gültigen E-Mail-Adresse erforderlich.

![](../images/user-guide/profiles-show-profile.png)

Nachdem ein Wert eingegeben wurde, wählen Sie &quot;Profil **[!UICONTROL anzeigen]** &quot;und ein Profil, das dem Wert entspricht, wird zurückgegeben. Wählen Sie die **[!UICONTROL Profil-ID]** aus, um die Details des Profils Ansicht.

![](../images/user-guide/profiles-display-profile.png)

### Profil {#profile-detail}

Nach Auswahl der [!UICONTROL Profil-ID]wird die Registerkarte &quot; **[!UICONTROL Details]** &quot;geöffnet. The profile information displayed on the [!UICONTROL Detail] tab has been merged together from multiple profile fragments to form a single view of the individual customer. Dazu gehören Kundendetails wie grundlegende Attribute, verknüpfte Identitäten und Voreinstellungen für Kanal. Die angezeigten Standardfelder können auch auf organisatorischer Ebene geändert werden, um bevorzugte Profil-Attribute anzuzeigen. Weitere Informationen zum Anpassen dieser Felder, einschließlich einer schrittweisen Anleitung zum Hinzufügen und Entfernen von Attributen und zum Ändern der Größe von Dashboard-Bedienfeldern, finden Sie im Handbuch zur [Profil-Detailanpassung](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

Sie können weitere Informationen zum jeweiligen Profil durch Auswahl einer anderen verfügbaren Registerkarte Ansicht werden. Zu diesen Registerkarten gehören [!UICONTROL Attribute], [!UICONTROL Ereignis]und die [!UICONTROL Segmentmitgliedschaft], in der die [!UICONTROL Segmente] angezeigt werden, für die das Profil derzeit qualifiziert ist.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Zusammenführungsrichtlinien

Wählen Sie im Hauptmenü &quot; [!UICONTROL Profile] &quot;die Registerkarte &quot;Richtlinien **[!UICONTROL zusammenführen&quot;]** , um eine Liste der zu Ihrem Unternehmen gehörenden Zusammenführungsrichtlinien Ansicht. Jede aufgelistete Richtlinie zeigt an: ihren Namen; ob sie die standardmäßige Zusammenführungsrichtlinie ist oder nicht; das Schema, auf das sie angewendet wird.

For more information on merge policies, see the [merge policies user guide](merge-policies.md).

![](../images/user-guide/profiles-merge-policies.png)

## Vereinigungsschema {#union-schema}

Wählen Sie im Hauptmenü &quot; [!UICONTROL Profil] &quot;die Registerkarte &quot;Schema **[!UICONTROL der]** Vereinigung&quot;aus, um die Schema der Vereinigung für Ihre Profil-Daten Ansicht. A union schema is an amalgamation of all [!DNL Experience Data Model] (XDM) fields under the same class, whose schemas have been enabled for use in [!DNL Real-time Customer Profile]. Wenn Sie auf der linken Seite eine Klasse aus der [!UICONTROL Class] -Liste auswählen, können Sie die Struktur des Schemas auf der Arbeitsfläche Ansicht werden. Wenn Sie beispielsweise &quot;[!DNL XDM Profile]&quot;auswählen, wird das Schema &quot;Vereinigung&quot;für die [!DNL XDM Individual Profile] Klasse angezeigt.

Weitere Informationen zu Schemas der Vereinigung und ihrer Rolle in Adobe Experience Platform finden Sie im Abschnitt zu Schemas der Vereinigung im Handbuch zur [Schema-Zusammensetzung](../../xdm/schema/composition.md).

![](../images/user-guide/profiles-union-schema.png)

## Nächste Schritte

By reading this guide, you now know how to view and manage your [!DNL Profile] data using the [!DNL Experience Platform] UI. Informationen zum Arbeiten mit Profil-Daten mithilfe der Echtzeit-Customer Profil-API finden Sie im [Profil Developer Guide](../api/overview.md).