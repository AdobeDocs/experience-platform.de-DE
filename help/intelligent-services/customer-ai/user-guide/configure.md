---
keywords: Experience Platform; Benutzerhandbuch; Kundenunterstützung; beliebte Themen; Instanz konfigurieren; Instanz erstellen;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Konfigurieren einer Customer AI-Instanz
topic-legacy: Instance creation
description: Intelligent Services stellen Customer AI als einfach zu verwendenden Adobe Sensei-Dienst bereit, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 26%

---

# Konfigurieren einer Customer AI-Instanz

Die Customer AI als Teil von Intelligent Services ermöglicht es Ihnen, benutzerspezifische Tendenzwerte zu generieren, ohne sich um Machine Learning kümmern zu müssen.

Intelligent Services stellen Customer AI als einfach zu verwendenden Adobe Sensei-Dienst bereit, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.

## Einrichten Ihrer Instanz {#set-up-your-instance}

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Dienste]** aus. Der Browser für **[!UICONTROL Dienste]** erscheint und zeigt alle Dienste an, die Ihnen zur Verfügung stehen. Wählen Sie im Container für Customer AI **[!UICONTROL Öffnen]** aus.

![](../images/user-guide/navigate-to-service.png)

Die Benutzeroberfläche **Customer AI** wird angezeigt und zeigt alle Ihre Dienstinstanzen an.

- Sie finden die Metrik **[!UICONTROL Gesamtzahl der bewerteten Profile]** unten rechts im Container **[!UICONTROL Instanz erstellen]** . Diese Metrik verfolgt die Gesamtzahl der Profile, die von Customer AI für das aktuelle Kalenderjahr bewertet wurden, einschließlich aller Sandbox-Umgebungen und aller gelöschten Dienstinstanzen.

![](../images/user-guide/total-profiles.png)

Dienstinstanzen können mithilfe der Steuerelemente auf der rechten Seite der Benutzeroberfläche bearbeitet, geklont und gelöscht werden. Um diese Steuerelemente anzuzeigen, wählen Sie eine Instanz aus Ihren vorhandenen **[!UICONTROL Dienstinstanzen]** aus. Die Steuerelemente enthalten Folgendes:

- **[!UICONTROL Bearbeiten]**: Durch Auswahl von  **** Bearbeiten können Sie eine vorhandene Dienstinstanz ändern. Sie können den Namen, die Beschreibung und die Scoring-Häufigkeit der Instanz bearbeiten.
- **[!UICONTROL Klonen]**: Durch Auswahl von  **** Clonecopies wird die derzeit ausgewählte Dienstinstanz-Einrichtung kopiert. Anschließend können Sie den Workflow ändern, um kleinere Änderungen vorzunehmen, und ihn in eine neue Instanz umbenennen.
- **[!UICONTROL Löschen]**: Sie können eine Dienstinstanz einschließlich aller historischen Ausführungen löschen.
- **[!UICONTROL Datenquelle]**: Ein Link zum Datensatz, der von dieser Instanz verwendet wird.
- **[!UICONTROL Letzte Ausführungsdetails]**: Dies wird nur angezeigt, wenn eine Ausführung fehlschlägt. Informationen dazu, warum die Ausführung fehlgeschlagen ist, wie z. B. Fehlercodes, werden hier angezeigt.
- **[!UICONTROL Score-Definition]**: Ein kurzer Überblick über das Ziel, das Sie für diese Instanz konfiguriert haben.

![](../images/user-guide/service-instance-panel.png)

Um eine neue Instanz zu erstellen, wählen Sie **[!UICONTROL Instanz erstellen]** aus.

![](../images/user-guide/dashboard.png)

Der Workflow für die Instanzerstellung wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Einrichtung]**.

Im Folgenden finden Sie wichtige Informationen zu Werten, die Sie für die Instanz angeben müssen:

- Der Name der Instanz wird an allen Stellen verwendet, an denen Customer AI-Bewertungen angezeigt werden. Daher sollten Namen beschreiben, was die Prognosewerte darstellen, z. B. „Wahrscheinlichkeit einer Kündigung eines Zeitschriftenabonnements“.

- Der Tendenztyp bestimmt den Zweck des Wertes und die Metrikpolarität. Sie können entweder **[!UICONTROL Abwanderung]** oder **[!UICONTROL Konversion]** wählen. Weitere Informationen darüber, wie sich der Tendenztyp auf Ihre Instanz auswirkt, finden Sie in der [Auswertungszusammenfassung](./discover-insights.md#scoring-summary) im Discover Insight-Dokument.

- Die Datenquelle befindet sich an der Stelle, an der sich die Daten befinden. Der Datensatz ist der Eingabedatensatz, mit dem Ergebnisse vorhergesagt werden. Standardmäßig verwendet Customer AI Daten aus Consumer Experience Event, Adobe Analytics und Adobe Audience Manager zur Berechnung von Tendenzwerten. Wenn Sie einen Datensatz in der Dropdown-Auswahl wählen, werden nur Datensätze aufgelistet, die mit Customer KI kompatibel sind.

- Standardmäßig werden Tendenzwerte für alle Profile generiert, es sei denn, es wurde eine qualifizierte Zielgruppe angegeben. Sie können eine qualifizierte Zielgruppe angeben, indem Sie Bedingungen festlegen, um Profile auf Grundlage von Ereignissen ein- oder auszuschließen.

Geben Sie die erforderlichen Werte ein und wählen Sie dann **[!UICONTROL Weiter]** aus.

![](../images/user-guide/setup.png)

### Ziel definieren {#define-a-goal}

Der Schritt **[!UICONTROL Ziel]** definieren wird angezeigt und bietet eine interaktive Umgebung, in der Sie ein Prognoseziel visuell definieren können. Ein Ziel besteht aus einem oder mehreren Ereignissen, bei denen das Auftreten eines jeden Ereignisses auf der Bedingung basiert, die es enthält. Ziel einer Customer AI-Instanz ist es, die Wahrscheinlichkeit zu bestimmen, mit der ihr Ziel innerhalb eines bestimmten Zeitraums erreicht wird.

Um ein Ziel zu erstellen, wählen Sie **[!UICONTROL Feldname eingeben]** und wählen Sie ein Feld aus der Dropdown-Liste aus. Wählen Sie die zweite Eingabe aus, wählen Sie eine Klausel für die Ereignisbedingung aus und geben Sie dann den Zielwert an, um das Ereignis abzuschließen. Zusätzliche Ereignisse können konfiguriert werden, indem Sie **[!UICONTROL Ereignis hinzufügen]** auswählen. Schließen Sie das Ziel ab, indem Sie einen Prognosezeitrahmen in Anzahl von Tagen anwenden, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![](../images/user-guide/goal.png)

#### Erfolgt und tritt nicht auf

Beim Definieren Ihres Ziels haben Sie die Möglichkeit, **[!UICONTROL Wird ausgeführt]** oder **[!UICONTROL Wird nicht ausgeführt]** auszuwählen. Wenn Sie **[!UICONTROL Wird ausgeführt]** auswählen, müssen die von Ihnen definierten Ereignisbedingungen erfüllt sein, damit die Ereignisdaten eines Kunden in die Insight-Benutzeroberfläche aufgenommen werden.

Wenn Sie beispielsweise eine App einrichten möchten, um vorherzusagen, ob ein Kunde einen Kauf tätigt, können Sie **[!UICONTROL Wird ausgeführt]**, gefolgt von **[!UICONTROL Alle von]** auswählen und dann **commerce.purchases.id** und **exists** als Operator eingeben.

![wird](../images/user-guide/occur.png)

Es kann jedoch vorkommen, dass Sie vorhersagen möchten, ob ein Ereignis innerhalb eines bestimmten Zeitraums nicht eintritt. Um ein Ziel mit dieser Option zu konfigurieren, wählen Sie **[!UICONTROL Wird nicht ausgeführt]** aus der Dropdown-Liste der obersten Ebene aus.

Wenn Sie beispielsweise vorhersagen möchten, welche Kunden weniger engagiert sind und Ihre Kontoanmeldeseite im nächsten Monat nicht besuchen. Wählen Sie **[!UICONTROL Wird nicht ausgeführt]** gefolgt von **[!UICONTROL Alle von]** und geben Sie **web.webInteraction.URL** und **[!UICONTROL entspricht]** als Operator mit **account-login** als Wert ein.

![wird nicht ausgeführt](../images/user-guide/not-occur.png)

#### Alle und beliebige von

In einigen Fällen können Sie vorhersagen, ob eine Kombination von Ereignissen eintritt, in anderen Fällen können Sie das Auftreten eines Ereignisses aus einem vordefinierten Satz vorhersagen. Um vorherzusagen, ob ein Kunde eine Kombination von Ereignissen haben wird, wählen Sie die Option **[!UICONTROL Alle von]** aus der Dropdown-Liste der zweiten Ebene auf der Seite **[!UICONTROL Ziel definieren]** .

Sie können beispielsweise vorhersagen, ob ein Kunde ein bestimmtes Produkt kauft. Dieses Prognoseziel wird durch zwei Bedingungen definiert: a `commerce.order.purchaseID` **exists** und the `productListItems.SKU` **equals** ein bestimmter Wert.

![Alles Beispiel](../images/user-guide/all-of.png)

Um vorherzusagen, ob ein Kunde ein Ereignis aus einem bestimmten Satz hat, können Sie die Option **[!UICONTROL Beliebig von]** verwenden.

Sie können beispielsweise vorhersagen, ob ein Kunde eine bestimmte URL oder eine Webseite mit einem bestimmten Namen besucht. Dieses Prognoseziel wird durch zwei Bedingungen definiert: `web.webPageDetails.URL` **beginnt mit** einem bestimmten Wert und `web.webPageDetails.name` **beginnt mit** einem bestimmten Wert.

![Beispiel](../images/user-guide/any-of.png)

### Benutzerdefinierte Ereignisse (*optional*) {#custom-events}

Wenn Sie zusätzlich zu den [Standardereignisfeldern](../input-output.md#standard-events) weitere Informationen haben, die von Customer AI zum Generieren von Tendenzwerten verwendet werden, wird eine Option für benutzerdefinierte Ereignisse bereitgestellt. Wenn der ausgewählte Datensatz benutzerdefinierte Ereignisse enthält, die in Ihrem Schema definiert sind, können Sie sie zu Ihrer Instanz hinzufügen.

![Ereignisfunktion](../images/user-guide/event-feature.png)

Um ein benutzerspezifisches Ereignis hinzuzufügen, wählen Sie **[!UICONTROL Benutzerdefiniertes Ereignis hinzufügen]** aus. Geben Sie anschließend einen benutzerdefinierten Ereignisnamen ein und ordnen Sie ihn dem Ereignisfeld in Ihrem Schema zu. Benutzerdefinierte Ereignisnamen werden anstelle des Feldwerts angezeigt, wenn Einflussfaktoren und andere Einblicke betrachtet werden. Das bedeutet, dass Benutzer-IDs, Reservierungs-IDs, Geräteinformationen und andere benutzerdefinierte Werte mit dem benutzerspezifischen Ereignisnamen anstelle der ID/des Ereigniswerts aufgelistet werden. Diese zusätzlichen benutzerspezifischen Ereignisse werden von Customer AI verwendet, um die Qualität Ihres Modells zu verbessern und genauere Ergebnisse zu liefern.

![Feld &quot;Benutzerspezifisches Ereignis&quot;](../images/user-guide/custom-event.png)

Wählen Sie anschließend den zu verwendenden Benutzer aus der Dropdown-Liste der verfügbaren Benutzer aus. Es werden nur Benutzer aufgelistet, die mit dem Ereignis kompatibel sind.

![Benutzerspezifischer Ereignisoperator](../images/user-guide/custom-operator.png)

Geben Sie abschließend die Feldwerte an, wenn der ausgewählte Benutzer einen Wert benötigt. In diesem Beispiel müssen wir nur sehen, ob eine Hotel- oder Restaurantreservierung vorhanden ist. Wenn wir jedoch genauer sein wollten, könnten wir den Operator gleich verwenden und einen genauen Wert in die Werteaufforderung eingeben.

![Feldwert für benutzerspezifisches Ereignis](../images/user-guide/custom-value.png)

Wählen Sie nach Abschluss **[!UICONTROL Weiter]** in der oberen rechten Ecke aus, um fortzufahren.

### Zeitplan konfigurieren *(optional)* {#configure-a-schedule}

Der Schritt **[!UICONTROL Erweitert]** wird angezeigt. Dieser optionale Schritt ermöglicht es Ihnen, einen Zeitplan zu konfigurieren, um die Ausführung von Prognosen zu automatisieren, Prognoseausschlüsse zum Filtern bestimmter Ereignisse zu definieren oder **[!UICONTROL Finish]** auszuwählen, wenn nichts erforderlich ist.

Richten Sie einen Auswertungszeitplan ein, indem Sie die **[!UICONTROL Auswertungshäufigkeit]** festlegen. Die Ausführung automatisierter Prognosen kann entweder wöchentlich oder monatlich geplant werden.

![](../images/user-guide/schedule.png)

### Prognoseausschlüsse

Wenn Ihr Datensatz Spalten enthielt, die als Testdaten hinzugefügt wurden, können Sie diese Spalte oder dieses Ereignis zu einer Ausschlussliste hinzufügen, indem Sie **Ausschluss hinzufügen** auswählen und anschließend das Feld eingeben, das Sie ausschließen möchten. Dadurch wird verhindert, dass Ereignisse, die bestimmte Bedingungen erfüllen, beim Generieren von Werten ausgewertet werden. Diese Funktion kann verwendet werden, um irrelevante Dateneingaben oder bestimmte Promotions herauszufiltern.

Um ein Ereignis auszuschließen, wählen Sie **[!UICONTROL Ausschluss hinzufügen]** aus und definieren Sie das Ereignis. Um einen Ausschluss zu entfernen, wählen Sie die Auslassungszeichen (**[!UICONTROL ...]**) oben rechts neben dem Ereigniscontainer und wählen Sie dann **[!UICONTROL Container entfernen]** aus.

![](../images/user-guide/exclusion.png)

Schließen Sie Ereignisse nach Bedarf aus und wählen Sie dann **[!UICONTROL Beenden]** aus, um die Instanz zu erstellen.

![](../images/user-guide/advanced.png)

Wenn die Instanz erfolgreich erstellt wurde, wird sofort eine Prognose ausgeführt; nachfolgende Ausführungen erfolgen dann gemäß Ihrem definierten Zeitplan.

>[!NOTE]
>
>Je nach Umfang der Eingabedaten kann die Ausführung von Prognosen bis zu 24 Stunden dauern.

In diesem Abschnitt haben Sie eine Instanz von Customer AI konfiguriert und eine Prognose durchgeführt. Nach erfolgreicher Ausführung sorgen Auswertungsdaten für ein automatisches Ausfüllen von Profilen mit Prognosewerten. Warten Sie bis zu 24 Stunden, bevor Sie mit dem nächsten Abschnitt dieses Tutorials fortfahren.

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich eine Instanz von Customer AI konfiguriert und Tendenzwerte generiert. Sie können jetzt den Segment Builder verwenden, um [Kundensegmente mit prognostizierten Werten](./create-segment.md) oder [mit Customer AI](./discover-insights.md) zu erstellen.

## Weitere Ressourcen

Das folgende Video unterstützt Sie beim Verständnis des Konfigurations-Workflows für Customer AI. Darüber hinaus werden Best Practices und Anwendungsfallbeispiele bereitgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
