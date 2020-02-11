:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

How To
======

Clean up **All** Job Workspaces
-------------------------------

Leeroy runs the `jenkins-node-cleanup`_ job periodically in order to
automatically clean up job workspaces when the node on which they are located
drops below a set free space threshold. In the event that there is stale state
and/or corruption of workspaces, there is a job parameter named
``FORCE_CLEANUP`` that when set to ``true``, will force workspaces on a node to
be cleaned up regardless of the remaining free space.

.. note::

   This is a big hammer. Use it wisely.

.. note::

   `jenkins-node-cleanup`_ does not remove the workspace of running builds.  As an example, if a ``stack-os-matrix`` build is running when `jenkins-node-cleanup`_ is triggered, even with ``FORCE_CLEANUP==true``, the ``stack-os-matrix`` workspaces on active node(s) will not be disturbed.

.. figure:: /_static/jenkins-node-cleanup_force_cleanup.png
   :name: fig-jenkins-node-cleanup_force_cleanup
   :alt: Jenkins screenshot

   Example of triggering a build with ``FORCE_CLEANUP==true``:

.. _jenkins-node-cleanup: https://ci.lsst.codes/blue/organizations/jenkins/sqre%2Finfra%2Fjenkins-node-cleanup/activity

Disable OSX jobs
----------------

To disable OSX jobs, you must comment out sections of `build_matrix.yaml`_.
Note that there are two secctions that need comments.
Make sure not to miss commenting out the tarball builds as well.

.. _build_matrix.yaml: https://github.com/lsst-dm/jenkins-dm-jobs/blob/master/etc/scipipe/build_matrix.yaml

Make a branch, then you can make your edits.
File a PR, and when approved self merge or the reviewer can do so.

See the following screenshot from an example `PR`_.

.. figure:: /_static/disable_osx_diff.png
   :name: disable_osx_diff
   :alt: PR screenshot

   Example diff of a PR for turning off OSX builds.

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
