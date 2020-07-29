---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Übersicht über die Datenschutzmischung
topic: guide
translation-type: tm+mt
source-git-commit: 02014c503dc9d4597e1129cafe3ba86f4abe37e9
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 1%

---


# [!DNL Privacy Consent] mixin-Übersicht

Das [!DNL Privacy/Marketing Preferences (Consent)] Mixin (im Folgenden &quot;Mixin&quot; genannt) ist ein[!DNL Privacy Consent] [!DNL Experience Data Model] (XDM) Mixin, das die Erfassung von Benutzerberechtigungen und Voreinstellungen unterstützen soll, die von CMPs und anderen Quellen von Kunden generiert wurden. Dieses Dokument umfasst die Struktur und die vorgesehene Verwendung der verschiedenen Felder, die von der Mischung bereitgestellt werden.

## Voraussetzungen  {#prerequisites}

Dieses Dokument erfordert ein funktionierendes Verständnis von [!DNL Experience Data Model] (XDM) und der Verwendung der Schema in [!DNL Experience Platform]. Bitte lesen Sie die folgende Dokumentation, bevor Sie fortfahren:

* [XDM-System – Übersicht](http://www.adobe.com/go/xdm-home-en)
* [Grundlagen der Schemakomposition](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Schema-Beispiel {#schema}

>[!NOTE]
>
>Das nachstehende Beispiel soll die Struktur der Daten veranschaulichen, die [!DNL Platform] über das [!DNL Privacy Consent] Mixin gesendet werden, um dem nächsten Abschnitt in diesem Dokument, in dem die Hauptfelder des Mixins erläutert werden, einen Kontext zu geben. Ein vollständiges Beispiel der Struktur des Schemas finden Sie im [Anhang](#full-schema) zu Referenzzwecken.

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp, den das [!DNL Privacy Consent] Mixin verarbeiten kann. Informationen zur spezifischen Verwendung der einzelnen Felder finden Sie im nächsten Abschnitt.

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## Felder {#fields}

Die folgenden Abschnitte behandeln die Verwendung der wichtigsten Felder, die vom [!DNL Privacy Consent] Mixin bereitgestellt werden, und wie ihre Unterfelder strukturiert sein sollten.

### xdm:privacyOptOuts {#privacyOptOuts}

`xdm:privacyOptOuts` ist ein Array, das die vom Kunden ausgewählten allgemeinen Ausschluss-Einstellungen darstellt. In diesem Array können mehrere Objekte enthalten sein, von denen jedes einen bestimmten Ausschluss-Typ und die vom Kunden für diesen Typ gewählten Voreinstellungen darstellt.

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:optOutType` | Die Art der Abmeldung. Zulässige Werte und Definitionen finden Sie im [Anhang](#optOutType-values) . |
| `xdm:optOutValue` | Die ausgewählte Präferenz, die der Kunde für diesen bestimmten Ausschluss-Typ gewählt hat. Zulässige Werte und Definitionen finden Sie im [Anhang](#choice-optOutValue-values) . |
| `xdm:timestamp` | Ein Zeitstempel nach ISO 8601, der angibt, wann sich die Opt-out-Voreinstellung geändert hat (falls zutreffend). |
| `xdm:basisOfProcessing` | Gibt die datenschutzbezogene Grundlage an, auf der die Daten erfasst und verarbeitet werden sollen. Standardmäßig ist dieses Feld auf `consent`festgelegt. Dies bedeutet, dass die Daten nur verarbeitet werden sollten, wenn der Benutzer seine Einwilligung gegeben hat (wie in `xdm:optOutValue`).<br><br>Unter bestimmten Umständen wurden Kunden nicht aufgefordert, die Zustimmung zur Datenverarbeitung zu erteilen. `xdm:basisOfProcessing` in diesen Fällen in das Opt-out-Objekt aufgenommen werden, unter Angabe des Grundes, aus dem eine Aufforderung zur Einwilligung nicht erteilt wurde. Zulässige Werte und Definitionen finden Sie im [Anhang](#basisOfProcessing-values) . |

### xdm:personalizationPreferences {#personalizationPreferences}

`xdm:personalizationPreferences` erfasst Kundenvoreinstellungen darüber, auf welche Weise ihre Daten für die Personalisierung verwendet werden können. Benutzer können bestimmte Personalisierungs-Anwendungsfälle Opt-out oder ganz Opt-out Personalisierung.

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` umfasst nicht Anwendungsfälle für das Inverkehrbringen. Wenn ein Kunde beispielsweise die Personalisierung für E-Mails ablehnt, wird er nicht aufhören, E-Mails zu empfangen. Vielmehr werden die E-Mails, die sie erhalten, generisch sein und nicht auf ihrem Profil basieren.
>
>Wenn sich ein Kunde in demselben Beispiel vom E-Mail-Marketing abmeldet (bis `xdm:marketingPreferences`, wie im [nächsten Abschnitt](#marketingPreferences)erläutert), erhält dieser Kunde keine E-Mails, auch wenn eine Personalisierung per E-Mail zulässig ist.

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:default` | Die in diesem Objekt bereitgestellten Daten entsprechen den Vorlieben des Kunden für die Personalisierung insgesamt. |
| `xdm:details` | Ein Array von Objekten, eines für jeden bestimmten Personalisierungstyp, für den der Kunde Voreinstellungen festgelegt hat. |
| `xdm:choice` | Die vom Kunden bereitgestellte Einwilligung zur Personalisierung im Allgemeinen oder zu einem bestimmten Personalisierungstyp, je nachdem, ob sie unter `xdm:default` bzw. `xdm:details`unter bereitgestellt wird. Zulässige Werte und Definitionen finden Sie im [Anhang](#choice-optOutValue-values) . |
| `xdm:type` | Objekte im `xdm:details` Array müssen dieses Feld bereitstellen, um anzugeben, für welchen speziellen Personalisierungsfall der Kunde seine Einwilligungsdaten bereitstellt. Zulässige Werte und Definitionen finden Sie im [Anhang](#type-values) . |
| `xdm:timestamp` | Ein Zeitstempel nach ISO 8601, der angibt, wann sich die Opt-out-Voreinstellung geändert hat (falls zutreffend). |
| `xdm:basisOfProcessing` | Gibt die datenschutzbezogene Grundlage an, auf der die Daten erfasst und verarbeitet werden sollen. Standardmäßig ist dieses Feld auf `consent`festgelegt. Dies bedeutet, dass die Daten nur verarbeitet werden sollten, wenn der Benutzer seine Einwilligung gegeben hat (wie in `xdm:choice`).<br><br>Unter bestimmten Umständen wurden Kunden nicht aufgefordert, ihre Zustimmung zur Personalisierung zu geben. `xdm:basisOfProcessing` in diesen Fällen in das Opt-out-Objekt aufgenommen werden, unter Angabe des Grundes, aus dem eine Aufforderung zur Einwilligung nicht erteilt wurde. Zulässige Werte und Definitionen finden Sie im [Anhang](#basisOfProcessing-values) . |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` erfasst Kundenpräferenzen hinsichtlich der Marketingzwecke, für die ihre Daten verwendet werden können. Benutzer können bestimmte Anwendungsfälle Opt-out oder ganz Opt-out Direktmarketing.

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:default` | Die in diesem Objekt bereitgestellten Daten stellen die Präferenzen des Kunden für Direktmarketing als Ganzes dar. |
| `xdm:details` | Ein Array von Objekten, eines für jeden bestimmten Marketinganwendungsfall, für den der Kunde Voreinstellungen festgelegt hat. |
| `xdm:choice` | Die vom Kunden erteilte Zustimmung bevorzugte Vermarktung im Allgemeinen oder einen bestimmten Anwendungsfall für das Inverkehrbringen, je nachdem, ob sie im Rahmen `xdm:default` bzw. `xdm:details`in einem bestimmten Fall bereitgestellt wird. Zulässige Werte und Definitionen finden Sie im [Anhang](#choice-optOutValue-values) . |
| `xdm:subscriptions` | Ein Objekt, dessen Schlüssel Firmen-spezifische Abonnement wie z. B. Mailing-Listen oder Newsletter darstellen. Jedes Abonnement-Objekt sollte wiederum einen `xdm:choice` Wert für das betreffende Abonnement enthalten. |
| `xdm:type` | Objekte im `xdm:details` Array müssen dieses Feld bereitstellen, um den spezifischen Anwendungsfall anzugeben, für den der Kunde seine Zustimmung erteilt. Zulässige Werte und Definitionen finden Sie im [Anhang](#type-values) . |
| `xdm:timestamp` | Ein Zeitstempel nach ISO 8601, der angibt, wann sich die Opt-out-Voreinstellung geändert hat (falls zutreffend). |
| `xdm:basisOfProcessing` | Gibt die datenschutzbezogene Grundlage an, auf der die Daten erfasst und verarbeitet werden sollen. Standardmäßig ist dieses Feld auf `consent`festgelegt. Dies bedeutet, dass die Daten nur verarbeitet werden sollten, wenn der Benutzer seine Einwilligung gegeben hat (wie in `xdm:choice`).<br><br>Unter bestimmten Umständen wurden Kunden nicht aufgefordert, ihre Zustimmung zum Direktmarketing zu erteilen. `xdm:basisOfProcessing` in diesen Fällen in das Opt-out-Objekt aufgenommen werden, unter Angabe des Grundes, aus dem eine Aufforderung zur Einwilligung nicht erteilt wurde. Zulässige Werte und Definitionen finden Sie im [Anhang](#basisOfProcessing-values) . |

## Daten zur Einwilligung mit dem Mixin erfassen {#ingest}

Um das [!DNL Privacy Consent] Mixin zum Erfassen von Daten zur Einwilligung Ihrer Kunden verwenden zu können, müssen Sie das Mixin einem neuen oder vorhandenen Schema hinzufügen und einen Datensatz erstellen, der auf diesem Schema basiert.

Anweisungen zum Hinzufügen von Mixins zu einem Schema finden Sie im Lernprogramm zum [Erstellen eines Schemas in der Benutzeroberfläche](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) . Das[!DNL  Privacy Consent] Mixin ist mit Schemas kompatibel, die auf den Klassen [!DNL XDM Individual Profile] oder [!DNL XDM ExperienceEvent]basieren.

Nachdem Sie ein Schema mit dem [!DNL Privacy Consent] Mixin erstellt haben, lesen Sie den Abschnitt zum [Erstellen eines Datensatzes](../../catalog/datasets/user-guide.md#create) im DataSet-Benutzerhandbuch, wie Sie einen Datensatz mit einem vorhandenen Schema erstellen.

>[!IMPORTANT]
>
>Wenn Sie Genehmigungsdaten an senden möchten, müssen Sie ein [!DNL Real-time Customer Profile]aktiviertes Schema erstellen, das auf der [!DNL Profile]Klasse basiert, in der das [!DNL XDM Individual Profile] [!DNL Privacy Consent] Mixin enthalten ist. Der Datensatz, den Sie auf der Grundlage dieses Schemas erstellen, muss ebenfalls aktiviert werden [!DNL Profile]. Spezifische Schritte zu [!DNL Real-time Customer Profile] Anforderungen finden Sie in den oben stehenden Lernprogrammen.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Referenzinformationen zum [!DNL Privacy Consent] Mixin.

### Akzeptierte Werte für xdm:optOutType {#optOutType-values}

In der folgenden Tabelle sind die zulässigen Werte für `xdm:optOutType`die

| Wert | Beschreibung |
| --- | --- |
| `general_opt_out` | Die Daten können für keinen Zweck verwendet werden. Dies blockiert in der Regel die Datenerfassung, es sei denn, die Verarbeitungsgrundlage ist nicht &quot;Zustimmung&quot;.<br><br>Bei Verwendung dieses Ausschluss-Typs erhalten die akzeptierten Werte `in` und `out` die folgende kontextuelle Bedeutung:<ul><li>`in`: Der Nutzer **hat seine Einwilligung** zur Verwendung seiner Daten für die allgemeine Verarbeitung gegeben.</li><li>`out`: Der Nutzer stimmt **nicht zu, dass seine Daten für die allgemeine Verarbeitung verwendet werden** .</li></ul>Weitere Informationen finden Sie in der Tabelle zu [akzeptierten Werten für xdm:optOutValue](#choice-optOutValue-values) . |
| `anonymous_analysis` | Die Daten können nicht für allgemeine Webmetriken verwendet werden, für die keine Benutzer-ID erforderlich ist, z. B. wie oft eine bestimmte Seite angezeigt wurde. |
| `device_linking` | Die Daten eines von einem Besucher verwendeten Geräts können nicht mit Daten eines anderen Geräts kombiniert werden, das von demselben Besucher verwendet wird. Geräte werden mit Techniken wie einem gemeinsamen Benutzernamen oder einer E-Mail-Adresse verknüpft, oft über die Adobe Device Co-op oder ein eigenes Gerätediagramm. |
| `pseudonymous_analysis` | Die Daten können nicht für Webmetriken verwendet werden, die von Adobe Analytics bereitgestellt werden. Dies erfordert pseudonyme IDs, um die Pfade zu identifizieren, die Benutzer über eine Website (z. B. einen Trichteranalysebericht) einschlagen, Sitzungen einzurichten und Zuordnungszwecke zu nutzen. |
| `sales_sharing_opt_out` | Die Daten dürfen nicht für Verkaufszwecke oder zur Weitergabe an Dritte verwendet werden.<br><br>Bei Verwendung dieses Ausschluss-Typs erhalten die akzeptierten Werte `in` und `out` die folgende kontextuelle Bedeutung:<ul><li>`in`: Der Nutzer **hat seine Einwilligung** zur Verwendung seiner Daten für Verkaufs- und Freigabezwecke erteilt.</li><li>`out`: Der Nutzer stimmt **nicht zu, dass** seine Daten für Verkaufs- und Freigabezwecke verwendet werden.</li></ul>Weitere Informationen finden Sie in der Tabelle zu [akzeptierten Werten für xdm:optOutValue](#choice-optOutValue-values) . |

### Akzeptierte Werte für xdm:baseOfProcessing {#basisOfProcessing-values}

In der folgenden Tabelle sind die zulässigen Werte für `xdm:basisOfProcessing`die

| Wert | Beschreibung |
| --- | --- |
| `consent` **(Standard)** | Die Datenerfassung für den angegebenen Zweck ist zulässig, da die Person ausdrücklich ihre Erlaubnis erteilt hat. Dies ist der Standardwert, `xdm:basisOfProcessing` wenn kein anderer Wert angegeben wird. <br><br>**WICHTIG **: Die Werte für`xdm:choice`und`xdm:optOutValue`werden nur berücksichtigt, wenn`xdm:basisOfProcessing`auf`consent`. Wenn`xdm:basisOfProcessing`stattdessen einer der anderen in dieser Tabelle aufgeführten Werte verwendet wird, werden die Einwilligungsentscheidungen des Einzelnen ignoriert. |
| `compliance` | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `contract` | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertraglichen Verpflichtungen mit der Einzelperson nachzukommen. |
| `legitimate_interest` | Das legitime Geschäftsinteresse, diese Daten für den angegebenen Zweck zu erheben und zu verarbeiten, überwiegt den potenziellen Schaden, den sie dem Einzelnen verursachen. |
| `public_interest` | Die Erhebung von Daten zu dem festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt durchzuführen. |
| `vital_interest` | Die Erhebung von Daten für den angegebenen Zweck ist zum Schutz der vitalen Interessen des Einzelnen erforderlich. |

### Akzeptierte Werte für xdm:choice und xdm:optOutValue {#choice-optOutValue-values}

In der folgenden Tabelle sind die zulässigen Werte für `xdm:choice` und `xdm:optOutValue`:

| Wert | Beschreibung |
| --- | --- |
| `pending` | Das System hat vom Kunden noch keine Informationen über die Zustimmung erhalten. Kann für die erste Seite einer Website verwendet werden, während die Zustimmung eingeholt wird. Es kann auch verwendet werden, um anzugeben, dass die Zustimmung &quot;angenommen&quot;und nicht explizit angegeben wird. |
| `in` | Der Benutzer hat sich für die Einwilligung entschieden. Mit anderen Worten, sie **stimmen** der Verwendung ihrer Daten zu, wie sie in der betreffenden Einwilligung angegeben ist. |
| `out` | Der Benutzer hat sich von der Voreinstellung für die Zustimmung abgemeldet. Mit anderen Worten, sie stimmen **nicht** der Verwendung ihrer Daten zu, wie sie in der betreffenden Einwilligung angegeben ist. |
| `not_applicable` | Die betreffende Präferenz für die Zustimmung gilt nicht für den Kunden. |
| `not_provided` | Der Kunde hat keine Informationen zur Präferenz für seine Zustimmung vorgelegt. |
| `unknown` | Die Informationen des Kunden zur Einwilligung sind unbekannt. |

### Akzeptierte Werte für xdm:type {#type-values}

In der folgenden Tabelle sind die zulässigen Werte für `xdm:type`die

| Wert | Beschreibung |
| --- | --- |
| `ads` | Anzeigen, die von Websites ohne Bezug angezeigt werden können. |
| `content` | Inhalte auf Ihrer Website. |
| `customer_support` | Daten zum Kundensupport. |
| `email` | E-Mail-Nachrichten. |
| `iot` | Daten zum &quot;Internet der Dinge&quot; (IoT). |
| `in_app_messages` | In-App-Nachrichten. |
| `in_home` | In-Home-Nachrichten. |
| `in_store` | In-Store-Nachrichten. |
| `in_vehicle` | Fahrzeuginterne Meldungen. |
| `offers` | Besondere Angebote. |
| `phone_calls` | Daten zu Telefongesprächen. |
| `push_notifications` | Push-Benachrichtigungen. |
| `sms` | SMS-Nachrichten. |
| `social_media` | Social-Media-Inhalte |
| `snail_mail` | Nachrichten, die über herkömmliche Postleitzahlen gesendet werden. |
| `third_party_content` | Auf Ihrer Website angezeigte Inhalte oder Artikel, die von einer nicht verwandten Entität bereitgestellt werden. |
| `third_party_offers` | Angebote oder Anzeigen, die auf Ihrer Website von einer unabhängigen Stelle angezeigt werden. |

### Vollständiges [!DNL Privacy Consent] Schema {#full-schema}

Das folgende JSON stellt das vollständige [!DNL Privacy Consent] Schema dar, wie es in der Schema-Registrierung angezeigt wird:

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```
