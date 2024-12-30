---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Konfigurieren eines Datensatzes zur Erfassung von Einverständnis- und Präferenzdaten
description: Erfahren Sie, wie Sie ein Experience-Datenmodell-Schema (XDM) und einen Datensatz konfigurieren, um Einverständnis- und Voreinstellungsdaten in Adobe Experience Platform zu erfassen.
role: Developer
feature: Consent, Schemas, Datasets
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: bf651967714745a0b501dcb27373379fe014c9e1
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 4%

---

# Konfigurieren eines Datensatzes zur Erfassung von Einwilligungs- und Präferenzdaten

Damit Adobe Experience Platform Ihre Einverständnis-/Präferenzdaten von Kunden verarbeiten kann, müssen diese Daten an einen Datensatz gesendet werden, dessen Schema Felder enthält, die mit Einverständnissen und anderen Berechtigungen in Verbindung stehen. Insbesondere muss dieser Datensatz auf der [!DNL XDM Individual Profile]-Klasse basieren und für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert sein.

In diesem Dokument werden die Schritte zum Konfigurieren eines Datensatzes für die Verarbeitung von Einverständnisdaten im Experience Platform beschrieben. Einen Überblick über den vollständigen Workflow für die Verarbeitung von Einverständnis-/Voreinstellungsdaten in Platform erhalten Sie im Abschnitt [Übersicht zur Einverständnisverarbeitung](./overview.md).

>[!IMPORTANT]
>
>Die Beispiele in diesem Handbuch verwenden einen standardisierten Satz von Feldern zur Darstellung von Kundeneinverständniswerten, wie er in der Schemafeldgruppe [[!UICONTROL Einverständnis und ]) ](../../../../xdm/field-groups/profile/consents.md). Die Struktur dieser Felder soll ein effizientes Datenmodell bereitstellen, um viele gängige Anwendungsfälle für die Einverständniserfassung abzudecken.
>
>Sie können jedoch auch eigene Feldergruppen definieren, um das Einverständnis entsprechend Ihren eigenen Datenmodellen darzustellen. Wenden Sie sich an Ihre Rechtsabteilung, um die Genehmigung für ein Einverständnisdatenmodell zu erhalten, das Ihren Geschäftsanforderungen entspricht und auf den folgenden Optionen basiert:
>
>* Die standardisierte Einverständnis-Feldergruppe
>* Eine benutzerdefinierte Einverständnisfeldgruppe , die von Ihrer Organisation erstellt wurde
>* Eine Kombination aus der standardisierten Einverständnisfeldgruppe und zusätzlichen Feldern, die von einer benutzerdefinierten Einverständnisfeldgruppe bereitgestellt werden

## Voraussetzungen

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)](../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemata.
* [Echtzeit-Kundenprofil](../../../../profile/home.md): Fasst Kundendaten aus unterschiedlichen Quellen in einer vollständigen, einheitlichen Ansicht zusammen und bietet eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel.

>[!IMPORTANT]
>
>In diesem Tutorial wird davon ausgegangen, dass Sie das [!DNL Profile] in Platform kennen, das Sie zum Erfassen von Kundenattributinformationen verwenden möchten. Unabhängig von der Methode, die Sie zum Erfassen von Einverständnisdaten verwenden, muss dieses Schema [für das Echtzeit-Kundenprofil aktiviert) ](../../../../xdm/ui/resources/schemas.md#profile). Darüber hinaus kann die primäre Identität des Schemas kein direkt identifizierbares Feld sein, das in interessenbasierter Werbung, wie z. B. einer E-Mail-Adresse, nicht verwendet werden darf. Wenden Sie sich an Ihren Rechtsbeistand, wenn Sie sich nicht sicher sind, welche Felder eingeschränkt sind.

## [!UICONTROL Details zu Einverständnis und Voreinstellungen] Feldergruppenstruktur {#structure}

Die [!UICONTROL Einverständnis- und Voreinstellungsdetails] stellt standardisierte Einverständnisfelder für ein Schema bereit. Derzeit ist diese Feldergruppe nur mit Schemata kompatibel, die auf der [!DNL XDM Individual Profile]-Klasse basieren.

Die Feldergruppe stellt das Feld `consents` vom Typ „Objekt“ bereit, dessen Untereigenschaften einen Satz standardisierter Einverständnisfelder erfassen. Die folgende JSON-Datei ist ein Beispiel für die Art von Daten, die `consents` bei der Datenaufnahme erwartet:

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
>Weitere Informationen zur Struktur und Bedeutung der Untereigenschaften in `consents` finden Sie in der Übersicht zur [[!UICONTROL Einverständnis und ]-Feldergruppe](../../../../xdm/field-groups/profile/consents.md).

## Hinzufügen erforderlicher Feldergruppen zu Ihrem [!DNL Profile] {#add-field-group}

Um Einverständnisdaten mit dem Adobe-Standard zu erfassen, müssen Sie über ein profilaktiviertes Schema verfügen, das die folgenden beiden Feldergruppen enthält:

* [[!UICONTROL Details zu Einverständnis und Voreinstellungen]](../../../../xdm/field-groups/profile/consents.md)
* [[!UICONTROL IdentityMap]](../../../../xdm/field-groups/profile/identitymap.md) (erforderlich, wenn Platform Web oder Mobile SDK zum Senden von Einverständnissignalen verwendet wird)

Wählen Sie in der Platform **[!UICONTROL Benutzeroberfläche im linken Navigationsbereich die Option]** Schemata“ und dann die Registerkarte **[!UICONTROL Durchsuchen]** aus, um eine Liste der vorhandenen Schemata anzuzeigen. Wählen Sie hier den Namen des [!DNL Profile] Schemas aus, dem Sie Einverständnisfelder hinzufügen möchten. Die Screenshots in diesem Abschnitt verwenden das Schema „Mitglieder des Treueprogramms“, das im [Tutorial zur Schemaerstellung](../../../../xdm/tutorials/create-schema-ui.md) erstellt wurde.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>Sie können die Such- und Filterfunktionen des Arbeitsbereichs verwenden, um Ihr Schema leichter zu finden. Weitere Informationen finden Sie im Handbuch [Erkunden von XDM](../../../../xdm/ui/explore.md)Ressourcen“.

Das [!DNL Schema Editor] wird angezeigt und zeigt die Struktur des Schemas auf der Arbeitsfläche an. Wählen Sie auf der linken Seite der Arbeitsfläche **[!UICONTROL Hinzufügen]** im Abschnitt **[!UICONTROL Feldergruppen]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

Der **[!UICONTROL Feldergruppe hinzufügen]** wird angezeigt. Wählen Sie von hier aus **[!UICONTROL Einverständnis und]**) aus der Liste aus. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzugrenzen und die Feldergruppe leichter zu finden.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

Suchen Sie als Nächstes die **[!UICONTROL IdentityMap]**-Feldergruppe aus der Liste und wählen Sie sie ebenfalls aus. Sobald beide Feldergruppen in der rechten Leiste aufgeführt sind, wählen Sie **[!UICONTROL Feldergruppen hinzufügen]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

Die Arbeitsfläche wird erneut angezeigt und zeigt an, dass die Felder `consents` und `identityMap` zur Schemastruktur hinzugefügt wurden. Wenn Sie zusätzliche Einverständnis- und Präferenzfelder benötigen, die nicht von der Standardfeldgruppe erfasst werden, finden Sie weitere Informationen im Anhang unter [Hinzufügen benutzerdefinierter Einverständnis- und Präferenzfelder zum Schema](#custom-consent). Wählen Sie andernfalls **[!UICONTROL Speichern]**, um die Änderungen am Schema abzuschließen.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>Wenn Sie ein neues Schema erstellen oder ein vorhandenes Schema bearbeiten, das nicht für das Profil aktiviert wurde, müssen Sie [Schema für das Profil aktivieren](../../../../xdm/ui/resources/schemas.md#profile) vor dem Speichern.

Wenn das von Ihnen bearbeitete Schema von dem [!UICONTROL Profildatensatz) verwendet wird, ] in Ihrem Platform Web SDK-Datenstrom angegeben ist, enthält dieser Datensatz jetzt die neuen Einverständnisfelder. Sie können jetzt zum [Handbuch zur Einverständnisverarbeitung“ zurückkehren](./overview.md#merge-policies) um mit dem Konfigurieren von Experience Platform zur Verarbeitung von Einverständnisdaten fortzufahren. Wenn Sie keinen Datensatz für dieses Schema erstellt haben, befolgen Sie die Schritte im nächsten Abschnitt.

## Erstellen eines Datensatzes basierend auf Ihrem Einverständnisschema {#dataset}

Nachdem Sie ein Schema mit Einverständnisfeldern erstellt haben, müssen Sie einen Datensatz erstellen, der letztendlich die Einverständnisdaten Ihrer Kunden aufnimmt. Dieser Datensatz muss für [!DNL Real-Time Customer Profile] aktiviert sein.

Wählen Sie zunächst **[!UICONTROL linken Navigationsbereich]** Datensätze“ und dann oben rechts **[!UICONTROL Datensatz erstellen]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

Wählen Sie auf der nächsten Seite **[!UICONTROL Datensatz aus Schema erstellen]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

Der **[!UICONTROL Datensatz aus Schema erstellen]** wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Schema auswählen]**. Suchen Sie in der bereitgestellten Liste nach einem der Einverständnisschemata, die Sie zuvor erstellt haben. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzugrenzen und Ihr Schema leichter zu finden. Klicken Sie auf das Optionsfeld neben dem gewünschten Schema und dann auf **[!UICONTROL Weiter]** um fortzufahren.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

Der Schritt **[!UICONTROL Datensatz konfigurieren]** wird angezeigt. Geben Sie einen eindeutigen, leicht identifizierbaren Namen und eine Beschreibung für den Datensatz an, bevor Sie **[!UICONTROL Beenden]** auswählen.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

Die Detailseite für den neu erstellten Datensatz wird angezeigt. Wenn der Datensatz auf Ihrem Zeitreihenschema basiert, ist der Prozess abgeschlossen. Wenn der Datensatz auf Ihrem Datensatzschema basiert, besteht der letzte Schritt des Prozesses darin, den Datensatz für die Verwendung in [!DNL Real-Time Customer Profile] zu aktivieren.

Wählen Sie in der rechten Leiste den **[!UICONTROL Profil]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Wählen Sie abschließend **[!UICONTROL Aktivieren]** im Bestätigungs-Pop-up aus, um das Schema für die [!DNL Profile] zu aktivieren.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

Der Datensatz ist jetzt gespeichert und für die Verwendung in [!DNL Profile] aktiviert. Wenn Sie planen, mit der Platform Web SDK Einverständnisdaten an Profile zu senden, müssen Sie diesen Datensatz als [!UICONTROL Profildatensatz] beim Einrichten Ihres [Datenstroms](../../../../datastreams/overview.md) auswählen.

## Nächste Schritte

In diesem Tutorial haben Sie Einverständnisfelder zu einem [!DNL Profile] Schema hinzugefügt, dessen Datensatz zum Aufnehmen von Einverständnisdaten mithilfe der Platform Web SDK oder der direkten XDM-Aufnahme verwendet wird.

Sie können jetzt zur [Übersicht über die Einverständnisverarbeitung) zurückkehren, ](./overview.md#merge-policies) mit der Konfiguration von Experience Platform zur Verarbeitung von Einverständnisdaten fortzufahren.

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Erstellen eines Datensatzes zur Aufnahme von Einverständnis- und Präferenzdaten von Kunden.

### Hinzufügen benutzerdefinierter Einverständnis- und Präferenzfelder zum Schema {#custom-consent}

Wenn Sie zusätzliche Einverständnissignale erfassen müssen, die nicht in der standardmäßigen Feldergruppe &quot;[!UICONTROL  und Präferenzdetails] enthalten sind, können Sie benutzerdefinierte XDM-Komponenten verwenden, um Ihr Einverständnisschema an Ihre speziellen Geschäftsanforderungen anzupassen. In diesem Abschnitt werden die grundlegenden Prinzipien beschrieben, wie Sie Ihr Einverständnisschema anpassen können, um diese Signale in Profile aufzunehmen.

>[!IMPORTANT]
>
>Die Platform Web- und Mobile-SDKs unterstützen in ihren Befehlen zur Einverständnisänderung keine benutzerdefinierten Felder. Derzeit ist die einzige Möglichkeit, benutzerdefinierte Einverständnisfelder in Profile aufzunehmen, [Batch-Aufnahme](../../../../ingestion/batch-ingestion/overview.md) oder eine [Quellverbindung](../../../../sources/home.md).

Es wird dringend empfohlen, die Feldergruppe [!UICONTROL Einverständnis und Voreinstellungsdetails] als Grundlage für die Struktur Ihrer Einverständnisdaten zu verwenden und bei Bedarf zusätzliche Felder hinzuzufügen, anstatt zu versuchen, die gesamte Struktur von Grund auf neu zu erstellen.

Um benutzerdefinierte Felder zur Struktur einer Standardfeldergruppe hinzuzufügen, müssen Sie zunächst eine benutzerdefinierte Feldergruppe erstellen. Nachdem Sie die Feldergruppe [!UICONTROL Einverständnis und Voreinstellungsdetails] zum Schema hinzugefügt haben, wählen Sie das Symbol **Plus (+)** im Abschnitt **[!UICONTROL Feldergruppen]** aus und klicken Sie dann auf **[!UICONTROL Neue Feldergruppe erstellen]**. Geben Sie einen Namen und eine optionale Beschreibung für die Feldergruppe ein und wählen Sie dann **[!UICONTROL Feldergruppe hinzufügen]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

Der [!DNL Schema Editor] wird erneut angezeigt, wobei die neue benutzerdefinierte Feldergruppe in der linken Leiste ausgewählt ist. Auf der Arbeitsfläche werden Steuerelemente angezeigt, mit denen Sie der Schemastruktur benutzerdefinierte Felder hinzufügen können. Um ein neues Einverständnis- oder Präferenzfeld hinzuzufügen, klicken Sie auf das **Plus (+)** Symbol neben dem `consents`.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

Ein neues Feld wird innerhalb des `consents`-Objekts angezeigt. Da Sie ein benutzerdefiniertes Feld zu einem standardmäßigen XDM-Objekt hinzufügen, wird das neue Feld unter einem -Objekt erstellt, das den Namespace zu Ihrer Mandanten-ID erhält.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

Geben Sie in der rechten Leiste unter **[!UICONTROL Feldeigenschaften]** einen Namen und eine Beschreibung für das Feld ein. Bei der Auswahl des Felds **[!UICONTROL Typ]** müssen Sie den entsprechenden Standarddatentyp für ein benutzerdefiniertes Einverständnis- oder Präferenzfeld verwenden:

* [[!UICONTROL Generisches Einverständnisfeld]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Feld „Allgemeine Marketing-Voreinstellungen“]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Generisches Feld für Marketing-Voreinstellungen mit Abonnements]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Generisches Personalization-Präferenzfeld]](../../../../xdm/data-types/personalization-field.md)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

Das Feld Einverständnis oder Voreinstellung wird zur Schemastruktur hinzugefügt. Beachten Sie, [!UICONTROL  der in ] rechten Leiste angezeigte „Pfad“ den `_tenantId` Namespace enthält. Dieser Namespace muss immer dann eingeschlossen werden, wenn Sie in Ihren Datenvorgängen auf den Pfad zu diesem Feld verweisen.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Führen Sie die oben genannten Schritte aus, um weiterhin die erforderlichen Einverständnis- und Voreinstellungsfelder hinzuzufügen. Klicken Sie abschließend auf **[!UICONTROL Speichern]**, um Ihre Änderungen zu bestätigen.

Wenn Sie keinen Datensatz für dieses Schema erstellt haben, fahren Sie mit dem Abschnitt über das [ eines Datensatzes ](#dataset).
