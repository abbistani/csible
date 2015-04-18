CSIBLE
======

An Ansible + Rake wrapper to interact with the CollectionSpace backend REST API.

Configuration file
------------------

```bash
cp api.json.example api.json
```

Edit `api.json` as needed. See [Ansible](docs/ANSIBLE.md) for more detail.

Quickstart
----------

Requires `rake` (Ruby):

```bash
gem install rake
gem install json

rake cs:config # dump api.json to terminal

# GET
rake cs:get:path[/media]
rake cs:get:path[/locationauthorities/38cc1b61-a597-4b12-b820/items,kw=EwoodPark702918]
rake cs:get:url[https://cspace.lyrasistechnology.org/cspace-services/locationauthorities]

# GET items from a list with properties delimitied by "~" written to CSV
rake cs:get:list[/media,uri~csid,"wf_deleted=false&pgSz=100"]

# POST
rake cs:post:directory[/locationauthorities/38cc1b61-a597-4b12-b820/items,locations,1]
rake cs:post:file[/locationauthorities/XYZ/items,examples/locations/1.xml]

# DELETE
rake cs:delete:path[/locationauthorities/38cc1b61-a597-4b12-b820/items/a22a97ec-57fc-4b86-a366]
rake cs:delete:url[https://cspace.lyrasistechnology.org/cspace-services/locationauthorities/38cc1b61-a597-4b12-b820/items/a22a97ec-57fc-4b86-a366]
rake cs:delete:file[deletes.txt] # assumes file of urls
rake cs:delete:file[deletes.txt,path] # file of paths
```

Depending on the actions it may be necessary to clear the `imports` and / or `tmp` folders:

```bash
rake cs:clear:imports
rake cs:clear:tmp
```

These tasks ensure that only XML files are removed.

Raw Examples
------------

See the [Ansible](docs/ANSIBLE.md) docs for detailed instructions.

Tidy XML output
---------------

CollectionSpace GET requests return XML. To improve readability:

```bash
sudo apt-get install libxml2-utils
xmllint --format response.xml
```

---
