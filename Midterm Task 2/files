let
    Source = Csv.Document(File.Contents("C:\Users\COMLAB\Downloads\Uncleaned_DS_jobs.csv"),[Delimiter=",", Columns=15, Encoding=1252, QuoteStyle=QuoteStyle.Csv]),
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"index", Int64.Type}, {"Job Title", type text}, {"Salary Estimate", type text}, {"Job Description", type text}, {"Rating", type number}, {"Company Name", type text}, {"Location", type text}, {"Headquarters", type text}, {"Size", type text}, {"Founded", Int64.Type}, {"Type of ownership", type text}, {"Industry", type text}, {"Sector", type text}, {"Revenue", type text}, {"Competitors", type text}}),
    #"Extracted Text Before Delimiter" = Table.TransformColumns(#"Changed Type", {{"Salary Estimate", each Text.BeforeDelimiter(_, "("), type text}}),
    #"Sorted Rows" = Table.Sort(#"Extracted Text Before Delimiter",{{"Salary Estimate", Order.Ascending}}),
    #"Inserted Text Between Delimiters" = Table.AddColumn(#"Sorted Rows", "Text Between Delimiters", each Text.BetweenDelimiters([Salary Estimate], "$", "K"), type text),
    #"Renamed Columns" = Table.RenameColumns(#"Inserted Text Between Delimiters",{{"Text Between Delimiters", "Min Sal"}}),
    #"Inserted Text Between Delimiters1" = Table.AddColumn(#"Renamed Columns", "Text Between Delimiters", each Text.BetweenDelimiters([Salary Estimate], "$", "K"), type text),
    #"Renamed Columns1" = Table.RenameColumns(#"Inserted Text Between Delimiters1",{{"Text Between Delimiters", "Max Sal"}}),
    #"Added Custom" = Table.AddColumn(#"Renamed Columns1", "Role Type", each if Text.Contains([Job Title], "Data Scientist") then
"Data Scientist"
else if Text.Contains([Job Title], "Data Analyst") then
"Data Analyst"
else if Text.Contains([Job Title], "Data Engineer") then
"Data Engineer"
else if Text.Contains([Job Title], "Machine Learning") then
"Machine Learning Engineer"
else
"other"),
    #"Changed Type1" = Table.TransformColumnTypes(#"Added Custom",{{"Role Type", type text}}),
    #"Added Custom1" = Table.AddColumn(#"Changed Type1", "Custom", each if [Location]= "New Jersey" then ", NJ"
else if [Location] = "Remote" then ", other"
else if [Location]= "United States" then ", other"
else if [Location]= "Texas" then ", TX"
else if [Location]= "Patuxent" then ", MA"
else if [Location]= "California" then ", CA"
else if [Location]= "Utah" then ", UT"
else [Location]),
    #"Split Column by Delimiter" = Table.SplitColumn(#"Added Custom1", "Custom", Splitter.SplitTextByDelimiter(",", QuoteStyle.Csv), {"Custom.1", "Custom.2"}),
    #"Changed Type2" = Table.TransformColumnTypes(#"Split Column by Delimiter",{{"Custom.1", type text}, {"Custom.2", type text}}),
    #"Replaced Value" = Table.ReplaceValue(#"Changed Type2","Anne Rundell","MA",Replacer.ReplaceText,{"Custom.2"}),
    #"Renamed Columns2" = Table.RenameColumns(#"Replaced Value",{{"Custom.2", "State Abbreviations"}}),
    #"Inserted Literal" = Table.AddColumn(#"Renamed Columns2", "Literal", each "101", type text),
    #"Renamed Columns3" = Table.RenameColumns(#"Inserted Literal",{{"Literal", "Min Company Size"}}),
    #"Inserted Literal1" = Table.AddColumn(#"Renamed Columns3", "Literal", each "101", type text),
    #"Renamed Columns4" = Table.RenameColumns(#"Inserted Literal1",{{"Literal", "Max Company Size"}, {"Custom.1", "Location Correction 2"}}),
    #"Removed Columns" = Table.RemoveColumns(#"Renamed Columns4",{"Location"}),
    #"Renamed Columns5" = Table.RenameColumns(#"Removed Columns",{{"Location Correction 2", "State"}, {"State Abbreviations", "Abbreviations"}}),
    #"Filtered Rows" = Table.SelectRows(#"Renamed Columns5", each ([Competitors] <> "-1") and ([Industry] <> "-1") and ([Revenue] <> "Unknown / Non-Applicable")),
    #"Split Column by Delimiter1" = Table.SplitColumn(#"Filtered Rows", "Company Name", Splitter.SplitTextByDelimiter("#(lf)", QuoteStyle.Csv), {"Company Name.1", "Company Name.2"}),
    #"Changed Type3" = Table.TransformColumnTypes(#"Split Column by Delimiter1",{{"Company Name.1", type text}, {"Company Name.2", type number}}),
    #"Removed Columns1" = Table.RemoveColumns(#"Changed Type3",{"Company Name.2"}),
    #"Renamed Columns6" = Table.RenameColumns(#"Removed Columns1",{{"Company Name.1", "Company Name"}, {"Abbreviations", "State Abbreviations"}, {"State", "Location"}})
in
    #"Renamed Columns6"
