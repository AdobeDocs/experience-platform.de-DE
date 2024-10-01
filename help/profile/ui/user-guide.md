---
keywords: Experience Platform; profile; Echtzeit-Kundenprofil; Fehlerbehebung; API; einheitliches Profil; einheitliches Profil; einheitliches Profil; Profil; rtcp; Profil aktivieren; Profil aktivieren; Vereinigungsschema; UNION PROFILE; Vereinigungsprofil
title: Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils
description: Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Ansicht Ihrer einzelnen Kunden und kombiniert Daten aus verschiedenen Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten. Dieses Dokument dient als Leitfaden für die Interaktion mit dem Echtzeit-Kundenprofil in der Benutzeroberfläche von Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: dc31258dad5cf03a8f4f60db4d4aefc29e8157c8
workflow-type: tm+mt
source-wordcount: '2212'
ht-degree: 9%

---

# Handbuch für die [!DNL Real-Time Customer Profile]-Benutzeroberfläche

[!DNL Real-Time Customer Profile] erstellt eine ganzheitliche Ansicht Ihrer einzelnen Kunden und kombiniert Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten. Dieses Dokument dient als Anleitung für die Interaktion mit [!DNL Real-Time Customer Profile] -Daten in der Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses UI-Handbuch setzt ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste voraus, die mit der Verwaltung von [!DNL Real-Time Customer Profiles] verbunden sind. Bevor Sie dieses Handbuch lesen oder in der Benutzeroberfläche arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Real-Time Customer Profile] overview](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Identity Service]](../../identity-service/home.md): Aktiviert [!DNL Real-Time Customer Profile] durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, während sie in [!DNL Platform] erfasst werden.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.

## [!UICONTROL Übersicht]

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich die Option **[!UICONTROL Profile]** aus, um die Registerkarte **[!UICONTROL Übersicht]** zu öffnen, auf der das Profil-Dashboard angezeigt wird.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, ist das Dashboard [!UICONTROL Profile] nicht sichtbar. Stattdessen werden auf der Registerkarte [!UICONTROL Übersicht] Links und Dokumentation angezeigt, die Ihnen bei den ersten Schritten mit dem Echtzeit-Kundenprofil helfen.

### Profil-Dashboard {#profile-dashboard}

Im Profil-Dashboard werden Schlüsselmetriken im Zusammenhang mit den Profildaten Ihres Unternehmens beschrieben.

Weitere Informationen finden Sie im Dashboard-Handbuch für Profile [1}.](../../dashboards/guides/profiles.md)

![Das Profil-Dashboard wird angezeigt.](../../dashboards/images/profiles/dashboard-overview.png)

## Registerkartenmetriken [!UICONTROL Durchsuchen]

Wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** aus, um mehrere Metriken anzuzeigen, die sich auf die Profildaten Ihres Unternehmens beziehen. Sie können diese Registerkarte auch verwenden, um den Profilspeicher mithilfe einer Zusammenführungsrichtlinie oder einer Identität zu durchsuchen, wie im nächsten Abschnitt dieses Handbuchs beschrieben.

Auf der rechten Seite der Registerkarte **[!UICONTROL Durchsuchen]** befinden sich die [Profilanzahl](#profile-count) sowie eine Liste mit [Profilen nach Namespace](#profiles-by-namespace).

>[!NOTE]
>
>Diese Profilmetriken können von den im [Profil-Dashboard](#profile-dashboard) angezeigten Metriken abweichen, da sie mit der standardmäßigen Zusammenführungsrichtlinie Ihres Unternehmens ausgewertet werden. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien, einschließlich der Definition einer standardmäßigen Zusammenführungsrichtlinie, finden Sie unter [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

Zusätzlich zu diesen Metriken bietet dieser Abschnitt ein Datum und eine Uhrzeit der letzten Aktualisierung, die zeigen, wann die Metriken zuletzt ausgewertet wurden.

![Die Profilmetriken werden angezeigt und hervorgehoben.](../images/user-guide/browse-metrics.png)

### Anzahl der Profile {#profile-count}

Die Anzahl der Profile zeigt die Gesamtanzahl der Profile an, über die Ihre Organisation in Experience Platform verfügt, nachdem die standardmäßige Zusammenführungsrichtlinie Ihrer Organisation Profilfragmente zusammengeführt hat, um für jeden Kunden ein einzelnes Profil zu erstellen. Mit anderen Worten: Ihre Organisation hat möglicherweise verschiedene Profilfragmente, die sich auf einen einzelnen Kunden beziehen, der mit Ihrer Marke über unterschiedliche Kanäle interagiert. Diese Fragmente würden jedoch zusammengeführt (gemäß der standardmäßigen Zusammenführungsrichtlinie) und eine Anzahl von „1“ zurückgeben, da sie alle mit derselben Person verbunden sind.

Die Profilanzahl umfasst auch Profile mit Attributen (Datensatzdaten) sowie Profile, die nur Zeitreihendaten (Ereignisdaten) enthalten, z. B. Adobe Analytics-Profile. Die Profilanzahl wird regelmäßig aktualisiert, um eine aktuelle Gesamtanzahl von Profilen in Platform bereitzustellen.

#### Profilzählungsmetrik aktualisieren

Wenn die Aufnahme von Datensätzen in den Speicher [!DNL Profile] die Anzahl um mehr als 5 % erhöht oder verringert, wird ein Auftrag ausgelöst, der die Anzahl aktualisiert. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für eine Zu- oder Abnahme um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Profilanzahl zu aktualisieren. Bei der Batch-Erfassung wird innerhalb von 15 Minuten nach erfolgreicher Aufnahme eines Batches in den Profilspeicher ein Auftrag ausgeführt, um die Profilanzahl zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht ist.

### [!UICONTROL Profile nach Namespace] {#profiles-by-namespace}

Die Metrik **[!UICONTROL Profile nach Namespace]** zeigt die Gesamtanzahl und Aufschlüsselung der Namespaces für alle zusammengeführten Profile in Ihrem Profilspeicher an. Die Gesamtzahl der Profile nach Namespace (d. h. das Addieren der für jeden Namespace angezeigten Werte) ist immer höher als die Metrik für die Profilanzahl, da einem Profil mehrere Namespaces zugeordnet sein können. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

#### Aktualisieren der Metrik [!UICONTROL Profile nach Namespace]

Ähnlich wie bei der Metrik [Profilanzahl](#profile-count) wird ein Auftrag ausgelöst, um die Namespace-Metriken zu aktualisieren, wenn die Erfassung von Datensätzen im [!DNL Profile] -Speicher die Anzahl um mehr als 5 % erhöht oder verringert. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für eine Zu- oder Abnahme um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Profilanzahl zu aktualisieren. Bei der Batch-Erfassung wird innerhalb von 15 Minuten nach erfolgreicher Aufnahme eines Batches in den [!DNL Profile]-Speicher ein Auftrag ausgeführt, um die Metriken zu aktualisieren, wenn der Schwellenwert für eine Erhöhung oder Verringerung um 5 % erreicht ist.

## Verwenden Sie die Registerkarte [!UICONTROL Durchsuchen] , um Profile anzuzeigen.

Auf der Registerkarte **[!UICONTROL Durchsuchen]** können Sie Beispielprofile mithilfe einer Zusammenführungsrichtlinie anzeigen oder mithilfe eines Identitäts-Namespace und -Werts nach bestimmten Profilen suchen.

![Die Profile, die zur Organisation gehören, werden angezeigt.](../images/user-guide/none-selected.png)

### Durchsuchen nach [!UICONTROL Zusammenführungsrichtlinie]

Die Registerkarte **[!UICONTROL Durchsuchen]** ist standardmäßig auf die standardmäßige Zusammenführungsrichtlinie für Ihre Organisation festgelegt. Um eine andere Zusammenführungsrichtlinie auszuwählen, wählen Sie den Wert &quot;`X`&quot;neben dem Namen der Zusammenführungsrichtlinie und verwenden Sie dann die Auswahl, um das Dialogfeld &quot;**[!UICONTROL Zusammenführungsrichtlinie auswählen]**&quot;zu öffnen.

>[!NOTE]
>
>Wenn keine Zusammenführungsrichtlinie ausgewählt ist, verwenden Sie die Auswahlschaltfläche neben dem Feld **[!UICONTROL Zusammenführungsrichtlinie]** , um das Auswahldialogfeld zu öffnen.

![Der Selektor für Zusammenführungsrichtlinien ist hervorgehoben.](../images/user-guide/browse-by-merge-policy.png)

Um eine Zusammenführungsrichtlinie aus dem Dialogfeld **[!UICONTROL Zusammenführungsrichtlinie auswählen]** auszuwählen, wählen Sie das Optionsfeld neben dem Richtliniennamen aus und verwenden Sie dann **[!UICONTROL Auswählen]** , um zur Registerkarte [!UICONTROL Durchsuchen] zurückzukehren. Sie können dann **[!UICONTROL Ansicht]** auswählen, um die Beispielprofile zu aktualisieren und eine Auswahl von Profilen mit der neuen angewendeten Zusammenführungsrichtlinie anzuzeigen.

![Ein Dialogfeld, in dem Sie die Zusammenführungsrichtlinie auswählen können, nach der gefiltert werden soll, wird angezeigt.](../images/user-guide/select-merge-policy.png)

Die angezeigten Profile stellen ein Beispiel von bis zu 20 Profilen aus dem Profilspeicher Ihres Unternehmens dar, nachdem die ausgewählte Zusammenführungsrichtlinie angewendet wurde. Die Beispielprofile für die ausgewählte Zusammenführungsrichtlinie werden aktualisiert, wenn dem Profilspeicher Ihres Unternehmens neue Daten hinzugefügt werden.

Um die Details eines der Beispielprofile anzuzeigen, wählen Sie die **[!UICONTROL Profil-ID]** aus. Weitere Informationen finden Sie im Abschnitt weiter unten in diesem Handbuch zum [Anzeigen von Profildetails](#profile-detail).

![Es werden Beispielprofile angezeigt, die mit der Zusammenführungsrichtlinie übereinstimmen.](../images/user-guide/sample-profiles.png)

Weitere Informationen zu Zusammenführungsrichtlinien und ihrer Rolle in Platform finden Sie in der [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

### Durchsuchen nach [!UICONTROL Identität] {#browse-identity}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** können Sie einen Identitäts-Namespace verwenden, um ein bestimmtes Profil anhand eines Identitätswerts nachzuschlagen. Für das Durchsuchen nach einer Identität müssen Sie eine Zusammenführungsrichtlinie, einen Identitäts-Namespace und einen Identitätswert angeben.

![Der Selektor für Zusammenführungsrichtlinien ist hervorgehoben.](../images/user-guide/browse-by-merge-policy.png)

Verwenden Sie bei Bedarf den Selektor **[!UICONTROL Zusammenführungsrichtlinie]** , um das Dialogfeld **[!UICONTROL Zusammenführungsrichtlinie auswählen]** zu öffnen und die gewünschte Zusammenführungsrichtlinie auszuwählen.

![Ein Dialogfeld, in dem Sie die Zusammenführungsrichtlinie auswählen können, nach der gefiltert werden soll, wird angezeigt.](../images/user-guide/select-merge-policy.png)

Verwenden Sie dann den Selektor **[!UICONTROL Identitäts-Namespace]** , um das Dialogfeld **[!UICONTROL Identitäts-Namespace auswählen]** zu öffnen und den Namespace auszuwählen, nach dem Sie suchen möchten. Wenn Ihr Unternehmen über viele Namespaces verfügt, können Sie über die Suchleiste im Dialogfeld mit der Eingabe des Namens eines Namespace beginnen.

Sie können einen Namespace auswählen, um weitere Details anzuzeigen, oder das Optionsfeld auswählen, um einen Namespace auszuwählen. Sie können dann **[!UICONTROL Select]** verwenden, um fortzufahren.

![Ein Dialogfeld, in dem Sie den Identitäts-Namespace auswählen können, nach dem gefiltert werden soll, wird angezeigt.](../images/user-guide/select-identity-namespace.png)

Nachdem Sie einen [!UICONTROL Identitäts-Namespace] ausgewählt und zur Registerkarte [!UICONTROL Durchsuchen] zurückkehren, können Sie einen **[!UICONTROL Identitätswert]** eingeben, der sich auf den ausgewählten Namespace bezieht.

>[!NOTE]
>
>Dieser Wert ist spezifisch für ein einzelnes Kundenprofil und muss ein gültiger Eintrag für den angegebenen Namespace sein. Beispielsweise würde die Auswahl des Identitäts-Namespace &quot;E-Mail&quot;einen Identitätswert in Form einer gültigen E-Mail-Adresse erfordern.

![Der Identitätswert, nach dem Sie filtern möchten, ist hervorgehoben.](../images/user-guide/filter-identity-value.png)

Nachdem ein Wert eingegeben wurde, wählen Sie **[!UICONTROL Ansicht]** und ein einzelnes Profil, das dem Wert entspricht, wird zurückgegeben. Wählen Sie die **[!UICONTROL Profil-ID]** aus, um die Profildetails anzuzeigen.

![Das Profil, das dem Identitätswert entspricht, wird hervorgehoben.](../images/user-guide/filtered-identity-value.png)

## Anzeigen von Profildetails {#profile-detail}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_201001_404"
>title="Entität nicht gefunden"
>abstract="Das bedeutet, dass die angeforderte Entität von Platform nicht gefunden wurde. Versuchen Sie eine der folgenden Lösungen, um diesen Fehler zu beheben:<ul><li>Stellen Sie sicher, dass die richtige Profilkennung in der URL der Entität aufgeführt ist, auf die Sie zugreifen möchten.</li><li>Stellen Sie sicher, dass Sie über die richtige Kombination aus Organisation und Sandbox für die Entität verfügen, auf die Sie zugreifen möchten.</li></ul>"

Nach Auswahl einer **[!UICONTROL Profil-ID]** wird die Registerkarte **[!UICONTROL Detail]** geöffnet. Die auf der Registerkarte **[!UICONTROL Detail]** angezeigten Profilinformationen wurden aus mehreren Profilfragmenten zusammengeführt, um eine einzige Ansicht des einzelnen Kunden zu bilden. Dazu gehören Kundendetails wie grundlegende Attribute, verknüpfte Identitäten und Kanalpräferenzen.

Die angezeigten Standardfelder können auch auf Organisationsebene geändert werden, um die bevorzugten Profilattribute anzuzeigen. Weitere Informationen zum Anpassen dieser Felder, einschließlich einer schrittweisen Anleitung zum Hinzufügen und Entfernen von Attributen und zum Ändern der Größe von Dashboard-Bedienfeldern, finden Sie im [Handbuch zur Anpassung der Profildetails](profile-customization.md).

![Die Registerkarte &quot;Details&quot;ist hervorgehoben. Die Profildetails werden angezeigt.](../images/user-guide/profile-detail-row-name.png)

Sie können auch zwischen der Anzeige der Attributnamen als Anzeigenamen und den Feldpfadnamen umschalten. Um zwischen diesen beiden Anzeigen zu wechseln, wählen Sie den Umschalter **[!UICONTROL Anzeigenamen anzeigen]** aus.

![Der Umschalter Anzeigenamen anzeigen wird hervorgehoben und die Anzeigenamen werden unter den Attributen angezeigt.](../images/user-guide/profile-detail.png)

Um weitere Informationen zum individuellen Kundenprofil anzuzeigen, wählen Sie eine der anderen verfügbaren Registerkarten aus. Diese Registerkarten umfassen Attribute, Ereignisse und die Registerkarte &quot;Zielgruppenmitgliedschaft&quot;, auf der die Zielgruppen angezeigt werden, für die das Profil derzeit qualifiziert ist.

### Registerkarte „Attribute“

Die Registerkarte **[!UICONTROL Attribute]** bietet eine Listenansicht, die alle Attribute, die sich auf ein einzelnes Profil beziehen, zusammenfasst, nachdem die angegebene Zusammenführungsrichtlinie angewendet wurde.

Diese Attribute können auch als JSON-Objekt angezeigt werden, indem Sie auf **[!UICONTROL JSON anzeigen]** klicken. Dies ist hilfreich für alle Benutzer, die besser verstehen möchten, wie die Profilattribute in Platform erfasst werden.

![Die Registerkarte &quot;Attribute&quot;ist hervorgehoben. Die Profilattribute werden angezeigt.](../images/user-guide/attributes.png)

Um die in der Edge verfügbaren Attribute anzuzeigen, wählen Sie im Datenspeicherort-Selektor **[!UICONTROL Edge]** aus.

![Die Auswahl des Datenspeicherorts auf der Registerkarte &quot;Attribute&quot;wird hervorgehoben.](../images/user-guide/attributes-select.png)

Weitere Informationen zu Edge-Profilen finden Sie in der Dokumentation zu [Edge-Profilen](../edge-profiles.md) .

### Registerkarte „Ereignisse“

Die Registerkarte **[!UICONTROL Ereignisse]** enthält Daten aus den 100 neuesten ExperienceEvents, die mit dem Kunden verknüpft sind. Diese Daten können E-Mail-Öffnungen, Warenkorbaktivitäten und Seitenansichten umfassen. Wenn Sie **[!UICONTROL Alle anzeigen]** für ein einzelnes Ereignis auswählen, werden zusätzliche Felder und Werte bereitgestellt, die im Rahmen des Ereignisses erfasst werden.

Ereignisse können auch als JSON-Objekt angezeigt werden, indem Sie auf **[!UICONTROL JSON anzeigen]** klicken. Dies ist hilfreich, um zu verstehen, wie Ereignisse in Platform erfasst werden.

![Die Registerkarte &quot;Ereignisse&quot;ist hervorgehoben. Die Profilereignisse werden angezeigt.](../images/user-guide/events.png)

### Registerkarte &quot;Zielgruppenmitgliedschaft&quot;

Auf der Registerkarte **[!UICONTROL Zielgruppenmitgliedschaft]** wird eine Liste mit dem Namen und der Beschreibung der Zielgruppen angezeigt, zu denen das individuelle Kundenprofil derzeit gehört. Diese Liste wird automatisch aktualisiert, wenn das Profil für Zielgruppen qualifiziert ist oder von diesen abläuft. Die Gesamtzahl der Zielgruppen, für die das Profil derzeit qualifiziert ist, wird auf der rechten Seite des Tabs angezeigt.

Weitere Informationen zur Segmentierung in Experience Platform finden Sie in der Dokumentation zum [Adobe Experience Platform Segmentation Service-](../../segmentation/home.md).

![Die Registerkarte &quot;Zielgruppenmitgliedschaft&quot;ist hervorgehoben. Die Details der Zielgruppenmitgliedschaft des Profils werden angezeigt.](../images/user-guide/audience-membership.png)

Um die Zielgruppenzugehörigkeit der in Edge verfügbaren Profile anzuzeigen, wählen Sie in der Datenspeicherortauswahl **[!UICONTROL Edge]** aus. Weitere Informationen zur Kantensegmentierung finden Sie im [Kantensegmentierungshandbuch](../../segmentation/ui/edge-segmentation.md).

![Die Auswahl des Datenspeicherorts auf der Registerkarte &quot;Zielgruppenmitgliedschaft&quot;wird hervorgehoben.](../images/user-guide/audience-membership-select.png)

## Zusammenführungsrichtlinien

Wählen Sie im Hauptmenü **[!UICONTROL Profile]** die Registerkarte **[!UICONTROL Zusammenführungsrichtlinien]** aus, um eine Liste der zu Ihrer Organisation gehörenden Zusammenführungsrichtlinien anzuzeigen. Jede aufgelistete Richtlinie zeigt ihren Namen an, unabhängig davon, ob es sich um die standardmäßige Zusammenführungsrichtlinie handelt oder nicht, und die Schemaklasse, für die sie gilt.

Weiterführende Informationen zu Zusammenführungsrichtlinien finden Sie unter [Zusammenführungsrichtlinien – Übersicht](../merge-policies/overview.md).

![Die Registerkarte &quot;Zusammenführungsrichtlinien&quot;ist hervorgehoben. Die zu der Organisation gehörenden Zusammenführungsrichtlinien werden angezeigt.](../images/user-guide/merge-policies.png)

## Vereinigungsschema {#union-schema}

Wählen Sie im Hauptmenü **[!UICONTROL Profile]** die Registerkarte **[!UICONTROL Vereinigungsschema]** aus, um die verfügbaren Vereinigungsschemas für die erfassten Daten anzuzeigen. Ein Vereinigungsschema ist eine Kombination aller [!DNL Experience Data Model] (XDM)-Felder unter derselben Klasse, deren Schemas für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert wurden.

Weitere Informationen zu Vereinigungsschemas finden Sie im Handbuch [UI-Handbuch für Vereinigungsschemas](union-schema.md) .

![Die Registerkarte &quot;Vereinigungsschema&quot;ist hervorgehoben. Es werden Vereinigungsschemas der Organisation angezeigt.](../images/user-guide/union-schema.png)

## Berechnete Attribute {#computed-attributes}

Wählen Sie im Hauptmenü **[!UICONTROL Profile]** die Registerkarte **[!UICONTROL Berechnete Attribute]** aus, um eine Liste der berechneten Attribute anzuzeigen, die zu Ihrer Organisation gehören.

![Die Registerkarte &quot;Berechnete Attribute&quot;ist hervorgehoben.](../images/user-guide/computed-attributes.png)

Weiterführende Informationen zu berechneten Attributen finden Sie in der [Übersicht über berechnete Attribute](../computed-attributes/overview.md). Weitere Informationen zur Verwendung berechneter Attribute in der Platform-Benutzeroberfläche finden Sie im Handbuch [für die Benutzeroberfläche für berechnete Attribute](../computed-attributes/ui.md).

## Nächste Schritte

Durch Lesen dieses Handbuchs wissen Sie, wie Sie die Profildaten Ihres Unternehmens mithilfe der Experience Platform-Benutzeroberfläche anzeigen und verwalten können. Informationen zum Arbeiten mit Profildaten mithilfe von Experience Platform-APIs finden Sie im [Handbuch zur Echtzeit-Kundenprofil-API](../api/overview.md).
