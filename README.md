yum-elrepo Cookbook
============

The yum-elrepo cookbook takes over management of the default
repositoryids that ship with CentOS systems. It allows attribute
manipulation of base updates extras centosplus contrib.

Requirements
------------
* Chef 11 or higher
* yum cookbook version 3.0.0 or higher

Attributes
----------
The following attributes are set by default

``` ruby
default['yum']['elrepo']['baseurl'] = 'http://elrepo.org/mirrors-elrepo.el6'
default['yum']['elrepo']['baseurl'] = 'ELRepo.org Yum Repository'
default['yum']['elrepo']['gpgkey'] = 'http://elrepo.org/RPM-GPG-KEY-elrepo.org'
default['yum']['elrepo']['enabled'] = true
```

Recipes
-------
* default - Walks through node attributes and feeds a yum_resource
  parameters. The following is an example a resource generated by the
  recipe during compilation.

```ruby
  yum_repository 'elrepo' do
    mirrorlist 'http://elrepo.org/mirrors-elrepo.el6'
    description 'ELRepo.org Yum Repository'
    enabled true
    gpgcheck true
    gpgkey 'http://elrepo.org/RPM-GPG-KEY-elrepo.org'
  end
```

Usage Example
-------------
To disable the elrepo repository through a Role or Environment definition

```
default_attributes(
  :yum => {
    :elrepo => {
      :enabled => {
        false
       }
     }
   }
 )
```

To enable the elrepo repository with a wrapper cookbook, place
the following in a recipe:

```
node.default['yum']['elrepo']['enabled'] = true
include_recipe 'yum-elrepo'
```

More Examples
-------------
Point the elrepo repositories at an internally hosted server.

```
node.default['yum']['elrepo']['enabled'] = true
node.default['yum']['elrepo']['baseurl'] = 'https://internal.example.com/elrepo'
node.default['yum']['elrepo']['sslverify'] = false

include_recipe 'yum-elrepo'
```

License & Authors
-----------------
- Author:: Sean OMeara (<someara@opscode.com>)

```text
Copyright:: 2011-2013 Opscode, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```