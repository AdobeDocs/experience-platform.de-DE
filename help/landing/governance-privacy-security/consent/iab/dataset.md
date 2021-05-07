---
keywords: Experience Platform;Home;IAB;IAB 2.0;Zustimmung;Zustimmung
solution: Experience Platform
title: Erstellen von Datenbeständen zur Erfassung von IAB TCF 2.0-Genehmigungsdaten
topic-legacy: privacy events
description: In diesem Dokument werden Schritte zur Einrichtung der beiden erforderlichen Datensätze zur Erfassung der IAB TCF 2.0-Genehmigungsdaten beschrieben.
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 3%

---

# Erstellen von Datensätzen zur Erfassung von IAB TCF 2.0-Genehmigungsdaten

Damit Adobe Experience Platform die Daten zur Kundengenehmigung gemäß IAB [!DNL Transparency & Consent Framework] (TCF) 2.0 verarbeiten kann, müssen diese Daten an Datasets gesendet werden, deren Schemas TCF 2.0-Einwilligungsfelder enthalten.

Für die Erfassung von TCF 2.0-Genehmigungsdaten sind insbesondere zwei Datensätze erforderlich:

* Ein Datensatz, der auf der [!DNL XDM Individual Profile]-Klasse basiert und für die Verwendung in [!DNL Real-time Customer Profile] aktiviert ist.
* Ein Datensatz, der auf der [!DNL XDM ExperienceEvent]-Klasse basiert.

In diesem Dokument werden Schritte zur Einrichtung dieser beiden Datensätze zur Erhebung der IAB TCF 2.0-Genehmigungsdaten beschrieben. Eine Übersicht über den vollständigen Arbeitsablauf zum Konfigurieren der Plattformdatenvorgänge für TCF 2.0 finden Sie in der [IAB TCF 2.0 Compliance-Übersicht](./overview.md).

## Voraussetzungen 

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)](../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemas.
* [Adobe Experience Platform-Identitätsdienst](../../../../identity-service/home.md): Ermöglicht Ihnen, Kunden-Identitäten von unterschiedlichen Datenquellen über Geräte und Systeme hinweg zu überbrücken.
   * [Identitäts-Namensraum](../../../../identity-service/namespaces.md): Die Daten zur Kundenidentität müssen unter einem bestimmten, vom Identitätsdienst anerkannten Namensraum bereitgestellt werden.
* [Echtzeit-Profil](../../../../profile/home.md): Ermöglicht  [!DNL Identity Service] die Erstellung detaillierter Kundendaten aus Ihren Datensätzen in Echtzeit. [!DNL Real-time Customer Profile] ruft Daten aus dem Data Lake ab und behält die Profil der Kunden in einem eigenen separaten Datenspeicher bei.

## [!UICONTROL Gruppenstruktur ] der Datenschutzdetails  {#structure}

Die Feldgruppe [!UICONTROL Datenschutzdetails] enthält Schema-Felder für die Kundengenehmigung, die für den TCF 2.0-Support erforderlich sind. Es gibt zwei Versionen dieser Feldgruppe: eine mit der Klasse [!DNL XDM Individual Profile] und die andere mit der Klasse [!DNL XDM ExperienceEvent] kompatibel.

Die folgenden Abschnitte erläutern die Struktur jeder dieser Feldgruppen, einschließlich der Daten, die sie während der Erfassung erwarten.

### Profil-Feldgruppe {#profile-field-group}

Bei Schemas, die auf [!DNL XDM Individual Profile] basieren, stellt die Feldgruppe [!UICONTROL Datenschutzdetails] ein einzelnes Zuordnungsfeld bereit, `xdm:identityPrivacyInfo`, das die Kundenidentitäten ihren TCF-Genehmigungsvoreinstellungen zuordnet. Die folgende JSON-Datei ist ein Beispiel für die Art von Daten, die `xdm:identityPrivacyInfo` bei der Datenerfassung erwartet:

```json
{
  "xdm:identityPrivacyInfo": {
      "ECID": {
        "13782522493631189": {
          "xdm:identityIABConsent": {
            "xdm:consentTimestamp": "2020-04-11T05:05:05Z",
            "xdm:consentString": {
              "xdm:consentStandard": "IAB TCF",
              "xdm:consentStandardVersion": "2.0",
              "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
              "xdm:gdprApplies": true,
              "xdm:containsPersonalData": false
            }
          }
        }
      }
    }
}
```

Wie das Beispiel zeigt, entspricht jeder Schlüssel auf der Stammebene von `xdm:identityPrivacyInfo` einem vom Identitätsdienst erkannten Identitäts-Namensraum. Jede Namensraum-Eigenschaft muss wiederum über mindestens eine Untereigenschaft verfügen, deren Schlüssel mit dem entsprechenden Identitätswert des Kunden für diesen Namensraum übereinstimmt. In diesem Beispiel wird der Kunde mit einem Experience Cloud-ID-Wert (`ECID`) von `13782522493631189` identifiziert.

>[!NOTE]
>
>Während im obigen Beispiel ein Namensraum/Wert-Paar zur Darstellung der Kundenidentität verwendet wird, können Sie zusätzliche Schlüssel für andere Namensraum hinzufügen. Jeder Namensraum kann über mehrere Identitätswerte verfügen, jeweils mit eigenen TCF-Voreinstellungen für die Zustimmung.

Innerhalb des Identitätswertobjekts befindet sich ein einzelnes Feld, `xdm:identityIABConsent`. Dieses Objekt erfasst die TCF-Zustimmungswerte des Kunden für den angegebenen Identitäts-Namensraum und den angegebenen Wert. Die in diesem Feld enthaltenen Untereigenschaften sind unten aufgeführt:

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:consentTimestamp` | Ein [ISO 8601](https://www.ietf.org/rfc/rfc3339.txt) Zeitstempel, der angibt, wann sich die TCF-Zustimmungswerte geändert haben. |
| `xdm:consentString` | Ein Objekt, das die aktualisierten Daten zur Zustimmung des Kunden und andere Kontextinformationen enthält. Weitere Informationen zu den erforderlichen Untereigenschaften dieses Objekts finden Sie im Abschnitt [Eigenschaften der Einwilligungszeichenfolge](#consent-string). |

### Ereignis-Feldgruppe {#event-field-group}

Bei Schemas, die auf [!DNL XDM ExperienceEvent] basieren, stellt die Feldgruppe [!UICONTROL Datenschutzdetails] ein einzelnes Feld vom Typ Array bereit: `xdm:consentStrings`. Jedes Element in diesem Array muss ein Objekt sein, das die erforderlichen Eigenschaften für eine TCF-Genehmigungszeichenfolge enthält, ähnlich dem Feld `xdm:consentString` in der Feldgruppe &quot;Profil&quot;. Weitere Informationen zu diesen Untereigenschaften finden Sie im [nächsten Abschnitt](#consent-string).

```json
{
  "xdm:consentStrings": [
    {
      "xdm:consentStandard": "IAB TCF",
      "xdm:consentStandardVersion": "2.0",
      "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
      "xdm:gdprApplies": true,
      "xdm:containsPersonalData": false
    }
  ]
}
```

### Eigenschaften von Genehmigungszeichenfolgen {#consent-string}

Beide Versionen der Feldgruppe [!UICONTROL Datenschutzdetails] erfordern mindestens ein Objekt, das die erforderlichen Felder erfasst, die die TCF-Zustimmungszeichenfolge für den Kunden beschreiben. Die folgenden Eigenschaften werden erläutert:

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:consentStandard` | Der Rahmen für die Zustimmung, für den die Daten gelten. Für die TCF-Kompatibilität muss der Wert `IAB TCF` sein. |
| `xdm:consentStandardVersion` | Die Versionsnummer des Genehmigungsrahmens, die durch `xdm:consentStandard` angegeben wird. Für die TCF 2.0-Kompatibilität muss der Wert `2.0` sein. |
| `xdm:consentStringValue` | Die Zustimmungszeichenfolge, die von der Plattform für das Zustimmungsmanagement (CMP) basierend auf den ausgewählten Einstellungen des Kunden generiert wurde. |
| `xdm:gdprApplies` | Ein boolescher Wert, der angibt, ob der GDPR für diesen Kunden gilt. Der Wert muss auf `true` gesetzt werden, damit eine TCF 2.0-Durchsetzung erfolgt. Die Standardeinstellung ist `true`, wenn nicht enthalten. |
| `xdm:containsPersonalData` | Ein boolescher Wert, der angibt, ob die Aktualisierung der Zustimmung personenbezogene Daten enthält. Die Standardeinstellung ist `false`, wenn nicht enthalten. |

## Schemas zur Kundeneinwilligung {#create-schemas} erstellen

Um Datasets zu erstellen, die Genehmigungsdaten erfassen, müssen Sie zunächst XDM-Schema erstellen, auf denen diese Datensätze basieren.

Wählen Sie in der Benutzeroberfläche &quot;Plattform&quot;im linken Navigationsbereich **[!UICONTROL Schema]** aus, um den Arbeitsbereich [!UICONTROL Schemas] zu öffnen. Gehen Sie von hier aus wie folgt vor, um jedes erforderliche Schema zu erstellen.

>[!NOTE]
>
>Wenn Sie vorhandene XDM-Schema haben, die Sie stattdessen zur Erfassung von Genehmigungsdaten verwenden möchten, können Sie diese Schema bearbeiten, anstatt neue zu erstellen. Wenn jedoch ein bestehendes Schema für die Verwendung im Echtzeit-Kundendienst aktiviert wurde, kann seine primäre Identität nicht ein direkt identifizierbares Feld sein, das für interessensbasierte Werbung, wie z. B. eine E-Mail-Adresse, nicht verwendet werden darf. Wenden Sie sich an Ihren Rechtsbeistand, wenn Sie nicht sicher sind, welche Felder eingeschränkt sind.
>
>Darüber hinaus können bei der Bearbeitung vorhandener Schema nur additive (nicht-innovative) Änderungen vorgenommen werden. Weitere Informationen finden Sie im Abschnitt zu den [Grundsätzen der Schema-Evolution](../../../../xdm/schema/composition.md#evolution).

### Erstellen Sie ein Schema für die Einwilligung in einen Datensatz {#profile-schema}

Wählen Sie im Arbeitsbereich **[!UICONTROL Schemas]** **[!UICONTROL Schema erstellen]** und wählen Sie dann **[!UICONTROL XDM Individuelles Profil]** aus der Dropdownliste.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Das Symbol [!DNL Schema Editor] wird angezeigt und zeigt die Struktur des Schemas auf der Arbeitsfläche an. Verwenden Sie die rechte Leiste, um einen Namen und eine Beschreibung für das Schema anzugeben, und wählen Sie dann **[!UICONTROL Hinzufügen]** im Bereich **[!UICONTROL Feldgruppen]** links auf der Arbeitsfläche aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Das Dialogfeld **[!UICONTROL Hinzufügen Feldgruppen]** wird angezeigt. Wählen Sie **[!UICONTROL Datenschutzdetails]** aus der Liste. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzuschränken, um die Feldgruppe einfacher zu finden. Wählen Sie nach Auswahl der Feldgruppe **[!UICONTROL Hinzufügen Feldgruppen]** aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Die Arbeitsfläche wird wieder angezeigt und zeigt an, dass das Feld `identityPrivacyInfo` der Schema-Struktur hinzugefügt wurde.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Wiederholen Sie die oben genannten Schritte, um dem Schema die folgenden zusätzlichen Feldgruppen hinzuzufügen:

* [!UICONTROL IdentityMap]
* [!UICONTROL Datenerfassungsregion für Profil]
* [!UICONTROL Demografische Details]
* [!UICONTROL Persönliche Kontaktangaben]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-field-groups.png)

Wenn Sie ein vorhandenes Schema bearbeiten, das bereits für die Verwendung in [!DNL Real-time Customer Profile] aktiviert wurde, wählen Sie **[!UICONTROL Speichern]**, um Ihre Änderungen zu bestätigen, bevor Sie mit dem Abschnitt [Erstellen eines Datensatzes auf der Grundlage Ihres Schemas für die Einwilligung](#dataset) fortfahren. Wenn Sie ein neues Schema erstellen, führen Sie die im Unterabschnitt unten beschriebenen Schritte aus.

#### Schema zur Verwendung in [!DNL Real-time Customer Profile] aktivieren

Damit Platform die von ihr empfangenen Daten für bestimmte Profil der Zustimmung verknüpfen kann, muss das Schema für die Zustimmung für die Verwendung in [!DNL Real-time Customer Profile] aktiviert werden.

>[!NOTE]
>
>Das in diesem Schema dargestellte Beispiel verwendet das zugehörige `identityMap`-Feld als primäre Identität. Wenn Sie ein anderes Feld als primäre Identität festlegen möchten, stellen Sie sicher, dass Sie einen indirekten Bezeichner wie eine Cookie-ID verwenden und nicht ein direkt identifizierbares Feld, das nicht für interessensbasierte Werbung wie eine E-Mail-Adresse verwendet werden darf. Wenden Sie sich an Ihren Rechtsbeistand, wenn Sie nicht sicher sind, welche Felder eingeschränkt sind.
>
>Schritte zum Festlegen eines primären Identitätsfelds für ein Schema finden Sie im Tutorial [Schema-Erstellung](../../../../xdm/tutorials/create-schema-ui.md#identity-field).

Um das Schema für [!DNL Profile] zu aktivieren, wählen Sie in der linken Leiste den Namen des Schemas aus, um das Dialogfeld **[!UICONTROL Schema properties]** in der rechten Leiste zu öffnen. Wählen Sie von hier die Umschalter-Schaltfläche **[!UICONTROL Profil]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Es wird ein Popup mit einer fehlenden primären Identität angezeigt. Aktivieren Sie das Kontrollkästchen für die Verwendung einer alternativen primären Identität, da die primäre Identität im Feld `identityMap` enthalten ist.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Wählen Sie **[!UICONTROL Speichern]**, um Ihre Änderungen zu bestätigen.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Erstellen eines zeitreihenbasierten Schemas für die Zustimmung {#event-schema}

Wählen Sie im Arbeitsbereich **[!UICONTROL Schemas]** **[!UICONTROL Schema erstellen]** und wählen Sie dann **[!UICONTROL XDM ExperienceEvent]** aus der Dropdownliste.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Das Symbol [!DNL Schema Editor] wird angezeigt und zeigt die Struktur des Schemas auf der Arbeitsfläche an. Verwenden Sie die rechte Leiste, um einen Namen und eine Beschreibung für das Schema anzugeben, und wählen Sie dann **[!UICONTROL Hinzufügen]** im Bereich **[!UICONTROL Feldgruppen]** links auf der Arbeitsfläche aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Das Dialogfeld **[!UICONTROL Hinzufügen Feldgruppen]** wird angezeigt. Wählen Sie **[!UICONTROL Datenschutzdetails]** aus der Liste. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzuschränken, um die Feldgruppe einfacher zu finden. Wenn Sie eine Feldgruppe ausgewählt haben, wählen Sie **[!UICONTROL Hinzufügen Feldgruppen]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Die Arbeitsfläche wird wieder angezeigt und zeigt an, dass das `consentStrings`-Array zur Schema-Struktur hinzugefügt wurde.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Wiederholen Sie die oben genannten Schritte, um dem Schema die folgenden zusätzlichen Feldgruppen hinzuzufügen:

* [!UICONTROL IdentityMap]
* [!UICONTROL Umgebung]
* [!UICONTROL Webdetails]
* [!UICONTROL Implementierungsdetails]

Nachdem die Feldgruppen hinzugefügt wurden, beenden Sie die Auswahl von **[!UICONTROL Speichern]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Erstellen Sie Datensätze basierend auf Ihren Schemas für die Zustimmung {#datasets}

Für jedes der oben beschriebenen erforderlichen Schema müssen Sie einen Datensatz erstellen, der letztendlich die Daten zur Einwilligung Ihrer Kunden erfasst. Der Datensatz, der auf dem Schema record basiert, muss für [!DNL Real-time Customer Profile] aktiviert sein, während der Datensatz, der auf dem Schema der Zeitreihe **basiert, nicht** [!DNL Profile]-fähig sein sollte.

Wählen Sie zunächst **[!UICONTROL Datensätze]** in der linken Navigation und dann **[!UICONTROL Datensatz erstellen]** in der oberen rechten Ecke aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Wählen Sie auf der nächsten Seite **[!UICONTROL Datensatz aus Schema]** erstellen.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

Der Arbeitsablauf **[!UICONTROL Datensatz aus Schema]** erstellen wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Schema auswählen]**. Suchen Sie in der bereitgestellten Liste nach einem der Schema für die Zustimmung, die Sie zuvor erstellt haben. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzugrenzen und Ihr Schema einfacher zu finden. Klicken Sie auf das Optionsfeld neben dem gewünschten Schema und wählen Sie dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

Der Schritt **[!UICONTROL Datensatz konfigurieren]** wird angezeigt. Geben Sie einen eindeutigen, leicht identifizierbaren Namen und eine Beschreibung für den Datensatz ein, bevor Sie **[!UICONTROL Fertigstellen]** auswählen.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

Die Detailseite für den neu erstellten Datensatz wird angezeigt. Wenn der Datensatz auf Ihrem Zeitreihen-Schema basiert, ist der Vorgang abgeschlossen. Wenn der Datensatz auf Ihrem Record-Schema basiert, besteht der letzte Schritt darin, den Datensatz für die Verwendung in [!DNL Real-time Customer Profile] zu aktivieren.

Wählen Sie in der rechten Leiste den Umschalter **[!UICONTROL Profil]** und wählen Sie dann **[!UICONTROL Aktivieren]** im Bestätigungs-Popup, um das Schema für [!DNL Profile] zu aktivieren.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Führen Sie die oben genannten Schritte erneut aus, um den anderen erforderlichen Datensatz für die TCF 2.0-Kompatibilität zu erstellen.

## Nächste Schritte

In diesem Lernprogramm haben Sie zwei Datensätze erstellt, die jetzt zur Erfassung von Daten zur Kundeneinwilligung verwendet werden können:

* Ein Datensatzbasierter Datensatz, der für die Verwendung im Echtzeit-Customer-Profil aktiviert ist.
* Ein zeitreihenbasierter Datensatz, der nicht für [!DNL Profile] aktiviert ist.

Sie können nun zum IAB TCF 2.0-Überblick [zurückkehren, um den Prozess zur Konfiguration der Plattform für TCF 2.0-Konformität fortzusetzen.](./overview.md#merge-policies)
