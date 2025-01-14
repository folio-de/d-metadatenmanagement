# folio-reference-data

Dieses Verzeichnis dient der verbundübergreifenden Pflege von FOLIO-Referenzwerten der Inventory-/Katalog-App.

## Funktionsweise

Pro Referenzwerteliste muss ein Verzeichnis angelegt werden, das nach der API benannt ist, an die die Anfragen gesendet werden sollen. Innerhalb des Verzeichnissen wird pro Referenzwert eine JSON-Datei erstellt, die beliebig benannt sein kann.

Diese JSON-Dateien werden bei Aufruf des Scripts `insert_reference_data.sh` an den Endpunkt gesendet. Wenn innerhalb der JSON-Datei das Attribut `id` vorhanden ist, wird daraus die UUID extrahiert. Wenn das Attribut `id` nicht vorhanden ist, wird ein `POST` an den Endpunkt gesendet, um den Referenzwert mit zufälliger generierter UUID zu erstellen. Wenn das Attribut `id` vorhanden ist, versucht das Script zuerst, einen bestehenden Referenzwert per `PUT` zu aktualisieren. Falls der HTTP-Statuscode `404` (Ressource nicht vorhanden) zurückgeliefert wird, wird stattdessen ein `POST` gesendet, um den Referenzwert mit der im Attribut`id` enthaltenen UUID anzulegen.

## Aufruf

```bash
insert_reference_data.sh <OKAPI> <TENANT> <OKAPIUSERNAME> <OKAPIPASSWORD>
```
