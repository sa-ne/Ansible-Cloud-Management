# Ansible Cloud Management

Ansible playbooks to manage AWS accounts.

## Tagging Taxonomy

|Tag|Values|Purpose|
|:---|:---|:---|
|AlwaysUp|yes, no, true, false|If positive, the instance should remain online. If negative, the instance should be shutdown automatically|
|Contact|email@redhat.com|A valid email address for primary point-of-contact|
|DeleteBy|YYYY-MM-DD|Expected date the instance will be removed. Used for reporting purposes|

## Roles

### normalize-tags
This role will attempt to normalize tag values. For AlwaysUp, positive values (varying cases of true/yes) will be reset to "true". Negative values (varying cases of false/no) will be reset to "false". Unexpected (invalid) values will always be reset to "false".

### shutdown-instances

This role will query running instances that have the AlwaysUp tag set to "false". If the instance has been running for over 24 hours, it will be shutdown.
