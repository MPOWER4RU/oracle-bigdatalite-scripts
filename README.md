oracle-bigdatalite-scripts
==========================

Scripts for Oracle BigData Appliance tests

# Scenario

1. Export from Oracle 12c DB into HDFS drive / Hive DB with sqoop
2. Create External Hive Table for CREW Files (Scenario 1.c,1.d)

# First steps:

1. Start Oracle 12c Database

  in Terminal:
  1. lsnrctl start
  2. sqlplus / as sysdba
     startup;
     exit;


## Scenario 1
a, Load Table information direct from DB into Hive Tables (with create Table) - Simplie append
```
sqoop import --connect jdbc:oracle:thin:@localhost:1521/orcl --username MOVIEDEMO --password welcome1 --table CREW --hive-import
```

b, Load Table information direct from DB into Hive Tables (with create Table) - Incremental with a PK column name
```
sqoop import --connect jdbc:oracle:thin:@localhost:1521/orcl --username MOVIEDEMO --password welcome1 --table CREW --hive-import --incremental append --check-column CREW_ID
```

c, Load Table information into HDFS 
```
sqoop import --connect jdbc:oracle:thin:@localhost:1521/orcl --username MOVIEDEMO --password welcome1 --table CREW
```

d, Load Table information into HDFS incremental
```
sqoop import --connect jdbc:oracle:thin:@localhost:1521/orcl --username MOVIEDEMO --password welcome1 --table CREW --incremental append --check-column CREW_ID
```

## Scenario 2
```
hive -f  hive/create_external_crew_table.hql
```
