---
solution: Experience Platform
title: Schemafeldgruppe „Einverständnis und Voreinstellungen“
description: Erfahren Sie mehr über die Schemafeldgruppe „Einverständnis und Voreinstellungen“.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# [!UICONTROL Consents and Preferences] Feldergruppe

[!UICONTROL Consents and Preferences] ist eine Standardfeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md) die Einverständnis- und Präferenzinformationen für einen einzelnen Kunden erfasst.

>[!NOTE]
>
>Da diese Feldergruppe nur mit [!DNL XDM Individual Profile] kompatibel ist, kann sie nicht für [!DNL XDM ExperienceEvent] verwendet werden. Wenn Sie Einverständnis- und Präferenzdaten in Ihr Erlebnisereignisschema aufnehmen möchten, fügen Sie [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] den &#x200B;](../../data-types/consents.md)-Datentyp mithilfe einer [benutzerdefinierten Feldergruppe“ zum &#x200B;](../../ui/resources/field-groups.md#create) hinzu.

## Feldgruppenstruktur {#structure}

Die [!UICONTROL Consents and Preferences] Feldergruppe bietet ein einzelnes Feld vom Typ „Objekt“, `consents`. B. , um Einverständnis- und Voreinstellungsinformationen zu erfassen. Dieses Feld erweitert den Datentyp [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences]](../../data-types/consents.md) entfernt das `adID` Feld und fügt ein `idSpecific` Zuordnungsfeld hinzu.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Anweisungen zum Suchen einer XDM[Ressource und Überprüfen ihrer Struktur in der Benutzeroberfläche von Experience Platform finden Sie im Handbuch &#x200B;](../../ui/explore.md)Erkunden von XDM-Ressourcen“ zu .

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp, den die [!UICONTROL Consents and Preferences]-Feldergruppe verarbeiten kann. Informationen zur Verwendung der meisten von der Feldergruppe bereitgestellten Felder finden Sie im Handbuch zum Datentyp [Einverständnisse und Voreinstellungen](../../data-types/consents.md). Die folgenden Unterabschnitte konzentrieren sich auf die eindeutigen Attribute, die die Feldergruppe zum Datentyp hinzufügt.

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
>Sie können JSON-Beispieldaten für jedes XDM-Schema generieren, das Sie in Experience Platform definieren, um zu visualisieren, wie Ihre Kundeneinwilligungs- und Präferenzdaten zugeordnet werden sollten. In der folgenden Dokumentation finden Sie weitere Informationen:
>
>* [Generieren von Beispieldaten in der Benutzeroberfläche](../../ui/sample.md)
>* [Generieren von Beispieldaten in der API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` kann verwendet werden, wenn eine bestimmte Einwilligung oder Präferenz nicht allgemein für einen Kunden gilt, sondern auf ein einzelnes Gerät oder eine einzelne ID beschränkt ist. Beispielsweise kann ein Kunde den Empfang von E-Mails an eine Adresse deaktivieren und gleichzeitig möglicherweise E-Mails an eine andere Adresse senden.

>[!IMPORTANT]
>
>Einverständnisse und Voreinstellungen auf Kanalebene (d. h. diejenigen, die unter `consents` außerhalb von `idSpecific` bereitgestellt werden) gelten für alle IDs innerhalb dieses Kanals. Daher wirken sich alle Einverständnisse und Voreinstellungen auf Kanalebene direkt darauf aus, ob äquivalente ID- oder gerätespezifische Einstellungen berücksichtigt werden:
>
>* Wenn der Kunde sich auf Kanalebene abgemeldet hat, werden alle entsprechenden Einverständnisse oder Voreinstellungen in `idSpecific` ignoriert.
>* Wenn das Einverständnis oder die Voreinstellung auf Kanalebene nicht festgelegt ist oder der Kunde sich dafür entschieden hat, werden die entsprechenden Einverständnisse oder Voreinstellungen in `idSpecific` berücksichtigt.

Jeder Schlüssel im `idSpecific`-Objekt repräsentiert einen bestimmten Identity-Namespace, der vom Adobe Experience Platform Identity Service erkannt wird. Sie können zwar eigene benutzerdefinierte Namespaces definieren, um verschiedene Kennungen zu kategorisieren, es wird jedoch empfohlen, einen der von Identity Service bereitgestellten Standard-Namespaces zu verwenden, um die Speichergröße für das Echtzeit-Kundenprofil zu reduzieren. Weitere Informationen zu Identity-Namespaces finden Sie unter [Übersicht zu Identity-Namespaces](/help/identity-service/features/namespaces.md) in der Identity Service-Dokumentation.

Die Schlüssel für jedes Namespace-Objekt stellen die eindeutigen Identitätswerte dar, für die der Kunde Voreinstellungen festgelegt hat. Jeder Identitätswert kann einen vollständigen Satz von Einverständnissen und Voreinstellungen enthalten, die auf die gleiche Weise formatiert sind wie `consents`.

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

Innerhalb `marketing` im Abschnitt `idSpecific` angegebenen Objekte werden die Felder `any` und `preferred` nicht unterstützt. Diese Felder können nur auf Benutzerebene konfiguriert werden. Darüber hinaus unterstützen die `idSpecific` Marketing-Voreinstellungen für `email`, `sms` und `push` keine `subscriptions`.

Es gibt auch ein Einverständnis, das nur im `idSpecific` Abschnitt erteilt werden kann: `adID`. Dieses Feld wird im folgenden Unterabschnitt behandelt.

#### `adID`

Das `adID` Einverständnis stellt das Einverständnis des Kunden dar, ob eine Advertiser-ID (IDFA oder GAID) verwendet werden kann, um den Kunden über Apps hinweg auf diesem Gerät zu verknüpfen. Dieser Wert kann nur unter dem `ECID` Identity-Namespace im Abschnitt `idSpecific` konfiguriert werden und kann nicht für andere Namespaces oder auf Benutzerebene für diese Feldergruppe festgelegt werden.

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
>Es wird nicht erwartet, dass Sie diesen Wert direkt festlegen, da Adobe Experience Platform Mobile SDK ihn bei Bedarf automatisch festlegt.

## Aufnehmen von Daten mithilfe der Feldergruppe {#ingest}

Damit Sie die [!UICONTROL Consents and Preferences] Feldergruppe verwenden können, um Einverständnisdaten von Ihren Kunden aufzunehmen, müssen Sie einen Datensatz erstellen, der auf einem Schema basiert, das diese Feldergruppe enthält.

Anweisungen zum Zuweisen von Feldergruppen zu Feldern [&#x200B; Sie im Tutorial &#x200B;](https://www.adobe.com/go/xdm-schema-editor-tutorial-en)Erstellen eines Schemas in der Benutzeroberfläche“. Nachdem Sie ein Schema erstellt haben, das ein Feld mit der [!UICONTROL Consents and Preferences] Feldergruppe enthält, lesen Sie den Abschnitt [Erstellen eines &#x200B;](/help/catalog/datasets/user-guide.md#create)) im Benutzerhandbuch zu Datensätzen, indem Sie die Schritte zum Erstellen eines Datensatzes mit einem vorhandenen Schema befolgen.

>[!IMPORTANT]
>
>Wenn Sie Einverständnisdaten an [!DNL Real-Time Customer Profile] senden möchten, ist es erforderlich, dass Sie ein [!DNL Profile]-aktiviertes Schema erstellen, das auf der [!DNL XDM Individual Profile]-Klasse basiert, die die [!UICONTROL Consents and Preferences]-Feldergruppe enthält. Der Datensatz, den Sie basierend auf diesem Schema erstellen, muss auch für die [!DNL Profile] aktiviert sein. Die einzelnen Schritte im Zusammenhang mit den [!DNL Real-Time Customer Profile] für Schemata und Datensätze finden Sie in den oben verlinkten Tutorials.
>
>Darüber hinaus müssen Sie auch sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass die Datensätze, die die neuesten Einverständnis- und Präferenzdaten enthalten, priorisiert werden, damit Kundenprofile korrekt aktualisiert werden. Weitere Informationen finden Sie in der Übersicht [Zusammenführungsrichtlinien](/help/rtcdp/profile/merge-policies.md) .

## Umgang mit Einverständnis- und Voreinstellungsänderungen

Wenn ein Kunde sein Einverständnis oder seine Voreinstellungen auf Ihrer Website ändert, sollten diese Änderungen erfasst und sofort durchgesetzt werden, indem das Einverständnis in der verwendeten Datenerfassungsbibliothek festgelegt wird. Wenn ein Kunde die Datenerfassung ablehnt, muss diese sofort eingestellt werden. Wenn sich ein Kunde gegen die Personalisierung entscheidet, sollte auf der nächsten Seite, die er lädt, keine Personalisierung vorhanden sein. Weitere Informationen finden Sie unter [`setConsent`](/help/collection/js/commands/setconsent.md) mit der JavaScript-Bibliothek oder unter [[!UICONTROL Set consent]](/help/tags/extensions/client/web-sdk/actions/set-consent.md) mit der SDK-Web-Tag-Erweiterung .

## Nächste Schritte

In diesem Dokument wurden die Struktur und Verwendung der [!UICONTROL Consents and Preferences] Feldergruppe behandelt. Weitere Informationen zu den anderen Feldern, die von der Feldergruppe bereitgestellt werden, finden Sie im Dokument zum [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] Datentyp &#x200B;](../../data-types/consents.md).
