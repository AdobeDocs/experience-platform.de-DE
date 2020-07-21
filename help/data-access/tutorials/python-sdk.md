---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Secure Python Data Access SDK
topic: tutorial
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Sicheres [!DNL Python][!DNL Data Access] SDK

Das Secure [!DNL Python][!DNL Data Access] SDK ist ein Softwareentwicklungs-Kit, das das Lesen und Schreiben von Datensätzen aus der Adobe Experience Platform ermöglicht.

## Erste Schritte

Sie müssen das [Authentifizierungs](../../tutorials/authentication.md) -Tutorial abgeschlossen haben, um Zugriff auf die Werte zu haben, mit denen das sichere [!DNL Python] [!DNL Data Access] SDK aufgerufen werden kann:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. Für die Verwendung des [!DNL Python] SDK sind der Name und die ID der Sandbox erforderlich, in der der Vorgang ausgeführt wird:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

## Umgebung einrichten

Standardmäßig sind die Dienstendpunkte auf Integrations-Umgebung-Endpunkte eingestellt. Setzen Sie daher die folgenden Umgebung auf die folgenden Werte, um auf die Produktion zu verweisen:

| Variable | Endpunkt |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

Darüber hinaus können Ihre Anmeldeinformationen als Umgebung-Variablen hinzugefügt werden.

| Variable | Wert |
| -------- | ----- |
| `ORG_ID` | Ihre `{IMS_ORG}` ID. |
| `SERVICE_API_KEY` | Ihr `{API_KEY}` Wert. |
| `USER_TOKEN` | Ihr `{ACCESS_TOKEN}` Wert. |
| `SERVICE_TOKEN` | Ihre `{SERVICE_TOKEN}`, die Sie ggf. benötigen, um Back-Kanal-Anfragen zwischen Diensten zu autorisieren. |
| `SANDBOX_ID` | Der `{SANDBOX_ID}` Wert Ihrer Sandbox. |
| `SANDBOX_NAME` | Der `{SANDBOX_NAME}` Wert Ihrer Sandbox. |

## Installation

Alle Pakete werden `./dist` nach dem Erstellen ausgegeben.

### Rad

```python
python3 setup.py bdist_wheel --universal
```

Laden Sie das Rad aus dem Projektverzeichnis in Ihre [!DNL Python] 3 Umgebung.

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### Eierdatei

```python
python3 setup.py bdist_egg
```

## Lesen eines Datensatzes

Nach dem Festlegen der Umgebung-Variablen und dem Abschluss der Installation kann der Datensatz jetzt in den Pandas-Dataframe gelesen werden.

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### Spalten aus dem Datensatz AUSWÄHLEN

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Partitionierungsinformationen abrufen:

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT-Klausel

Mit der DISTINCT-Klausel können Sie alle eindeutigen Werte auf Zeilen-/Spaltenebene abrufen und alle Duplikat-Werte aus der Antwort entfernen.

Ein Beispiel für die Verwendung der `distinct()` Funktion ist unten aufgeführt:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WO-Klausel

Das [!DNL Python] SDK unterstützt bestimmte Operatoren zum Filtern des Datensatzes.

>[!NOTE] Bei den zum Filtern verwendeten Funktionen wird zwischen Groß- und Kleinschreibung unterschieden.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

Nachfolgend sehen Sie ein Beispiel für die Verwendung dieser Filterfunktionen:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY-Klausel

Die ORDER BY-Klausel ermöglicht es, die empfangenen Ergebnisse in einer bestimmten Reihenfolge (aufsteigend oder absteigend) nach einer bestimmten Spalte zu sortieren. Im [!DNL Python] SDK erfolgt dies mithilfe der `sort()` Funktion.

Ein Beispiel für die Verwendung der `sort()` Funktion ist unten aufgeführt:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT-Klausel

Die LIMIT-Klausel ermöglicht es Benutzern, die Anzahl der vom Datensatz erhaltenen Datensätze zu begrenzen.

Ein Beispiel für die Verwendung der `limit()` Funktion ist unten aufgeführt:

```python
df = dataset_reader.limit(100).read()
```

### OFFSET-Klausel

Mit der OFFSET-Klausel können Benutzer Zeilen von Anfang an überspringen, bis der Beginn Zeilen von einem späteren Zeitpunkt zurückgibt. In Verbindung mit LIMIT kann dies zur Iteration von Zeilen in Blöcken verwendet werden.

Ein Beispiel für die Verwendung der `offset()` Funktion ist unten aufgeführt:

```python
df = dataset_reader.offset(100).read()
```

## Schreiben eines Datensatzes

Das [!DNL Python] SDK unterstützt das Schreiben von Datensätzen. Die Benutzer müssen das Pandas-Datenformat bereitstellen, das in den Datensatz geschrieben werden muss.

### Schreiben des Pandas-Dataframs

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## Verzeichnis &quot;Userspace&quot;(Checkpoint)

Bei längeren Aufträgen müssen Benutzer möglicherweise Zwischenschritte speichern. In solchen Fällen bietet das [!DNL Python] SDK dem Benutzer die Möglichkeit, in einen Benutzerbereich zu lesen und zu schreiben.

>!![NOTE] Pfade zu den Daten werden vom SDK **nicht** gespeichert. Die Benutzer müssen den entsprechenden Pfad zu ihren jeweiligen Daten speichern.

### In den Benutzerbereich schreiben

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Aus dem Benutzerbereich lesen

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
