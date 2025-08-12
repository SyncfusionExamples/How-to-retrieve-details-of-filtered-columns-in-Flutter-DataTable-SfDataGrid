# How-to-retrieve-details-of-filtered-columns-in-Flutter-DataTable-SfDataGrid

In this article, we will show how to retrieve details of filtered columns in [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with the necessary properties. The SfDataGrid provides a callback named [onFilterChanged](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/onFilterChanged.html), which is triggered after a filter is applied to a specific column through the UI. 

Within the onFilterChanged callback, you can access the details property to retrieve information about the filtered column, such as its name and the filter conditions.

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Syncfusion Flutter DataGrid')),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: TextButton(
              onPressed: () {
                showDialog(
                  context: context,
                  builder: (_) => AlertDialog(
                    title: Text('Filtered Columns'),
                    content: filteredColumns.isEmpty
                        ? Text('No columns filtered')
                        : Column(
                            mainAxisSize: MainAxisSize.min,
                            crossAxisAlignment: CrossAxisAlignment.start,
                            children: filteredColumns
                                .map(
                                  (col) =>
                                      Text('• $col', textAlign: TextAlign.left),
                                )
                                .toList(),
                          ),
                    actions: [
                      TextButton(
                        onPressed: () => Navigator.of(context).pop(),
                        child: Text('Close'),
                      ),
                    ],
                  ),
                );
              },
              child: Text('Show Filtered Columns'),
            ),
          ),
          Expanded(
            child: SfDataGrid(
              source: employeeDataSource,
              columnWidthMode: ColumnWidthMode.fill,
              allowFiltering: true,
              onFilterChanged: (details) {
                setState(() {
                  //Retrieving filtering details
                  final colName = details.column.columnName;
                  final isFilterApplied = details.filterConditions.isNotEmpty;
                  if (isFilterApplied) {
                    if (!filteredColumns.contains(colName)) {
                      filteredColumns.add(colName);
                    }
                  } else {
                    filteredColumns.remove(colName);
                  }
                });
              },
              columns: <GridColumn>[
                GridColumn(
                  columnName: 'id',
                  label: Container(
                    padding: EdgeInsets.all(16.0),
                    alignment: Alignment.center,
                    child: Text('ID'),
                  ),
                ),
                GridColumn(
                  columnName: 'name',
                  label: Container(
                    padding: EdgeInsets.all(8.0),
                    alignment: Alignment.center,
                    child: Text('Name'),
                  ),
                ),
                GridColumn(
                  columnName: 'designation',
                  label: Container(
                    padding: EdgeInsets.all(8.0),
                    alignment: Alignment.center,
                    child: Text('Designation', overflow: TextOverflow.ellipsis),
                  ),
                ),
                GridColumn(
                  columnName: 'salary',
                  label: Container(
                    padding: EdgeInsets.all(8.0),
                    alignment: Alignment.center,
                    child: Text('Salary'),
                  ),
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-retrieve-details-of-filtered-columns-in-Flutter-DataTable-SfDataGrid.git).

