---
title: Verbinden von Google Ads mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Benutzeroberfläche Ihr Google Ads-Konto mit Adobe Experience Platform verbinden.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 10%

---

# Verbinden von [!DNL Google Ads] mit Experience Platform über die Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Google Ads]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Google Ads]-Konto mithilfe des Quellarbeitsbereichs in der Experience Platform-Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Google Ads]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [ eines Datenflusses fortfahren](../../dataflow/advertising.md)

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung finden Sie im Abschnitt [[!DNL Google Ads] Quellenübersicht](../../../../connectors/advertising/ads.md).

## Verbinden Ihres Google Ads-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich *[!UICONTROL Quellen]* zuzugreifen. Sie können die entsprechende Kategorie im Bedienfeld *[!UICONTROL Kategorien]* auswählen. Alternativ können Sie über die Suchleiste zu der spezifischen Quelle navigieren, die Sie verwenden möchten.

Um [!DNL Google Ads] zu verwenden, wählen Sie die Quellkarte **[!UICONTROL Google Ads]** unter *[!UICONTROL Advertising]* und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog in der Experience Platform-Benutzeroberfläche.](../../../../images/tutorials/create/ads/catalog.png).

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das Konto, das Sie verwenden möchten, aus der Liste der Konten in der Benutzeroberfläche aus.

Nachdem Sie Ihr Konto ausgewählt haben, klicken Sie auf **[!UICONTROL Weiter]**, um mit dem nächsten Schritt fortzufahren.

![Die Auswahlseite für vorhandene Konten im Quell-Workflow.](../../../../images/tutorials/create/ads/existing.png).

### Neues Konto

Wenn Sie noch kein -Konto haben, müssen Sie ein neues Konto erstellen, indem Sie die Authentifizierungsdaten angeben, die Ihrer Quelle entsprechen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Kontonamen und optional eine Beschreibung für Ihre Kontodetails an. Geben Sie als Nächstes die entsprechenden Authentifizierungswerte an, um Ihre Quelle für Experience Platform zu authentifizieren:

* **Client-Kunden-ID**: Die Kunden-ID ist die Kontonummer, die dem [!DNL Google Ads] Client-Konto entspricht, das Sie mit der [!DNL Google Ads]-API verwalten möchten. Diese ID folgt der Vorlage von `123-456-7890`.
* **Kunden-ID anmelden**: Die Kunden-ID für die Anmeldung ist die Kontonummer, die Ihrem [!DNL Google Ads] Manager-Konto entspricht und zum Abrufen von Berichtsdaten von einem bestimmten aktiven Kunden verwendet wird. Weitere Informationen zur Anmelde-Kunden-ID finden Sie in der [[!DNL Google Ads] API-Dokumentation](https://developers.google.com/search-ads/reporting/concepts/login-customer-id).
* **Entwickler-Token**: Mit dem Entwickler-Token können Sie auf die [!DNL Google Ads]-API zugreifen. Sie können dasselbe Entwickler-Token verwenden, um Anfragen an alle Ihre [!DNL Google Ads]-Konten zu richten. Rufen Sie Ihr Entwickler-Token ab[ indem Sie sich bei Ihrem Manager-Konto ](https://ads.google.com/home/tools/manager-accounts/) und dann zur Seite „API-Center“ navigieren.
* **Aktualisierungstoken**: Das Aktualisierungstoken ist Teil [!DNL OAuth2] Authentifizierung. Mit diesem Token können Sie Ihre Zugriffs-Token nach ihrem Ablauf neu generieren.
* **Client-ID**: Die Client-ID wird zusammen mit dem Client-Geheimnis im Rahmen [!DNL OAuth2] Authentifizierung verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre zu [!DNL Google] Anwendung identifizieren.
* **Client-Geheimnis**: Das Client-Geheimnis wird zusammen mit der Client-ID als Teil [!DNL OAuth2] Authentifizierung verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre zu [!DNL Google] Anwendung identifizieren.
* **[!DNL Google Ads]API-Version**: Die aktuelle API-Version, die von [!DNL Google Ads] unterstützt wird. Die neueste Version ist zwar `v18`, die neueste unterstützte Version für Experience Platform ist jedoch `v17`.

Nachdem Sie Ihre Anmeldedaten eingegeben haben, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie einige Augenblicke, bis die Verbindung verarbeitet wird. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Die neue Kontoschnittstelle im Quell-Workflow.](../../../../images/tutorials/create/ads/new.png).

## Daten auswählen {#select-data}

Bei [!DNL Google Ads] müssen Sie die Liste der Attribute bereitstellen, die während der Datenauswahlphase des Workflows aufgenommen werden sollen. Um diese Attribute abzurufen, müssen Sie die [[!DNL Google Ads Query Builder]](https://developers.google.com/google-ads/api/fields/v17/overview_query_builder) verwenden.

Navigieren Sie in der [!DNL Google Ads Query Builder] zu dem Ressourcentyp, den Sie verwenden möchten, und wählen Sie dann über die Attributauswahl Ihre Attribute, Segmente und Metriken aus.

![Die Attributauswahl im Query Builder von Google Ads.](../../../../images/tutorials/create/ads/attributes.png)

Mit den von Ihnen ausgewählten Attributen wird das [!DNL Google Ads Query Language] ausgefüllt. Stellen Sie sicher, dass Sie den [!DNL Standard] verwenden und dann **[!DNL Enter or edit a query]** auswählen.

![Die ausgewählten Attribute, in einer Abfrage gruppiert.](../../../../images/tutorials/create/ads/enter-query.png)

Wählen Sie als Nächstes **[!DNL Validate Query]** aus, um Ihre [!DNL Google Ads] zu validieren.

![Der Google Ads Query Builder-Validator.](../../../../images/tutorials/create/ads/validate-query.png)

Bei Erfolg gibt die [!DNL Google Ads Query Builder] eine Meldung zurück, die angibt, dass Ihre Abfrage gültig ist. Kopieren Sie als Nächstes **nur die Attribute** aus der Abfrage.

![Eine erfolgreich validierte Abfrage.](../../../../images/tutorials/create/ads/copy-query.png)

Navigieren Sie zurück zur Datenauswahlphase des Quell-Workflows in der Experience Platform-Benutzeroberfläche und fügen Sie die Attribute *[!UICONTROL Bedienfeld &quot;]*&quot; ein.

Wählen Sie **[!UICONTROL Vorschau]** aus, um eine Vorschau der Daten anzuzeigen, und wählen Sie dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![Das Bedienfeld „Listenattribute“ im Quell-Workflow.](../../../../images/tutorials/create/ads/list-attributes.png)

## Erstellen eines Datenflusses zum Aufnehmen von Werbedaten

In diesem Tutorial haben Sie eine Verbindung zu Ihrem Google Ads-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Werbedaten in Experience Platform zu importieren](../../dataflow/advertising.md).
