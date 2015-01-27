*******
Preface
*******

The most up to date version of this documentation can be found in **html** and **PDF** form on `ReadTheDocs <https://readthedocs.org/projects/hlutool-technicalguide/>`_.

Recommended Knowledge
=====================

Administrators
--------------
We recommend that a person within each organisation should be designated as the tool and database administrator. This person should:

* Have an understanding and experience of IT systems management.
* Understand relational database structures.
* Be an expert user of the chosen database system.
* Have qualifications, certified training or equivalent experience in managing databases using that system.
* Have certified training or equivalent experience in advanced features of the relevant GIS software, including defining, joining and exporting layers and creating spatial and attribute indexes.

Users
-----
A user guide is also available at `HLUTool-UserGuide <https://readthedocs.org/projects/hlugistool-userguide/>`_ for those who will be regular users of the HLU Tool but are not concerned with how to install or configure the tool or how to perform database administration.


Reading Guide
=============

This Preface explains a little about the HLU Tool, the community of people who develop and use it, and the licensing conditions for using and distributing it and the associated guides.

:doc:`../installation/installation` details the system requirements and describes how to install the HLU Tool.

:doc:`../configuration/configuration` describes how to connect to a HLU Tool database and GIS application.

:doc:`../access/access` provides instructions on how to link an Access front-end to a SQL Server database.

:doc:`../database/database` outlines the database structure and how to adapt the data for local requirements.

:doc:`../updater/updater` describes the mechanism for apply updates to the database structure and contents.

:doc:`../optimisation/optimisation` introduces tips for optimising the performance of the tool.

:doc:`../appendix/appendix` contains a copy of the GNU Free Documentation License v1.3 covering this guide.


.. index::
	single: Licensing

Licensing
=========

The code for the HLU Tool is 'open source' and is released under `GNU General Public License (GPL) v3 <http://www.gnu.org/licenses/gpl.html>`_. Users are free to install it on as many computers as they like, and to redistribute it according to the GPLv3 license.

This guide is released under `GNU Free Documentation License (FDL) v1.3 <http://www.gnu.org/licenses/fdl.html>`_. Permission is granted to copy, distribute and/or modify this document under the terms of the license.

Please remember, however, that the tool cost a lot of money to develop and still requires further development and ongoing support. Hence any contributions towards costs would be gratefully received. Enquiries can be made via the `ALERC forum <http://forum.lrcs.org.uk/viewforum.php?id=24>`_.


.. index::
	single: Useful Links

Useful links
============

Related community links:

* `Users <http://forum.lrcs.org.uk/viewforum.php?id=24>`_ - Announcements, bug reports, user Q&A and feature discussions.
* `Administrators <https://github.com/HabitatFramework/HLUTool/releases>`_ - Release notes and installers for ArcGIS and MapInfo systems.
* `Developers <https://github.com/HabitatFramework/HLUTool>`_ - Tool source code.
* `Issues <https://github.com/HabitatFramework/HLUTool/issues>`_ - Known issues and existing change requests.


.. index::
	single: Acknowledgements

Acknowledgements
================

Many thanks are due to all the LRCs in the south-east of England and their staff who have, and continue to, fund and contribute to the HLU Tool.  It takes a small army of developers, testers and users to build a truly useful tool (especially users who care enough to test new releases, report bugs and discuss feature requests).


Conventions used in this manual
===============================

The following typographical conventions are used in this manual:

:kbd:`Ctrl-A`
	Indicates a key, or combination of keys, to press.

:guilabel:`Commit`
	Indicates a label, button or anything that appears in user interfaces.

**Tools... --> About**
	Indicates a menu choice, or a combination of menu choices, tab selections or GUI buttons.

:file:`C:\\Program Files\\HLU Tool`
	Indicates a filename or directory name.

.. tip::
	Tips can help save time or provide shortcuts.

.. note::
	Notes explain things in more detail or highlight important points.

.. caution::
	Warnings where administrators should pay attention.

