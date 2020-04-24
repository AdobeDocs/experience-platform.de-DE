---
source-git-commit: 1cf1e9c814601bdd4c7198463593be78452004dc
translation-type: tm+mt

---
# Kundensegmente mit prognostizierten Werten erstellen

Nach Abschluss einer Prognose werden die prognostizierten Tendenzwerte von Profilen automatisch übernommen. Die Anreicherung von Profilen mit Kundentreuewerten ermöglicht die Erstellung von Kundensegmenten, um Audiencen anhand ihrer Tendenzwerte zu finden. In diesem Abschnitt werden Schritte zum Erstellen von Segmenten mit Segment Builder beschrieben. Eine genauere Anleitung zum Erstellen von Segmenten finden Sie im [Segment Builder-Benutzerhandbuch](../../../segmentation/tutorials/create-a-segment.md).

>[!IMPORTANT] Um diese Methode verwenden zu können, muss Echtzeit-Kundendaten-Profil für den Datensatz aktiviert werden.

In the Platform UI, click **[!UICONTROL Segments]** in the left navigation, and then click **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

*Segment Builder* wird angezeigt. From the left *Fields* column and under the *Attributes* tab, click the folder named **[!UICONTROL XDM Individual Profile]** and then click the folder with the namespace of your organization. Der Ordner **[!UICONTROL Customer AI]** enthält die Ergebnisse von Prognoseausführungen und wird nach der Instanz benannt, zu der die Werte gehören. Klicken Sie auf einen Instanzordner, um auf die Ergebnisse der gewünschten Instanz zuzugreifen.

![](../images/user-guide/results.png)

Located in the center of Segment Builder, drag and drop the **[!UICONTROL Score]** attribute onto the *rule builder canvas* to define a rule.

Geben Sie in der rechten Spalte *Segmenteigenschaften* einen Namen für das Segment ein.

![](../images/user-guide/properties.png)

Klicken Sie über der Spalte &quot; *Felder* links&quot;auf das **Zahnradsymbol** und wählen Sie aus der Dropdownliste eine Richtlinie *für die* Zusammenführung aus. Klicken Sie auf **[!UICONTROL Save]** , um das Segment zu erstellen.

![](../images/user-guide/merge_policy.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe des Segmentaufbaus Audiencen anhand ihrer Tendenzwerte erfolgreich gefunden. Sie können Ihre Audiencen jetzt in Zielgruppen aktivieren, indem Sie sie an Zielorten aktivieren. See the [destinations overview](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) for more information.