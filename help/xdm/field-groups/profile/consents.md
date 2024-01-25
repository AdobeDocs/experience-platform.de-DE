---
solution: Experience Platform
title: Einverständnis und Voreinstellungsfeldgruppe
description: Erfahren Sie mehr über die Feldgruppe "Einverständnis und Voreinstellungen".
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL Einverständnis und Voreinstellungen] Feldergruppe

[!UICONTROL Einverständnis und Voreinstellungen] ist eine Standardfeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) , das Einverständnis und Präferenzinformationen für einen einzelnen Kunden erfasst.

>[!NOTE]
>
>Da diese Feldergruppe nur mit [!DNL XDM Individual Profile], kann sie nicht für [!DNL XDM ExperienceEvent] Schemas. Wenn Sie Einwilligungs- und Präferenzdaten in Ihr Erlebnisereignis-Schema einbeziehen möchten, fügen Sie die [[!UICONTROL Einverständnis für Datenschutz-, Personalisierungs- und Marketing-Voreinstellungen] Datentyp](../../data-types/consents.md) durch Verwendung eines [benutzerspezifische Feldergruppe](../../ui/resources/field-groups.md#create) anstatt.

## Feldgruppenstruktur {#structure}

Die [!UICONTROL Einverständnis und Voreinstellungen] Feldergruppe stellt ein einzelnes Feld vom Typ Objekt bereit; `consents`, um Einverständniserklärungen und Präferenzinformationen zu erfassen. Dieses Feld erweitert die [[!UICONTROL Einverständnis für Datenschutz-, Personalisierungs- und Marketing-Voreinstellungen] Datentyp](../../data-types/consents.md), wodurch die `adID` und das Hinzufügen eines `idSpecific` Zuordnungsfeld.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Siehe Handbuch unter [Erkunden von XDM-Ressourcen](../../ui/explore.md) zu finden, wie Sie eine beliebige XDM-Ressource nachschlagen und ihre Struktur in der Platform-Benutzeroberfläche überprüfen können.

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp, bei dem die [!UICONTROL Einverständnis und Voreinstellungen] -Feldergruppe kann verarbeitet werden. Informationen zur Verwendung der meisten von der Feldergruppe bereitgestellten Felder finden Sie im Handbuch im [Datentyp &quot;Einwilligungen und Voreinstellungen&quot;](../../data-types/consents.md). Die folgenden Unterabschnitte konzentrieren sich auf die eindeutigen Attribute, die die Feldergruppe zum Datentyp hinzufügt.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
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
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>Sie können JSON-Beispieldaten für jedes XDM-Schema generieren, das Sie in Experience Platform definieren, um zu veranschaulichen, wie Ihre Kundenzustimmungs- und -bevorzugte Daten zugeordnet werden sollen. Weitere Informationen finden Sie in der folgenden Dokumentation:
>
>* [Generieren von Beispieldaten in der Benutzeroberfläche](../../ui/sample.md)
>* [Beispieldaten in der API generieren](../../api/sample-data.md)

### `idSpecific`

`idSpecific` kann verwendet werden, wenn eine bestimmte Zustimmung oder Voreinstellung nicht allgemein für einen Kunden gilt, sondern auf ein einzelnes Gerät oder eine einzelne ID beschränkt ist. Beispielsweise kann ein Kunde den Erhalt von E-Mails an eine Adresse deaktivieren und gleichzeitig E-Mails an eine andere Adresse zulassen.

>[!IMPORTANT]
>
>Zustimmung und Voreinstellungen auf Kanalebene (d. h. die unter `consents` außerhalb von `idSpecific`) auf alle IDs in diesem Kanal angewendet werden. Daher wirken sich alle Zustimmung und Voreinstellungen auf Kanalebene direkt darauf aus, ob entsprechende ID- oder gerätespezifische Einstellungen berücksichtigt werden:
>
>* Wenn der Kunde sich auf Kanalebene abgemeldet hat, werden alle entsprechenden Zustimmungen oder Voreinstellungen unter `idSpecific` werden ignoriert.
>* Wenn die Zustimmung oder Voreinstellung auf Kanalebene nicht festgelegt ist oder der Kunde sich angemeldet hat, werden die entsprechenden Zustimmungen oder Voreinstellungen unter `idSpecific` werden geehrt.

Jeder Schlüssel im `idSpecific` -Objekt stellt einen bestimmten Identitäts-Namespace dar, der vom Adobe Experience Platform Identity Service erkannt wird. Sie können Ihre eigenen benutzerdefinierten Namespaces definieren, um verschiedene IDs zu kategorisieren. Es wird jedoch empfohlen, einen der Standard-Namespaces zu verwenden, die von Identity Service bereitgestellt werden, um die Speichergrößen für das Echtzeit-Kundenprofil zu reduzieren. Weitere Informationen zu Identitäts-Namespaces finden Sie unter [Übersicht über Identitäts-Namespace](../../../identity-service/features/namespaces.md) in der Dokumentation zu Identity Service .

Die Schlüssel für jedes Namespace-Objekt stellen die eindeutigen Identitätswerte dar, für die der Kunde Voreinstellungen festgelegt hat. Jeder Identitätswert kann einen vollständigen Satz von Einverständnissen und Voreinstellungen enthalten, der auf dieselbe Weise formatiert ist wie `consents`.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

Within `marketing` Objekte, die in der `idSpecific` -Abschnitt `any` und `preferred` -Felder werden nicht unterstützt. Diese Felder können nur auf Benutzerebene konfiguriert werden. Darüber hinaus wird die `idSpecific` Marketing-Voreinstellungen für `email`, `sms`, und `push` nicht unterstützen `subscriptions` -Felder.

Es gibt auch eine Zustimmung, die nur im `idSpecific` Abschnitt: `adID`. Dieses Feld wird im folgenden Unterabschnitt behandelt.

#### `adID`

Die `adID` Das Einverständnis stellt die Zustimmung des Kunden dar, ob eine Advertiser-ID (IDFA oder GAID) verwendet werden kann, um den Kunden über Apps auf diesem Gerät hinweg zu verknüpfen. Dieser Wert kann nur unter der Variablen `ECID` Identitäts-Namespace im `idSpecific` und kann nicht für andere Namespaces oder auf Benutzerebene für diese Feldergruppe festgelegt werden.

```json
"idSpecific": {
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
>
>Es wird nicht erwartet, dass Sie diesen Wert direkt festlegen, da das Adobe Experience Platform Mobile-SDK ihn gegebenenfalls automatisch festlegt.

## Erfassen von Daten mithilfe der Feldergruppe {#ingest}

Um die [!UICONTROL Einverständnis und Voreinstellungen] -Feldergruppe verwenden, um Einwilligungsdaten von Ihren Kunden zu erfassen, müssen Sie einen Datensatz erstellen, der auf einem Schema basiert, das diese Feldergruppe enthält.

Siehe Tutorial zu [Erstellen eines Schemas in der Benutzeroberfläche](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) für Schritte zum Zuweisen von Feldergruppen zu Feldern. Nachdem Sie ein Schema erstellt haben, das ein Feld mit der [!UICONTROL Einverständnis und Voreinstellungen] Feldergruppe, siehe Abschnitt [Datensatz erstellen](../../../catalog/datasets/user-guide.md#create) Führen Sie im Benutzerhandbuch zu Datensätzen die Schritte zum Erstellen eines Datensatzes mit einem vorhandenen Schema aus.

>[!IMPORTANT]
>
>Wenn Sie Einwilligungsdaten an senden möchten [!DNL Real-Time Customer Profile]müssen Sie eine [!DNL Profile]-aktiviertes Schema basierend auf dem [!DNL XDM Individual Profile] -Klasse, die die [!UICONTROL Einverständnis und Voreinstellungen] Feldergruppe. Der Datensatz, den Sie auf Grundlage dieses Schemas erstellen, muss auch für [!DNL Profile]. Spezifische Schritte zum Thema [!DNL Real-Time Customer Profile] Anforderungen für Schemas und Datensätze.
>
>Darüber hinaus müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass sie die Datensätze priorisieren, die die neuesten Zustimmungs- und Voreinstellungsdaten enthalten, damit Kundenprofile korrekt aktualisiert werden. Siehe Übersicht unter [Zusammenführungsrichtlinien](../../../rtcdp/profile/merge-policies.md) für weitere Informationen.

## Handhabung von Zustimmungs- und Vorgabenänderungen

Wenn ein Kunde seine Zustimmung oder Voreinstellungen auf Ihrer Website ändert, sollten diese Änderungen erfasst und sofort mit der [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Wenn ein Kunde die Datenerfassung ablehnt, muss die Datenerfassung sofort eingestellt werden. Wenn ein Kunde die Personalisierung ablehnt, sollte auf der nächsten besuchten Seite keine Personalisierung vorhanden sein.

## Nächste Schritte

In diesem Dokument ging es um die Struktur und Verwendung der [!UICONTROL Einverständnis und Voreinstellungen] Feldergruppe. Weitere Informationen zu den anderen von der Feldergruppe bereitgestellten Feldern finden Sie im Dokument auf der [[!UICONTROL Einverständnis für Datenschutz-, Personalisierungs- und Marketing-Voreinstellungen] Datentyp](../../data-types/consents.md).
