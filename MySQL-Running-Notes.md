
## To Know when was the table created/updated:
1. select table_name, create_time, update_time from information_schema.tables where table_schema='THE_VAULT_00';

## To clear console in command window:
1. system clear;

## To know what all procedures exists within a schema:
1. show procedure status where db = 'THE_VAULT_00';

## Stored Proc vs Functions:
1. Stored procedure is precompiled execution plan where as functions are not. Function Parsed and compiled at runtime. Stored procedures, Stored as a pseudo-code in database i.e. compiled form.
2. Functions are normally used for computations where as procedures are normally used for executing business logic.
3. Procedure parameters can be defined as input-only, output-only, or both. This means that a procedure can pass values back to the caller by using output parameters. These values can be accessed in statements that follow the CALL statement.
4. Functions return value, so there must be a RETURNS clause in a function definition to indicate the data type of the return value. Also, there must be at least one RETURN statement within the function body to return a value to the caller.
5. RETURNS and RETURN do not appear in procedure definitions.
6. A procedure is invoked using a CALL statement, and can only pass back values using output variables. A function can be called from inside a statement just like any other function (that is, by invoking the function's name), and can return a scalar valu
7. functions can be used within sql expressions whereas stored procs have to be called indepdently outside of any sql expression.
