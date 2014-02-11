
*********************
Linking to SQL Server
*********************

If your HLU Tool is configured to use SQL Server but some users don't have access to SQL Server's Management Studio (SSMS), or aren't familiar with using SSMS, then one solution is to create an Access data and link it to the HLU Tool database in SQL Server. Many users will be more familiar with Access and linking Access to SQL Server in this way allows users to view and edit the HLU Tool data without any risk of altering the database structure. Using Access as a front-end to the database in this way allows users to create and share Access queries, forms and reports specific to their needs.

.. note::
	Database administrators need to ensure that users of the Access database have the necessary permissions to view, add and edit the target SQL Server database.


.. _new_link:

Linking a new Access database
=============================

The process of linking an Access database to a SQL Server database can be complex and necessitates that you know the connection settings for the target database. The following instructions describe how to link to an existing installation of the HLU Tool database running on SQL Server. It should not matter which version (i.e. SQL Server or SQL Server Express) is installed or which release (as long as it is meets the :ref:`requirements`.

.. sidebar:: Versions of Access

	The steps in this procedure are based on using Microsoft Access 2012. Instructions for different versions of Microsoft Access will vary depending on your version.

1. Make sure your SQL Server service is running and the HLU Tool database is attached.
2. Open the destination Access database in which you wish to create the linked tables.
3. On the 'External Data' tab, in the 'Import & Link' group, click **ODBC Database**.

	.. _figALED:

	.. figure:: ../images/figures/AccessLinkExternalDataTab.png
		:align: center

		External Data tab


5. Click **Link to the data source by creating a linked table** and then click **OK**.

	.. _figALODD:

	.. figure:: ../images/figures/AccessLinkODBCDataDialog.png
		:align: center

		Get External Data - OBDC Database dialog

6. In the 'Select Data Source' dialog box, if the DSN file you want to use already exists, locate and select the DSN file. If you haven't yet created a DSN file for the target database skip to :ref:`create_dsn` then continue from the next step.

	.. _figALSDSD:

	.. figure:: ../images/figures/AccessLinkSelectDataSourceDialog.png
		:align: center

		Select Data Source dialog

	.. note:: Creating a new .dsn file
		If have haven't already created a data source name (DSN) file for the HLU Tool database see :ref:`create_dsn`.

6. Click **OK**. Access will display the 'Link Tables' dialog box.

	.. _figALSLTD:

	.. figure:: ../images/figures/AccessLinkSelectTablesDialog.png
		:align: center

		Select Link Tables dialog

7. Under 'Tables', click each table that you want to link to, and then click **OK**.

.. note::
	Many of the tables in the list are internal SQL Server tables. Do not select these - only select the HLU Tool export, data and lookup tables.

8. If the 'Select Unique Record Identifier' dialog box appears, Access was unable to determine which field or fields uniquely identify each row of the source data. In this case, select the field or combination of fields that is unique for each row, and then click **OK**. If you are not sure, check with the SQL Server database administrator.
9. If the link is successful Access will display the new linked tables in the Objects Navigation Pane.

	.. _figALATD:

	.. figure:: ../images/figures/AccessLinkObjectsNavigationPane.png
		:align: center

		Access Objects Navigation Pane


.. raw:: latex

	\newpage

.. _create_dsn:

Creating a new DSN file
=======================

The following instructions describe how to create a new .dsn file for the HLU Tool database:

.. sidebar:: Versions of Access

	The steps in this procedure are based on using Microsoft Access 2012. Instructions for different versions of Microsoft Access will vary depending on your version.

1. Click **New** to create a new data source name (DSN) file. The 'Create New Data Source' wizard will start.
2. Select **SQL Server** in the list of drivers and then click **Next**. If you are connecting to a different database then select the relevant driver.

	.. _figALSDD:

	.. figure:: ../images/figures/AccessLinkSelectDriverDialog.png
		:align: center

		Create New Data Source - Select Driver dialog

3. If you wish to enter the 'Server Name' and 'Database Name' at this stage click on **Advanced...** and enter them under the DRIVER keyword (see below for example). Then click *OK** to return to the 'Create New Data Source' wizard.
	
	.. _figALADD:

	.. figure:: ../images/figures/AccessLinkAdvancedDSNDialog.png
		:align: center

		Create New Data Source - Advanced DSN dialog

	.. note::
		If you don't enter the 'Server Name' and 'Database Name' here you will be prompted for them later.

4. Click **Next** and then choose a suitable file path and file name for your new DSN. Then click **Save**.
5. The file path and file name of the select DSN will be displayed. Click **Next**.

	.. _figALSDSD2:

	.. figure:: ../images/figures/AccessLinkSelectDataSourceDialog.png
		:align: center

		Select Data Source dialog

6. A summary of the DSN settings will be shown. Click **Finish**.

	.. _figALOSSD:

	.. figure:: ../images/figures/AccessLinkSummaryODBCDialog.png
		:align: center

		ODBC Setup Summary dialog

7. If you didn't enter the server and database names earlier you will be prompted for them now. Enter a description for the data source and then from the list choose which server you want to connect to (if the server doesn't appear in the list then manually type the server name it into the Server field). Then click **Next**.

	.. _figALSSD:

	.. figure:: ../images/figures/AccessLinkSelectServerDialog.png
		:align: center

		Create New Data Source - Select Server dialog

8.	Choose either **Windows NT authentication** or **SQL Server authentication** depending on how the security settings have been defined in the SQL Server database then click **Next**. If you are not sure, check with the SQL Server database administrator.

	.. _figALAD:

	.. figure:: ../images/figures/AccessLinkSQLAuthenticationDialog.png
		:align: center

		Create New Data Source - Authentication dialog

9.	Select the 'Change the default database to' check box and then from the list select which database to connect to. Then click *Next**.

	.. _figALSDBD:

	.. figure:: ../images/figures/AccessLinkSelectDatabaseDialog.png
		:align: center

		Create New Data Source - Select Database dialog

10.	Leave all the settings as the default values and click **Finish**.
11.	A summary of the ODBC Setup will be displayed. Click *Test Data Source ...** to ensure the settings are correct and the connection works and then click **OK** to close the test window.

	.. _figALSD:

	.. figure:: ../images/figures/AccessLinkSummaryDialog.png
		:align: center

		Create New Data Source - Summary dialog

12.	Click **OK** to save the DSN. You will then be returned to the 'Select Data Source' window to continue linking a new database (see :ref:`new_link`).
 

.. note::
	Once you have defined a DSN for your HLU Tool database you won't need to repeat steps 6 to 14 if you need to link another Access database in future.

.. note::
	It is also possible to link the exporter database to other relational databases, such as PostGIS, but instructions for this are not provided in this guide.


.. raw:: latex

	\newpage

.. _update_link:

Updating a linked table
=======================

Each time you open a linked table you will see the latest data displayed in it. However, structural changes made to a SQL Server table are not automatically reflected in a linked table. In this case you will need to update the linked table by applying the latest SQL Server object structure.

.. sidebar:: Versions of Access

	The steps in this procedure are based on using Microsoft Access 2012. Instructions for different versions of Microsoft Access will vary depending on your version.

1. Make sure your SQL Server service is running and the HLU Tool database is attached.
2. Open the destination Access database in which you wish to create the linked tables.
3. On the 'Database Tools' menu click **Linked Table Manager**.

	.. _figARED:

	.. figure:: ../images/figures/AccessRelinkExternalDataTab.png
		:align: center

		External Data tab

4. The 'Linked Table Manager' dialog will appear.

	.. _figARTMD:

	.. figure:: ../images/figures/AccessRelinkTableManagerDialog.png
		:align: center

		Linked Table Manager dialog

5. Select the **Always prompt for new location** check box.
6. Click the tables that you wish to update or click the **Select All** button and then click **OK**.

	.. _figARTMSD:

	.. figure:: ../images/figures/AccessRelinkTableManagerSelectedDialog.png
		:align: center

		Linked Table Manager selected tables

7. If the update if successful Access will display a message to that effect. Otherwise Access will display an error message.

	.. _figARTMSD:

	.. figure:: ../images/figures/AccessRelinkSuccessDialog.png
		:align: center

		Linked Table Manager Success dialog

8. Click **OK** to close the Linked Table Manager.

