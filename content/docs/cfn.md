---
title: "Cloud Formation"
# bookFlatSection: false
# bookToc: 6
# bookHidden: false
---
# Cloud Formation
**Cloud formation template** defines Cloud Formation **stack**. Stack creates, updates, deletes resources based on template

* Template an be written using __JSON__ or __YAML__
* Template an contain up to 200 resources
* When Stack is deleted - all resources are deleted
* Stack can be updated with new version of template
* When __logical__ resources added to templates new __physical__ resources added to stack
* When __logical__ resources deleted - __physical__ are deleted
* When __logical__ resources updated - __physical__ can be updated or deleted (depends on resource)


## Template elements
* Version
* Description. __Should go after version if defined__
* Metadata
* Parameters
* Mappings
* Conditions
* Transforms
* Outputs
* Resources

