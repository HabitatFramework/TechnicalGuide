****************
Database Updater
****************

.. index::
	single: Database Updater

In order to apply structural and data changes to the HLU tool database you will need to use the HLU Tool Database Updater **HLUDbUpdater.exe**. The HLU Tool Database Updater provides an automated mechanism of applying changes to a target HLU Tool relational database. It will process one or more script files and execute all the SQL commands in the files.


.. _database_updater_source_code:

**Source Code**
	The source code for this program is open source and can be downloaded from <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater>.

.. _database_updater_latest_release:

**Latest Release**
	The latest release of this program can be downloaded from <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater/releases>.

.. _database_updater_latest_scripts:

**Latest Scripts**
	The latest scripts for this program can be downloaded from <https://github.com/HabitatFramework/HLUTool-DatabaseUpdater/archive/scripts.zip>.


.. index::
	single: Database Updater; Requirements

System Requirements
===================

The HLU Tool Database Updater requires the following to operate:

**Hardware**

	* 2 GHz or higher processor
	* 2 GB RAM
	* 10 MB of free hard disk space


**Software**

	* Microsoft Windows XP/2003/2008/Vista/Windows 7 or Windows 8
	* Microsoft .NET Framework 3.5 SP1, 4.0, or 4.5 installed


.. index::
	single: Database Updater; Instructions

Instructions
============

The program does not need to be installed - it can be run as a standalone program and will connect to any of the HLU Tool relation database formats, including Access, SQL Server, PostgreSQL and Oracle (although connections to PostgreSQL and Oracle have not been tested). However, it must be run by a user with sufficient database permissions to drop, create & alter tables and to delete, insert, update and select data in the target relational database.

To run the program:

	* Download and unpack the latest .zip release file (see :ref:`database_updater_latest_release`).
	* Download the latest scripts from GitHub (see :ref:`database_updater_latest_scripts`).
	* Ensure that any scripts to be processed are placed in the 'Scripts' folder directly under the program path.
	* Double-click the program to start it.
	* Click :guilabel:`Connect` to connect to the target database to be updated.
	* Follow the instructions to select the connection type and target database.
	* Click :guilabel:`Ok` once the connection has been established.
	* Click :guilabel:`Proceed` to process the script files found in the 'Scripts' folder.
	* Progress bars and a text window will show the progress and success of the processing.
	* Click :guilabel:`Close` once all scripts have been processed.
	
.. tip::
	If you have more than one target HLU tool database, copy the script files from the 'Scripts/Archive' folder back into the'Scripts' folder and run the program again - connecting to the next database to be updated.

