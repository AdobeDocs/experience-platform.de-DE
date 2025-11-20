---
title: Handbuch zur Benutzeroberfläche für berechnete Attribute
description: Erfahren Sie, wie Sie berechnete Attribute mithilfe der Adobe Experience Platform-Benutzeroberfläche erstellen, anzeigen und aktualisieren.
exl-id: bc621167-6dba-473e-90e4-aac7ceb6579a
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 7%

---

# Handbuch zur Benutzeroberfläche für berechnete Attribute

>[!NOTE]
>
>Für den Zugriff auf berechnete Attribute benötigen Sie die entsprechenden Berechtigungen (**Berechnete Attribute anzeigen** und **Berechnete Attribute verwalten**). Weitere Informationen zu den erforderlichen Berechtigungen finden Sie in der [Dokumentation zur Zugriffssteuerung](../../access-control/home.md). Informationen zum Anwenden dieser Berechtigungen finden Sie im [Handbuch zum Verwalten von Berechtigungen](../../access-control/ui/permissions.md).

In Adobe Experience Platform sind berechnete Attribute Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Diese Funktionen werden automatisch berechnet, damit sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.

Dieses Dokument enthält eine Anleitung zum Erstellen und Aktualisieren berechneter Attribute mithilfe der Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Handbuch für die Benutzeroberfläche setzt ein Verständnis der verschiedenen [!DNL Experience Platform]-Services voraus, die mit der Verwaltung von [!DNL Real-Time Customer Profiles] zusammenhängen. Bevor Sie dieses Handbuch lesen oder in der Benutzeroberfläche arbeiten, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.

## Berechnete Attribute anzeigen {#view}

Wählen Sie in der Benutzeroberfläche von Experience Platform im linken Navigationsbereich die Option **[!UICONTROL Profiles]** und dann **[!UICONTROL Computed attributes]** aus, um eine Liste der für Ihr Unternehmen verfügbaren berechneten Attribute anzuzeigen. Dazu gehören Informationen zum Namen, zur Beschreibung, zum letzten Auswertungsdatum und zum letzten Auswertungsstatus des berechneten Attributs.

![Der Abschnitt [!UICONTROL Profile] und die Registerkarten [!UICONTROL Computed attributes] sind hervorgehoben und zeigen Benutzern, wie sie auf die Seite zum Durchsuchen berechneter Attribute zugreifen können.](./images/ui/browse.png)

Um auszuwählen, welche Felder angezeigt werden sollen, können Sie ![das Symbol Spalten konfigurieren](/help/images/icons/column-settings.png) auswählen, um die anzuzeigenden Felder hinzuzufügen oder zu entfernen.

| Feld | Beschreibung |
| ----- | ----------- |
| [!UICONTROL Name] | Der Anzeigename des berechneten Attributs. |
| [!UICONTROL Description] | Die Beschreibung für das berechnete Attribut. |
| [!UICONTROL Evaluation method] | Die Auswertungsmethode für das berechnete Attribut. Derzeit wird nur **batch** unterstützt. |
| [!UICONTROL Last evaluated] | Dieser Zeitstempel stellt den letzten erfolgreichen Auswertungsdurchgang dar. Nur Ereignisse, die **vor** diesem Zeitstempel aufgetreten sind, werden bei der letzten erfolgreichen Auswertung berücksichtigt. |
| [!UICONTROL Last evaluation status] | Der Status, der angibt, ob das berechnete Attribut im letzten Auswertungsdurchgang erfolgreich berechnet wurde. Mögliche Werte sind **[!UICONTROL Success]** oder **[!UICONTROL Failed]**. |
| [!UICONTROL Refresh frequency] | Ein Hinweis darauf, wie oft das berechnete Attribut voraussichtlich aktualisiert wird. Mögliche Werte sind stündlich, täglich, wöchentlich oder monatlich. |
| [!UICONTROL Fast refresh] | Ein -Wert, der anzeigt, ob die schnelle Aktualisierung für dieses Compute-Attribut aktiviert ist. Wenn die schnelle Aktualisierung aktiviert ist, kann das berechnete Attribut täglich und nicht wöchentlich, alle zwei Wochen oder monatlich aktualisiert werden. Dieser Wert gilt nur für berechnete Attribute mit einem Lookback-Zeitraum von mehr als einer Woche. |
| [!UICONTROL Lifecycle status] | Der aktuelle Status des berechneten Attributs. Es gibt drei mögliche Status: <ul><li>**[!UICONTROL Draft]:** Für das berechnete Attribut **noch** Feld für das Schema erstellt. In diesem Zustand kann das berechnete Attribut bearbeitet werden. </li><li>**[!UICONTROL Published]:** Das berechnete Attribut verfügt über ein für das Schema erstelltes Feld, das verwendet werden kann. In diesem Zustand kann das berechnete Attribut **nicht** bearbeitet werden.</li><li>**[!UICONTROL Inactive]:** Das berechnete Attribut ist deaktiviert. Weitere Informationen zum inaktiven Status finden Sie auf der [FAQ-Seite](./faq.md#inactive-status). </li> |
| [!UICONTROL Created] | Ein Zeitstempel, der das Datum und die Uhrzeit der Erstellung des berechneten Attributs anzeigt. |
| [!UICONTROL Last modified] | Ein Zeitstempel, der das Datum und die Uhrzeit der letzten Änderung des berechneten Attributs anzeigt. |

Sie können die angezeigten berechneten Attribute auch nach dem Lebenszyklusstatus filtern. Wählen Sie das Symbol ![funnel](/help/images/icons/filter.png) aus.

![Das Filtersymbol ist hervorgehoben.](./images/ui/select-filter.png)

Sie können jetzt die berechneten Attribute nach Status filtern ([!UICONTROL Draft], [!UICONTROL Published] und [!UICONTROL Inactive]).

![Die Optionen, nach denen Sie die berechneten Attribute filtern können, sind hervorgehoben. Zu diesen Optionen gehören [!UICONTROL Draft], [!UICONTROL Published] und [!UICONTROL Inactive].](./images/ui/view-filters.png)

Darüber hinaus können Sie ein berechnetes Attribut auswählen, um detailliertere Informationen dazu anzuzeigen. Weitere Informationen zur Detailseite für berechnete Attribute finden Sie im Abschnitt [Details eines berechneten Attributs anzeigen](#view-details).

## Berechnetes Attribut erstellen {#create}

Um ein neues berechnetes Attribut zu erstellen, wählen Sie **[!UICONTROL Create computed attribute]** aus, um den neuen Workflow für berechnete Attribute einzugeben.

![Die Schaltfläche &quot;[!UICONTROL Create computed attributes]&quot; ist hervorgehoben und zeigt den Benutzern, wie sie die Seite zum Erstellen eines berechneten Attributs erreichen.](./images/ui/create.png)

Die Seite **[!UICONTROL Create computed attribute]** wird angezeigt. Auf dieser Seite können Sie die grundlegenden Informationen für das berechnete Attribut hinzufügen, das Sie erstellen möchten.

| Feld | Beschreibung |
| ----- | ----------- |
| [!UICONTROL Display name] | Der Name, unter dem das berechnete Attribut bekannt ist. Sie sollten diesen Anzeigenamen für jedes berechnete Attribut eindeutig halten. Als Best Practice sollte dieser Anzeigename Kennungen enthalten, die sich auf das berechnete Attribut beziehen. Beispiel: „Summe der Schuhkäufe der letzten 7 Tage“. |
| [!UICONTROL Field name] | Ein Name, der verwendet wird, um auf das berechnete Attribut in anderen nachgelagerten -Services zu verweisen. Dieser Name wird automatisch aus dem Anzeigenamen abgeleitet und in Binnenmajuskel-Schreibweise geschrieben. |
| [!UICONTROL Description] | Eine Beschreibung des berechneten Attributs, das Sie erstellen möchten. |

![Der [!UICONTROL Basic information] Abschnitt der [!UICONTROL Create computed attribute] ist hervorgehoben.](./images/ui/basic-information.png)

Nachdem Sie die berechneten Attributdetails hinzugefügt haben, können Sie mit der Definition Ihrer Regeln beginnen.

### Angeben der Filterbedingungen für Ereignisse

Um eine Regel zu erstellen, wählen Sie zunächst Attribute aus dem Abschnitt **[!UICONTROL Events]** aus, um nach Ereignissen zu filtern, die aggregiert werden sollen. Derzeit werden nur Ereignisattribute unterstützt, die nicht vom Array-Typ sind.

![Der [!UICONTROL Events] ist hervorgehoben.](./images/ui/events.png)

Nachdem Sie das Attribut ausgewählt haben, das in der Definition des berechneten Attributs verwendet werden soll, können Sie auswählen, mit welchem Wert dieser verglichen werden soll.

![Die verfügbaren Vergleichstypen werden angezeigt.](./images/ui/select-comparison.png)

### Aggregationsfunktion anwenden

Jetzt können Sie eine Funktion aus der bedingten Ausgabe auf das Feld anwenden. Wählen Sie zunächst den Typ der Aggregationsfunktion aus. Zu den verfügbaren Optionen gehören [!UICONTROL Sum], [!UICONTROL Min], [!UICONTROL Max], [!UICONTROL Count] und [!UICONTROL Most Recent]. Weitere Informationen zu diesen Funktionen finden Sie im Abschnitt [Funktionen](./overview.md#functions) der Übersicht über berechnete Attribute .

![Die Funktionen für berechnete Attribute werden angezeigt.](./images/ui/select-function.png)

Nach Auswahl einer Funktion können Sie das Feld auswählen, nach dem aggregiert werden soll. Welche Felder ausgewählt werden können, hängt von der ausgewählten Funktion ab.

![Das hervorgehobene Feld zeigt das Attribut an, für das Sie die Funktion aggregieren möchten.](./images/ui/select-eligible-field.png)

### Lookback-Dauer

Nach Anwendung der Aggregationsfunktion müssen Sie den Lookback-Zeitraum des berechneten Attributs definieren. Dieser Lookback-Zeitraum gibt die Zeitdauer an, für die Sie Ereignisse aggregieren möchten. Diese Lookback-Dauer kann in Stunden, Tagen, Wochen oder Monaten angegeben werden.

![Die Lookback-Dauer ist hervorgehoben.](./images/ui/select-lookback-duration.png)

### Schnelle Aktualisierung {#fast-refresh}

>[!CONTEXTUALHELP]
>id="platform_profile_computedAttributes_fastRefresh"
>title="Schnelle Aktualisierung"
>abstract="Mit der schnellen Aktualisierung können Sie Ihre Attribute auf dem neuesten Stand halten. Wenn Sie diese Option aktivieren, können Sie Ihre berechneten Attribute täglich aktualisieren, auch über längere Lookback-Zeiträume, sodass Sie schnell auf Benutzeraktivitäten reagieren können. Dieser Wert gilt nur für berechnete Attribute mit einem Lookback-Zeitraum von mehr als einer Woche."

Bei Anwendung der Aggregationsfunktion können Sie eine schnelle Aktualisierung aktivieren, wenn der Lookback-Zeitraum länger als eine Woche ist.

![Das Kontrollkästchen &quot;[!UICONTROL Fast Refresh]&quot; ist hervorgehoben.](./images/ui/enable-fast-refresh.png)

Mit der schnellen Aktualisierung können Sie Ihre Attribute auf dem neuesten Stand halten. Durch Aktivierung dieser Option können Sie Ihre berechneten Attribute täglich aktualisieren, auch für längere Lookback-Zeiträume, sodass Sie schnell auf Benutzeraktivitäten reagieren können.

Weitere Informationen zur schnellen Aktualisierung finden Sie im Abschnitt [schnelle Aktualisierung](./overview.md#fast-refresh) der Übersicht über berechnete Attribute.

Nachdem diese Schritte abgeschlossen sind, können Sie jetzt entweder wählen, dieses berechnete Attribut als Entwurf zu speichern oder es sofort zu veröffentlichen.

![Die Schaltflächen &quot;[!UICONTROL Save as draft]&quot; und &quot;[!UICONTROL Publish]&quot; sind hervorgehoben.](./images/ui/draft-or-publish.png)

## Anzeigen der Details eines berechneten Attributs {#view-details}

Um die Details eines berechneten Attributs anzuzeigen, wählen Sie das berechnete Attribut aus, zu dem Sie Details auf der Seite [!UICONTROL **Durchsuchen**] anzeigen möchten.

![Ein berechnetes Attribut ist hervorgehoben.](./images/ui/select.png)

Der Inhalt der Seite unterscheidet sich, je nachdem, ob das berechnete Attribut **[!UICONTROL Published]** oder in **[!UICONTROL Draft]** ist.

### Berechnetes Attribut veröffentlicht {#published}

Bei Auswahl eines veröffentlichten berechneten Attributs wird die Detailseite für berechnete Attribute angezeigt.

![Die Detailseite des berechneten Attributs wird angezeigt.](./images/ui/details.png)

Auf dieser Seite wird eine Zusammenfassung der Details des berechneten Attributs sowie ein Diagramm angezeigt, das die Werteverteilung sowie Beispielprofile anzeigt, die für das berechnete Attribut qualifiziert sind.

>[!NOTE]
>
>Die Werteverteilung spiegelt die Verteilung der Attributwerte für Profile zum Zeitpunkt des Sampling-Auftrags wider. Der berechnete Attributwert im Beispielprofil spiegelt den neuesten zusammengeführten Profilwert für einige Beispielprofile wider.

### Berechnetes Entwurfsattribut {#draft}

Bei Auswahl eines Entwurfs für ein berechnetes Attribut wird die Seite **[!UICONTROL Edit computed attributes]** angezeigt. Auf dieser Seite können Sie, ähnlich wie auf der Seite [!UICONTROL Create computed attributes], die grundlegenden Informationen des berechneten Attributs sowie dessen Definition bearbeiten, bevor Sie den Entwurf aktualisieren oder veröffentlichen.

![Die [!UICONTROL Edit computed attributes] wird angezeigt.](./images/ui/edit.png)

## Verwenden berechneter Attribute {#usage}

>[!IMPORTANT]
>
>Wenn Sie ein berechnetes Attribut mit der Funktion **Zuletzt verwendet** in einer Segmentdefinition verwenden, **müssen** sowohl **&#x200B;**&#x200B;Wert als auch den Zeitstempelwert im berechneten Attributobjekt einbeziehen.
>
>Wenn Sie beispielsweise eine Segmentdefinition erstellen, die nach „Alle Profile mit einer gültigen E-Mail-Adresse“ sucht, in der das Feld „E-Mail-Adresse“ mit einem berechneten Attribut mit der neuesten Funktion gefüllt ist, **Sie** sowohl den Wert der E-Mail-Adresse als auch **&#x200B;**&#x200B;Zeitstempel der E-Mail-Adresse“ einbeziehen.

Nachdem Sie ein berechnetes Attribut erstellt haben, können Sie **veröffentlichte** berechneten Attribute in anderen nachgelagerten -Services verwenden. Da berechnete Attribute Profilattributfelder sind, die für Ihr Profilvereinigungsschema erstellt wurden, können Sie berechnete Attributwerte für ein Echtzeit-Kundenprofil nachschlagen, sie in einer Zielgruppe verwenden, für ein Ziel aktivieren oder sie für die Personalisierung in Journey in Adobe Journey Optimizer verwenden.

>[!NOTE]
>
>Berechnete Attribute **können nicht** in Zielgruppen-**verwendet**.

![Der Segment Builder wird angezeigt und zeigt ein berechnetes Attribut als Teil der Segmentdefinitionskomposition an.](./images/ui/use-ca.png)

## Nächste Schritte

Weitere Informationen zu berechneten Attributen finden Sie unter [Berechnete Attribute - Übersicht](./overview.md). Informationen zum Erstellen und Konfigurieren berechneter Attribute mithilfe der API finden Sie im [Entwicklerhandbuch für berechnete Attribute](./api.md).
