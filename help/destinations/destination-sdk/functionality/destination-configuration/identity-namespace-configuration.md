---
description: Erfahren Sie, wie Sie die unterstützten Zielidentitäten für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Identitäts-Namespace-Konfiguration
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 14%

---


# Identitäts-Namespace-Konfiguration

Experience Platform verwendet Identitäts-Namespaces, um den Typ bestimmter Identitäten zu beschreiben. Beispiel: ein Identitäts-Namespace namens `Email` identifiziert einen Wert wie `name@email.com` als E-Mail-Adresse.

Beim Erstellen eines Ziels über eine Destination SDK zusätzlich zu [Partnerschema konfigurieren](schema-configuration.md) Damit Benutzer Profilattribute und Identitäten zuordnen können, können Sie auch Identitäts-Namespaces definieren, die von Ihrer Zielplattform unterstützt werden.

In diesem Fall können Benutzer zusätzlich zu den Zielprofilattributen auch Zielidentitäten auswählen.

Weitere Informationen zu Identitäts-Namespaces in Experience Platform finden Sie unter [Dokumentation zu Identitäts-Namespaces](../../../../identity-service/namespaces.md).

Beim Konfigurieren von Identitäts-Namespaces für Ihr Ziel können Sie das von Ihrem Ziel unterstützte Zielidentitätszuordnung anpassen, z. B.:

* Ermöglicht Benutzern, XDM-Attribute Identitäts-Namespaces zuzuordnen.
* Zuordnen von Benutzern [Standard-Identitäts-Namespaces](../../../../identity-service/namespaces.md#standard) zu Ihren eigenen Identitäts-Namespaces hinzu.
* Zuordnen von Benutzern [benutzerdefinierte Identitäts-Namespaces](../../../../identity-service/namespaces.md#manage-namespaces) zu Ihren eigenen Identitäts-Namespaces hinzu.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder lesen Sie das Handbuch zu [Destination SDK zum Konfigurieren eines dateibasierten Ziels verwenden](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Sie können Ihre unterstützten Identitäts-Namespaces über die `/authoring/destinations` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Konfigurationsoptionen für Identitäts-Namespaces beschrieben, die Sie für Ihr Ziel verwenden können, und es wird gezeigt, was Kunden in der Platform-Benutzeroberfläche sehen werden.

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |

## Unterstützte Parameter {#supported-parameters}

Bei der Definition der Zielidentitäten, die Ihr Ziel unterstützt, können Sie die in der folgenden Tabelle beschriebenen Parameter verwenden, um ihr Verhalten zu konfigurieren.

| Parameter | Typ | Erforderlich/Optional | Beschreibung |
|---------|----------|---|------|
| `acceptsAttributes` | Boolesch | Optional | Gibt an, ob Kunden der Identität, die Sie konfigurieren, standardmäßige Profilattribute zuordnen können. |
| `acceptsCustomNamespaces` | Boolesch | Optional | Gibt an, ob Kunden benutzerdefinierte Identitäts-Namespaces dem Identitäts-Namespace zuordnen können, den Sie konfigurieren. |
| `acceptedGlobalNamespaces` | – | Optional | Gibt an, [Standard-Identitäts-Namespaces](../../../../identity-service/namespaces.md#standard) (z. B. [!UICONTROL IDFA]) -Kunden können der Identität zuordnen, die Sie konfigurieren. |
| `transformation` | Zeichenfolge | Optional | Zeigt die [[!UICONTROL Umwandlung anwenden]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) aktivieren, wenn das Quellfeld entweder ein XDM-Attribut oder einen benutzerdefinierten Identitäts-Namespace ist. Verwenden Sie diese Option, um Benutzern die Möglichkeit zu geben, beim Export Quell-Attribute zu hashen. Um diese Option zu aktivieren, setzen Sie den Wert auf `sha256(lower($))`. |
| `requiredTransformation` | Zeichenfolge | Optional | Wenn Kunden diesen Quell-Identitäts-Namespace auswählen, wird die [[!UICONTROL Umwandlung anwenden]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) wird automatisch auf die Zuordnung angewendet und Kunden können sie nicht deaktivieren. Um diese Option zu aktivieren, setzen Sie den Wert auf `sha256(lower($))`. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

Sie müssen angeben, welche [!DNL Platform]-Identitäten Kunden in Ihr Ziel exportieren können. Einige Beispiele: [!DNL Experience Cloud ID], gehashte E-Mail, Geräte-ID ([!DNL IDFA], [!DNL GAID]). Diese Werte sind Identitäts-Namespaces von [!DNL Platform], die Kunden von Ihrem Ziel aus Identitäts-Namespaces zuordnen können.

Identitäts-Namespaces erfordern keine 1:1-Korrespondenz zwischen [!DNL Platform] und Ihrem Ziel.
Kunden können beispielsweise einen [!DNL IDFA]-Namespace in [!DNL Platform] einem [!DNL IDFA]-Namespace Ihres Ziels zuordnen oder sie können denselben [!DNL IDFA]-Namespace in [!DNL Platform] einem [!DNL Customer ID]-Namespace in Ihrem Ziel zuordnen.

Weitere Informationen zu Identitäten finden Sie im Abschnitt [Übersicht über Identitäts-Namespace](../../../../identity-service/namespaces.md).

## Zuordnungsüberlegungen

Wenn Kunden einen Quell-Identitäts-Namespace auswählen und kein Zielgruppen-Mapping wählen, füllt Platform das Zielgruppen-Mapping automatisch mit einem Attribut mit demselben Namen.

## Optionales Hashing für Quellfelder konfigurieren

Experience Platform-Kunden können Daten im Hash-Format oder im Klartext in Platform erfassen. Wenn Ihre Zielplattform sowohl Hash- als auch Hash-Daten akzeptiert, können Sie Kunden die Möglichkeit geben, festzulegen, ob Platform beim Export in Ihr Ziel die Quellfeldwerte hashen soll.

Die folgende Konfiguration ermöglicht die optionale [Umwandlung anwenden](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) -Option in der Platform-Benutzeroberfläche im Schritt &quot;Zuordnung&quot;angezeigt.

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

Aktivieren Sie diese Option, wenn Sie nicht gehashte Quellfelder verwenden, damit diese automatisch von Adobe Experience Platform bei der Aktivierung gehasht werden.

Wenn Sie ungehashte Quellattribute Zielattributen zuordnen, von denen das Ziel erwartet, dass sie gehasht werden (z. B.: `email_lc_sha256` oder `phone_sha256`), überprüfen Sie die **Umwandlung anwenden** Option, damit Adobe Experience Platform die Quellattribute bei Aktivierung automatisch hasst.

## obligatorisches Hashing für Quellfelder konfigurieren

Wenn Ihr Ziel nur Hash-Daten akzeptiert, können Sie die exportierten Attribute so konfigurieren, dass sie automatisch von Platform gehasht werden. Die folgende Konfiguration überprüft automatisch die **Umwandlung anwenden** -Option, wenn die `Email` und `Phone` -Identitäten zugeordnet werden.

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, wie Sie Ihre Identitäts-Namespaces für Ziele konfigurieren, die mit Destination SDK erstellt wurden.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)
