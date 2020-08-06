==================================
Creating Custom Graphs and Reports
==================================

The best resources to reference when creating custom graphs and reports in Spira are listed below. 

* `Writing Custom Reports with Spira`_ (4-part series)

* `Creating Custom Graphs with Spira`_ (4-part series)

* There is also a wealth of information available in the `Inflectra Knowledge Base`_.

To date, the quickest way to find out what columns are available in a table is to run this ESQL query in the report/graph editor:
::
  select value R
  from {tableName}
  where PROJECT_ID = ${ProjectId}

where ``{tableName}`` is the Spira Entity table. 

Since we will most likely be using the same tables/columns, a `list of available Tables and Columns`_ has been collated for easy reference. Some sample queries are in the same sheet.

.. _Writing Custom Reports with Spira: https://www.inflectra.com/Ideas/Entry/writing-custom-reports-with-spira-part-1-301.aspx
.. _Creating Custom Graphs with Spira: https://www.inflectra.com/Ideas/Entry/creating-custom-graphs-with-spira-part-1-911.aspx
.. _list of available Tables and Columns: https://docs.google.com/spreadsheets/d/1Nlt3UfbfIcJmXJRLcD1-G5Pq5weTqsl3PTzfstqT9wg/edit?usp=sharing
.. _Inflectra Knowledge Base: https://www.inflectra.com/Support/KnowledgeBase.aspx
