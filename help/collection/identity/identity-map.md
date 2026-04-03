---
title: Verwenden von identityMap in der Datenerfassung
description: Erfahren Sie, wie Sie IdentityMap-Payloads erstellen und senden, um bekannte Besucher über Namespaces hinweg in Ihrer Web SDK-Implementierung zu identifizieren.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# Verwenden von identityMap in der Datenerfassung

Mit dem `identityMap` Payload-Objekt können Sie dem Edge Network mitteilen, wer ein Besucher ist, der über die Geräteebene ([) ](./overview.md). Wenn sich ein Besucher anmeldet, einen Kauf abschließt oder anderweitig bekannt wird, können Sie neben der ECID Kennungen auf Personenebene (CRM-ID, gehashte E-Mail, Treueprogramm-ID usw.) senden. Diese Kennungen auf Personenebene bieten nachgelagerten -Services wertvolle Informationen, damit sie:

* **Aktivität einer Person über Geräte und Kanäle hinweg zuordnen.** [Identity Service](/help/identity-service/home.md) verknüpft die von Ihnen gesendeten Identitäten mit einem [Identitätsdiagramm](/help/identity-service/features/identity-graph-viewer.md) und verbindet das anonyme Verhalten auf Geräteebene mit einer bekannten Person.
* **Erstellen einheitlicher Kundenprofile.** [Echtzeit-Kundenprofil](/help/profile/home.md) verwendet die primäre Identität, die Sie festlegen, um Ereignisse und Attribute in einem einzelnen Profil zu verankern, was eine Segmentierung auf Personenebene und die Erstellung von Zielgruppen ermöglicht.
* **Aktivieren von Zielgruppen für nachgelagerte Ziele.** Viele [Ziele](/help/destinations/home.md) erfordern aufgelöste Identitäten auf Personenebene (Hash-E-Mails, Telefonnummern usw.), um Ihre Zielgruppen mit ihren Benutzerbasen abzugleichen.
* **Orchestrieren von Cross-Channel-Journey.** [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de) verwendet aufgelöste Identitäten, um Journey über E-Mail-, Push- und In-App-Kanäle auf der Grundlage des authentifizierten Verhaltens eines Besuchers Trigger und zu personalisieren.

Auf dieser Seite wird beschrieben, wie Sie `identityMap` Payloads erstellen, die richtigen Einstellungen für jede Identität auswählen und gängige Implementierungsszenarien behandeln.

## Payload-Struktur {#structure}

Der `identityMap` ist ein JSON-Objekt, bei dem jeder Schlüssel der obersten Ebene ein Namespace und der Wert ein Array von Identitätsdeskriptoren ist. Sie können einen oder mehrere Namespaces in eine einzige Payload einbeziehen, wobei jeder Deskriptor drei Felder enthält: `id`, `authenticatedState` und `primary`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| Feld | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `id` | Zeichenfolge | Ja | Der Kennungswert (z. B. `user@example.com` oder `ABC123`). |
| `authenticatedState` | Zeichenfolge | Ja | Wie sicher Sie wissen, dass diese Identität zum Besucher gehört. Gültige Werte sind `ambiguous`, `authenticated` und `loggedOut`. |
| `primary` | Boolesch | Ja | Ob diese Identität die primäre Kennung für das Ereignis sein soll. Es muss genau eine Identität über alle Namespaces `primary: true` markiert werden. |

Die folgenden Abschnitte behandeln jeden Teil der Payload im Detail.

### Namespace-Schlüssel {#namespace-keys}

Jeder Schlüssel der obersten Ebene in `identityMap` ist ein [Identity-Namespace](/help/identity-service/features/namespaces.md) - eine Zeichenfolge, die den Typ der Kennung klassifiziert (z. B. `CRMID`, `Email`, `Phone` oder `LoyaltyId`). Namespaces müssen in Identity Service vorhanden sein, bevor Sie in einer Payload auf sie verweisen. Sie können mehrere Namespace-Schlüssel in dasselbe Ereignis einbeziehen, wenn Sie mehr als eine Kennung für den Besucher haben.

Sie müssen die ECID nicht als Namespace-Schlüssel einschließen. Edge Network fügt die ECID automatisch zur Identity-Payload hinzu. Wenn Sie die ECID explizit einschließen, markieren Sie sie nicht als `primary`, wenn auch eine Identität auf Personenebene vorhanden ist.

### `id` {#id}

Das `id` Feld ist die Kennungszeichenfolge selbst - der Wert, der Experience Platform mitteilt, welche bestimmte Person oder Gerät diese Identität darstellt. Jeder [Identity-Namespace](/help/identity-service/features/namespaces.md) erwartet ein bestimmtes Wertformat, und das Senden eines Werts im falschen Format erstellt eine eindeutige Identität, die nicht mit der korrekt formatierten Version zusammengeführt werden kann, was zu fragmentierten Profilen führt.

Bevor Sie einen Wert in `identityMap` aufnehmen, bereiten Sie ihn entsprechend dem Format vor, das Ihr Ziel-Namespace erwartet:

| Allgemeine Namespace-Typen | So bereiten Sie den Wert vor | Beispiel |
| --- | --- | --- |
| **CRM / interne ID** | Verwenden Sie die genaue Kennung, die Ihr Datensatzsystem zuweist. Halten Sie das Format über alle Ereignisse hinweg konsistent (Groß- und Kleinschreibung, führende Nullen, Präfixe). | `ABC-12345`, `00098765` |
| **E-Mail (unbearbeitet)** | Kleinschreibung der vollständigen E-Mail-Adresse und Kürzung vorangestellter und nachgestellter Leerzeichen. | `user@example.com` |
| **E-Mail (gehasht)** | Kleinbuchstaben verwenden und die E-Mail-Adresse zuerst kürzen und dann mit SHA-256 hashen. Senden Sie die resultierende 64-stellige Hex-Zeichenfolge. Fügen Sie kein Salz hinzu, es sei denn, Ihre Namespace-Definition erfordert eines. | `a1b2c3d4e5f6a7b8c9...` |
| **Telefon (E.164)** | Formatieren Sie die Nummer in [E.164](https://en.wikipedia.org/wiki/E.164): eine vorangestellte `+`, den Ländercode und die Teilnehmernummer ohne Leerzeichen oder Satzzeichen. | `+15551234567` |
| **FPID** | Generieren Sie eine [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122)-Zeichenfolge. Generierungsanforderungen finden [ unter ](./fpid.md)-IDs von Erstanbietern . | `123e4567-e89b-42d3-9456-426614174000` |

Eine vollständige Liste der Standard-Namespaces und ihrer Definitionen finden Sie unter [Übersicht zu Identitäts-Namespaces](/help/identity-service/features/namespaces.md#standard).

>[!TIP]
>
>Beim `id` wird zwischen Groß- und Kleinschreibung unterschieden. `User@Example.com` und `user@example.com` werden als zwei separate Identitäten behandelt. Normalisieren Sie die Groß-/Kleinschreibung, bevor Sie den Wert senden (in der Regel durch Kleinschreibung von E-Mails und Abschneiden von Leerzeichen), um zu vermeiden, dass im Diagramm doppelte Identitäten erstellt werden.

#### Erfassen von `id` zur Laufzeit {#collect-id}

Die benötigte Kennung ist selten direkt auf der Seite verfügbar. Zu den gängigen Sammelstrategien gehören:

* **Datenschicht**: Lesen Sie die Kennung aus der Datenschicht Ihrer Site, nachdem sich der Besucher angemeldet hat. Dieser Speicherort ist der zuverlässigste Ansatz, da die Datenschicht durch das Backend Ihrer Anwendung gefüllt wird und den authentifizierten Sitzungsstatus widerspiegelt.
* **Authentifizierungs-Token oder Sitzungs** Cookie: Dekodieren Sie die Kennung aus einem JWT- oder Sitzungs-Cookie, das Ihr Authentifizierungssystem setzt, oder suchen Sie sie nach. Überprüfen Sie, ob das Token noch aktiv ist, bevor Sie den Wert verwenden.
* **Server-seitige Anreicherung**: Verwenden Sie [Datenvorbereitung für die ](/help/datastreams/data-prep.md) oder eine [Ereignisweiterleitungsregel](/help/tags/ui/event-forwarding/overview.md), um die Kennung auf der Edge zuzuordnen oder zu transformieren, bevor sie nachgelagerte Services erreicht. Dieser Speicherort ist nützlich, wenn der Client nur über ein undurchsichtiges Sitzungstoken verfügt, das einer internen ID auf der Server-Seite zugeordnet ist.

>[!TIP]
>
>Wenn ein gegebener `id` in eine leere Zeichenfolge, ein leeres `null` oder ein leeres `undefined` aufgelöst wird, schließen Sie den Namespace nicht in die `identityMap` ein. Durch das Senden eines leeren `id` wird ein beschädigter Identitätseintrag erstellt. Schützen Sie Ihre Implementierung mit einer Prüfung, bevor Sie die Payload erstellen.

### `authenticatedState` {#authenticated-state}

Das Feld `authenticatedState` gibt den nachgelagerten Services an, wie viel Vertrauen einer bestimmten Identität gesetzt werden soll. Die folgenden Werte sind für dieses Feld gültig:

| Wert | Verwendungszeitpunkt |
| --- | --- |
| **`authenticated`** | Der Besucher hat seine Identität während der aktuellen Sitzung aktiv nachgewiesen (z. B. durch Anmeldung mit Anmeldeinformationen, Abschluss der Makrofinanzhilfe oder ähnliche Verifizierung). |
| **`loggedOut`** | Der Besucher wurde zuvor authentifiziert, hat sich aber seitdem abgemeldet. Die Identität ist weiterhin mit dem Gerät verknüpft, aber die Sitzung ist nicht mehr aktiv. |
| **`ambiguous`** | Die Identität kann nicht als zum aktuellen Besucher gehörend bestätigt werden. Verwenden Sie diesen Wert für Kennungen auf Geräteebene wie FPIDs oder alle Kennungen, bei denen die Authentifizierung noch nicht stattgefunden hat. |

>[!TIP]
>
>Der `authenticatedState` beeinflusst, wie Adobe Experience Platform Identity Service Identitätsdiagramme erstellt und zusammenführt. Das Senden von `authenticated` für eine nicht verifizierte Identität kann zu falschen geräteübergreifenden Links führen, die schwer rückgängig zu machen sind.

### `primary` {#primary-identity}

Jede `identityMap`-Payload muss genau eine als `primary: true` markierte Identität aufweisen. Die primäre Identität bestimmt, welche Identität als Anker für das Ereignis in Experience Platform verwendet wird.

Befolgen Sie beim Festlegen der primären Identität die folgenden Richtlinien:

* **Wenn eine Identität auf Personenebene verfügbar ist** (der Besucher ist angemeldet), markieren Sie den Namespace auf Personenebene als primär und die ECID als nicht primär. Dadurch wird Experience Platform angewiesen, das Ereignis an der Person und nicht am Gerät zu verankern.
* **Wenn nur Identitäten auf Geräteebene verfügbar sind** (der Besucher ist anonym), wird die ECID automatisch als primäre Identität verwendet. Sie müssen die ECID nicht in Ihr `identityMap` aufnehmen - Edge Network fügt sie automatisch hinzu.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## Senden von identityMap in Ihrer Implementierung {#send-identity}

>[!BEGINTABS]

>[!TAB JavaScript-Bibliothek]

Übergeben Sie die `identityMap` im `xdm`-Objekt eines [`sendEvent`](/help/collection/js/commands/sendevent/overview.md):

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB Web SDK-Tag-Erweiterung]

Verwenden Sie den Datenelementtyp [Identitätszuordnung](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) um Ihre Identitäts-Payload in der Tags-Benutzeroberfläche zu erstellen:

1. Erstellen Sie ein Datenelement mit der **[!UICONTROL Adobe Experience Platform Web SDK]**-Erweiterung und dem **[!UICONTROL Identity map]** Datenelementtyp.
2. Fügen Sie Identitäten hinzu, indem Sie den Namespace, das Datenelement oder den Wert, das bzw. der für die Kennung aufgelöst wird, und den authentifizierten Status angeben.
3. Eine Identität als primär markieren.
4. Referenzieren Sie dieses Datenelement in Ihrer **[!UICONTROL Send event]** Aktion unter **[!UICONTROL Identity map]**.

>[!ENDTABS]

## Häufige Szenarien {#common-scenarios}

+++**Anmelden**

Wenn sich ein Besucher anmeldet, senden Sie seine Kennung auf Personenebene mit `authenticatedState: "authenticated"` und `primary: true`. Schließen Sie diese Identität beim ersten Ereignis nach der Authentifizierung und bei allen nachfolgenden Ereignissen in der Sitzung ein.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**Abmelden**

Wenn sich ein Besucher abmeldet, aktualisieren Sie `authenticatedState` auf `loggedOut`, wobei die gleiche Kennung beibehalten wird. Dadurch wird die Zuordnung zwischen Gerät und Person beibehalten, während signalisiert wird, dass die Sitzung nicht mehr aktiv ist.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

Nach dem Abmelden ist die ECID wieder die effektive primäre Identität (die Edge Network wendet sie automatisch an). Markieren Sie keine andere Identität auf Personenebene als primär, es sei denn, der Besucher meldet sich mit einem anderen Konto an.

>[!IMPORTANT]
>
>Beenden Sie den Versand der Kennung nicht vollständig nach dem Abmelden. Beim Wechsel von `authenticated` zu `loggedOut` wird nachgelagerten Services mitgeteilt, dass die Sitzung beendet wurde. Wenn Sie die Kennung vollständig weglassen, entsteht eine Lücke im Identitätsdiagramm, die zu fragmentierten Profilen führen kann.

+++

+++**Mehrere Namespaces**

Sie können mehrere Identity-Namespaces im selben Ereignis senden. Dieses Szenario tritt häufig auf, wenn ein Besucher angemeldet ist und Sie über mehrere Kennungen verfügen (z. B. eine CRM-ID, eine gehashte E-Mail-Adresse und eine Treueprogramm-ID). Alle bekannten Kennungen einschließen, nur eine als primär markieren und die anderen auf `primary: false` setzen.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>Das Senden mehrerer Namespaces mit demselben `authenticatedState` für dasselbe Ereignis gibt dem Identity Service das stärkste Signal zur Verknüpfung dieser Identitäten. Alle verfügbaren Kennungen am Authentifizierungspunkt einbeziehen, anstatt sie auf separate Ereignisse zu verteilen.

+++

+++**Anonyme Besucher**

Für anonyme Besucher ist es in der Regel nicht erforderlich, überhaupt `identityMap` zu senden. Edge Network weist automatisch eine ECID zu und verwendet diese als primäre Identität. Wenn Sie [Erstanbieter-Geräte-IDs](./fpid.md) verwenden, ist die FPID die einzige Identität, die Sie für anonyme Besucher einschließen müssen.

+++

## Auswirkungen von identityMap auf das Identitätsdiagramm {#identity-graph}

Jede `identityMap`-Payload, die Experience Platform erreicht, wird von [Identity Service](/help/identity-service/home.md) verarbeitet, der die von Ihnen gesendeten Identitäten in einem [Identitätsdiagramm](/help/identity-service/features/identity-graph-viewer.md) verknüpft. Welche Namespaces Sie einbeziehen, wie Sie `authenticatedState` festlegen und welche Identität Sie als `primary` markieren, bestimmt direkt, wie Identity Service diese Diagramme erstellt und zusammenführt.

Wichtige Verhaltensweisen, die zu beachten sind:

* **Identitäten, die für dasselbe Ereignis gesendet werden, sind miteinander verknüpft.** Wenn Sie beim selben `sendEvent`-Aufruf eine CRMID und einen E-Mail-Namespace einbeziehen, erstellt Identity Service eine Verknüpfung zwischen diesen beiden Identitäten. Wenn Kennungen auf verschiedene Ereignisse verteilt werden, entstehen schwächere Links und fragmentierte Diagramme können die Folge sein.
* **Die `primary` Identität verankert das Ereignis im Echtzeit-Kundenprofil.** Profil verwendet die primäre Identität, um zu bestimmen, zu welchem Profil das Ereignis gehört. Wenn Sie die falsche Identität als primär kennzeichnen (z. B. wenn Sie ECID als primär festlegen, wenn eine ID auf Personenebene verfügbar ist), können Ereignisse für Profile auf Geräteebene und nicht für Profile auf Personenebene gespeichert werden.
* **Die `authenticatedState` beeinflusst die Konfidenz von Diagrammen.** Senden von `authenticated` für eine Identität, die noch nicht verifiziert wurde, kann zu falschen geräteübergreifenden Links führen, die schwer rückgängig zu machen sind. Verwenden Sie `authenticated` nur, wenn der Besucher während der aktuellen Sitzung aktiv seine Identität bewiesen hat.

Wenn Ihre Implementierung Regeln [zur Verknüpfung von Identitätsdiagrammen](/help/identity-service/identity-graph-linking-rules/overview.md) verwendet (z. B. Namespace-Priorität oder Algorithmus zur Identitätsoptimierung), lesen Sie das [Implementierungshandbuch](/help/identity-service/identity-graph-linking-rules/implementation-guide.md) um zu verstehen, wie diese Regeln mit den Identitäten interagieren, die Sie über `identityMap` senden.

>[!NOTE]
>
>Die `identityMap` wird nur gesendet, wenn die Web-SDK eine Anfrage an die Edge Network sendet, die durch den Einverständnisstatus des Besuchers geprüft wird. Wenn Ihre Implementierung `defaultConsent: "pending"` verwendet, werden Identitäten erst gesendet, nachdem die Zustimmung erteilt wurde. Siehe [Einverständnis und Identität](./consent.md) für Details.
