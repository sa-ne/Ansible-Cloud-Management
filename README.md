# Ansible Cloud Management

Ansible playbooks to manage AWS accounts.

## Tagging Taxonomy

|Tag|Values|Purpose|
|:---|:---|:---|
|AlwaysUp|yes, no, true, false|If positive, the instance should remain online. If negative, the instance should be shutdown automatically|
|Contact|email@redhat.com|A valid email address for primary point-of-contact|
|DeleteBy|YYYY-MM-DD|Expected date the instance will be removed. Used for reporting purposes|

## Roles

### google-hangouts-chat

A use-case specific implementation of Google Hangouts Chat webhooks.

### normalize-tags

This role will attempt to normalize tag values. For AlwaysUp, positive values (varying cases of true/yes) will be reset to "true". Negative values (varying cases of false/no) will be reset to "false". Unexpected (invalid) values will always be reset to "false".

### shutdown-openshift-clusters

This role will query for OpenShift clusters that have the AlwaysUp tag set to "false". It will also determine the longest running instance time, and shutdown the whole cluster if that time is over 48 hours.

### shutdown-instances

This role will query running instances that have the AlwaysUp tag set to "false". If the instance has been running for over 48 hours, it will be shutdown.

### util/route53-delete-zone

An attempt to purge all records from a route53 zone and delete the zone itself.

Example:

```yaml
- name: Delete Zones
  include_role:
    name: route53-delete-zone
    vars:
      aws_zone: "my.zone.local."
```