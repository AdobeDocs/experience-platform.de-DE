---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Benutzerhandbuch zum Echtzeit-Kundenprofil
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 11%

---


# [!DNL Real-time Customer Profile] Benutzerhandbuch

[!DNL Real-time Customer Profile] erstellt eine ganzheitliche Ansicht der einzelnen Kunden und kombiniert Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten.

This document serves as a guide for interacting with [!DNL Real-time Customer Profile] in the Adobe Experience Platform user interface.

## Erste Schritte

Dieses Benutzerhandbuch erfordert ein Verständnis der verschiedenen mit der Verwaltung verbundenen [!DNL Experience Platform] Dienste [!DNL Real-time Customer Profiles]. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Dienste:

* [!DNL Real-time Customer Profile](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [!DNL Identity Service](../../identity-service/home.md): Ermöglicht die [!DNL Real-time Customer Profile] Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die sie eingeordnet werden [!DNL Platform].
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

## Übersicht

Klicken Sie im [!DNL Experience Platform UI](http://platform.adobe.com)linken Navigationsbereich auf **[!UICONTROL Profile]** , um die Registerkarte _[!UICONTROL Übersicht]_zu öffnen. Diese Registerkarte enthält Links zu Dokumentationen und Videos, die Ihnen helfen, Profile zu verstehen und mit ihnen zu arbeiten.

![](../images/user-guide/profiles-overview.png)

## Durchsuchen

Wählen Sie die Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;aus, um nach Profilen anhand ihrer Identität zu suchen.

![](../images/user-guide/profiles-browse.png)

### Profil-Metriken {#profile-metrics}

Auf der rechten Seite der Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;finden Sie eine Reihe wichtiger Metriken zu Ihren Profil-Daten, darunter die Gesamtzahl der [Profil](#profile-count) sowie eine Auflistung der [Profil nach Namensraum](#profiles-by-namespace).

Diese Profil-Metriken werden mit der standardmäßigen Zusammenführungsrichtlinie Ihres Unternehmens ausgewertet. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien, einschließlich der Definition einer standardmäßigen Zusammenführungsrichtlinie, finden Sie im [Benutzerhandbuch](merge-policies.md)&quot;Richtlinien zusammenführen&quot;.

Zusätzlich zu diesen Metriken bietet der Bereich &quot;Profil-Metriken&quot;auch das Datum und die Uhrzeit der *letzten Aktualisierung* , die anzeigen, wann die Metriken zuletzt ausgewertet wurden.

![](../images/user-guide/profiles-profile-metrics.png)

### Anzahl der Profile {#profile-count}

The profile count displays the total number of profiles your organization has within [!DNL Experience Platform], after your organization&#39;s default merge policy has merged together profile fragments to form a single profile for each individual customer. Mit anderen Worten: Ihre Organisation hat möglicherweise verschiedene Profilfragmente, die sich auf einen einzelnen Kunden beziehen, der mit Ihrer Marke über unterschiedliche Kanäle interagiert. Diese Fragmente würden jedoch zusammengeführt (gemäß der standardmäßigen Zusammenführungsrichtlinie) und eine Anzahl von „1“ zurückgeben, da sie alle mit derselben Person verbunden sind.

Die Profil-Anzahl umfasst auch Profil mit Attributen (Datensatzdaten) sowie Profil, die nur Zeitreihendaten (Ereignis) enthalten, wie z. B. Adobe Analytics-Profil. Die Anzahl der Profil wird regelmäßig aktualisiert, um eine aktuelle Gesamtanzahl von Profilen innerhalb der Plattform bereitzustellen.

Wenn die Erfassung von Datensätzen in die [!DNL Profile Store] Anzahl um mehr als 5 % erhöht oder verringert wird, wird ein Auftrag zur Aktualisierung der Anzahl ausgelöst. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Anzahl der Profile zu aktualisieren. Bei der Stapelverarbeitung wird innerhalb von 15 Minuten nach dem erfolgreichen Einsetzen eines Stapels in den Profil Store ein Auftrag ausgeführt, um die Anzahl der Profil zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde.

### Profile nach Namensraum {#profiles-by-namespace}

Die Metrik &quot; *[!UICONTROL Profil nach Namensraum]* &quot;zeigt die Gesamtanzahl und Unterteilung der Namensraum für alle zusammengeführten Profil im Profil Store an. Die Gesamtanzahl der Profil nach Namensraum (d. h. das Addieren der für jeden Namensraum angezeigten Werte) ist immer höher als die Metrik für die Anzahl der Profil, da ein Profil mit mehreren Namensräumen verknüpft sein könnte. Wenn ein Kunde beispielsweise auf mehr als einem Kanal mit Ihrer Marke interagiert, werden mehrere Namensraum mit diesem Kunden verknüpft.

Ähnlich wie bei der Metrik für die [Profil-Zählung](#profile-count) wird ein Auftrag zur Aktualisierung der Namensraum-Metriken ausgelöst, wenn durch die Erfassung von Datensätzen in die [!DNL Profile Store] Metrik die Anzahl um mehr als 5 % erhöht oder verringert wird. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Anzahl der Profile zu aktualisieren. Bei der Stapelverarbeitung wird innerhalb von 15 Minuten nach dem erfolgreichen Einsetzen eines Stapels in den Bericht ein Auftrag zur Aktualisierung der Metriken ausgeführt, [!DNL Profile Store]wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde.

### Richtlinie zusammenführen

Mit der **[!UICONTROL Auswahl der Richtlinie]** zusammenführen wird automatisch die standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen ausgewählt. Wenn Sie diese Richtlinie nicht verwenden möchten, können Sie die `X` Option neben der Standardrichtlinie für die Zusammenführung auswählen auswählen, um ein Dialogfeld *[!UICONTROL zur Auswahl der Zusammenführungsrichtlinie]* zu öffnen, in dem Sie eine andere Zusammenführungsrichtlinie auswählen können. Weitere Informationen zu Richtlinien zum Zusammenführen finden Sie im Benutzerhandbuch [](merge-policies.md)&quot;Richtlinien zusammenführen&quot;.

![](../images/user-guide/profiles-search-merge-policy.png)

### Identitäts-Namensraum

Mit der **[!UICONTROL Identitäts-Namensraum]** -Auswahl wird ein Dialogfeld geöffnet, in dem Sie den Identitäts-Namensraum auswählen können, mit dem Sie suchen möchten, und die Attribute anpassen können, die bei der Suche angezeigt werden, indem Sie das Filtersymbol auswählen und festlegen, welche Attribute Sie hinzufügen oder entfernen möchten.

![](../images/user-guide/profiles-search-filter.png)

Wählen Sie im Dialogfeld &quot;Identitätsnamen ** auswählen&quot;den Namensraum aus, nach dem Sie suchen möchten, oder verwenden Sie die **[!UICONTROL Suchleiste]** im Dialogfeld, um mit der Eingabe des Namens eines Namensraums zu beginnen. Sie können einen Namensraum auswählen, um weitere Details Ansicht. Sobald Sie den Namensraum gefunden haben, den Sie suchen möchten, können Sie das Optionsfeld auswählen und die **[!UICONTROL Auswahl]** drücken, um fortzufahren.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Identitätswert

Nach Auswahl eines **[!UICONTROL Identitäts-Namensraums]** kehren Sie zur Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;zurück, auf der Sie einen **[!UICONTROL Identitätswert]** eingeben können. Dieser Wert ist spezifisch für ein einzelnes Profil und muss ein gültiger Eintrag für den bereitgestellten Namensraum sein. Wenn Sie beispielsweise den **[!UICONTROL Identitäts-Namensraum]** &quot;E-Mail&quot;auswählen, ist ein **[!UICONTROL Identitätswert]** in Form einer gültigen E-Mail-Adresse erforderlich.

![](../images/user-guide/profiles-show-profile.png)

Nachdem ein Wert eingegeben wurde, wählen Sie &quot;Profil **[!UICONTROL anzeigen]** &quot;und ein Profil, das dem Wert entspricht, wird zurückgegeben. Wählen Sie die **[!UICONTROL Profil-ID]** aus, um die Details des Profils Ansicht.

![](../images/user-guide/profiles-display-profile.png)

### Profil

Nach Auswahl der **[!UICONTROL Profil-ID]** wird die Registerkarte &quot; _[!UICONTROL Details]_&quot;geöffnet. Auf dieser Seite finden Sie Informationen zum ausgewählten Profil, einschließlich Basisattribute, verknüpfte Identitäten und verfügbare Kanal. Die angezeigten Profildaten wurden aus mehreren Profilfragmenten zusammengeführt, um eine zentrale Ansicht des jeweiligen Kunden zu erstellen.

![](../images/user-guide/profiles-profile-detail.png)

Sie können zusätzliche Informationen zum Profil, einschließlich *[!UICONTROL Attribute]*, *[!UICONTROL Ereignis]* und *[!UICONTROL Segmente]* , zu denen das Profil gehört, Ansicht leisten.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Zusammenführungsrichtlinien

Select the *[!UICONTROL Merge Policies]* tab to view a list of merge policies belonging to your organization. Jede aufgelistete Richtlinie zeigt an: ihren Namen; ob sie die standardmäßige Zusammenführungsrichtlinie ist oder nicht; das Schema, auf das sie angewendet wird.

For more information on merge policies, see the [Merge Policies user guide](merge-policies.md).

![](../images/user-guide/profiles-merge-policies.png)

## Vereinigungsschema

Wählen Sie die Registerkarte &quot;Schema *der* Vereinigung&quot;aus, um die Schema der Vereinigung für Ihre [!DNL Profile Store]Ansicht. A union schema is an amalgamation of all [!DNL Experience Data Model] (XDM) fields under the same class, whose schemas have been enabled for use in [!DNL Real-time Customer Profile]. Wählen Sie in der linken Liste eine Klasse aus, um die Struktur des Schemas &quot;Vereinigung&quot;auf der Arbeitsfläche Ansicht.

Wenn Sie beispielsweise &quot;[!DNL XDM Profile]&quot;auswählen, wird das Schema &quot;Vereinigung&quot;für die [!DNL XDM Individual Profile] Klasse angezeigt.

See the section on union schemas in the [schema composition guide](../../xdm/schema/composition.md) for more information on union schemas and their role in [!DNL Real-time Customer Profile].

![](../images/user-guide/profiles-union-schema.png)

## Nächste Schritte

By reading this guide, you now know how to view and manage your [!DNL Profile] data using the [!DNL Experience Platform] UI. For information on how to leverage [!DNL Real-time Customer Profile] data to generate audience segments, see the [Segmentation documentation](../../segmentation/home.md).