---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;rtcp;Profil aktivieren;Vereinigungsschema;Vereinigungsprofil;Vereinigungsprofil;Vereinigungsprofil
title: Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils
description: Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht auf Ihre einzelnen Kunden und führt Daten aus verschiedenen Kanälen (Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen. Dieses Dokument dient als Anleitung für die Interaktion mit dem Echtzeit-Kundenprofil in der Benutzeroberfläche von Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 9%

---

# Handbuch für die [!DNL Real-Time Customer Profile]-Benutzeroberfläche

[!DNL Real-Time Customer Profile] erstellt eine ganzheitliche Sicht auf Ihre einzelnen Kunden und kombiniert Daten aus verschiedenen Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten. Dieses Dokument dient als Anleitung für die Interaktion mit [!DNL Real-Time Customer Profile] in der Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Handbuch für die Benutzeroberfläche setzt ein Verständnis der verschiedenen [!DNL Experience Platform]-Services voraus, die mit der Verwaltung von [!DNL Real-Time Customer Profiles] zusammenhängen. Bevor Sie dieses Handbuch lesen oder in der Benutzeroberfläche arbeiten, lesen Sie bitte die Dokumentation für die folgenden Services:

* [[!DNL Real-Time Customer Profile] Übersicht](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Identity Service]](../../identity-service/home.md): Aktiviert die [!DNL Real-Time Customer Profile] durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, während sie in [!DNL Experience Platform] aufgenommen werden.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.

## [!UICONTROL Übersicht]

Wählen Sie in der Benutzeroberfläche von Experience Platform **[!UICONTROL Profile]** im linken Navigationsbereich aus, um die Registerkarte **[!UICONTROL Übersicht]** mit dem Profil-Dashboard zu öffnen.

>[!NOTE]
>
>Wenn Experience Platform neu in Ihrem Unternehmen ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt hat, wird das Dashboard [!UICONTROL Profile] nicht angezeigt. Stattdessen werden auf [!UICONTROL  Registerkarte ]Übersicht“ Links und Dokumentationen angezeigt, die Ihnen bei den ersten Schritten mit dem Echtzeit-Kundenprofil helfen können.

### Profil-Dashboard {#profile-dashboard}

Im Profil-Dashboard werden Schlüsselmetriken im Zusammenhang mit den Profildaten Ihres Unternehmens beschrieben.

Weitere Informationen finden Sie im [Handbuch zum Profil-Dashboard](../../dashboards/guides/profiles.md).

![Das Profil-Dashboard wird angezeigt.](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL Durchsuchen] Registerkartenmetriken

Wählen Sie die **[!UICONTROL Durchsuchen]** aus, um mehrere Metriken anzuzeigen, die mit den Profildaten Ihres Unternehmens in Verbindung stehen. Sie können diese Registerkarte auch verwenden, um den Profilspeicher mithilfe einer Zusammenführungsrichtlinie oder einer Identität zu durchsuchen, wie im nächsten Abschnitt dieses Handbuchs beschrieben.

Auf der rechten Seite der Registerkarte **[!UICONTROL Durchsuchen]** befinden sich die [Profilanzahl](#profile-count) sowie eine Liste von [Profilen nach Namespace](#profiles-by-namespace).

>[!NOTE]
>
>Diese Profilmetriken können von den im [Profil-Dashboard“ angezeigten Metriken abweichen](#profile-dashboard) da sie anhand der standardmäßigen Zusammenführungsrichtlinie Ihrer Organisation ausgewertet werden. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien, einschließlich der Definition einer standardmäßigen Zusammenführungsrichtlinie, finden Sie unter [Zusammenführungsrichtlinien - Übersicht](../merge-policies/overview.md).

Zusätzlich zu diesen Metriken finden Sie in diesem Abschnitt ein Datum und eine Uhrzeit der letzten Aktualisierung, die anzeigt, wann die Metriken zuletzt ausgewertet wurden.

![Die Profilmetriken werden angezeigt und hervorgehoben.](../images/user-guide/browse-metrics.png)

### Anzahl der Profile {#profile-count}

Die Anzahl der Profile zeigt die Gesamtanzahl der Profile an, über die Ihre Organisation in Experience Platform verfügt, nachdem die standardmäßige Zusammenführungsrichtlinie Ihrer Organisation Profilfragmente zusammengeführt hat, um für jeden Kunden ein einzelnes Profil zu erstellen. Mit anderen Worten: Ihre Organisation hat möglicherweise verschiedene Profilfragmente, die sich auf einen einzelnen Kunden beziehen, der mit Ihrer Marke über unterschiedliche Kanäle interagiert. Diese Fragmente würden jedoch zusammengeführt (gemäß der standardmäßigen Zusammenführungsrichtlinie) und eine Anzahl von „1“ zurückgeben, da sie alle mit derselben Person verbunden sind.

Die Profilanzahl umfasst auch Profile mit Attributen (Datensatzdaten) sowie Profile, die nur Zeitreihen-(Ereignis-)Daten enthalten, z. B. Adobe Analytics-Profile. Die Profilanzahl wird regelmäßig aktualisiert, um eine aktuelle Gesamtzahl von Profilen in Experience Platform bereitzustellen.

#### Profilzählungs-Metrik aktualisieren

Wenn die Aufnahme von Datensätzen in den [!DNL Profile] die Anzahl um mehr als 5 % erhöht oder verringert, wird ein Auftrag ausgelöst, um die Anzahl zu aktualisieren. Bei Streaming-Daten-Workflows wird stündlich überprüft, ob der Anstieg- oder Absenkungsschwellenwert von 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Vorgang ausgelöst, um die Profilanzahl zu aktualisieren. Bei der Batch-Aufnahme wird innerhalb von 15 Minuten nach der erfolgreichen Aufnahme eines Batches in den Profilspeicher ein Auftrag ausgeführt, um die Profilanzahl zu aktualisieren, wenn der Schwellenwert von 5 % für Erhöhung oder Verringerung erreicht ist.

### [!UICONTROL Profile nach Namespace] {#profiles-by-namespace}

Die Metrik **[!UICONTROL Profile nach Namespace]** zeigt die Gesamtanzahl und Aufschlüsselung der Namespaces für alle zusammengeführten Profile in Ihrem Profilspeicher an. Die Gesamtzahl der Profile nach Namespace (d. h. das Addieren der für jeden Namespace angezeigten Werte) ist immer höher als die Metrik zur Profilanzahl, da einem Profil mehrere Namespaces zugeordnet sein könnten. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

#### Aktualisieren der Metrik [!UICONTROL Profile nach Namespace]

Ähnlich wie bei der Metrik [Profilanzahl](#profile-count) wird ein Auftrag zur Aktualisierung der Namespace-Metriken ausgelöst, wenn die Aufnahme von Datensätzen in den [!DNL Profile] die Anzahl um mehr als 5 % erhöht oder verringert. Bei Streaming-Daten-Workflows wird stündlich überprüft, ob der Anstieg- oder Absenkungsschwellenwert von 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Vorgang ausgelöst, um die Profilanzahl zu aktualisieren. Bei der Batch-Aufnahme wird innerhalb von 15 Minuten nach der erfolgreichen Aufnahme eines Batches in den [!DNL Profile] ein Auftrag ausgeführt, um die Metriken zu aktualisieren, wenn der Schwellenwert von 5 % für die Erhöhung oder Verringerung erreicht wird.

## Registerkarte [!UICONTROL Durchsuchen] zum Anzeigen von Profilen verwenden

Auf der Registerkarte **[!UICONTROL Durchsuchen]** können Sie Beispielprofile mithilfe einer Zusammenführungsrichtlinie anzeigen oder mithilfe eines Identity-Namespace und -Werts nach bestimmten Profilen suchen.

![Die Profile, die zur Organisation gehören, werden angezeigt.](../images/user-guide/none-selected.png)

### Durchsuchen nach [!UICONTROL Zusammenführungsrichtlinie]

Die **[!UICONTROL Durchsuchen]** ist standardmäßig auf die standardmäßige Zusammenführungsrichtlinie für Ihre Organisation festgelegt. Um eine andere Zusammenführungsrichtlinie auszuwählen, wählen Sie die `X` neben dem Namen der Zusammenführungsrichtlinie aus und öffnen Sie dann mit der Auswahl das Dialogfeld **[!UICONTROL Zusammenführungsrichtlinie auswählen]**.

>[!NOTE]
>
>Wenn keine Zusammenführungsrichtlinie ausgewählt ist, verwenden Sie die Auswahlschaltfläche neben dem Feld **[!UICONTROL Zusammenführungsrichtlinie]**, um das Auswahldialogfeld zu öffnen.

![Die Auswahl für die Zusammenführungsrichtlinie ist hervorgehoben.](../images/user-guide/browse-by-merge-policy.png)

Um eine Zusammenführungsrichtlinie im Dialogfeld **[!UICONTROL Zusammenführungsrichtlinie auswählen]** auszuwählen, wählen Sie das Optionsfeld neben dem Richtliniennamen aus und verwenden Sie dann **[!UICONTROL Auswählen]**, um zur Registerkarte [!UICONTROL Durchsuchen] zurückzukehren. Sie können dann auf **[!UICONTROL Anzeigen]** klicken, um die Beispielprofile zu aktualisieren und ein Sampling der Profile mit der neuen angewendeten Zusammenführungsrichtlinie anzuzeigen.

![Es wird ein Dialogfeld angezeigt, in dem Sie die Zusammenführungsrichtlinie auswählen können, nach der gefiltert werden soll.](../images/user-guide/select-merge-policy.png)

Die angezeigten Profile stellen ein Beispiel von bis zu 20 Profilen aus dem Profilspeicher Ihres Unternehmens dar, nachdem die ausgewählte Zusammenführungsrichtlinie angewendet wurde. Die Beispielprofile für die ausgewählte Zusammenführungsrichtlinie werden aktualisiert, wenn neue Daten zum Profilspeicher Ihres Unternehmens hinzugefügt werden.

Um die Details eines der Beispielprofile anzuzeigen, wählen Sie die **[!UICONTROL Profilkennung]** aus. Weitere Informationen finden Sie im Abschnitt weiter unten in diesem Handbuch [Anzeigen von Profildetails](#profile-detail).

![Beispielprofile, die mit der Zusammenführungsrichtlinie übereinstimmen, werden angezeigt.](../images/user-guide/sample-profiles.png)

Weitere Informationen zu Zusammenführungsrichtlinien und ihrer Rolle in Experience Platform finden Sie unter [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

### Durchsuchen nach [!UICONTROL Identität] {#browse-identity}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** können Sie einen Identity-Namespace verwenden, um ein bestimmtes Profil anhand eines Identitätswerts nachzuschlagen. Zum Durchsuchen nach einer Identität müssen Sie eine Zusammenführungsrichtlinie, einen Identity-Namespace und einen Identitätswert angeben.

![Die Auswahl für die Zusammenführungsrichtlinie ist hervorgehoben.](../images/user-guide/browse-by-merge-policy.png)

Verwenden Sie bei Bedarf die Auswahl **[!UICONTROL Zusammenführungsrichtlinie]** , um das Dialogfeld **[!UICONTROL Zusammenführungsrichtlinie auswählen]** zu öffnen und die Zusammenführungsrichtlinie auszuwählen, die Sie verwenden möchten.

![Es wird ein Dialogfeld angezeigt, in dem Sie die Zusammenführungsrichtlinie auswählen können, nach der gefiltert werden soll.](../images/user-guide/select-merge-policy.png)

Verwenden Sie dann die **[!UICONTROL Identity-Namespace]**, um das Dialogfeld **[!UICONTROL Identity-Namespace auswählen]** zu öffnen und den Namespace auszuwählen, nach dem gesucht werden soll. Wenn Ihr Unternehmen über viele Namespaces verfügt, können Sie über die Suchleiste im Dialogfeld mit der Eingabe des Namens eines Namespace beginnen.

Sie können einen Namespace auswählen, um zusätzliche Details anzuzeigen, oder das Optionsfeld auswählen, um einen Namespace auszuwählen. Sie können dann **[!UICONTROL Auswählen]** verwenden, um fortzufahren.

![Es wird ein Dialogfeld angezeigt, in dem Sie den Identity-Namespace auswählen können, nach dem gefiltert werden soll.](../images/user-guide/select-identity-namespace.png)

Nachdem Sie einen [!UICONTROL Identity-Namespace] ausgewählt und zur Registerkarte [!UICONTROL Durchsuchen] zurückgekehrt sind, können Sie einen **[!UICONTROL Identitätswert]** eingeben, der sich auf den ausgewählten Namespace bezieht.

>[!NOTE]
>
>Dieser Wert ist spezifisch für ein einzelnes Kundenprofil und muss ein gültiger Eintrag für den bereitgestellten Namespace sein. Wenn Sie beispielsweise den Identity-Namespace „E-Mail“ auswählen, ist ein Identitätswert in Form einer gültigen E-Mail-Adresse erforderlich.

![Der Identitätswert, nach dem gefiltert werden soll, ist hervorgehoben.](../images/user-guide/filter-identity-value.png)

Nachdem Sie einen Wert eingegeben haben, wählen Sie **[!UICONTROL Anzeigen]** und ein einzelnes Profil, das dem Wert entspricht, wird zurückgegeben. Wählen Sie **[!UICONTROL Profil-ID]** aus, um die Profildetails anzuzeigen.

![Das Profil, das dem Identitätswert entspricht, ist hervorgehoben.](../images/user-guide/filtered-identity-value.png)

## Anzeigen von Profildetails {#profile-detail}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_201001_404"
>title="Entität nicht gefunden"
>abstract="Das bedeutet, dass die angeforderte Entität von Experience Platform nicht gefunden wurde. Versuchen Sie eine der folgenden Lösungen, um diesen Fehler zu beheben:<ul><li>Stellen Sie sicher, dass die richtige Profilkennung in der URL der Entität aufgeführt ist, auf die Sie zugreifen möchten.</li><li>Stellen Sie sicher, dass Sie über die richtige Kombination aus Organisation und Sandbox für die Entität verfügen, auf die Sie zugreifen möchten.</li></ul>"

Nach Auswahl einer **[!UICONTROL Profil-ID]** wird die Registerkarte **[!UICONTROL Detail]** geöffnet. Die auf der Registerkarte **[!UICONTROL Detail]** angezeigten Profilinformationen wurden aus mehreren Profilfragmenten zusammengeführt, um eine zentrale Ansicht des jeweiligen Kunden zu erstellen. Dazu gehören Kundendetails wie grundlegende Attribute, verknüpfte Identitäten und Kanalvoreinstellungen.

Die Standardfelder können auch auf Organisationsebene geändert werden, um die bevorzugten Profilattribute anzuzeigen. Weitere Informationen zum Anpassen dieser Felder, einschließlich schrittweiser Anweisungen zum Hinzufügen und Entfernen von Attributen und zum Ändern der Größe von Dashboard-Bedienfeldern, finden Sie im [Handbuch zur Anpassung von Profildetails](profile-customization.md).

![Die Registerkarte Details ist hervorgehoben. Die Profildetails werden angezeigt.](../images/user-guide/profile-detail-row-name.png)

Sie können auch zwischen der Anzeige der Attributnamen als Anzeigenamen und der Feldpfadnamen umschalten. Um zwischen diesen beiden Displays zu wechseln, wählen Sie den Umschalter **[!UICONTROL Anzeigenamen anzeigen]**.

![Der Umschalter Anzeigenamen anzeigen ist hervorgehoben, und die Anzeigenamen werden unter den Attributen angezeigt.](../images/user-guide/profile-detail.png)

Um zusätzliche Informationen zum jeweiligen Kundenprofil anzuzeigen, wählen Sie eine der anderen verfügbaren Registerkarten aus. Zu diesen Registerkarten gehören Attribute, Ereignisse und die Registerkarte Zielgruppenzugehörigkeit , auf der die Zielgruppen angezeigt werden, für die das Profil derzeit qualifiziert ist.

### Registerkarte „Attribute“

Die **[!UICONTROL Attribute]** bietet eine Listenansicht, in der alle Attribute zusammengefasst sind, die sich auf ein einzelnes Profil beziehen, nachdem die angegebene Zusammenführungsrichtlinie angewendet wurde.

Diese Attribute können auch als JSON-Objekt angezeigt werden, indem Sie auf &quot;**[!UICONTROL anzeigen“]**. Dies ist hilfreich für alle Benutzenden, die besser verstehen möchten, wie die Profilattribute in Experience Platform aufgenommen werden.

![Die Registerkarte Attribute ist hervorgehoben. Die Profilattribute werden angezeigt.](../images/user-guide/attributes.png)

Um die in der Edge verfügbaren Attribute anzuzeigen, wählen Sie **[!UICONTROL Edge]** in der Datenspeicherortauswahl aus.

![Die Datenspeicherortauswahl auf der Registerkarte „Attribute“ ist hervorgehoben.](../images/user-guide/attributes-select.png)

Weitere Informationen zu Edge-Profilen finden Sie in der [Dokumentation zu Edge-Profilen](../edge-profiles.md).

### Registerkarte „Ereignisse“

Die Registerkarte **[!UICONTROL Ereignisse]** enthält Daten aus den 100 neuesten ExperienceEvents, die mit dem Kunden verknüpft sind. Diese Daten können E-Mail-Öffnungen, Warenkorbaktivitäten und Seitenansichten umfassen. Wenn Sie **[!UICONTROL Alle anzeigen]** für ein einzelnes Ereignis auswählen, werden zusätzliche Felder und Werte als Teil des Ereignisses erfasst.

Ereignisse können auch als JSON-Objekt angezeigt werden, indem Sie auf **[!UICONTROL JSON anzeigen“]**. Dies ist hilfreich, um zu verstehen, wie Ereignisse in Experience Platform erfasst werden.

![Die Registerkarte Ereignisse ist hervorgehoben. Die Profilereignisse werden angezeigt.](../images/user-guide/events.png)

### Registerkarte „Zielgruppenzugehörigkeit“

Auf **[!UICONTROL Registerkarte]** Zielgruppenzugehörigkeit“ wird eine Liste mit dem Namen und der Beschreibung der Zielgruppen angezeigt, zu denen das einzelne Kundenprofil derzeit gehört. Diese Liste wird automatisch aktualisiert, wenn das Profil für Zielgruppen geeignet ist oder von diesen abläuft. Die Gesamtzahl der Zielgruppen, für die das Profil derzeit qualifiziert ist, wird auf der rechten Seite der Registerkarte angezeigt.

Weitere Informationen zur Segmentierung in Experience Platform finden Sie in der Dokumentation [Adobe Experience Platform Segmentation Service](../../segmentation/home.md).

![Die Registerkarte „Zielgruppenmitgliedschaft“ ist hervorgehoben. Die Details zur Zielgruppenzugehörigkeit des Profils werden angezeigt.](../images/user-guide/audience-membership.png)

Um die Zielgruppenzugehörigkeit der Profile anzuzeigen, die in der Edge verfügbar sind, wählen Sie **[!UICONTROL Edge]** in der Datenspeicherortauswahl aus. Weitere Informationen zur Edge-Segmentierung finden Sie im [Handbuch zur Edge-Segmentierung](../../segmentation/methods/edge-segmentation.md).

![Die Datenspeicherortauswahl auf der Registerkarte für die Zielgruppenzugehörigkeit ist hervorgehoben.](../images/user-guide/audience-membership-select.png)

## Zusammenführungsrichtlinien

Wählen Sie im Hauptmenü **[!UICONTROL Profile]** die Registerkarte **[!UICONTROL Zusammenführungsrichtlinien]**, um eine Liste der Zusammenführungsrichtlinien anzuzeigen, die zu Ihrer Organisation gehören. Jede aufgelistete Richtlinie zeigt ihren Namen an, unabhängig davon, ob es sich um die standardmäßige Zusammenführungsrichtlinie handelt oder nicht, und die Schemaklasse, für die sie gilt.

Weiterführende Informationen zu Zusammenführungsrichtlinien finden Sie unter [Zusammenführungsrichtlinien – Übersicht](../merge-policies/overview.md).

![Die Registerkarte „Zusammenführungsrichtlinien“ ist hervorgehoben. Es werden Zusammenführungsrichtlinien angezeigt, die zur Organisation gehören.](../images/user-guide/merge-policies.png)

## Vereinigungsschema {#union-schema}

Wählen Sie im Hauptmenü **[!UICONTROL Profile]** die Registerkarte **[!UICONTROL Vereinigungsschema]** aus, um verfügbare Vereinigungsschemata für Ihre aufgenommenen Daten anzuzeigen. Ein Vereinigungsschema ist eine Zusammenführung aller [!DNL Experience Data Model] (XDM)-Felder unter derselben Klasse, deren Schemata für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert wurden.

Weitere Informationen zu Vereinigungsschemata finden Sie im [Handbuch zur Vereinigungsschema-Benutzeroberfläche](union-schema.md).

![Die Registerkarte Vereinigungsschema ist hervorgehoben. Vereinigungsschemata, die zur Organisation gehören, werden angezeigt.](../images/user-guide/union-schema.png)

## Berechnete Attribute {#computed-attributes}

Wählen Sie im Hauptmenü **[!UICONTROL Profile]** die Registerkarte **[!UICONTROL Berechnete Attribute]**, um eine Liste der berechneten Attribute anzuzeigen, die zu Ihrer Organisation gehören.

![Die Registerkarte „Berechnete Attribute“ ist hervorgehoben.](../images/user-guide/computed-attributes.png)

Weitere Informationen zu berechneten Attributen finden Sie unter [Berechnete Attribute - Übersicht](../computed-attributes/overview.md). Weitere Informationen zur Verwendung berechneter Attribute in der Experience Platform-Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche für berechnete Attribute](../computed-attributes/ui.md).

## Nächste Schritte

Durch das Lesen dieses Handbuchs wissen Sie, wie Sie die Profildaten Ihres Unternehmens mithilfe der Experience Platform-Benutzeroberfläche anzeigen und verwalten können. Informationen zum Arbeiten mit Profildaten mithilfe von Experience Platform-APIs finden Sie im [Handbuch zur Echtzeit-Kundenprofil-API](../api/overview.md).
