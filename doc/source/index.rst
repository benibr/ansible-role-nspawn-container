=========================================
OpenStack-Ansible nspawn container create
=========================================

Ansible role for creating nspawn containers. This role creates several
directories on the nspawn host for use in bind-mounted storage within the
container.

To clone or view the source code for this repository, visit the role repository
for `nspawn_container_create <https://github.com/openstack/openstack-ansible-nspawn_container_create>`_.

Default variables
=================

.. literalinclude:: ../../defaults/main.yml
   :language: yaml
   :start-after: under the License.

Required variables
==================

None

Example playbook
~~~~~~~~~~~~~~~~

.. literalinclude:: ../../examples/playbook.yml
   :language: yaml
