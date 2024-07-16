---
title: Handbuch zur Benutzeroberfläche "Berechnete Attribute"
description: Erfahren Sie, wie Sie berechnete Attribute mithilfe der Adobe Experience Platform-Benutzeroberfläche erstellen, anzeigen und aktualisieren.
exl-id: bc621167-6dba-473e-90e4-aac7ceb6579a
source-git-commit: 762a7fc7dd00657e4e710eb763c5bb63b210593a
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 7%

---

# Handbuch zur Benutzeroberfläche für berechnete Attribute

>[!NOTE]
>
>Um Zugriff auf berechnete Attribute zu erhalten, benötigen Sie die entsprechenden Berechtigungen (**Berechnete Attribute anzeigen** und **Berechnete Attribute verwalten**). Weitere Informationen zu den erforderlichen Berechtigungen finden Sie in der Dokumentation zur Zugriffskontrolle [1}. ](../../access-control/home.md) Informationen zum Anwenden dieser Berechtigungen finden Sie im [Berechtigungshandbuch verwalten](../../access-control/ui/permissions.md) .

In Adobe Experience Platform sind berechnete Attribute Funktionen zum Aggregieren von Daten auf Ereignisebene in Profilattributen. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.

Dieses Dokument enthält eine Anleitung zum Erstellen und Aktualisieren berechneter Attribute mithilfe der Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses UI-Handbuch setzt ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste voraus, die mit der Verwaltung von [!DNL Real-Time Customer Profiles] verbunden sind. Bevor Sie dieses Handbuch lesen oder in der Benutzeroberfläche arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-Time Customer Profile]](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.

## Berechnete Attribute anzeigen {#view}

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Profile]** und dann **[!UICONTROL Berechnete Attribute]** aus, um eine Liste der für Ihr Unternehmen verfügbaren berechneten Attribute anzuzeigen. Dazu gehören Informationen zum Namen, zur Beschreibung, zum letzten Auswertungsdatum und zum letzten Auswertungsstatus des berechneten Attributs.

![Der Abschnitt [!UICONTROL Profil] und die Registerkarten [!UICONTROL Berechnete Attribute] sind hervorgehoben und zeigen Benutzern, wie sie auf die Durchsuchen-Seite für berechnete Attribute zugreifen können.](./images/ui/browse.png)

Um auszuwählen, welche Felder sichtbar sind, können Sie ![das Symbol zum Konfigurieren von Spalten](./images/ui/configure-icon.png) auswählen, um die Felder hinzuzufügen oder zu entfernen, die angezeigt werden sollen.

| Feld | Beschreibung |
| ----- | ----------- |
| [!UICONTROL Name] | Der Anzeigename des berechneten Attributs. |
| [!UICONTROL Beschreibung] | Die Beschreibung für das berechnete Attribut. |
| [!UICONTROL Auswertungsmethode] | Die Auswertungsmethode für das berechnete Attribut. Derzeit wird nur **batch** unterstützt. |
| [!UICONTROL Zuletzt ausgewertet] | Dieser Zeitstempel stellt den letzten erfolgreichen Evaluierungsablauf dar. Nur Ereignisse, die **vor** diesem Zeitstempel auftraten, werden bei der letzten erfolgreichen Auswertung berücksichtigt. |
| [!UICONTROL Letzter Bewertungsstatus] | Der Status, der angibt, ob das berechnete Attribut im letzten Bewertungslauf erfolgreich berechnet wurde oder nicht. Mögliche Werte sind **[!UICONTROL Erfolg]** oder **[!UICONTROL Fehlgeschlagen]**. |
| [!UICONTROL Aktualisierungshäufigkeit] | Ein Hinweis darauf, wie häufig das berechnete Attribut aktualisiert werden soll. Mögliche Werte sind stündlich, täglich, wöchentlich oder monatlich. |
| [!UICONTROL Schnelle Aktualisierung] | Ein Wert, der anzeigt, ob für dieses Compute-Attribut eine schnelle Aktualisierung aktiviert ist. Wenn die schnelle Aktualisierung aktiviert ist, kann das berechnete Attribut täglich aktualisiert werden, nicht wöchentlich, zweimal wöchentlich oder monatlich. Dieser Wert gilt nur für berechnete Attribute mit einem Lookback-Zeitraum von mehr als einer Woche. |
| [!UICONTROL Lebenszyklusstatus] | Der aktuelle Status des berechneten Attributs. Es gibt drei mögliche Status: <ul><li>**[!UICONTROL Entwurf]:** Für das berechnete Attribut wurde **noch kein Feld im Schema erstellt.** In diesem Status kann das berechnete Attribut bearbeitet werden. </li><li>**[!UICONTROL Veröffentlicht]:** Das berechnete Attribut hat ein Feld, das für das Schema erstellt wurde und zur Verwendung bereit ist. In diesem Status kann das berechnete Attribut **nicht** bearbeitet werden.</li><li>**[!UICONTROL Inaktiv]:** Das berechnete Attribut ist deaktiviert. Weitere Informationen zum inaktiven Status finden Sie auf der [FAQ-Seite](./faq.md#inactive-status). </li> |
| [!UICONTROL Erstellt] | Ein Zeitstempel, der das Datum und die Uhrzeit der Erstellung des berechneten Attributs anzeigt. |
| [!UICONTROL Zuletzt geändert] | Ein Zeitstempel, der das Datum und die Uhrzeit der letzten Änderung des berechneten Attributs anzeigt. |

Sie können auch die angezeigten berechneten Attribute basierend auf dem Lebenszyklusstatus filtern. Wählen Sie das Symbol ![Trichter](./images/ui/filter-icon.png) aus.

![Das Filtersymbol wird hervorgehoben.](./images/ui/select-filter.png)

Sie können jetzt die berechneten Attribute nach Status filtern ([!UICONTROL Entwurf], [!UICONTROL Veröffentlicht] und [!UICONTROL Inaktiv]).

![Die Optionen, nach denen Sie die berechneten Attribute filtern können, sind hervorgehoben. Zu diesen Optionen gehören [!UICONTROL Entwurf], [!UICONTROL Veröffentlicht] und [!UICONTROL Inaktiv].](./images/ui/view-filters.png)

Darüber hinaus können Sie ein berechnetes Attribut auswählen, um genauere Informationen dazu anzuzeigen. Weitere Informationen zur Detailseite für berechnete Attribute finden Sie im Abschnitt [Details eines berechneten Attributs anzeigen](#view-details).

## Berechnetes Attribut erstellen {#create}

Um ein neues berechnetes Attribut zu erstellen, wählen Sie **[!UICONTROL Berechnetes Attribut erstellen]** aus, um den neuen Workflow für berechnete Attribute einzugeben.

![Die Schaltfläche [!UICONTROL Berechnete Attribute erstellen] ist hervorgehoben und zeigt Benutzern, wie sie die Seite &quot;Berechnetes Attribut erstellen&quot;erreichen.](./images/ui/create.png)

Die Seite **[!UICONTROL Berechnetes Attribut erstellen]** wird angezeigt. Auf dieser Seite können Sie die grundlegenden Informationen für das berechnete Attribut hinzufügen, das Sie erstellen möchten.

| Feld | Beschreibung |
| ----- | ----------- |
| [!UICONTROL Anzeigename] | Der Name, durch den das berechnete Attribut bekannt sein wird. Dieser Anzeigename sollte für jedes berechnete Attribut eindeutig sein. Als Best Practice sollte dieser Anzeigename Kennungen zum berechneten Attribut enthalten. Beispielsweise &quot;Summe der Käufe für Schuhe in den letzten sieben Tagen&quot;. |
| [!UICONTROL Feldname] | Ein Name, mit dem auf das berechnete Attribut in anderen nachgelagerten Diensten verwiesen wird. Dieser Name wird automatisch aus dem Anzeigenamen abgeleitet und in camelCase geschrieben. |
| [!UICONTROL Beschreibung] | Eine Beschreibung des berechneten Attributs, das Sie erstellen möchten. |

![Der Abschnitt [!UICONTROL Grundlegende Informationen] der Seite [!UICONTROL Berechnetes Attribut erstellen] ist hervorgehoben.](./images/ui/basic-information.png)

Nachdem Sie die berechneten Attributdetails hinzugefügt haben, können Sie mit der Definition Ihrer Regeln beginnen.

### Filterbedingungen für Ereignisse festlegen

Um eine Regel zu erstellen, wählen Sie zunächst Attribute aus dem Abschnitt **[!UICONTROL Ereignisse]** aus, um Ereignisse zu filtern, die aggregiert werden sollen. Derzeit werden nur Ereignisattribute vom Typ Nicht-Array unterstützt.

![Der Abschnitt [!UICONTROL Ereignisse] ist hervorgehoben.](./images/ui/events.png)

Nachdem Sie das Attribut ausgewählt haben, das in der Definition des berechneten Attributs verwendet werden soll, können Sie auswählen, mit welchem Wert dieser Wert verglichen werden soll.

![Die verfügbaren Vergleichstypen werden angezeigt.](./images/ui/select-comparison.png)

### Aggregationsfunktion anwenden

Jetzt können Sie eine Funktion aus der bedingten Ausgabe auf das Feld anwenden. Wählen Sie zunächst den Aggregations-Funktionstyp aus. Zu den verfügbaren Optionen gehören [!UICONTROL Summe], [!UICONTROL Minimum], [!UICONTROL Max], [!UICONTROL Zählung] und [!UICONTROL Zuletzt verwendet]. Weitere Informationen zu diesen Funktionen finden Sie im Abschnitt [Funktionen}](./overview.md#functions) der Übersicht über berechnete Attribute.

![Die berechneten Attributfunktionen werden angezeigt.](./images/ui/select-function.png)

Nach Auswahl einer Funktion können Sie das zu aggregierende Feld auswählen. Die auszuwählenden Felder hängen von der ausgewählten Funktion ab.

![Das hervorgehobene Feld zeigt das Attribut an, für das Sie die Funktion aggregieren möchten.](./images/ui/select-eligible-field.png)

### Lookback-Dauer

Nach Anwendung der Aggregationsfunktion müssen Sie den Lookback-Zeitraum des berechneten Attributs definieren. Dieser Lookback-Zeitraum gibt die Zeitdauer an, für die Sie Ereignisse aggregieren möchten. Diese Lookback-Dauer kann in Stunden, Tagen, Wochen oder Monaten angegeben werden.

![Die Lookback-Dauer ist hervorgehoben.](./images/ui/select-lookback-duration.png)

### Schnelle Aktualisierung {#fast-refresh}

>[!CONTEXTUALHELP]
>id="platform_profile_computedAttributes_fastRefresh"
>title="Schnelle Aktualisierung"
>abstract="Mit der schnellen Aktualisierung können Sie Ihre Attribute auf dem neuesten Stand halten. Wenn Sie diese Option aktivieren, können Sie Ihre berechneten Attribute täglich aktualisieren, auch über längere Lookback-Zeiträume, sodass Sie schnell auf Benutzeraktivitäten reagieren können. Dieser Wert gilt nur für berechnete Attribute mit einem Lookback-Zeitraum von mehr als einer Woche."

Bei Anwendung der Aggregationsfunktion können Sie eine schnelle Aktualisierung aktivieren, wenn der Lookback-Zeitraum größer als eine Woche ist.

![Das Kontrollkästchen [!UICONTROL Schnelle Aktualisierung] ist hervorgehoben.](./images/ui/enable-fast-refresh.png)

Mit der schnellen Aktualisierung können Sie Ihre Attribute auf dem neuesten Stand halten. Durch Aktivierung dieser Option können Sie Ihre berechneten Attribute täglich aktualisieren, auch über längere Lookback-Zeiträume, sodass Sie schnell auf Benutzeraktivitäten reagieren können.

Weiterführende Informationen zur schnellen Aktualisierung finden Sie im Abschnitt [Schnelle Aktualisierung](./overview.md#fast-refresh) der Übersicht über berechnete Attribute.

Nach Abschluss dieser Schritte können Sie dieses berechnete Attribut nun entweder als Entwurf speichern oder es sofort veröffentlichen.

![Die Schaltflächen [!UICONTROL Als Entwurf speichern] und [!UICONTROL Publish] sind hervorgehoben.](./images/ui/draft-or-publish.png)

## Details eines berechneten Attributs anzeigen {#view-details}

Um die Details eines berechneten Attributs anzuzeigen, wählen Sie das berechnete Attribut aus, über das Details auf der Seite [!UICONTROL **Durchsuchen**] angezeigt werden sollen.

![Ein berechnetes Attribut wird hervorgehoben.](./images/ui/select.png)

Der Inhalt der Seite unterscheidet sich je nachdem, ob das berechnete Attribut **[!UICONTROL Veröffentlicht]** oder in **[!UICONTROL Entwurf]** ist.

### Veröffentlichtes berechnetes Attribut {#published}

Bei der Auswahl eines veröffentlichten berechneten Attributs wird die Detailseite für berechnete Attribute angezeigt.

![Die Detailseite des berechneten Attributs wird angezeigt.](./images/ui/details.png)

Auf dieser Seite werden eine Zusammenfassung der Details des berechneten Attributs sowie ein Diagramm mit der Wertverteilung sowie Beispielprofilen angezeigt, die für das berechnete Attribut qualifiziert sind.

>[!NOTE]
>
>Die Werteverteilung spiegelt die Verteilung der Attributwerte für Profile zum Zeitpunkt des Sampling-Auftrags wider. Der berechnete Attributwert im Beispielprofil spiegelt den neuesten zusammengeführten Profilwert für einige Beispielprofile wider.

### Berechnetes Entwurfsattribut {#draft}

Bei der Auswahl eines Entwurfs für ein berechnetes Attribut wird die Seite **[!UICONTROL Berechnete Attribute bearbeiten]** angezeigt. Auf dieser Seite, ähnlich der Seite [!UICONTROL Berechnete Attribute erstellen] , können Sie die grundlegenden Informationen Ihres berechneten Attributs sowie dessen Definition bearbeiten, bevor Sie den Entwurf aktualisieren oder veröffentlichen können.

![Die Seite [!UICONTROL Berechnete Attribute bearbeiten] wird angezeigt.](./images/ui/edit.png)

## Berechnete Attribute verwenden {#usage}

>[!IMPORTANT]
>
>Wenn Sie ein berechnetes Attribut mit der Funktion **Zuletzt verwendet** in einer Segmentdefinition verwenden, müssen Sie **3}** sowohl **den Wert als auch den Zeitstempelwert in das berechnete Attributobjekt aufnehmen.**
>
>Wenn Sie z. B. eine Segmentdefinition erstellen, die nach &quot;Alle Profile mit einer gültigen E-Mail-Adresse&quot;sucht, bei der das Feld für die E-Mail-Adresse durch ein berechnetes Attribut mit der neuesten Funktion ausgefüllt wird, müssen Sie **1} sowohl den Wert der E-Mail-Adresse einschließen,** als auch **, wenn der Zeitstempel der E-Mail-Adresse vorhanden ist.**

Nach der Erstellung eines berechneten Attributs können Sie **veröffentlichte** berechnete Attribute in anderen nachgelagerten Diensten verwenden. Da berechnete Attribute Profilattributfelder sind, die in Ihrem Profilvereinigungsschema erstellt wurden, können Sie berechnete Attributwerte für ein Echtzeit-Kundenprofil nachschlagen, sie in einer Zielgruppe verwenden, sie für ein Ziel aktivieren oder sie zur Personalisierung in Journey in Adobe Journey Optimizer verwenden.

>[!NOTE]
>
>Berechnete Attribute **können nicht** in Zielgruppen-Kompositionen **verwendet werden**.

![Der Segment Builder wird angezeigt, in dem ein berechnetes Attribut als Teil der Segmentdefinitionskomposition angezeigt wird.](./images/ui/use-ca.png)

## Nächste Schritte

Weitere Informationen zu berechneten Attributen finden Sie in der [Übersicht über berechnete Attribute](./overview.md). Informationen zum Erstellen und Konfigurieren von berechneten Attributen mithilfe der API finden Sie im Entwicklerhandbuch für berechnete Attribute [](./api.md).
