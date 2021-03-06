
.. _util.sh:

util.sh
=======

The ``util.sh`` script can add a file to be monitored by ``ospatrol-logcollector``. 
It can also add a full_command to check for changes to a website, or for changes to the name server of a domain.  

A `blogpost <http://dcid.me/2011/10/3woo-alerting-on-dns-ip-address-changes/>`_ from Daniel Cid (for 3WoO) introduced this utility.

util.sh argument options
~~~~~~~~~~~~~~~~~~~~~~~~

.. program:: util.sh

.. option:: addfile <filename> [<format>]

    Add a file to be monitored by ``ospatrol-logtest``. A ``localfile`` will be added to the ospatrol.conf.

.. option:: addsite <domain>

   Monitor a website for changes. A ``full_command`` will be added to the ``ospatrol.conf`` using lynx to dump the initial page.
   A rule can be written to monitor this output for changes.

   .. note::
      Requires `lynx <http://lynx.isc.org/current/>`_.

   .. warning::
      This may not be useful on pages with dynamic content.

.. option:: adddns <domain>

   Monitor the name server of a domain for changes. A ``full_command`` will be added to the ospatrol.conf using host

   .. note::
      Requites the ``host`` command.

util.sh example usage
~~~~~~~~~~~~~~~~~~~~~

Example: Running util.sh
^^^^^^^^^^^^^^^^^^^^^^^^

Running the following command:

.. code-block:: console

    # /var/ospatrol/bin/util.sh adddns ospatrol.net

will add the folling to that system's ``ospatrol.conf``:

.. code-block:: console

  <ospatrol_config>
     <localfile>
       <log_format>full_command</log_format>
       <command>host -W 5 -t NS ospatrol.net; host -W 5 -t A ospatrol.net | sort</command>
     </localfile>
   </ospatrol_config>


