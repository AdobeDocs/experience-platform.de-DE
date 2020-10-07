---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: Konfigurieren einer Customer AI-Instanz
topic: Instance creation
description: Intelligent Services stellen Customer AI als einfach zu verwendenden Adobe Sensei-Dienst bereit, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.
translation-type: tm+mt
source-git-commit: c5e2ea5daf813bf580a11f0182361197e55c6fe8
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 88%

---


# Konfigurieren einer Customer AI-Instanz

Die Customer AI als Teil von Intelligent Services ermöglicht es Ihnen, benutzerspezifische Tendenzwerte zu generieren, ohne sich um Machine Learning kümmern zu müssen.

Intelligent Services stellen Customer AI als einfach zu verwendenden Adobe Sensei-Dienst bereit, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.

## Einrichten Ihrer Instanz {#set-up-your-instance}

Klicken Sie in der Benutzeroberfläche von Platform im linken Navigationsbereich auf **[!UICONTROL Dienste]**. Der Browser für **[!UICONTROL Dienste]** erscheint und zeigt alle Dienste an, die Ihnen zur Verfügung stehen. Klicken Sie im Container für Customer AI auf **[!UICONTROL Öffnen]**.

![](../images/user-guide/navigate-to-service.png)

Im Bildschirm *Customer AI* werden alle vorhandenen Customer AI-Instanzen angezeigt. Klicken Sie auf **[!UICONTROL Instanz erstellen]**.

![](../images/user-guide/dashboard.png)

Der Workflow für die Instanzerstellung wird angezeigt, beginnend mit dem Schritt *Einrichtung*.

Im Folgenden finden Sie wichtige Informationen zu Werten, die Sie für die Instanz angeben müssen:

* Der Name der Instanz wird an allen Stellen verwendet, an denen der Customer KI-Wert angezeigt wird. Daher sollten Namen beschreiben, was die Prognosewerte darstellen, z. B. „Wahrscheinlichkeit einer Kündigung eines Zeitschriftenabonnements“.

* Der Tendenztyp bestimmt den Zweck des Wertes und die Metrikpolarität. You can either choose &quot;[!UICONTROL Churn]&quot; or &quot;[!UICONTROL Conversion]&quot;. Weitere Informationen darüber, wie sich der Tendenztyp auf Ihre Instanz auswirkt, finden Sie in der [Auswertungszusammenfassung](./discover-insights.md#scoring-summary) im Discover Insight-Dokument.

* Die Datenquelle befindet sich an der Stelle, an der sich die Daten befinden. Der Datensatz ist der Eingabedatensatz, mit dem Ergebnisse vorhergesagt werden. Standardmäßig nutzt Customer AI Kundenerlebnis-Ereignisdaten, um Tendenzwerte zu berechnen. Wenn Sie einen Datensatz in der Dropdown-Auswahl wählen, werden nur Datensätze aufgelistet, die mit Customer KI kompatibel sind.

* Standardmäßig werden Tendenzwerte für alle Profile generiert, es sei denn, es wurde eine qualifizierte Zielgruppe angegeben. Sie können eine qualifizierte Zielgruppe angeben, indem Sie Bedingungen festlegen, um Profile auf Grundlage von Ereignissen ein- oder auszuschließen.

Geben Sie die erforderlichen Werte ein und klicken Sie auf **[!UICONTROL Weiter]**.

![](../images/user-guide/setup.png)

### Ziel definieren {#define-a-goal}

Der Schritt **[!UICONTROL Ziel definieren]** wird angezeigt und bietet eine interaktive Umgebung, in der Sie ein Ziel visuell festlegen können. Ein Ziel besteht aus einem oder mehreren Ereignissen, bei denen das Auftreten eines jeden Ereignisses auf der Bedingung basiert, die es enthält. Ziel einer Customer AI-Instanz ist es, die Wahrscheinlichkeit zu bestimmen, mit der ihr Ziel innerhalb eines bestimmten Zeitraums erreicht wird.

Klicken Sie auf **[!UICONTROL Feldnamen eingeben]** und wählen Sie ein Feld aus der Dropdown-Liste aus. Klicken Sie auf die zweite Eingabe und wählen Sie eine Klausel für die Ereignisbedingung. Geben Sie dann einen Zielwert ein, um das Ereignis fertigzustellen. Weitere Ereignisse können durch Klicken auf **[!UICONTROL Ereignis hinzufügen]** konfiguriert werden. Schließen Sie das Ziel ab, indem Sie einen Prognosezeitrahmen (Zahl der Tage) anwenden, und klicken Sie dann auf **[!UICONTROL Weiter]**.

![](../images/user-guide/goal.png)

### Zeitplan konfigurieren *(optional)* {#configure-a-schedule}

The **[!UICONTROL Advanced]** step appears. In diesem optionalen Schritt können Sie einen Zeitplan konfigurieren, um die Ausführung von Prognosen zu automatisieren, Prognoseausschlüsse zum Filtern bestimmter Ereignisse definieren oder auf **[!UICONTROL Fertig stellen]** klicken, wenn nichts mehr erforderlich ist.

Richten Sie einen Auswertungszeitplan ein, indem Sie die *Auswertungshäufigkeit* festlegen. Die Ausführung automatisierter Prognosen kann entweder wöchentlich oder monatlich geplant werden.

![](../images/user-guide/schedule.png)

Unter der Zeitplankonfiguration können Sie Prognoseausschlüsse definieren, um zu verhindern, dass bei der Generierung von Werten Ereignisse ausgewertet werden, die bestimmte Bedingungen erfüllen. Mit dieser Funktion können irrelevante Dateneingaben herausgefiltert werden.

Um bestimmte Ereignisse auszuschließen, klicken Sie auf **[!UICONTROL Ausschluss hinzufügen]** und definieren Sie das Ereignis auf dieselbe Weise wie das Ziel. Um einen Ausschluss zu entfernen, klicken Sie auf die Auslassungspunkte (**[!UICONTROL ...]**) oben rechts neben dem Ereignis-Container und dann auf **[!UICONTROL Container entfernen]**.

![](../images/user-guide/exclusion.png)

Schließen Sie Ereignisse nach Bedarf aus und klicken Sie dann auf **[!UICONTROL Fertig stellen]**, um die Instanz zu erstellen.

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

