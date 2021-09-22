---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; einheitliches Profil; Einheitliches Profil; einheitliches Profil; Profil; rtcp; Profil aktivieren; Profil aktivieren; Vereinigungsschema; UNION PROFILE; Vereinigungsprofil
title: Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils
topic-legacy: guide
description: Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht Ihrer einzelnen Kunden und fasst Daten aus mehreren Kanälen (einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen. Dieses Dokument dient als Leitfaden für die Interaktion mit dem Echtzeit-Kundenprofil in der Benutzeroberfläche von Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 69e510c9a0f477ad7cab530128c6728f68dfdab1
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 12%

---

# Handbuch für die [!DNL Real-time Customer Profile]-Benutzeroberfläche

[!DNL Real-time Customer Profile] erstellt eine ganzheitliche Ansicht Ihrer einzelnen Kunden, wobei Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten, kombiniert werden. Dieses Dokument dient als Leitfaden für die Interaktion mit [!DNL Real-time Customer Profile]-Daten in der Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses UI-Handbuch setzt ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste voraus, die mit der Verwaltung von [!DNL Real-time Customer Profiles] verbunden sind. Bevor Sie dieses Handbuch lesen oder in der Benutzeroberfläche arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Real-time Customer Profile] Übersicht](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Identity Service]](../../identity-service/home.md): Ermöglicht  [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen bei der Erfassung in  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

## [!UICONTROL Übersicht]

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Profile]** aus, um die Registerkarte **[!UICONTROL Übersicht]** zu öffnen, auf der das Profil-Dashboard angezeigt wird.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, ist das Dashboard [!UICONTROL Profile] nicht sichtbar. Stattdessen werden auf der Registerkarte [!UICONTROL Übersicht] Links und Dokumentation angezeigt, die Ihnen bei den ersten Schritten mit dem Echtzeit-Kundenprofil helfen.

### Profil-Dashboard {#profile-dashboard}

Im Profil-Dashboard werden Schlüsselmetriken im Zusammenhang mit den Profildaten Ihres Unternehmens beschrieben.

Weitere Informationen finden Sie im [Profil-Dashboard-Handbuch](../../dashboards/guides/profiles.md).

![](../../dashboards/images/profiles/dashboard-overview.png)

##  Metriken der Registerkarte &quot;Durchsuchen&quot;

Wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** aus, um mehrere Metriken anzuzeigen, die sich auf die Profildaten Ihres Unternehmens beziehen. Sie können diese Registerkarte auch verwenden, um den Profilspeicher mithilfe einer Zusammenführungsrichtlinie oder einer Identität zu durchsuchen, wie im nächsten Abschnitt dieses Handbuchs beschrieben.

Auf der rechten Seite des Tabs **[!UICONTROL Durchsuchen]** befindet sich die [Profilanzahl](#profile-count) sowie eine Liste mit [Profilen nach Namespace](#profiles-by-namespace).

>[!NOTE]
>
>Diese Profilmetriken können von den Metriken abweichen, die im [Profil-Dashboard](#profile-dashboard) angezeigt werden, da sie mit der standardmäßigen Zusammenführungsrichtlinie Ihres Unternehmens ausgewertet werden. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien, einschließlich der Definition einer standardmäßigen Zusammenführungsrichtlinie, finden Sie unter [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

Zusätzlich zu diesen Metriken bietet dieser Abschnitt ein Datum und eine Uhrzeit der letzten Aktualisierung, die zeigen, wann die Metriken zuletzt ausgewertet wurden.

![](../images/user-guide/profiles-browse-metrics.png)

### Anzahl der Profile {#profile-count}

Die Anzahl der Profile zeigt die Gesamtanzahl der Profile an, über die Ihre Organisation in Experience Platform verfügt, nachdem die standardmäßige Zusammenführungsrichtlinie Ihrer Organisation Profilfragmente zusammengeführt hat, um für jeden Kunden ein einzelnes Profil zu erstellen. Mit anderen Worten: Ihre Organisation hat möglicherweise verschiedene Profilfragmente, die sich auf einen einzelnen Kunden beziehen, der mit Ihrer Marke über unterschiedliche Kanäle interagiert. Diese Fragmente würden jedoch zusammengeführt (gemäß der standardmäßigen Zusammenführungsrichtlinie) und eine Anzahl von „1“ zurückgeben, da sie alle mit derselben Person verbunden sind.

Die Profilanzahl umfasst auch Profile mit Attributen (Datensatzdaten) sowie Profile, die nur Zeitreihendaten (Ereignisdaten) enthalten, z. B. Adobe Analytics-Profile. Die Profilanzahl wird regelmäßig aktualisiert, um eine aktuelle Gesamtanzahl von Profilen in Platform bereitzustellen.

#### Profilzählungsmetrik aktualisieren

Wenn die Aufnahme von Datensätzen in den Speicher [!DNL Profile] die Anzahl um mehr als 5 % erhöht oder verringert, wird ein Auftrag ausgelöst, der die Anzahl aktualisiert. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für eine Zu- oder Abnahme um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Profilanzahl zu aktualisieren. Bei der Batch-Erfassung wird innerhalb von 15 Minuten nach erfolgreicher Aufnahme eines Batches in den Profilspeicher ein Auftrag ausgeführt, um die Profilanzahl zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht ist.

### [!UICONTROL Profile nach Namespace] {#profiles-by-namespace}

Die Metrik **[!UICONTROL Profile nach Namespace]** zeigt die Gesamtanzahl und Aufschlüsselung der Namespaces für alle zusammengeführten Profile in Ihrem Profilspeicher an. Die Gesamtzahl der Profile nach Namespace (d. h. das Addieren der für jeden Namespace angezeigten Werte) ist immer höher als die Metrik für die Profilanzahl, da einem Profil mehrere Namespaces zugeordnet sein können. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

#### Aktualisieren der Metrik [!UICONTROL Profile nach Namespace]

Ähnlich wie bei der Metrik [Profilanzahl](#profile-count) wird ein Auftrag ausgelöst, um die Namespace-Metriken zu aktualisieren, wenn durch die Aufnahme von Datensätzen in den [!DNL Profile]-Speicher die Anzahl um mehr als 5 % erhöht oder verringert wird. Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für eine Zu- oder Abnahme um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Profilanzahl zu aktualisieren. Bei der Batch-Erfassung wird innerhalb von 15 Minuten nach erfolgreicher Aufnahme eines Batches in den [!DNL Profile]-Speicher ein Auftrag ausgeführt, um die Metriken zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht ist.

## Verwenden Sie die Registerkarte [!UICONTROL Durchsuchen] , um Profile anzuzeigen.

Auf dem Tab **[!UICONTROL Durchsuchen]** können Sie Beispielprofile mithilfe einer Zusammenführungsrichtlinie anzeigen oder mithilfe eines Identitäts-Namespace und -Werts nach bestimmten Profilen suchen.

![](../images/user-guide/browse-by-none-selected.png)

### Durchsuchen nach [!UICONTROL Zusammenführungsrichtlinie]

Die Registerkarte **[!UICONTROL Durchsuchen]** ist standardmäßig auf die standardmäßige Zusammenführungsrichtlinie für Ihre Organisation festgelegt. Um eine andere Zusammenführungsrichtlinie auszuwählen, wählen Sie `X` neben dem Namen der Zusammenführungsrichtlinie aus und öffnen Sie dann mithilfe des Selektors das Dialogfeld **[!UICONTROL Zusammenführungsrichtlinie auswählen]**.

>[!NOTE]
>
>Wenn keine Zusammenführungsrichtlinie ausgewählt ist, verwenden Sie die Auswahlschaltfläche neben dem Feld **[!UICONTROL Zusammenführungsrichtlinie]** , um das Auswahldialogfeld zu öffnen.

![](../images/user-guide/browse-by-merge-policy.png)

Um eine Zusammenführungsrichtlinie aus dem Dialogfeld **[!UICONTROL Zusammenführungsrichtlinie auswählen]** auszuwählen, wählen Sie das Optionsfeld neben dem Richtliniennamen aus und verwenden Sie dann **[!UICONTROL Auswählen]**, um zur Registerkarte [!UICONTROL Durchsuchen] zurückzukehren. Sie können dann **[!UICONTROL Ansicht]** auswählen, um die Beispielprofile zu aktualisieren und eine Auswahl von Profilen mit der neuen angewendeten Zusammenführungsrichtlinie anzuzeigen.

![](../images/user-guide/select-merge-policy-dialog.png)

Die angezeigten Profile stellen ein Beispiel von bis zu 20 Profilen aus dem Profilspeicher Ihres Unternehmens dar, nachdem die ausgewählte Zusammenführungsrichtlinie angewendet wurde. Die Beispielprofile für die ausgewählte Zusammenführungsrichtlinie werden aktualisiert, wenn dem Profilspeicher Ihres Unternehmens neue Daten hinzugefügt werden.

Um die Details eines der Beispielprofile anzuzeigen, wählen Sie die **[!UICONTROL Profil-ID]** aus. Weitere Informationen finden Sie im Abschnitt weiter unten in diesem Handbuch zu [Anzeigen von Profildetails](#profile-detail).

![](../images/user-guide/sample-profiles.png)

Weitere Informationen zu Zusammenführungsrichtlinien und ihrer Rolle in Platform finden Sie unter [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).


### Durchsuchen nach [!UICONTROL Identität] {#browse-identity}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** können Sie einen Identitäts-Namespace verwenden, um ein bestimmtes Profil nach einem Identitätswert zu suchen. Für das Durchsuchen nach einer Identität müssen Sie eine Zusammenführungsrichtlinie, einen Identitäts-Namespace und einen Identitätswert angeben.

![](../images/user-guide/browse-by-identity.png)

Verwenden Sie bei Bedarf den Selektor **[!UICONTROL Zusammenführungsrichtlinie]** , um das Dialogfeld **[!UICONTROL Zusammenführungsrichtlinie auswählen]** zu öffnen und die gewünschte Zusammenführungsrichtlinie auszuwählen.

![](../images/user-guide/select-merge-policy-dialog.png)

Verwenden Sie dann den Selektor **[!UICONTROL Identitäts-Namespace]** , um das Dialogfeld **[!UICONTROL Wählen Sie den Identitäts-Namespace]** und wählen Sie den Namespace aus, nach dem Sie suchen möchten. Wenn Ihr Unternehmen über viele Namespaces verfügt, können Sie über die Suchleiste im Dialogfeld mit der Eingabe des Namens eines Namespace beginnen.

Sie können einen Namespace auswählen, um weitere Details anzuzeigen, oder das Optionsfeld auswählen, um einen Namespace auszuwählen. Sie können dann **[!UICONTROL Wählen]** verwenden, um fortzufahren.

![](../images/user-guide/profiles-select-identity-namespace.png)

Nachdem Sie einen [!UICONTROL Identitäts-Namespace] ausgewählt und zum Tab [!UICONTROL Durchsuchen] zurückgekehrt haben, können Sie einen **[!UICONTROL Identitätswert]** eingeben, der sich auf den ausgewählten Namespace bezieht.

>[!NOTE]
>
>Dieser Wert ist spezifisch für ein einzelnes Kundenprofil und muss ein gültiger Eintrag für den angegebenen Namespace sein. Beispielsweise würde die Auswahl des Identitäts-Namespace &quot;E-Mail&quot;einen Identitätswert in Form einer gültigen E-Mail-Adresse erfordern.

![](../images/user-guide/browse-by-identity-values.png)

Nachdem ein Wert eingegeben wurde, wählen Sie **[!UICONTROL Ansicht]** und ein einzelnes Profil, das dem Wert entspricht, wird zurückgegeben. Wählen Sie **[!UICONTROL Profil-ID]** aus, um die Profildetails anzuzeigen.

![](../images/user-guide/browse-by-identity-profile.png)

## Profildetails anzeigen {#profile-detail}

Nach Auswahl einer **[!UICONTROL Profil-ID]** wird die Registerkarte **[!UICONTROL Detail]** geöffnet. Die auf der Registerkarte **[!UICONTROL Detail]** angezeigten Profilinformationen wurden aus mehreren Profilfragmenten zusammengeführt, um eine einzige Ansicht des einzelnen Kunden zu bilden. Dazu gehören Kundendetails wie grundlegende Attribute, verknüpfte Identitäten und Kanalpräferenzen.

Die angezeigten Standardfelder können auch auf Organisationsebene geändert werden, um die bevorzugten Profilattribute anzuzeigen. Weitere Informationen zum Anpassen dieser Felder, einschließlich einer schrittweisen Anleitung zum Hinzufügen und Entfernen von Attributen und zum Ändern der Größe von Dashboard-Bedienfeldern, finden Sie im [Handbuch zur Profildetailanpassung](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

Sie können zusätzliche Informationen zum jeweiligen Profil anzeigen, indem Sie eine andere der verfügbaren Registerkarten auswählen. Diese Registerkarten umfassen Attribute, Ereignisse und die Registerkarte Segmentmitgliedschaft , auf der die Segmente angezeigt werden, für die das Profil derzeit qualifiziert ist.

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

Durch Lesen dieses Handbuchs wissen Sie, wie Sie die Profildaten Ihres Unternehmens mithilfe der Experience Platform-Benutzeroberfläche anzeigen und verwalten können. Informationen zum Arbeiten mit Profildaten mithilfe von Experience Platform-APIs finden Sie im [Handbuch zur Echtzeit-Kundenprofil-API](../api/overview.md).
