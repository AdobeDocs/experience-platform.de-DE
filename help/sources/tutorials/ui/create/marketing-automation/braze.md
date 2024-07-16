---
title: Erstellen eines Datenflusses für Braze-Daten in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche einen Datenfluss für Ihr Braze-Konto erstellen.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 6e94414a-176c-4810-80ff-02cf9e797756
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 24%

---

# Erstellen eines Quell-Connectors für [!DNL Braze Currents] in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Braze Currents]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../../../home.md#terms-and-conditions) .

[!DNL Braze] ermöglicht kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit. [!DNL Braze Currents] ist ein Echtzeit-Datenstrom von Interaktionsereignissen aus der Braze-Plattform, der den robusten, aber granularsten Export aus der [!DNL Braze]-Plattform darstellt.

Lesen Sie das folgende Tutorial , um zu erfahren, wie Sie Interaktionsereignisdaten aus Ihrem [!DNL Braze] -Konto in der Benutzeroberfläche an Adobe Experience Platform übertragen können.

## Voraussetzungen

Um die Schritte in diesem Handbuch abzuschließen, benötigen Sie:

* Anmeldung bei [Adobe Experience Platform](https://platform.adobe.com) und Berechtigung zum Erstellen einer neuen Streaming-Quellverbindung.
* Anmeldung bei Ihrem [[!DNL Braze] Dashboard](https://dashboard.braze.com/sign_in), eine nicht verwendete [Lizenz für den aktuellen Connector](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) und Berechtigungen zum Erstellen eines Connectors. Weitere Informationen finden Sie in den [Anforderungen zum Einrichten von  [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements) .

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Für dieses Tutorial ist auch ein grundlegendes Verständnis von [[!DNL Braze] Aktuellen ](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) erforderlich.

Wenn Sie bereits über eine [!DNL Braze] -Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [ fortfahren.](../../dataflow/marketing-automation.md)

## [!DNL Braze]-Konto mit Experience Platform verbinden

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Marketing-Automatisierung* die Option **[!UICONTROL Aktuelles einblenden]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Der Quellenkatalog auf der Experience Platform-Benutzeroberfläche mit ausgewählter Quelle Aktuelles reduzieren](../../../../images/tutorials/create/braze/catalog.png).

Laden Sie als Nächstes die bereitgestellte Beispieldatei [Aktuelle Elemente reduzieren](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json) hoch. Diese Datei enthält alle möglichen Felder, die Braze im Rahmen eines Ereignisses senden kann.

![ Der Bildschirm &quot;Daten hinzufügen&quot;.](../../../../images/tutorials/create/braze/select-data.png)

Nach dem Hochladen Ihrer Datei müssen Sie Ihre Datenflussdetails angeben, einschließlich Informationen zu Ihrem Datensatz und dem Schema, dem Sie zuordnen.
![Der Bildschirm &quot;Datenflussdetails&quot;mit der Meldung &quot;Datensatzdetails&quot;](../../../../images/tutorials/create/braze/dataflow-detail.png).

Konfigurieren Sie dann die Zuordnung für Ihre Daten über die Zuordnungsschnittstelle.

![ Der Bildschirm &quot;Zuordnung&quot;.](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>Zeitstempel mit Braze werden nicht in Millisekunden, sondern in Sekunden ausgedrückt. Damit die Zeitstempel in Experience Platform korrekt dargestellt werden können, müssen berechnete Felder in Millisekunden erstellt werden. Eine Berechnung von &quot;Zeit * 1000&quot;wird ordnungsgemäß in Millisekunden konvertiert, die für die Zuordnung zu einem Zeitstempelfeld innerhalb von Experience Platform geeignet sind.
>
>![Erstellen eines berechneten Felds für den Zeitstempel ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### Sammeln erforderlicher Anmeldeinformationen

Nachdem die Verbindung erstellt wurde, müssen Sie die folgenden Anmeldewerte erfassen, die Sie dann im Dashboard &quot;Braze&quot;bereitstellen, um Daten an Experience Platform zu senden. Weitere Informationen finden Sie in der Anleitung [!DNL Braze] [für die Navigation zu den aktuellen Elementen](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Feld | Beschreibung |
| --- | --- |
| Client-ID | Die Client-ID, die Ihrer Experience Platform-Quelle zugeordnet ist. |
| Client-Geheimnis | Das Client-Geheimnis, das mit Ihrer Experience Platform-Quelle verknüpft ist. |
| Mandanten-ID | Die Mandantenkennung, die Ihrer Experience Platform-Quelle zugeordnet ist. |
| Sandbox-Name | Die mit Ihrer Experience Platform-Quelle verknüpfte Sandbox. |
| Datenfluss-ID | Die mit Ihrer Experience Platform-Quelle verknüpfte Datenfluss-ID. |
| Streaming-Endpunkt | Der Streaming-Endpunkt, der Ihrer Experience Platform-Quelle zugeordnet ist. **Hinweis**: [!DNL Braze] konvertiert dies automatisch in den Batch-Streaming-Endpunkt. |

### Konfigurieren von [!DNL Braze Currents] zum Streamen von Daten an Ihre Datenquelle

Navigieren Sie im Bereich &quot;[!DNL Braze Dashboard]&quot;zu &quot;Partnerintegrationen&quot;**-> &quot;2} Datenexport&quot;und wählen Sie dann &quot;**[!DNL Create New Current]**&quot;.** Sie werden aufgefordert, einen Namen für den Connector, Kontaktinformationen für Benachrichtigungen über den Connector und die oben aufgeführten Anmeldeinformationen anzugeben. Wählen Sie die Ereignisse aus, die Sie empfangen möchten, konfigurieren Sie optional alle gewünschten Feldausschlüsse/-transformationen und wählen Sie dann **[!DNL Launch Current]** aus.

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Braze]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss [konfigurieren, um Systemdaten aus der Marketing-Automatisierung in  [!DNL Platform]](../../dataflow/marketing-automation.md) zu integrieren.
