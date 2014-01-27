************
Introduction
************

Requirement for Tool
====================

In August 2009 Hampshire Biodiversity Information Centre (HBIC) awarded exeGesIS SDM the contract to develop a new toolkit which would manage their Habitat and Land Use spatial data. The new toolkit would be used by HBIC and Local Record Centres in the South-East of England, and therefore needed to be compatible with both ArcGIS and MapInfo.

The Habitat and Land Use (HLU) data consisted of a set of habitat polygons. Each habitat polygon had approximately 80 attributes. The decision was taken by Local Records Centres to split these habitat polygons into Ordnance Survey (OS) Mastermap derived polygons.

Whilst there are benefits to splitting the habitat polygons by OS Mastermap, such as ensuring polygon boundaries are accurate, the splitting process significantly increases the volume of data. On average, there are 33.5 Mastermap-derived polygons for each habitat polygon in the HLU data.

For example, the table below indicates the effect on a 500 polygon dataset if the data was held in a single GIS layer.

.. tabularcolumns:: |L|R|R|

.. table:: Effect of OS Mastermap Split (Single Dataset)

	+-----------------+-------------+--------------------+
	|                 | Original    | Split by Mastermap |
	+=================+=============+====================+
	| Polygons        |         500 | 16,750             |
	+-----------------+-------------+--------------------+
	| Attributes      |      40,000 | 1,340,000          |
	+-----------------+-------------+--------------------+
	| Total           |      40,500 | 1,356,750          |
	+-----------------+-------------+--------------------+

Due to the complexity of the attribute data required by the Local Records Centres and to minimise data duplication, the habitat attribute and spatial data were split into a relational database with an associated GIS layer. Splitting the attribute and spatial data, reduces the number of attributes required for the spatial layer to 6.

This offers a significant reduction in total attributes as shown in the table below. Nevertheless, there is still a significant increase in data volume versus the original HLU dataset.

.. tabularcolumns:: |L|R|R|

.. table:: Effect of OS Mastermap Split (Attribute and Spatial Datasets)

	+--------------------+----------+------------------------+
	|                    | Original | Attribute database and |
	|                    |          | associated GIS Layer   |
	+====================+==========+========================+
	| HLU Records        | 500      | 500                    |
	+--------------------+----------+------------------------+
	| HLU Attributes     | 40,000   | 40,000                 |
	+--------------------+----------+------------------------+
	| Spatial Polygons   |          | 16,750                 |
	+--------------------+----------+------------------------+
	| Spatial Attributes |          | 100,500                |
	+--------------------+----------+------------------------+
	| Total              | 40,500   | 157,750                |
	+--------------------+----------+------------------------+

The HLU GIS Tool provides a user interface for maintaining the habitat and spatial data, including changes to attributes and changes to the spatial data. It also provides an audit trail to indicate when it was last edited, why and by whom.

The toolkit provides an interface that links the spatial and attribute data in multiple software environments. It can link ArcGIS and MapInfo with databases held in Access or SQL Server In principle, the toolkit could link to other database systems such as PostgreSQL and Oracle but these have not been tested and are not supported.

The performance of the tool is limited by the capabilities of third party software, particularly GIS software, which were not designed to handle large datasets split across multiple platforms.

In addition, one of the key requirements for this tool was the ability to use multiple GIS and database environments. Significant improvements in performance could have been achieved if the tool had been designed to work with a single environment e.g. ArcGIS and SQL Server but multiple environment functionality was a key requirement.

The HLU GIS Tool has been optimised as far as possible and there are no further technological enhancements that can be made to significantly improve performance. It is important therefore to ensure performance is optimised wherever possible through user operation. The following section suggests some simple approaches to improving performance.

The code for the HLU GIS Tool is ‘open source’.

.. raw:: latex

	\newpage

Optimising Performance
======================

Creation of ArcGIS Map Document or MapInfo Workspace
----------------------------------------------------

An ArcGIS Map Document (.mxd) or MapInfo Workspace (.wor) must be created for use with the HLU GIS Tool. This should be optimised to ensure maximum performance, which should include the following:

* Ensure that the .mxd or .wor file only contains one copy of the HLU layer
* Add zoom layering to datasets so that detailed datasets such as the HLU layer and aerial photography are not displayed at smaller scales. Our recommended maximum extents are:

	* ArcGIS – Do not display out beyond:

		* HLU Layer:		1:24,000
		* Aerial Photography:	1:10,000

	* MapInfo – Max Zoom:

		* HLU Layer:		7.5 km
		* Aerial Photography:	3 km

* Ensure that the .mxd or .wor is saved at a sensible view level such as 1:10,000 scale rather the full extent of the HLU dataset

Use of HLU GIS Tool with ArcGIS or MapInfo
------------------------------------------

It takes a significant length of time for ArcGIS or MapInfo to draw an entire HLU GIS layer, therefore care should be taken when using certain tools to avoid this issue.

* ‘Zoom to Selection’ is useful for identifying the habitat polygons on the map, however if zoom layering is not used it may take a significant length of time to display the result depending upon the number of polygons selected and their geographical distribution.
* ‘Select by Attributes’ performs complex queries and selects the results in the GIS window. If a large number of results are returned, it could take a long time to select the spatial polygons in the GIS.
* If the layer is taking a long time to draw, pause or cancel the drawing using:

	* ArcGIS - Click the Pause button in the bottom left corner of the map window
	* MapInfo – Press the Esc key on your keyboard

* For ArcGIS users, if an ArcMap error occurs when the tool is used, check that the HLU ArcMap Extension is enabled in Tools > Extensions – see section ref:`?`.
* For ArcGIS users, we strongly recommend that the HLU layer is stored as a file geodatabase or personal geodatabase. **The tool will be significantly slower if the HLU layer is stored as a shapefile due to the limitations of the file format.**

	.. topic:: Example

	**Exporting 152 features takes 18 minutes from a shapefile but takes under 3 minutes from a file geodatabase.**

* For MapInfo users, ensure the Cosmetic layer is editable when digitising a polygon for a split operation. The polygon will be added to the layer much faster than if the HLU layer was used and also removes the possibility that the polygon is not deleted after the split.

Selection of Database Type
--------------------------

The HLU GIS Tool is supplied with both Microsoft Access 2000 and SQL Server 2008 databases.

Microsoft Access is a versatile desktop database application, but does not have the same performance as other database systems. Database management systems such as SQL Server are optimised to handle large data volumes and complex queries, and can be significantly faster.

We therefore recommend using the HLU GIS Tool with SQL Server or a similar database management system, as this will improve performance when filtering the database records and updating attribute data.

Local vs. Network Storage
-------------------------

It is important to remember that application performance will depend upon the data transfer speed. Data stored locally on a single computer will provide good performance, but will limit access to the data to a single user. Data stored on a network drive is accessible to all users, but performance will be limited by the speed that the data can be transferred across the network.

Data Management
---------------

Only one copy of the database and the GIS layer should be used to avoid data becoming corrupted. If multiple copies are used e.g. an ArcGIS layer and a MapInfo layer or an Access database and a SQL Server database, changes to one GIS layer or database will not be present on the other, causing a mismatch between the attribute and spatial data.

Habitat data must not be edited directly in either the database or the GIS layer. Any modifications made outside the HLU GIS Tool could cause data corruption particularly if unique identifiers are altered.

However, if additional entries are required in the lookup tables, these may be added to the database directly. It is essential that the structure of these tables is not altered and we recommend that any updates to the data in these tables are carried out solely by the database administrator.

