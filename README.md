# posmulten-dump

Suggestion:
1. Reserve index that will be added to name of tables that are going to be exported.
Index is assigned to specific tenant which is going to be exorted.

Before creating tables, restrict any write access for tenant that is suppose to migrated with proper RLS policy

2. Create table that suppose to be exported
```sudocode
forearch (table : tablesToExport) {

CREATE TABLE export_tab_{index}_{table}
 SELECT * FROM {table}
}
```
3. Export data (in one or multiple files) with pg_dump

4. Create sql script for assertion that checks total amount of records for all tables

IMPORT

5. Chec sequnce values in exported database
- Check what is the highest (current value) in sequence
- Alternative, if configuration has information which table and column use specific sequence then based on "export_tab" the value of sequnece that might be required to update can be calculated based on export tables and not current value of sequence which can be higher
6. Update sequences in target database
7. Import data from files to target database (all constraint for operation has to be turned off)
AFTER IMPORT
Execute potential script and pass tenant id as argument
8 Delete tables for {index} like export_tab_{index}_{table}
