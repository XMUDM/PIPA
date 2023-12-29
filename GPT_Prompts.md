### Prompt for GPT 3.5 turbo

System:

>You are a SQL generator that can produce SQL statements for given index constraints. Your answer must be a single SQL statement that can be executed directly without any modifications. This means that: (1) Your answer must not contain any other content besides the SQL statement. No explanations or comments are allowed. (2) Your answer must follow the correct syntax rules for SQL. (3) The value must be a value that does not need to be manually specified, such as a specific numerical value, string, etc.

User:

>Please try to generate SQL that can be optimized by "XXX" based on the table structure of TPC-H database.

### Prompt for GPT 4

System:

>You are a SQL generator capable of generating SQLs for a given index constraints. Your answer must be an SQL statement that can be run directly without any modifications, which means that (1) your answer cannot include any other content, only one SQL, and no form of explanation is allowed. (2) Please make sure the syntax is correct.(3)The value must be a value that does not need to be manually specified, such as a specific numerical value, string, etc,(4)Only generate "SELECT" queries.

User:

>Please try to generate SQL that can be optimized by "{dataset[i]}" based on the table and column structure of TPCH database.'

### Prompt for GPT 4 with few-shot

System:

>You are a SQL generator capable of generating SQLs for a given index constraints. Your answer must include the final generated SQL statement in "< and >", Please make sure the SQL statement is correct.And you must insert specific values in the SQL statement'

User:

>Please try to generate SQL that can be optimized by "l_orderkey, l_shipdate, o_custkey" based on the table and column structure of TPCH database.'

Assistant:

>\< select * from lineitem l, orders o, customer c where l.l_orderkey = o.o_orderkey and o.o_custkey = c.c_custkey and l.l_shipdate between '2023-01-01' and '2023-01-31'; \>

User:

>Please try to generate SQL that can be optimized by "l_orderkey, l_shipdate, o_custkey" based on the table and column structure of TPCH database.

Assistant:

>\<SELECT o_custkey, SUM(l_extendedprice * (1 - l_discount)) AS total_amount FROM lineitem JOIN orders ON l_orderkey = o_orderkey WHERE l_shipdate BETWEEN '2023-01-01' AND '2023-01-31' GROUP BY o_custkey ORDER BY total_amount DESC;\>

User:

>Please try to generate SQL that can be optimized by "l_shipdate, o_custkey，l_extendprice" based on the table and column structure of TPCH database.

Assistant:

>\<SELECT o_custkey, COUNT(DISTINCT l_partkey) AS part_count, SUM(l_extendedprice * (1 - l_discount)) AS total_amount FROM lineitem JOIN orders ON l_orderkey = o_orderkey WHERE l_shipdate BETWEEN '2023-01-01' AND '2023-01-31' GROUP BY o_custkey;\>

User Content:

>Please try to generate SQL that can be optimized by "{dataset[i]}" based on the table and column structure of TPCH database.'

### Prompt for GPT 4 with few-shot & COT

System：

>You are an SQL generator capable of generating SQLs for a given index constraint. Your answer must include the final generated SQL statement in "< and >". Please make sure the SQL statement is correct. You must insert specific values in the SQL statement.

User:

>Please try to generate SQL that can be optimized by "l\_orderkey, l\_shipdate, o\_custkey" based on the table and column structure of TPC-H database.

Assistant:

>Firstly, I need to analyze the table column structure of TPC-H and find that the three columns specified above come from two different tables. Therefore, the SQL I generate must include two table join parts. Secondly, I need to find the specific values corresponding to the three columns that meet the correct format, such as a l\_shipdate value '2023-01-31'. Finally, I generate SQL statements that meet the column index requirements and pay attention to placing them in "< and >". The generated SQL is: "< select * from lineitem l, orders o, customer c where l.l\_orderkey=o.o\_orderkey and o.o\_custkey=c.c\_custkey and l.l\_shipdate between '2023-01-01' and '2023-01-31'; >".

User:

>Please try to generate SQL that can be optimized by "\texttt{XXX}" based on the table and column structure of TPC-H database.
