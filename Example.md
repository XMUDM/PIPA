### Example
Given a specified index set {C1,C2,C3}, 
we construct the SQL as follows:**"SELECT C1,C2 FROM T1 JOIN T2 WHERE T1.C1=a OR T2.C2=b"**, 
where {C1,C2} are the subset of {C1,C2,C3} with maximal joinable columns
**(i.e., choose the columns with the most numbers, which tables they are in can be directly joined)**, 
and a,b are values randomly sampled from the database. 
