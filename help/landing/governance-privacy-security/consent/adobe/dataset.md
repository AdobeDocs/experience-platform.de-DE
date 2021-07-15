---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Konfigurieren eines Datensatzes zur Erfassung von Einwilligungs- und Präferenzdaten
topic-legacy: getting started
description: Erfahren Sie, wie Sie ein Experience-Datenmodell (XDM)-Schema und einen -Datensatz konfigurieren, um Einwilligungs- und Präferenzdaten in Adobe Experience Platform zu erfassen.
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: ff793c207a181ca6d2486e7fd6ef5c4f57744fba
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 4%

---

# Konfigurieren eines Datensatzes zur Erfassung von Einwilligungs- und Präferenzdaten

Damit Adobe Experience Platform Ihre Zustimmungs-/Präferenzdaten von Kunden verarbeiten kann, müssen diese Daten an einen Datensatz gesendet werden, dessen Schema Felder enthält, die mit Zustimmung und anderen Berechtigungen zusammenhängen. Insbesondere muss dieser Datensatz auf der [!DNL XDM Individual Profile]-Klasse basieren und für die Verwendung in [!DNL Real-time Customer Profile] aktiviert sein.

In diesem Dokument werden Schritte zum Konfigurieren eines Datensatzes zur Verarbeitung von Einwilligungsdaten in Experience Platform beschrieben. Einen Überblick über den gesamten Workflow zur Verarbeitung von Zustimmungs-/Voreinstellungsdaten in Platform finden Sie in der [Übersicht zur Zustimmungsverarbeitung](./overview.md).

>[!IMPORTANT]
>
>Die Beispiele in diesem Handbuch verwenden einen standardisierten Satz von Feldern zur Darstellung von Kundenzustimmungswerten, wie durch die Schemafeldgruppe [[!UICONTROL Einverständnisse und Voreinstellungen] definiert. ](../../../../xdm/field-groups/profile/consents.md) Die Struktur dieser Felder soll ein effizientes Datenmodell für viele gängige Nutzungsszenarien bei der Einwilligungserfassung bieten.
>
>Sie können jedoch auch Ihre eigenen Feldergruppen definieren, um die Zustimmung gemäß Ihren eigenen Datenmodellen darzustellen. Wenden Sie sich an Ihr Rechtsteam, um die Genehmigung für ein Datenmodell zur Einwilligung zu erhalten, das Ihren geschäftlichen Anforderungen entspricht. Mögliche Optionen sind:
>
>* Die standardisierte Einwilligungsfeldgruppe
>* Eine benutzerdefinierte Einwilligungsfeldgruppe, die von Ihrer Organisation erstellt wurde
>* Eine Kombination aus der standardisierten Einwilligungsfeldgruppe und zusätzlichen Feldern, die von einer benutzerdefinierten Einwilligungsfeldgruppe bereitgestellt werden


## Voraussetzungen

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)](../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemas.
* [Echtzeit-Kundenprofil](../../../../profile/home.md): Fasst Kundendaten aus unterschiedlichen Quellen in einer vollständigen, einheitlichen Ansicht zusammen und bietet gleichzeitig eine verwertbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion.

>[!IMPORTANT]
>
>In diesem Tutorial wird davon ausgegangen, dass Sie das [!DNL Profile]-Schema in Platform kennen, das Sie zum Erfassen von Kundenattributinformationen verwenden möchten. Unabhängig von der Methode, mit der Sie Einwilligungsdaten erfassen, muss dieses Schema für das Echtzeit-Kundenprofil ](../../../../xdm/ui/resources/schemas.md#profile)aktiviert sein. [ Darüber hinaus darf die primäre Identität des Schemas nicht ein direkt identifizierbares Feld sein, das in interessensbasierter Werbung, wie z. B. einer E-Mail-Adresse, nicht verwendet werden darf. Wenden Sie sich an Ihren Rechtsbeistand, wenn Sie sich nicht sicher sind, welche Felder eingeschränkt sind.

## [!UICONTROL Struktur von Einverständnis- und ] Voreinstellungsfeldgruppen {#structure}

Die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] stellt standardisierte Einwilligungsfelder für ein Schema bereit. Derzeit ist diese Feldergruppe nur mit Schemas kompatibel, die auf der [!DNL XDM Individual Profile]-Klasse basieren.

Die Feldergruppe stellt ein einzelnes Objekt-Feld bereit, `consents`, dessen Untereigenschaften eine Reihe standardisierter Zustimmungsfelder erfassen. Die folgende JSON-Datei ist ein Beispiel für die Art von Daten, die `consents` bei der Datenerfassung erwartet:

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Weitere Informationen zur Struktur und Bedeutung der Untereigenschaften in `consents` finden Sie in der Übersicht zur Feldergruppe [[!UICONTROL Einverständnisse und Voreinstellungen]](../../../../xdm/field-groups/profile/consents.md).

## Fügen Sie die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] zu Ihrem [!DNL Profile]-Schema hinzu. {#add-field-group}

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Schemas]** und dann den Tab **[!UICONTROL Durchsuchen]** aus, um eine Liste der vorhandenen Schemas anzuzeigen. Wählen Sie hier den Namen des [!DNL Profile]-aktivierten Schemas aus, dem Sie Einwilligungsfelder hinzufügen möchten. Die Screenshots in diesem Abschnitt verwenden als Beispiel das Schema &quot;Loyalty Members&quot;, das im Tutorial [zur Schemaerstellung](../../../../xdm/tutorials/create-schema-ui.md) erstellt wurde.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>Sie können die Such- und Filterfunktionen des Arbeitsbereichs verwenden, um Ihr Schema leichter zu finden. Weitere Informationen finden Sie im Handbuch [Erkunden von XDM-Ressourcen](../../../../xdm/ui/explore.md) .

Der [!DNL Schema Editor] wird angezeigt, der die Struktur des Schemas auf der Arbeitsfläche anzeigt. Wählen Sie auf der linken Seite der Arbeitsfläche **[!UICONTROL Hinzufügen]** unter dem Abschnitt **[!UICONTROL Feldergruppen]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

Das Dialogfeld **[!UICONTROL Feldergruppe hinzufügen]** wird angezeigt. Wählen Sie von hier aus **[!UICONTROL Einverständnisse und Voreinstellungen]** aus der Liste aus. Sie können optional die Suchleiste verwenden, um Ergebnisse einzugrenzen und die Feldergruppe leichter zu finden. Nachdem die Feldergruppe ausgewählt wurde, wählen Sie **[!UICONTROL Feldergruppen hinzufügen]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

Die Arbeitsfläche wird wieder angezeigt und zeigt an, dass das `consents`-Objekt zur Schemastruktur hinzugefügt wurde. Wenn Sie zusätzliche Einverständnisfelder und Voreinstellungsfelder benötigen, die nicht von der Standardfeldgruppe erfasst werden, lesen Sie den Anhang unter [Hinzufügen benutzerdefinierter Einwilligungs- und Präferenzfelder zum Schema](#custom-consent). Klicken Sie andernfalls auf **[!UICONTROL Speichern]** , um die Änderungen am Schema abzuschließen.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

Wenn das bearbeitete Schema von dem [!UICONTROL Profildatensatz] verwendet wird, der in Ihrer Platform Web SDK-Edge-Konfiguration angegeben ist, enthält dieser Datensatz jetzt die neuen Einwilligungsfelder. Sie können jetzt zum [Handbuch zur Verarbeitung von Einwilligungen](./overview.md#merge-policies) zurückkehren, um die Konfiguration der Experience Platform zur Verarbeitung von Einwilligungsdaten fortzusetzen.

Wenn Sie keinen Datensatz für dieses Schema erstellt haben, führen Sie die Schritte im nächsten Abschnitt aus.

## Datensatz basierend auf Ihrem Einverständnisschema erstellen {#dataset}

Nachdem Sie ein Schema mit Einverständnisfeldern erstellt haben, müssen Sie einen Datensatz erstellen, in dem letztendlich die Einwilligungsdaten Ihrer Kunden erfasst werden. Dieser Datensatz muss für [!DNL Real-time Customer Profile] aktiviert sein.

Wählen Sie zunächst **[!UICONTROL Datensätze]** im linken Navigationsbereich und dann **[!UICONTROL Datensatz erstellen]** in der oberen rechten Ecke aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

Wählen Sie auf der nächsten Seite **[!UICONTROL Datensatz aus Schema]** erstellen.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

Der Workflow **[!UICONTROL Datensatz aus Schema]** erstellen wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Schema]** auswählen . Suchen Sie in der bereitgestellten Liste eines der zuvor erstellten Einwilligungsschemas. Sie können optional die Suchleiste verwenden, um Ergebnisse einzuschränken und Ihr Schema leichter zu finden. Wählen Sie das Optionsfeld neben dem gewünschten Schema aus und wählen Sie dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

Der Schritt **[!UICONTROL Datensatz konfigurieren]** wird angezeigt. Geben Sie einen eindeutigen, leicht identifizierbaren Namen und eine Beschreibung für den Datensatz ein, bevor Sie **[!UICONTROL Finish]** auswählen.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

Die Detailseite für den neu erstellten Datensatz wird angezeigt. Wenn der Datensatz auf Ihrem Zeitreihenschema basiert, ist der Prozess abgeschlossen. Wenn der Datensatz auf Ihrem Datensatzschema basiert, besteht der letzte Schritt im Prozess darin, den Datensatz zur Verwendung in [!DNL Real-time Customer Profile] zu aktivieren.

Wählen Sie in der rechten Leiste den Umschalter **[!UICONTROL Profil]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Wählen Sie abschließend **[!UICONTROL Aktivieren]** im Bestätigungs-Popup aus, um das Schema für [!DNL Profile] zu aktivieren.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

Der Datensatz wird jetzt gespeichert und für die Verwendung in [!DNL Profile] aktiviert. Wenn Sie planen, das Platform Web SDK zum Senden von Zustimmungsdaten an Profile zu verwenden, müssen Sie diesen Datensatz als [!UICONTROL Profildatensatz] auswählen, wenn Sie Ihre [Edge-Konfiguration](../../../../edge/fundamentals/datastreams.md) einrichten.

## Nächste Schritte

In diesem Tutorial haben Sie Einwilligungsfelder zu einem [!DNL Profile]-aktivierten Schema hinzugefügt, dessen Datensatz verwendet wird, um Einwilligungsdaten mithilfe des Platform Web SDK oder der direkten XDM-Erfassung zu erfassen.

Sie können jetzt zur [Übersicht über die Zustimmungsverarbeitung](./overview.md#merge-policies) zurückkehren, um mit der Konfiguration der Experience Platform zur Verarbeitung von Zustimmungsdaten fortzufahren.

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Erstellen eines Datensatzes zur Erfassung von Einwilligungs- und Präferenzdaten von Kunden.

### Hinzufügen benutzerdefinierter Einverständnisfelder und Präferenzfelder zum Schema {#custom-consent}

Wenn Sie zusätzliche Zustimmungssignale außerhalb der von der standardmäßigen Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] repräsentierten Signale erfassen müssen, können Sie benutzerdefinierte XDM-Komponenten verwenden, um Ihr Einwilligungsschema entsprechend Ihren jeweiligen Geschäftsanforderungen zu erweitern. In diesem Abschnitt werden die grundlegenden Prinzipien erläutert, wie Sie Ihr Einverständnisschema anpassen können, um diese Signale in das Profil aufzunehmen.

>[!IMPORTANT]
>
>Die Platform Web- und Mobile-SDKs unterstützen keine benutzerdefinierten Felder in ihren Befehlen zur Änderung der Zustimmung. Derzeit ist die einzige Möglichkeit, benutzerdefinierte Einwilligungsfelder in Profile zu erfassen, über [Batch-Erfassung](../../../../ingestion/batch-ingestion/overview.md) oder eine [Quellverbindung](../../../../sources/home.md).

Es wird dringend empfohlen, die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] als Grundlage für die Struktur Ihrer Einwilligungsdaten zu verwenden und nach Bedarf zusätzliche Felder hinzuzufügen, anstatt zu versuchen, die gesamte Struktur von Grund auf neu zu erstellen.

Um der Struktur einer Standardfeldgruppe benutzerdefinierte Felder hinzuzufügen, müssen Sie zunächst eine benutzerdefinierte Feldergruppe erstellen. Nachdem Sie die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] zum Schema hinzugefügt haben, wählen Sie das Symbol **plus (+)** im Abschnitt **[!UICONTROL Feldergruppen]** aus und klicken Sie dann auf **[!UICONTROL Neue Feldergruppe]** erstellen. Geben Sie einen Namen und eine optionale Beschreibung für die Feldergruppe ein und wählen Sie dann **[!UICONTROL Feldergruppe hinzufügen]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

Das [!DNL Schema Editor] wird wieder angezeigt, wobei die neue benutzerdefinierte Feldergruppe in der linken Leiste ausgewählt ist. Auf der Arbeitsfläche werden Steuerelemente angezeigt, mit denen Sie benutzerdefinierte Felder zur Schemastruktur hinzufügen können. Um ein neues Einverständnis- oder Präferenzfeld hinzuzufügen, wählen Sie das Symbol **plus (+)** neben dem Objekt `consents` aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

Innerhalb des Objekts `consents` wird ein neues Feld angezeigt. Da Sie ein benutzerdefiniertes Feld zu einem Standard-XDM-Objekt hinzufügen, wird das neue Feld unter einem Objekt erstellt, das mit Ihrer Mandanten-ID benannt ist.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

Geben Sie in der rechten Leiste unter **[!UICONTROL Feldeigenschaften]** einen Namen und eine Beschreibung für das Feld ein. Bei der Auswahl des Felds **[!UICONTROL Typ]** müssen Sie den entsprechenden Standarddatentyp für ein benutzerdefiniertes Einwilligungs- oder Präferenzfeld verwenden:

* [[!UICONTROL Generisches Einverständnisfeld]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Feld für allgemeine Marketing-Voreinstellungen]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Allgemeines Marketing-Präferenzfeld mit Abonnements]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Feld für allgemeine Personalisierungseinstellungen]](../../../../xdm/data-types/personalization-field.md)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Apply]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

Das Einverständnis- oder Präferenzfeld wird der Schemastruktur hinzugefügt. Beachten Sie, dass der in der rechten Leiste angezeigte [!UICONTROL Pfad] den Namespace `_tenantId` enthält. Dieser Namespace muss immer dann enthalten sein, wenn Sie in Ihren Datenvorgängen auf den Pfad zu diesem Feld verweisen.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Führen Sie die oben beschriebenen Schritte aus, um mit dem Hinzufügen der erforderlichen Zustimmungs- und Voreinstellungsfelder fortzufahren. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Änderungen zu bestätigen.

Wenn Sie keinen Datensatz für dieses Schema erstellt haben, fahren Sie mit dem Abschnitt [Erstellen eines Datensatzes](#dataset) fort.
