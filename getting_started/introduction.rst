============
Introduction
============

A Package and Dependency Manager for Code Igniter
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Splint is a product inspired by the wonderful core of CodeIgniter, a light-weight MVC Framework with a 
lot of functionalities embedded in it.

`Composer <https://getcomposer.org/>`_ has always been the package and dependency manager for php all round 
since the dawn of time, however, when it comes to using libraries from Composer within a Code Igniter project, 
the library can't fully take advantage of the functionalities that Code Igniter offers. Hence, these libraries 
end up re-writing the functions for features that might already exist within Code Igniter. After all, composer is 
a generic repository for all php packages regardless of the framework being used.

This can lead to bloated distributions of Code Igniter projects/applications, or even a slightly less effective 
duplicate of a function that Code Igniter offers already.

Splint provides a way for which developers can write libraries and at the same time use the functionalities which 
CodeIgniter provides (such as Image Processing, Form Validation, Zip Class, Database Libraries, etc.) to provide 
efficient and powerful light-weight libraries.

Writing libraries for Splint also gives you the ability to write sub CodeIgniter applications that can be installed 
within a CodeIgniter application bundle.

This means you can split your project into functional units and turn some of them that you find repeatedly useful 
into Splint packages so that all you need to do when working on a new project and require such functionality, is to 
run the ''splint install'' command from the root of your Code Igniter project within a terminal window.

Install and use a Splint Library
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To use a Splint library, simply download and install the Splint client from `here <https://splint.cynobit.com/downloads/splint>`_ 
then run ``splint install <vendor\library_name>`` at the root of your CodeIgniter project with a terminal for a given package.

All Splint packages are hosted on `GitHub <https://github.com>`_ so you can visit the package's GitHub page and view it's README 
on how to load/use it.

The README appears on the packages's page on the `Splint <https://splint.cynobit.com>`_ website as well.

.. code-block:: php

   $this->load->splint("vendor_name/library_name", "+LibraryClassName" , $params, "alias"); // Library loaded and initialized with $alias.
   $this->alias->someMethod();

The ``$this->load->splint();`` method call among others, is available when you patch your ``Loader`` class and fortunately, the Splint command 
line tool does that automatically for you the moment you install a library. 

Notice the ``+`` character before ``LibraryClassName`` in the above code. This tells splint to load a library from the specified package 
``vendor_name/library_name`` or rather search for a ``php`` file in with the name ``LibraryClassName`` from the libraries folder in the specified 
package and load it.

You can also load ``views``, ``models``, ``helpers`` and ``configs``. All you need to do is use the required character as a prefix to the file 
name of the asset or php file you want to load from the package.

Load Prefixes
^^^^^^^^^^^^^

The table below shows the characters and what they instruct the splint loader to load/search for.

+-----------+---------+
| Character | To Load |
+===========+=========+
| ``+``     | Library |
+-----------+---------+
| ``*``     | Model   |
+-----------+---------+
| ``-``     | View    |
+-----------+---------+
| ``@``     | Config  |
+-----------+---------+
| ``%``     | Helpers |
+-----------+---------+

Examples
^^^^^^^^
For a library called ci-preference created by a vendor named francis94c, we can load a ``Library``, 
``Model``, ``View``, ``Config``, or ``Helper`` in the manner shown below.

.. code-block:: php
   
   // Library.
   $this->load->splint("francis94c/ci-preference", "+CIPreferences", null, "prefo");
   $this->prefo->get("a_key", "defaultVal");
   // Model.
   $this->load->splint("francis94c/ci-preference", "*ModelClass", "alias");
   $this->alias->someMethod();
   // View.
   $this->load->splint("francis94c/ci-preference", "-view_header", array("text" => "Hello"));
   // Config.
   $this->load->splint("francis94c/ci-preference", "@config_file");
   // Helper.
   $this->load->splint("francis94c/ci-preference", "%helper");

Load Multiple Libraries Or Resources
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can load libraries/resources at the same time using an array of associative arrays of arrays as shown below.

.. code-block:: php

   $autoload = array();
   $autoload[] = array("library" => array("CIPreferences", null, "alias"));
   $autoload[] = array("model"   => array("CIPrefModel", "alias"));         // Model with alias.
   $autoload[] = array("model"   => "CIPrefModel");                         // Model without alias.
   $autoload[] = array("config"  => "pref_config");                         
   $autoload[] = array("helper"  => "pref_helper");                         
   $autoload[] = array("view"    => "view_name");                           

   $this->load->splint("francis94c/ci-preference", $autoload);

   // For loaded library.
   $this->alias->someMethod();
   
