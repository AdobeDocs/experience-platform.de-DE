---
title: _container
description: Anzeigen des gesamten Tag-Containers in einem einzelnen Objekt.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

Das `_satellite._container`-Objekt enthält die vollständige Konfiguration und den Laufzeitkontext der Tag-Eigenschaft, die auf der Seite geladen wird. Alle Informationen wie Regeln, Datenelemente, Erweiterungen und Umgebungen sind in diesem Objekt verfügbar. Der Hauptzweck besteht darin, Sie beim Debuggen Ihrer Implementierung zu unterstützen, damit Sie genau sehen können, welche Logik bereitgestellt oder veröffentlicht wird.

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>Dieses Objekt dient nur Debugging-Zwecken. Binden Sie keine Produktionslogik an dieses Objekt, referenzieren Sie dieses Objekt nicht in Ihrer Implementierung oder bearbeiten Sie keine Werte in diesem Objekt. Die Verfügbarkeit von Eigenschaften oder Namen innerhalb dieses Objekts kann von Adobe jederzeit geändert werden.

## Verfügbare Felder

Die folgenden Objekte stehen als Referenz zur Verfügung:

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

Das `_satellite._container.buildInfo`-Objekt enthält eine Kopie von [`_satellite.buildInfo`](buildinfo.md).

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

Das `_satellite._container.company`-Objekt enthält eine Kopie von [`_satellite.company`](company.md).

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

Das `_satellite._container.dataElements`-Objekt stellt einen Verweis auf alle Datenelemente in Ihrer Tag-Eigenschaft bereit.

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

Jedes Datenelement enthält die folgenden Eigenschaften:

| Name | Typ | Beschreibung |
|---|---|---|
| **`modulePath`** | `string` | Der Pfad der JavaScript-Datei, die die Logik dieses Datenelementtyps bestimmt. |
| **`settings`** | `Settings` | Die Einstellungen des Datenelements. Die Eigenschaften in diesem Objekt hängen vom Datenelementtyp ab. |

## `environment`

Das `_satellite._container.environment`-Objekt enthält eine Kopie von [`_satellite.environment`](environment.md).

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

Das `_satellite._container.extensions`-Objekt listet alle Erweiterungen auf, die in der Tag-Eigenschaft veröffentlicht wurden.

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

Jede Erweiterung umfasst die folgenden Eigenschaften:

| Name | Typ | Beschreibung |
|---|---|---|
| **`displayName`** | `string` | Der Anzeigename der Erweiterung. |
| **`hostedLibFilesUrl`** | `string` | Der Speicherort im CDN, in dem sich die Erweiterung befindet. |
| **`modules`** | `Modules` | Die JavaScript-Logik für alle Ereignisse, Aktionen, Bedingungen und Datenelemente, die von der Erweiterung verwendet werden. Der Inhalt dieses Objekts ist für jede Erweiterung unterschiedlich. |

## `property`

Das `_satellite._container.property`-Objekt stellt Informationen zur Tag-Eigenschaft selbst bereit.

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| Name | Typ | Beschreibung |
|---|---|---|
| **`id`** | `string` | Die eindeutige Kennung für die Tag-Eigenschaft. |
| **`name`** | `string` | Der Anzeigename für die Tag-Eigenschaft. |
| **`settings`** | `PropertySettings` | Einstellungen für diese Eigenschaft. Siehe Tabelle unten. |

| Name der Einstellung | Typ | Beschreibung |
|---|---|---|
| **`domains`** | `string[]` | Die konfigurierten Domains für die Eigenschaft, wie sie beim [Konfigurieren einer Tag-Eigenschaft“ festgelegt &#x200B;](/help/tags/ui/administration/companies-and-properties.md). |
| **`ruleComponentSequencingEnabled`** | `boolean` | Bestimmt, ob das Kontrollkästchen **[!UICONTROL Run rule components in sequence]** beim Konfigurieren der Tag-Eigenschaft aktiviert ist. |
| **`undefinedVarsReturnEmpty`** | `boolean` | Bestimmt, ob das Kontrollkästchen **[!UICONTROL Return an empty string for undefined data elements]** beim Konfigurieren der Tag-Eigenschaft aktiviert ist. |

## `_container.rules`

Das `rules`-Objekt-Array stellt einen Verweis auf alle Regeln in Ihrer Tag-Eigenschaft bereit.

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

Jede Regel enthält die folgenden Felder:

| Name | Typ | Beschreibung |
|---|---|---|
| **`id`** | `string` | Die eindeutige Kennung der Regel. |
| **`name`** | `string` | Der Anzeigename der Regel. |
| **`events`** | `Event[]` | Ein Array von Ereignissen, die Sie zum Trigger der Regel konfiguriert haben. |
| **`conditions`** | `Condition[]` | Ein Array von Bedingungen, die zum Trigger der Regel konfiguriert wurden. |
| **`actions`** | `Action[]` | Ein Array von Aktionen, deren Ausführung konfiguriert wurde, wenn die Regel ausgelöst wird. |
