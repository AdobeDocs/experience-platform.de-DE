---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: Konfigurieren einer Customer AI-Instanz
topic: Instance creation
translation-type: tm+mt
source-git-commit: ec0de4c8775367be9e6016529471254ad9f8f453

---


# Konfigurieren einer Customer AI-Instanz

Die Kundentechnik als Teil von Intelligent Services ermöglicht es Ihnen, benutzerspezifische Tendenzwerte zu generieren, ohne sich um maschinelles Lernen kümmern zu müssen.

Intelligent Services bieten Kunden-AI als einfach zu verwendenden Adobe Sensei-Dienst, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.

## Instanz einrichten {#set-up-your-instance}

In the Platform UI, click **[!UICONTROL Services]** in the left navigation. The **[!UICONTROL Services]** browser appears and displays all available services at your disposal. In the container for Customer AI, click **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

Im Bildschirm *Customer AI* werden alle vorhandenen Customer AI-Instanzen angezeigt. Klicken Sie auf **[!UICONTROL Create instance]**.

![](../images/user-guide/dashboard.png)

Der Workflow für die Instanzerstellung wird angezeigt, beginnend mit dem Schritt *Einrichtung*.

Im Folgenden finden Sie wichtige Informationen zu Werten, die Sie der Instanz bereitstellen müssen:

* Der Name der Instanz wird an allen Stellen verwendet, an denen die Kunden-AI-Bewertung angezeigt wird. Daher sollte man in Namen beschreiben, was die Prognosewerte darstellen, z. B. &quot;Wahrscheinlichkeit, das Abonnement eines Magazins abzubrechen&quot;.

* Der Tendenztyp bestimmt den Zweck des Wertes und die Metrikpolarität. Sie können entweder wählen **[!UICONTROL Churn]** oder **[!UICONTROL Conversion]**. Weitere Informationen darüber, wie sich der Tendenztyp auf Ihre Instanz auswirkt, finden Sie in der [Bewertungszusammenfassung](./discover-insights.md#scoring-summary) im Discover Insight-Dokument.

* Die Datenquelle befindet sich an der Stelle, an der sich die Daten befinden. Der Datensatz ist der Eingabedatensatz, mit dem Ergebnisse vorhergesagt werden. Standardmäßig nutzt Customer AI Kundenerlebnis-Ereignisdaten, um Tendenzwerte zu berechnen. Wenn Sie einen Datensatz aus der Dropdown-Auswahl auswählen, werden nur die Datensätze aufgelistet, die mit der Kunden-API kompatibel sind.

* Standardmäßig werden Tendenzwerte für alle Profile generiert, es sei denn, es wurde eine qualifizierte Zielgruppe angegeben. Sie können eine qualifizierte Zielgruppe angeben, indem Sie Bedingungen festlegen, um Profile auf Grundlage von Ereignissen ein- oder auszuschließen.

Provide the required values and then click **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### Ziel definieren {#define-a-goal}

Der Schritt *Ziel definieren* wird angezeigt und bietet eine interaktive Umgebung, in der Sie ein Ziel visuell festlegen können. Ein Ziel besteht aus einem oder mehreren Ereignissen, bei denen das Auftreten eines jeden Ereignisses auf der Bedingung basiert, die es enthält. Ziel einer Customer AI-Instanz ist es, die Wahrscheinlichkeit zu bestimmen, mit der ihr Ziel innerhalb eines bestimmten Zeitraums erreicht wird.

Klicken Sie auf **[!UICONTROL Enter Field Name]** und wählen Sie ein Feld aus der Dropdown-Liste aus. Klicken Sie auf die zweite Eingabe und wählen Sie eine Klausel für die Ereignisbedingung. Geben Sie dann einen Zielwert ein, um das Ereignis fertigzustellen. Additional events can be configured by clicking **[!UICONTROL Add event]**. Lastly, complete the goal by applying a prediction time frame in number of days, then click **[!UICONTROL Next]**.

![](../images/user-guide/goal.png)

### Zeitplan konfigurieren *(optional)* {#configure-a-schedule}

Der Schritt *Erweitert* wird angezeigt. This optional step allows you to configure a schedule to automate prediction runs, define prediction exclusions to filter certain events, or click **[!UICONTROL Finish]** if nothing is needed.

Richten Sie einen Bewertungszeitplan ein, indem Sie die *Bewertungshäufigkeit* festlegen. Die Ausführung automatisierter Prognosen kann entweder wöchentlich oder monatlich geplant werden.

![](../images/user-guide/schedule.png)

Unter der Zeitplankonfiguration können Sie Prognoseausschlüsse definieren, um zu verhindern, dass bei der Generierung von Werten Ereignisse ausgewertet werden, die bestimmte Bedingungen erfüllen. Mit dieser Funktion können irrelevante Dateneingaben herausgefiltert werden.

To exclude certain events, click **[!UICONTROL Add exclusion]** and define the event in the same fashion as to how the goal is defined. To remove an exclusion, click the ellipses (**[!UICONTROL ...]**) to the top-right of the event container and then click **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

Exclude events as needed and then click **[!UICONTROL Finish]** to create the instance.

![](../images/user-guide/advanced.png)

Wenn die Instanz erfolgreich erstellt wurde, wird sofort eine Prognoseausführung ausgelöst und die nachfolgenden Ausläufe werden gemäß Ihrem definierten Zeitplan ausgeführt.

>[!NOTE] Je nach Größe der Eingabedaten kann die Ausführung von Prognosen bis zu 24 Stunden dauern.

In diesem Abschnitt haben Sie eine Instanz von Customer AI konfiguriert und eine Prognose durchgeführt. Nach erfolgreichem Abschluss des Vorgangs werden die Profil automatisch mit Ergebniswerten gefüllt. Bitte warten Sie bis zu 24 Stunden, bevor Sie mit dem nächsten Abschnitt dieses Tutorials fortfahren.

## Nächste Schritte {#next-steps}

In diesem Lernprogramm haben Sie erfolgreich eine Instanz der Kunden-API konfiguriert und Tendenzwerte generiert. Sie können jetzt den Segment Builder verwenden, um Kundensegmente mit prognostizierten Ergebnissen zu [erstellen](./create-segment.md) oder Einblicke in die Kundentoftware [zu erhalten](./discover-insights.md).

## Zusätzliche Ressourcen

Das folgende Video unterstützt Sie dabei, den Konfigurationsarbeitsablauf für Kunden-API zu verstehen. Darüber hinaus werden Best Practices und Verwendungsfallbeispiele bereitgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

