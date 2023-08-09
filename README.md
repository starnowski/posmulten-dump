# posmulten-dump

Suggestion:
Reserve index that will be added to name of tables that are going to be exported.
Index is assigned to specific tenant which is going to be exorted.

Before creating tables, restric any write access for tenant that is suppose to migrated with proper RLS policy

Create table that suppose to be exported
```sudocode
forearch (table : tablesToExport) {

CREATE TABLE export_tab_{index}_{table}
 SELECT * FROM {table}
}
```
