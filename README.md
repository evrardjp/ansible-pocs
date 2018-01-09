This tests ansible 2.4 relative include behavior.

Step 1
======

Create an ansible.cfg so that you can define where your roles will be stored (this folder should do)

Step 2
======

Go into this folder. You should have a tasks/ folder relative to a playbook named test.yml.
This test.yml loads a role, not tasks.

Step 3
======

Run ansible-playbook test.yml. See it execute tasks/relative.yml instead of the role relative include.

-- That's for me an unexpected behavior but it runs the same under ansible 2.3 and ansible 2.4

Step 4
======

Go to roles/include-relative-failure2 folder. This is to confirm the phenomenon.

Step 5
======

Run ansible-playbook tests/test.yml. See it execute tasks/relative.yml from include-relative-failure2
instead of the role asked in the playbook.

-- This is a discrepency compared to ansible 2.3

This proves that the precedence has changed between Ansible 2.3 and 2.4, with paths from the CLI/playbookdir
having more precedence for the include than paths from the role itself, in a role.


Results
=======

For 2.3, during step 5 (-vv):

TASK [include-relative-failure : debug] ********************************************************************************************************************************************************************************************************************************************************************
task path: /Users/jean0000/evrardjp/ansible-pocs/roles/include-relative-failure/tasks/another-relative.yml:2
ok: [localhost] => {
    "changed": false,
    "msg": "This is a role relative include"
}

For 2.4 during step 5 (-vv):

TASK [include-relative-failure : debug] ********************************************************************************************************************************************************************************************************************************************************************
task path: /Users/jean0000/evrardjp/ansible-pocs/roles/include-relative-failure2/tasks/another-relative.yml:2
ok: [localhost] => {
    "msg": "This is a task relative from my run dir"
}
