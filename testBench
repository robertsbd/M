let
    testBenchTables = (a_tbl as table, a_name as text, b_tbl as table, b_name as text) as text =>
        let

            // a wrapper to so you can specify the type of test
            runTest = (testFunc, a as table, a_name as text, b as table, b_name as text) as text => testFunc(a, b),

            // basic equality test for tables, if this is true all the other tests will be true, other tests included to be able to identfy where the error exists
            tableEquality = (a as table, b as table) as text => "Equality test (table equality): " & (if (a = b) then "PASSED." else "FAILED."), 

            // table length test
            tableLength = (a as table, b as table) as text => 
                let
                    rowcount_a = Table.RowCount(a), 
                    rowcount_b = Table.RowCount(b), 
                    return = "Length test (RowNum equality): " & (if (rowcount_a = rowcount_b) then "PASSED." else "FAILED.") & " Number of rows TABLE A=" & Number.ToText(rowcount_a) & " TABLE B=" & Number.ToText(rowcount_b)
                in
                    return,

            // table number of columns
            tableColNum = (a as table, b as table) as text => 
                let
                    colcount_a = Table.ColumnCount(a), 
                    colcount_b = Table.ColumnCount(b), 
                    return = "Column number test (ColNum equality): " & (if (colcount_a = colcount_b) then "PASSED." else "FAILED.") & " Number of cols TABLE A=" & Number.ToText(colcount_a) & " TABLE B=" & Number.ToText(colcount_b)
                in
                    return,

            // are the column names of the tables the same
            tableColNames = (a as table, b as table) as text =>                 
                let
                    colnames_a = Table.ColumnNames(a), 
                    colnames_b = Table.ColumnNames(b), 
                    colnames_a_str = Text.TrimEnd(List.Accumulate(colnames_a, "", (acc, current) => acc & current & ", "), {" ", ","}),
                    colnames_b_str = Text.TrimEnd(List.Accumulate(colnames_b, "", (acc, current) => acc & current & ", "), {" ", ","}),
                    return = "Column name test (ColName equality): " & (if (colnames_a = colnames_b) then "PASSED." else "FAILED.") & " Names of cols TABLE A= {" & colnames_a_str & "} TABLE B= {" & colnames_b_str & "}" 
                in
                    return,

            buffer_a_tbl = Table.Buffer(a_tbl),
            buffer_b_tbl = Table.Buffer(b_tbl),

            test_summary =  "Testing tables: (" & Text.From(DateTime.From(DateTimeZone.LocalNow())) & ")#(cr)#(lf)" & "TABLE A = " & a_name & "#(cr)#(lf)" & "TABLE B = " & b_name & "#(cr)#(lf)#(cr)#(lf)" &
                            runTest(tableEquality, buffer_a_tbl, a_name, buffer_b_tbl, b_name) & "#(cr)#(lf)" & 
                            runTest(tableLength, buffer_a_tbl, a_name, buffer_b_tbl, b_name) & "#(cr)#(lf)" & 
                            runTest(tableColNum, buffer_a_tbl, a_name, buffer_b_tbl, b_name) & "#(cr)#(lf)" & 
                            runTest(tableColNames, buffer_a_tbl, a_name, buffer_b_tbl, b_name)
        in
            test_summary
    in
testBenchTables
