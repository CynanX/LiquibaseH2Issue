# LiquibaseMultiSchemaIssue

Demo showing creating a table with INT(10) no longer works with H2.x, whereas it does under H2 v1.x

## Getting started

`./mvnw test`

## Expected behaviour

The changelog included should create a new `persons` table.

## Actual behaviour

The table will be created in the default database, but error on the second. The third will not be touched.

```
2022-09-07 10:11:41.855  WARN 23829 --- [           main] o.s.w.c.s.GenericWebApplicationContext   : Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'liquibase' defined in class path resource [org/springframework/boot/autoconfigure/liquibase/LiquibaseAutoConfiguration$LiquibaseConfiguration.class]: Invocation of init method failed; nested exception is liquibase.exception.LiquibaseException: liquibase.exception.MigrationFailedException: Migration failed for change set changelog/1.0.0/tables/create_persons_table.xml::createPersonsTable::mark:
     Reason: liquibase.exception.DatabaseException: Syntax error in SQL statement "CREATE TABLE PUBLIC.persons (personId INT[*](10), lastName VARCHAR(255), firstName VARCHAR(255), address VARCHAR(255), city VARCHAR(255))"; expected "ARRAY, INVISIBLE, VISIBLE, NOT NULL, NULL, AS, DEFAULT, GENERATED, ON UPDATE, NOT NULL, NULL, AUTO_INCREMENT, DEFAULT ON NULL, NULL_TO_DEFAULT, SEQUENCE, SELECTIVITY, COMMENT, CONSTRAINT, COMMENT, PRIMARY KEY, UNIQUE, NOT NULL, NULL, CHECK, REFERENCES, AUTO_INCREMENT, ,, )"; SQL statement:
CREATE TABLE PUBLIC.persons (personId INT(10), lastName VARCHAR(255), firstName VARCHAR(255), address VARCHAR(255), city VARCHAR(255)) [42001-214] [Failed SQL: (42001) CREATE TABLE PUBLIC.persons (personId INT(10), lastName VARCHAR(255), firstName VARCHAR(255), address VARCHAR(255), city VARCHAR(255))]
```
