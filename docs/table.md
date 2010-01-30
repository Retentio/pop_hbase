Table operations: List, create, modify and delete HBase tables
==============================================================

Those operations are handled by the class "PopHbaseTable" which can be retrieved from an instance of "PopHbase" through the "tables" property.

Grab an instance of "PopHbaseTables"
------------------------------------

	$tables = $hbase->tables;
	assert($tables instanceof PopHbaseTables);
	assert($tables === $hbase->tables);

List tables names in HBase
--------------------------

The "PopHbaseTables->names" method takes no argument and return a list of tables names. The term "list" being a reserved keywords in PHP, we used the term "names" to call this method.

	$tables = $hbase->tables->names();
	foreach($tables as $table){
		assert(is_string($table));
	}

Loop through table instances
---------------------------

The "PopHbaseTables" class implement the PHP "Iterator" interface so you can directly obtain an instance of it and loop through it.

	$tables = $hbase->tables;
	foreach($tables as $table){
		assert($table instanceof PopHbaseTable);
		assert(is_string($table->name));
	}

Count the number of table in HBase
----------------------------------

The "PopHbaseTables" class implement the PHP "Countable" interface so you can directly use the PHP "count" function while passing an instance of it as an argument.

	$tables = $hbase->tables;
	assert(is_int($tables));

Create a new table in HBase
---------------------------

The simplest way is to provide two string arguments. The first one is the table name and the second one is the column family name.

	$tables = $hbase->tables;
	$tables->create("my_table","my_column_family");

For more control on the table and column family schema configuration, the argument may take the form of an associative array. The table argument must contain the key "name" and may also contain the keys "is_meta" and "is_root". The column family arguments must contain the key "name" and may also contain the keys  "blocksize", "bloomfilter", "blockcache", "compression", "length", "versions", "ttl" and "in_memory".


	$tables = $hbase->tables;
	$tables->create(
		array("name"=>"my_table"),
		arrary("name"=>"my_column_family_1"),
		arrary("name"=>"my_column_family_2")
	);

Drop an existing table from HBase
---------------------------------

Disabling and drop of a table is achieved through the "delete" method.

	$tables = $hbase->tables;
	$tables->delete('my_table');
	
