This tests tags and their include.

Context
=======

A contributor of ansible-keepalived wanted to avoid 'tags: always'
Reason: On his environement, the lookup failed (yet another include precedence failure I guess).
While we need to figure out why the inclusion failed, we can try to avoid the tag always.

But how?

Step 1
======

Any role can't know what it is wrapped with (check the test-install playbook).
So we can only figure out the tags that are inside the role.

If we replace the 'always' tag with ALL THE TAGS of the role, it could work.

PoC in this branch.

Step 2
======

Run ansible-playbook -i inventory play.yml --tags keepalived.
It does all the tasks, as expected.

Run ansible=playbook -i inventory play.yml --tags keepalived-config 
It does only config tasks, as expected.

Run ansible-playbook -i inventory play.yml --tags etcd
It skips the include and skip all the role tasks, as expected.
