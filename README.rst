========================
Team and repository tags
========================

.. image:: http://governance.openstack.org/badges/deb-zaqar-ui.svg
    :target: http://governance.openstack.org/reference/tags/index.html

.. Change things from this point on

===============================
zaqar-ui
===============================

Zaqar Dashboard

* Free software: Apache license
* Source: http://git.openstack.org/cgit/openstack/zaqar-ui
* Bugs: http://bugs.launchpad.net/zaqar-ui

Enabling in DevStack
--------------------

Add this repo as an external repository into your ``local.conf`` file::

    [[local|localrc]]
    enable_plugin zaqar-ui https://github.com/openstack/zaqar-ui

Manual Installation
-------------------

Begin by cloning the Horizon and Zaqar UI repositories::

    git clone https://github.com/openstack/horizon
    git clone https://github.com/openstack/zaqar-ui

Create a virtual environment and install Horizon dependencies::

    cd horizon
    python tools/install_venv.py

Set up your ``local_settings.py`` file::

    cp openstack_dashboard/local/local_settings.py.example openstack_dashboard/local/local_settings.py

Open up the copied ``local_settings.py`` file in your preferred text
editor. You will want to customize several settings:

-  ``OPENSTACK_HOST`` should be configured with the hostname of your
   OpenStack server. Verify that the ``OPENSTACK_KEYSTONE_URL`` and
   ``OPENSTACK_KEYSTONE_DEFAULT_ROLE`` settings are correct for your
   environment. (They should be correct unless you modified your
   OpenStack server to change them.)


Install Zaqar UI with all dependencies in your virtual environment::

    tools/with_venv.sh pip install -e ../zaqar-ui/

And enable it in Horizon::

    cp ../zaqar-ui/zaqar_ui/enabled/_1510_project_messaging_group.py openstack_dashboard/local/enabled
    cp ../zaqar-ui/zaqar_ui/enabled/_1520_project_queues.py openstack_dashboard/local/enabled

To run horizon with the newly enabled Zaqar UI plugin run::

    ./run_tests.sh --runserver 0.0.0.0:8080

to have the application start on port 8080 and the horizon dashboard will be
available in your browser at http://localhost:8080/
