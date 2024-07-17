---
title: Erstellen eines Datenflusses für Braze-Daten in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche einen Datenfluss für Ihr Braze-Konto erstellen.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 6e94414a-176c-4810-80ff-02cf9e797756
source-git-commit: 59600165328181e41750b9b2a1f4fbf162dd1df5
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 17%

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

## Erstellen eines XDM-Schemas

>[!TIP]
>
>Sie müssen ein Experience-Datenmodell (XDM)-Schema erstellen, wenn Sie zum ersten Mal eine [!DNL Braze Currents] -Verbindung erstellen. Wenn Sie bereits ein Schema für [!DNL Braze Currents] erstellt haben, können Sie diesen Schritt überspringen und mit [Verbinden Ihres Kontos mit Experience Platform](#connect) fortfahren.

Verwenden Sie in der Platform-Benutzeroberfläche den linken Navigationsbereich und wählen Sie dann **[!UICONTROL Schemas]** aus, um auf den Arbeitsbereich [!UICONTROL Schemas] zuzugreifen. Wählen Sie als Nächstes **[!UICONTROL Schema erstellen]** und dann **[!UICONTROL Erlebnisereignis]**. Um fortzufahren, wählen Sie **[!UICONTROL Weiter]** aus.

![Ein abgeschlossenes Schema.](../../../../images/tutorials/create/braze/schema.png)

Geben Sie einen Namen und eine Beschreibung für Ihr Schema an. Konfigurieren Sie dann Ihre Schemaattribute im Bedienfeld [!UICONTROL Komposition] . Wählen Sie unter [!UICONTROL Feldergruppen] die Option **[!UICONTROL Hinzufügen]** aus und fügen Sie die Feldergruppe [!UICONTROL Aktuelles Benutzerereignis einblenden] hinzu. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

Weitere Informationen zu Schemas finden Sie in der Anleitung zum [Erstellen von Schemas in der Benutzeroberfläche](../../../../../xdm/tutorials/create-schema-ui.md).

## [!DNL Braze]-Konto mit Experience Platform verbinden {#connect}

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Marketing-Automatisierung* die Option **[!UICONTROL Aktuelles einblenden]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Der Quellenkatalog auf der Experience Platform-Benutzeroberfläche mit ausgewählter Quelle Aktuelles reduzieren](../../../../images/tutorials/create/braze/catalog.png).

Laden Sie als Nächstes die bereitgestellte Beispieldatei [Aktuelle Elemente reduzieren](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json) hoch. Diese Datei enthält alle möglichen Felder, die Braze im Rahmen eines Ereignisses senden kann.

![ Der Bildschirm &quot;Daten hinzufügen&quot;.](../../../../images/tutorials/create/braze/select-data.png)

Nach dem Hochladen Ihrer Datei müssen Sie Ihre Datenflussdetails angeben, einschließlich Informationen zu Ihrem Datensatz und dem Schema, dem Sie zuordnen.  Wenn Sie zum ersten Mal eine Quelle von &quot;Braze Currents&quot;verbinden, erstellen Sie einen neuen Datensatz.  Andernfalls können Sie jeden vorhandenen Datensatz verwenden, der auf das Schema &quot;Reduzieren&quot;verweist.  Verwenden Sie beim Erstellen eines neuen Datensatzes das Schema, das wir im vorherigen Abschnitt erstellt haben.
![Der Bildschirm &quot;Datenflussdetails&quot;mit der Meldung &quot;Datensatzdetails&quot;](../../../../images/tutorials/create/braze/dataflow-detail.png).

Konfigurieren Sie dann die Zuordnung für Ihre Daten über die Zuordnungsschnittstelle.

![ Der Bildschirm &quot;Zuordnung&quot;.](../../../../images/tutorials/create/braze/mapping_errors.png)

Die Zuordnung weist die folgenden Probleme auf, die behoben werden müssen.

In den Quelldaten wird *id* fälschlicherweise *_braze.appID* zugeordnet. Sie müssen das Zielzuordnungsfeld auf der Stammebene des Schemas in *_id* ändern. Stellen Sie als Nächstes sicher, dass *properties.is_amp* *_braze.messaging.email.isAMP* zugeordnet ist.

Löschen Sie anschließend die Zuordnung *Zeit* zu *Zeitstempel* , wählen Sie das Symbol zum Hinzufügen (`+`) und dann **[!UICONTROL Berechnetes Feld hinzufügen]** aus. Geben Sie in das bereitgestellte Feld *Zeit \* 1000* ein und wählen Sie **[!UICONTROL Speichern]** aus.

Nachdem das neue berechnete Feld hinzugefügt wurde, wählen Sie &quot;**[!UICONTROL Zielfeld zuordnen]**&quot;neben dem neuen Quellfeld und ordnen Sie es auf der Stammebene des Schemas *Zeitstempel* zu. Wählen Sie dann **[!UICONTROL Validieren]** aus, um sicherzustellen, dass keine Fehler mehr auftreten.

>[!IMPORTANT]
>
>Zeitstempel mit Braze werden nicht in Millisekunden, sondern in Sekunden ausgedrückt. Damit die Zeitstempel in Experience Platform korrekt dargestellt werden können, müssen berechnete Felder in Millisekunden erstellt werden. Eine Berechnung von &quot;Zeit * 1000&quot;wird ordnungsgemäß in Millisekunden konvertiert, die für die Zuordnung zu einem Zeitstempelfeld innerhalb von Experience Platform geeignet sind.
>
>![Erstellen eines berechneten Felds für den Zeitstempel ](../../../../images/tutorials/create/braze/create-calculated-field.png)

![Die Zuordnung ohne Fehler.](../../../../images/tutorials/create/braze/completed_mapping.png)

Wählen Sie nach Abschluss **[!UICONTROL Weiter]** aus. Verwenden Sie die Überprüfungsseite, um die Details Ihres Datenflusses zu bestätigen, und wählen Sie dann **[!UICONTROL Beenden]** aus.

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
