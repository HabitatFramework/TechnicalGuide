********
Database
********

The database consists of 3 types of tables as follows:

	1. Data tables
	2. Lookup tables
	3. Export tables


.. index::
	single: Data Tables

.. _data_tables:

Data Tables
===========

.. sidebar:: Key to Data Tables

	1. incid
	2. incid_ihs_matrix
	3. incid_ihs_formation
	4. incid_ihs_management
	5. incid_ihs_complex
	6. incid_bap
	7. incid_sources
	8. history

Tables in the database prefixed by 'incid' are **data** tables and hence contain all the attribute data relating to the GIS features. The attributes have been separated into 8 tables to 'normalise' the data which reduces storage space, improves performance and provides greater flexibility.

How the data tables relate to the fields in the user interface is demonstrated in the following figures:


		.. _figUICF:

		.. figure:: figures/UserInterfaceCommonDBFields.png
			:align: center
			:scale: 90

			User Interface Common Fields


		.. _figUIIF:

		.. figure:: figures/UserInterfaceIHSTabDBFields.png
			:align: center
			:scale: 90

			User Interface IHS Tab Fields


		.. _figUIDF:

		.. figure:: figures/UserInterfaceDetailsTabDBFields.png
			:align: center
			:scale: 90

			User Interface Details Tab Fields


		.. _figUISF:

		.. figure:: figures/UserInterfaceSourcesTabDBFields.png
			:align: center
			:scale: 90

			User Interface Sources Tab Fields


.. index::
	single: Data Tables; Incid

.. _incid_table:

incid
-----

This is the main data table with one record per INCID. All the other data tables relate to this table via the **INCID** field.

	incid
		Char(12) - A unique **Inc**\ remental **id**\ entifier for each logical group of features.

	legacy_habitat
		Char(50) - The primary pre-IHS habitat code carried over from the 'legacy' habitat data.

	site_ref
		Char(16) - A free-text field containing a reference for the location of the feature.

	site_name
		Char(100) - A free-text field containing a name for the location of the feature.

	boundary_base_map
		Char(2) - Foreign key to `Code` column in the 'lut_boundary_map' table representing the data map used to identify the feature boundary.

	digitisation_base_map
		Char(2) - Foreign key to `Code` column in the 'lut_boundary_map' table representing the data map used to digitise the feature boundary.

	ihs_version
		Char(20) - Foreign key to `ihs_version` in the 'lut_ihs_version' table storing the active version of IHS when the INCID attributes were last updated.

	ihs_habitat
		Char(8) - Foreign key to `code` in the 'lut_ihs_habitat' table representing the main IHS Habitat for the INCID.

	general_comments
		Char(254) - A free-text field containing any general comments relating to the INCID.

	created_date
		DateTime - The date and time that the INCID was first created (either during the initial framework conversion or following a logical split).

	created_user_id
		Char(40) - Foreign key to `user_id` in the 'lut_user' table representing the user that created the INCID.

	last_modified_date
		DateTime - The date and time that the INCID was last modified.

	last_modified_user_id
		Char(40) - Foreign key to `user_id` in the 'lut_user' table representing the user that last modified the INCID attributes or split or merged the INCID.


.. index::
	single: Data Tables; Incid_IHS_Matrix

.. _incid_ihs_matrix:

incid_ihs_matrix
----------------

This table contains any IHS Matrix codes recorded alongside an IHS Habitat code to refine the habitat definition for an INCID. There can be between 0 and 3 records for each INCID.

	matrix_id
		Integer - A unique ID for each record.

	incid
		Char(12) - Foreign key to `incid` in the 'incid' table.

	matrix
		Char(8) - Foreign key to `code` in the 'lut_ihs_matrix' table representing an IHS Matrix type.


.. index::
	single: Data Tables; Incid_IHS_Formation

.. _incid_ihs_formation:

incid_ihs_formation
-------------------

This table contains any IHS Formation codes recorded alongside an IHS Habitat code to refine the habitat definition for an INCID. There can be between 0 and 2 records for each INCID.

	formation_id
		Integer - A unique ID for each record.

	incid
		Char(12) - Foreign key to `incid` in the 'incid' table.

	formation
		Char(8) - Foreign key to `code` in the 'lut_ihs_formation' table representing an IHS Formation type.


.. index::
	single: Data Tables; Incid_IHS_Management

.. _incid_ihs_management:

incid_ihs_management
--------------------

This table contains any IHS Management codes recorded alongside an IHS Habitat code to refine the habitat definition for an INCID. There can be between 0 and 2 records for each INCID.

	management_id
		Integer - A unique ID for each record.

	incid
		Char(12) - Foreign key to `incid` in the 'incid' table.

	management
		Char(8) - Foreign key to `code` in the 'lut_ihs_management' table representing an IHS Management type.


.. index::
	single: Data Tables; Incid_IHS_Complex

.. _incid_ihs_complex:

incid_ihs_complex
-----------------

This table contains any IHS Complex codes recorded alongside an IHS Habitat code to refine the habitat definition for an INCID. There can be between 0 and 2 records for each INCID.

	complex_id
		Integer - A unique ID for each record.

	incid
		Char(12) - Foreign key to `incid` in the 'incid' table.

	complex
		Char(8) - Foreign key to `code` in the 'lut_ihs_complex' table representing an IHS Complex type.


.. index::
	single: Data Tables; Incid_BAP

.. _incid_bap_table:

incid_bap
---------

This table contains details of the priority habitats and potential priority habitats for an INCID. There can be between 0 and 3 records for each INCID.

	bap_id
		Integer - A unique ID for each record.

	incid
		Char(12) - Foreign key to `incid` in the 'incid' table.

	bap_habitat
		Char(11) - Foreign key to `code` in the 'lut_habitat_type' table representing a priority habitat (or potential priority habitat).

	quality_determination
		Char(2) - Foreign key to `code` in the 'lut_bap_quality_determination' table representing the accuracy with which the priority habitat has been determined.

	quality_interpretation
		Char(2) - Foreign key to `code` in the 'lut_bap_quality_interpretation' table representing how well the priority habitat was interpreted from the source data.

	interpretation_comments
		Char(254) - A free-text field containing any comments to explain the reasoning behind the priority habitat determination and interpretation.


.. index::
	single: Data Tables; Incid_Sources

.. _incid_sources:

incid_sources
-------------

This table contains details of the source datasets for an INCID. There can be between 0 and 3 records for each INCID.

	incid_source_id
		Integer - A unique ID for each record.

	incid
		Char(12) - Foreign key to `incid` in the 'incid' table.

	source_id
		Integer - Foreign key to `source_id` in the 'lut_sources' table representing a source dataset.

	source_date_start
		Integer - Start date of the data range covered by the source dataset represented as the number of days since 01/01/1900.

	source_date_end
		Integer - End date of the data range covered by the source dataset represented as the number of days since 01/01/1900.

	source_date_type
		Char(2) - String that describes the format of the date range covering the source dataset.

		.. tabularcolumns:: |L|L|L|

		.. table:: Vague date types

			+-----------+-------------------------------+---------------------------+
			| Date Type |          Description          |          Example          |
			+===========+===============================+===========================+
			| D         | Single day date               | 15/10/2010                |
			+-----------+-------------------------------+---------------------------+
			| DD        | Day-to-date date range        | 15/10/2010 - 18/10/2010   |
			+-----------+-------------------------------+---------------------------+
			| D-        | Day start with no end date    | 15/10/2010 -              |
			+-----------+-------------------------------+---------------------------+
			| -D        | Day end with no start date    | \- 18/10/2010             |
			+-----------+-------------------------------+---------------------------+
			| O         | Single month date             | Oct 2010                  |
			+-----------+-------------------------------+---------------------------+
			| OO        | Month-to-month date range     | Oct 2010 - Nov 2010       |
			+-----------+-------------------------------+---------------------------+
			| O-        | Month start with no end date  | Oct 2010 -                |
			+-----------+-------------------------------+---------------------------+
			| -O        | Month end with no start date  | \- Nov 2010               |
			+-----------+-------------------------------+---------------------------+
			| Y         | Single year date              | 2010                      |
			+-----------+-------------------------------+---------------------------+
			| YY        | Year-to-year date range       | 2010 - 2011               |
			+-----------+-------------------------------+---------------------------+
			| Y-        | Year start with no end date   | 2010 -                    |
			+-----------+-------------------------------+---------------------------+
			| -Y        | Year end with no start date   | \- 2011                   |
			+-----------+-------------------------------+---------------------------+
			| P         | Single season date            | Autumn 2010               |
			+-----------+-------------------------------+---------------------------+
			| PP        | Season-to-season date range   | Autumn 2010 - Winter 2010 |
			+-----------+-------------------------------+---------------------------+
			| P-        | Season start with no end date | Autumn 2010 -             |
			+-----------+-------------------------------+---------------------------+
			| -P        | Season end with no start date | \- Winter 2010            |
			+-----------+-------------------------------+---------------------------+
			| U         | Unknown date                  | Unknown                   |
			+-----------+-------------------------------+---------------------------+


	source_habitat_class
		Char(5) - Foreign key to `incid` in the 'lut_habitat_class' table representing the habitat classification of the source dataset.

	source_habitat_type
		Char(11) - Foreign key to `incid` in the 'lut_habitat_type' table representing the habitat type of the source dataset.

	source_boundary_importance
		Char(1) - Foreign key to `code` in the 'lut_important' table representing the relative importance of the source when determining the boundary location of all the features in the INCID.

	source_habitat_importance
		Char(1) - Foreign key to `code` in the 'lut_important' table representing the relative importance of the source when determining the IHS Habitat and associated multiplex codes of the INCID.

	sort_order
		Integer - Determines the (ascending) order the sources for each INCID will be displayed in the 'Sources' tab of the main window.


.. index::
	single: Data Tables; Incid_MM_Polygons

.. _incid_mm_polygons:

incid_mm_polygons
-----------------

This table is a local database **copy** of the attribute table for the GIS feature layer to improve performance. If the GIS features are split into separate GIS layers this table contains the attribute records for **all** the layers combined. There can be any number of records for each INCID, depending upon how many TOIDs and TOID fragments are associated with the INCID.

	incid
		Char(12) - Foreign key to `incid` in the 'incid' table.

	toid
		Char(20) - The unique Ordnance Survey **to**\ pographical **id**\ entifier of each feature.

	toid_fragment_id
		Char(5) - An incremental number (prefixed with zeros) used as a unique reference for each fragment of a single TOID.

	ihs_category
		Char(2) - Foreign key to `code` in the 'lut_ihs_category' table representing the first 2 characters of the IHS Habitat code.

	ihs_summary
		Char(50) - A concatenation of all the IHS habitat and multiplex codes from the INCID for this feature. This field is automatically maintained by the tool.

	shape_length
		Float - A decimal value of variable precision representing the perimeter length of the feature.

	shape_area
		Float - A decimal value of variable precision representing the spatial area of the feature.


.. index::
	single: Data Tables; History

.. _history:

history
-------

This table contains record of **every** change to **every** feature made using the HLU Tool.

	history_id
		Integer - A unique ID for each record.

	incid
		Char(12) - Foreign key to `incid` in the 'incid' table.

	toid
		Char(20) - The unique Ordnance Survey **to**\ pographical **id**\ entifier of each feature.

	toid_fragment_id
		Char(5) - An incremental number (prefixed with zeros) used as a unique reference for each fragment of a single TOID.

	modified_user_id
		Char(40) - Foreign key to `user_id` in the 'lut_user' table representing the user that modified the feature.

	modified_date
		DateTime - The date and time that the features was modified.

	modified_process
		Char(3) - Foreign key to `code` in the `lut_process` table representing the activity being undertaken when the feature was modified.

	modified_reason
		Char(3) - Foreign key to `code` in the `lut_reason` table representing the underlying explanation for the change to the feature.

	modified_ihs_category
		Char(2) - Foreign key to `code` in the 'lut_ihs_category' table representing the first 2 characters of the IHS Habitat code prior to the changes to the feature.

	modified_ihs_summary
		Char(50) - A concatenation of all the IHS habitat and multiplex codes from the INCID for this feature prior to the changes to the feature.

	modified_operation
		Char(3) - Foreign key to `code` in the `lut_operation` table representing the operation that undertaken to cause the change to the feature.

	modified_incid
		Char(12) - The incid prior to the changes to the feature. In the event of a logical split or logical merge this value will be different to the current 'incid', otherwise it will be the same as the current 'incid'.

	modified_toid_fragment_id
		Char(12) - The toid_fragment_id prior to the changes to the feature. In the event of a physical split or logical merge this value **may** be different to the current 'toid_fragment_id' otherwise it will be the same as the current 'toid_fragment_id'.

	modified_length
		Float - A decimal value of variable precision representing the perimeter length of the feature after the changes to the feature.

	modified_area
		Float - A decimal value of variable precision representing the spatial area of the feature after the changes to the feature.


.. raw:: latex

	\newpage

.. index::
	single: Lookup Tables

.. _lookup_tables:

Lookup Tables
=============

Tables in the database prefixed by 'lut\_' are **lookup** tables and are used in many drop-down lists in the user interfaces to restrict choices to only valid or appropriate values for the organisation.

Some of the lookup tables contain records and settings that are generic to all HLU Tool installations and hence should be considered as 'system' records (indicated by the **system_supplied** attribute set to 'True' (minus one). These records are configured centrally and updates are applied to HLU Tool installations using the HLUDbUpdater.exe tool (see :ref:`database_updater` for more details). The remaining lookup tables can be configured entirely for a given HLU Tool installation to tailor them to the specific requirements of each organisation.

	.. note::

		* Changes to the lookup tables won't take effect for HLU Tool instances that are running. The HLU Tool will need to be closed and re-started before any lookup table changes to take effect.
		* Lookup table values are relevant to the **whole** database system and hence any changes will affect **all** users of that database.
		* **All** records in tables containing a 'sort_order' attribute must have a numerical value set or they may not appear in the relevant drop-down lists.

The following lookup tables should be updated to tailor local requirements:

.. index::
	single: Lookup Tables; Lut_Users

.. _lut_users:

lut_users
---------

This table contains details of all the users that have editing capability with the HLU Tool and indicates if they are also able to perform 'bulk' updates.

	user_id
		The user's *Windows* login ID. If the user logs in to a domain then the login should be entered in the format: *[Domain]\\[LoginID]*. [1]_

	user_name
		The name which will be displayed in the 'By' fields of the INCID section and the History tab.

	bulk_update
		Determines whether the user has permissions to run a bulk update to change attributes for all selected records. Ticking this checkbox gives the user permission to run bulk updates.

	sort_order
		Determines the order user names would be displayed in any relevant drop-down. This field is not currently used (as there are no drop-down lists that display users.)

	.. caution::
		Bulk update permission should only be assigned to **expert** users and should only be used with caution as mistakes can have major affects on the data.

.. [1] The 'user_id' of the current user is shown in the **Tools... --> About** window.


.. seealso::
	See :ref:`configuring_users` for more information.


.. index::
	single: Lookup Tables Lut_Sources

.. _lut_sources:

lut_sources
-----------

This table contains details of all the source datasets that can be referenced as a 'Source' by an INCID.

	source_id
		A unique ID for each source.

	source_name
		The name which appears in the 'Name' drop-down list in the 'Sources' tab.

	source_date_default
		[Optional]. If a date is entered, the 'Vague Date' field in the 'Sources' tab will be set to this value (if blank) when this source is selected. If the date is left blank, the 'Vague Date' field will not be altered.

	sort_order
		Determines the order source names are displayed in the 'Name' drop-down list in the 'Sources' tab.


.. seealso::
	See :ref:`configuring_sources` for more information.


.. index::
	single: Lookup Tables; Lut_Process

.. _lut_process:

lut_process
-----------

This table contains details of all the processes that can be referenced as the activity being undertaken when applying updates with the HLU Tool.

	code
		A unique 3 character field for each source.

	description
		A brief description or name that will appear in the 'Process' drop-down list in the main window.

	sort_order
		Determines the order processes are displayed in the 'Process' drop-down list in the main window.


.. index::
	single: Lookup Tables; Lut_Reason

.. _lut_reason:

lut_reason
----------

This table contains details of all the reasons that can be referenced as the underlying explanation for applying updates with the HLU Tool.

	code
		A unique 3 character field for each source.

	description
		A brief description or name that will appear in the 'Reason' drop-down list in the main window.

	sort_order
		Determines the order processes are displayed in the 'Reason' drop-down list in the main window.


.. seealso:
	See :Ref:`configuring_luts` for more information on configuring lookup tables.


.. index::
	single: Lookup Tables; Sort Order
	single: Lookup Tables; Local Flags

Local Flags & Sort Orders
-------------------------

Regardless of whether records in a lookup table are 'system' supplied records or not, many can be configured to indicate if they are applicable to an organisation. For example, many lookup tables contain a **sort_order** field that will determine the order that the values appear in any related drop-down lists. Some tables also have a **is_local** field that can be used to 'hide' values that are not applicable to the local area or should not be used by the organisation.

	is_local
		Set to 'True' (minus 1) to include in drop-down lists, or 'False' (zero) to exclude from drop-down lists.

	sort_order
		Set to a sequential, positive numeric whole number to indicate the order records should appear in drop-down lists. Alternatively all records can be set to zero to use the default sort order for that table.

	.. note::

		* Changes to the lookup tables won't take effect for HLU Tool instances that are running. The HLU Tool will need to be closed and re-started before any lookup table changes to take effect.
		* Lookup table values are relevant to the **whole** database system and hence any changes will affect **all** users of that database.
		* **All** records in tables containing a 'sort_order' attribute must have a numerical value set or they may not appear in the relevant drop-down lists.

The following lookup tables can be updated to tailor their **is_local** and/or **sort_order** values:

	.. tabularcolumns:: |L|L|C|C|

	.. table:: Locally configurable lookup tables

		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		|             Table              |                                    Description                                    | is_local | sort_order |
		+================================+===================================================================================+==========+============+
		| lut_ihs_habitat                | Contains all the IHS Habitats that can be assigned to INCIDs using                | x        | x          |
		|                                | the 'Habitat' field on the IHS tab of the main window.                            |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_habitat_class              | Contains all of the Habitat Classifications that can be assigned to               | x        | x          |
		|                                | sources using the 'Habitat Class' field on the Sources tab of the main window.    |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_habitat_type               | Contains all of the Habitat Types that can be assigned to sources                 | x        | x          |
		|                                | using the 'Habitat Type' field on the Sources tab of the main window              |          |            |
		|                                | (for the selected 'Habitat Class').                                               |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_ihs_complex                | Contains all the IHS Complex codes that can be assigned using the 'Complex'       |          | x          |
		|                                | fields on the IHS table of the main window.                                       |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_ihs_formation              | Contains all the IHS Formation codes that can be assigned using the 'Formation'   |          | x          |
		|                                | fields on the IHS table of the main window.                                       |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_ihs_management             | Contains all the IHS Management codes that can be assigned using the 'Management' |          | x          |
		|                                | fields on the IHS table of the main window.                                       |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_ihs_matrix                 | Contains all the IHS Matrix codes that can be assigned using the 'Matrix'         |          | x          |
		|                                | fields on the IHS table of the main window.                                       |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_bap_quality_determination  | Contains the BAP determination quality types that can be assigned to Priority     |          | x          |
		|                                | Habitats and Potential Priority Habitats on the Details tab of the main window.   |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_bap_quality_interpretation | Contains the BAP interpretation quality types that can be assigned to Priority    |          | x          |
		|                                | Habitats and Potential Priority Habitats on the Details tab of the main window.   |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_boundary_map               | Contains the list of map types that can be assigned to the 'Boundary Map' and     |          | x          |
		|                                | 'Digitisation Map' fields on the Details tab of the main window.                  |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_importance                 | Contains the difference levels of Importance that can be assigned to Sources      |          | x          |
		|                                | using the 'Boundary Imp.' and 'Habitat Imp.' fields on the Sources tab of the     |          |            |
		|                                | main window.                                                                      |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_process                    | Contains details of all the processes that can be referenced in the 'Process'     |          | x          |
		|                                | field of the main window to indicate the activity being undertaken when using     |          |            |
		|                                | the HLU Tool. See :ref:`lut_process` for more details.                            |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_reason                     | Contains details of all the reasons that can be referenced in the 'Reason'        |          | x          |
		|                                | field of the main window to indicate the activity being undertaken when using     |          |            |
		|                                | the HLU Tool. See :ref:`lut_reason` for more details.                             |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_sources                    | Contains details of all the source datasets that can be referenced as a 'Source'  |          | x          |
		|                                | on the Sources tab of the main window. See :ref:`lut_sources` for more details.   |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+
		| lut_user                       | Contains details of all the users that have editing capability with the HLU Tool  |          | x          |
		|                                | and indicates if they are also able to perform 'bulk' updates.                    |          |            |
		|                                | See :ref:`lut_users` for more details.                                            |          |            |
		+--------------------------------+-----------------------------------------------------------------------------------+----------+------------+


.. seealso:
	See :Ref:`configuring_luts` for more information on configuring lookup tables.


.. raw:: latex

	\newpage

.. _export_tables:

Export Tables
=============

Tables in the database prefixed by 'export' are **export** tables and are used to define different formats that can be used to export data from the HLU Tool database and GIS layers to a new 'standalone' GIS layer.


.. index::
	single: Export Tables; Exports

.. _exports:

exports
-------

This table lists all the export 'formats' that can be used when exporting data.

	export_id
		A unique identifier used to determines which fields are selected from the 'exports_fields' table.

	export_name
		The name which will be displayed in the 'Export Format' drop-down list.

Once a new export format has been added to the 'exports' table the fields to be included in the export must be added to the 'exports_fields' table.

.. index::
	single: Export Tables; Exports Fields

.. _exports_fields:

exports_fields
--------------

This table defines which fields are to be exported for each export format in the 'exports' table. It also defines what the export fields will be called, the order they will appear in the new GIS layer and the number of occurrences of each field (where fields can appear in multiple table records.)

	export_field_id
		A unique identifier for the field.

	export_id
		The unique identifier for the export type in the 'exports' table (see :ref:`exports`).

	table_name
		The name of the source table in the database containing the column to be exported.

	column_name
		The name of the column within the source table.

	column_ordinal
		The number of the column within the source table starting from 1. The export function does not require this column to be completed.

	field_name
		The name of the column in the exported GIS layer. The 'field_name' must be a valid ArcGIS/MapInfo column name (i.e. containing no spaces or special characters.)

	field_ordinal
		Sets the order of the fields in the exported GIS layer.

	fields_count
		Allows users to set the number of child records to be exported.

	fields_type
		Allows users to set the data type of the field to be exported.

	fields_length
		Allows users to set the maximum length of text fields. Text input values longer than this length will be truncated during the export without warning.

	fields_format
		Allows users to determine the format of the exported field.

		.. tabularcolumns:: |L|L|L|

		.. table:: Valid Export Field Formats

			+--------------+-----------------+------------+
			| Field Format |   Description   |  Example   |
			+==============+=================+============+
			| D            | Single day date | 15/10/2010 |
			+--------------+-----------------+------------+



.. note::
	GIS controlled fields such as obj, shape, perimeter, area, x, y, etc. should not be included. These fields will be automatically added to the exported layer.


.. seealso::
	See :ref:`configuring_exports` for more information.


.. raw:: latex

	\newpage

.. index::
	single: Data Tables; Relationships

.. _table_relationships:

Table Relationships
===================

There are 37 tables in the HLU Tool relational database comprised of data tables, lookup tables and export tables. The relationships between the tables are too numerous and complex to display in a single diagram so the tables and relationships have therefore been separated into 7 logical groups, some of which connect and overlap with one another.

.. tip::
	Bespoke relationship diagrams between the various HLU Tool tables can be created using SQL Server Management Studio.


.. raw:: latex

	\newpage

Data Tables
-----------

.. _figDDDT:

.. figure:: ../diagrams/DatabaseDiagramDataTables.png
	:align: center
	:scale: 90

	Database Relationships - Data Tables


.. raw:: latex

	\newpage

IHS Lookup Tables
-----------------

.. _figDDILT:

.. figure:: ../diagrams/DatabaseDiagramIHSLookupTables.png
	:align: center
	:scale: 90

	Database Relationships - IHS Lookup Tables


.. raw:: latex

	\newpage

BAP Tables
----------

.. _figDDBT:

.. figure:: ../diagrams/DatabaseDiagramBAPTables.png
	:align: center
	:scale: 75

	Database Relationships - BAP Tables


.. raw:: latex

	\newpage

Habitat Tables
--------------

.. _figDDHaT:

.. figure:: ../diagrams/DatabaseDiagramHabitatTables.png
	:align: center
	:scale: 85

	Database Relationships - Habitat Tables


.. raw:: latex

	\newpage

Sources Tables
--------------

.. _figDDST:

.. figure:: ../diagrams/DatabaseDiagramSourcesTables.png
	:align: center
	:scale: 90

	Database Relationships - Sources Tables


.. raw:: latex

	\newpage

History Tables
--------------

.. _figDDHiT:

.. figure:: ../diagrams/DatabaseDiagramHistoryTables.png
	:align: center
	:scale: 90

	Database Relationships - History Tables


.. raw:: latex

	\newpage

Other Tables
------------

.. _figDDOT:

.. figure:: ../diagrams/DatabaseDiagramOtherTables.png
	:align: center
	:scale: 85

	Database Relationships - Other Tables


