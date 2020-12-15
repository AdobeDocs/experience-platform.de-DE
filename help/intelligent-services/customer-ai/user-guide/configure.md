---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Konfigurieren einer Customer AI-Instanz
topic: Instance creation
description: Intelligent Services stellen Customer AI als einfach zu verwendenden Adobe Sensei-Dienst bereit, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 35%

---


# Konfigurieren einer Customer AI-Instanz

Die Customer AI als Teil von Intelligent Services ermöglicht es Ihnen, benutzerspezifische Tendenzwerte zu generieren, ohne sich um Machine Learning kümmern zu müssen.

Intelligent Services stellen Customer AI als einfach zu verwendenden Adobe Sensei-Dienst bereit, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.

## Einrichten Ihrer Instanz {#set-up-your-instance}

In the Platform UI, select **[!UICONTROL Services]** in the left navigation. Der Browser für **[!UICONTROL Dienste]** erscheint und zeigt alle Dienste an, die Ihnen zur Verfügung stehen. In the container for Customer AI, select **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

Die Benutzeroberfläche **für Kunden-API** wird angezeigt und zeigt alle Ihre Dienstinstanzen an.

- Sie finden die Metrik **[!UICONTROL Gesamtanzahl der bewerteten]** Profil unten rechts im Container Instanz **** erstellen. Diese Metrik verfolgt die Gesamtanzahl der von der Kunden-API für das aktuelle Kalenderjahr bewerteten Profil einschließlich aller Sandbox-Umgebung und aller gelöschten Dienstinstanzen.

![](../images/user-guide/total-profiles.png)

Dienstinstanzen können mithilfe der Steuerelemente auf der rechten Seite der Benutzeroberfläche bearbeitet, geklont und gelöscht werden. Um diese Steuerelemente anzuzeigen, wählen Sie eine Instanz aus den vorhandenen **[!UICONTROL Dienstinstanzen]** aus. Die Steuerelemente enthalten Folgendes:

- **[!UICONTROL Bearbeiten]**: Durch Auswahl von **[!UICONTROL Bearbeiten]** können Sie eine vorhandene Dienstinstanz ändern. Sie können den Namen, die Beschreibung und die Bewertungsfrequenz der Instanz bearbeiten.
- **[!UICONTROL Klonen]**: Durch Auswahl von **[!UICONTROL Klonen]** wird die derzeit ausgewählte Dienstinstanzeinrichtung kopiert. Anschließend können Sie den Workflow ändern, um kleinere Änderungen vorzunehmen und ihn als neue Instanz umzubenennen.
- **[!UICONTROL Löschen]**: Sie können eine Dienstinstanz einschließlich aller historischen Ausführung löschen.
- **[!UICONTROL Datenquelle]**: Ein Link zum Datensatz, der von dieser Instanz verwendet wird.
- **[!UICONTROL Details]** der letzten Ausführung: Dies wird nur angezeigt, wenn eine Ausführung fehlschlägt. Informationen darüber, warum die Ausführung fehlgeschlagen ist, wie Fehlercodes werden hier angezeigt.
- **[!UICONTROL Score-Definition]**: Eine schnelle Übersicht über das Ziel, das Sie für diese Instanz konfiguriert haben.

![](../images/user-guide/service-instance-panel.png)

Um eine neue Instanz zu erstellen, wählen Sie &quot;Instanz **[!UICONTROL erstellen&quot;]**.

![](../images/user-guide/dashboard.png)

Der Workflow für die Instanzerstellung wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Einrichtung]**.

Im Folgenden finden Sie wichtige Informationen zu Werten, die Sie für die Instanz angeben müssen:

- Der Name der Instanz wird an allen Stellen verwendet, an denen Kunden-AI-Werte angezeigt werden. Daher sollten Namen beschreiben, was die Prognosewerte darstellen, z. B. „Wahrscheinlichkeit einer Kündigung eines Zeitschriftenabonnements“.

- Der Tendenztyp bestimmt den Zweck des Wertes und die Metrikpolarität. Sie können entweder **[!UICONTROL Abwanderung]** oder **[!UICONTROL Konversion]** wählen. Weitere Informationen darüber, wie sich der Tendenztyp auf Ihre Instanz auswirkt, finden Sie in der [Auswertungszusammenfassung](./discover-insights.md#scoring-summary) im Discover Insight-Dokument.

- Die Datenquelle befindet sich an der Stelle, an der sich die Daten befinden. Der Datensatz ist der Eingabedatensatz, mit dem Ergebnisse vorhergesagt werden. Standardmäßig nutzt Customer AI Kundenerlebnis-Ereignisdaten, um Tendenzwerte zu berechnen. Wenn Sie einen Datensatz in der Dropdown-Auswahl wählen, werden nur Datensätze aufgelistet, die mit Customer KI kompatibel sind.

- Standardmäßig werden Tendenzwerte für alle Profile generiert, es sei denn, es wurde eine qualifizierte Zielgruppe angegeben. Sie können eine qualifizierte Zielgruppe angeben, indem Sie Bedingungen festlegen, um Profile auf Grundlage von Ereignissen ein- oder auszuschließen.

Provide the required values and then select **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### Ziel definieren {#define-a-goal}

The **[!UICONTROL Define goal]** step appears and it provides an interactive environment for you to visually define a prediction goal. Ein Ziel besteht aus einem oder mehreren Ereignissen, bei denen das Auftreten eines jeden Ereignisses auf der Bedingung basiert, die es enthält. Ziel einer Customer AI-Instanz ist es, die Wahrscheinlichkeit zu bestimmen, mit der ihr Ziel innerhalb eines bestimmten Zeitraums erreicht wird.

Um ein Ziel zu erstellen, wählen Sie &quot;Feldnamen **[!UICONTROL eingeben&quot;]** und wählen Sie ein Feld aus der Dropdown-Liste aus. Wählen Sie die zweite Eingabe aus und wählen Sie eine Klausel für die Bedingung des Ereignisses. Geben Sie dann die Zielgruppe ein, um das Ereignis abzuschließen. Additional events can be configured by selecting **[!UICONTROL Add event]**. Lastly, complete the goal by applying a prediction time frame in number of days, then select **[!UICONTROL Next]**.

![](../images/user-guide/goal.png)

#### Wird ausgeführt und wird nicht ausgeführt

Beim Definieren Ihres Ziels haben Sie die Option **[!UICONTROL Wird auftreten]** oder **[!UICONTROL tritt nicht auf]**. Die Auswahl **[!UICONTROL Wird ausgeführt]** bedeutet, dass die von Ihnen festgelegten Ereignis-Bedingungen erfüllt werden müssen, damit die Ereignis-Daten eines Kunden in die Insight-Benutzeroberfläche aufgenommen werden.

Wenn Sie z. B. eine App einrichten möchten, um vorherzusagen, ob ein Kunde einen Kauf tätigt, können Sie &quot; **[!UICONTROL Vorkommen]** &quot;gefolgt von &quot; **[!UICONTROL Alle von]** &quot;auswählen und dann **commerce.purchase.id** eingeben, und als Operator **vorhanden** sein.

![wird](../images/user-guide/occur.png)

Es kann jedoch vorkommen, dass Sie sich für eine Vorhersage interessieren, ob ein Ereignis in einem bestimmten Zeitraum nicht eintritt. Um ein Ziel mit dieser Option zu konfigurieren, wählen Sie **[!UICONTROL Wird nicht auftreten]** aus der Dropdownliste auf der obersten Ebene.

Wenn Sie z. B. vorhersagen möchten, welche Kunden sich weniger engagieren und Ihre Kontoanmeldung im nächsten Monat nicht besuchen. Wählen Sie **[!UICONTROL Wird nicht auftreten]** gefolgt von **[!UICONTROL All of]** und geben Sie dann **web.webInteraction.URL** ein und **[!UICONTROL entspricht]** dem Operator mit **Kontoanmeldung** als Wert.

![wird nicht](../images/user-guide/not-occur.png)

#### Alle und beliebige

In einigen Fällen können Sie vorhersagen, ob eine Kombination von Ereignissen eintritt, und in anderen Fällen können Sie das Auftreten eines beliebigen Ereignisses aus einem vordefinierten Satz vorhersagen. Um vorherzusagen, ob ein Kunde eine Kombination von Ereignissen hat, wählen Sie die Option &quot; **[!UICONTROL Alle von]** &quot;aus der Dropdown-Liste &quot;Zweitstufe&quot;auf der Seite &quot;Ziel **[!UICONTROL definieren&quot;]** .

Sie können beispielsweise vorhersagen, ob ein Kunde ein bestimmtes Produkt kauft. Dieses Prognoseziel ist durch zwei Bedingungen definiert: a `commerce.order.purchaseID` vorhanden **und der Wert** entspricht `productListItems.SKU` **** einem bestimmten Wert.

![Alle Beispiele](../images/user-guide/all-of.png)

Um vorherzusagen, ob ein Kunde ein Ereignis aus einem bestimmten Satz hat, können Sie die Option **[!UICONTROL Beliebig]** verwenden.

Sie können beispielsweise vorhersagen, ob ein Kunde eine bestimmte URL oder eine Webseite mit einem bestimmten Namen besucht. Dieses Prognoseziel ist durch zwei Bedingungen definiert: `web.webPageDetails.URL` **beginn mit** einem bestimmten Wert und `web.webPageDetails.name` Beginn mit **** einem bestimmten Wert.

![Beispiel](../images/user-guide/any-of.png)

### Zeitplan konfigurieren *(optional)* {#configure-a-schedule}

The **[!UICONTROL Advanced]** step appears. This optional step allows you to configure a schedule to automate prediction runs, define prediction exclusions to filter certain events, or select **[!UICONTROL Finish]** if nothing is needed.

Richten Sie einen Auswertungszeitplan ein, indem Sie die **[!UICONTROL Auswertungshäufigkeit]** festlegen. Die Ausführung automatisierter Prognosen kann entweder wöchentlich oder monatlich geplant werden.

![](../images/user-guide/schedule.png)

Unter der Zeitplankonfiguration können Sie Prognoseausschlüsse definieren, um zu verhindern, dass bei der Generierung von Werten Ereignisse ausgewertet werden, die bestimmte Bedingungen erfüllen. Mit dieser Funktion können irrelevante Dateneingaben herausgefiltert werden.

To exclude certain events, select **[!UICONTROL Add exclusion]** and define the event in the same fashion as to how the goal is defined. To remove an exclusion, select the ellipses (**[!UICONTROL ...]**) to the top-right of the event container and then select **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

Exclude events as needed and then select **[!UICONTROL Finish]** to create the instance.

![](../images/user-guide/advanced.png)

Wenn die Instanz erfolgreich erstellt wurde, wird sofort eine Prognose ausgeführt; nachfolgende Ausführungen erfolgen dann gemäß Ihrem definierten Zeitplan.

>[!NOTE]
>
>Je nach Umfang der Eingabedaten kann die Ausführung von Prognosen bis zu 24 Stunden dauern.

In diesem Abschnitt haben Sie eine Instanz von Customer AI konfiguriert und eine Prognose durchgeführt. Nach erfolgreicher Ausführung sorgen Auswertungsdaten für ein automatisches Ausfüllen von Profilen mit Prognosewerten. Warten Sie bis zu 24 Stunden, bevor Sie mit dem nächsten Abschnitt dieses Tutorials fortfahren.

## Nächste Schritte {#next-steps}

In diesem Lernprogramm haben Sie erfolgreich eine Instanz der Kunden-API konfiguriert und Tendenzwerte generiert. Sie können jetzt den Segment Builder verwenden, um Kundensegmente mit prognostizierten Ergebnissen zu [erstellen](./create-segment.md) oder Einblicke in die Kundentoftware [zu erhalten](./discover-insights.md).

## Zusätzliche Ressourcen

Das folgende Video unterstützt Sie dabei, den Konfigurationsarbeitsablauf für Kunden-API zu verstehen. Darüber hinaus werden Best Practices und Verwendungsfallbeispiele bereitgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

