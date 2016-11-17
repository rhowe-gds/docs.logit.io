---
date: 2016-03-08T21:07:13+01:00
title: Changing a mapping
menu:
  main:
    pre: <i class="icon-folder-open"></i>
    weight: 21
---

Once an index has data inside it it's mapping cannot be changed, only added too.
This is because changing a mapping without also adjusting the data to match the new mapping
would make it unsearchable.

Logit creates daily (or even hourly) indexes to enable both retention and efficient searching.
This means indexes aren't typically created until data is ingested and thus are never empty.

So to change a mapping we need to adjust what happens at index creation.
A index template is a file that defines the settings and mappings that will be used when an index is created.

You can view your current index templates here

```sh
curl -XGET YOUR-ES-URL/_template?apikey=YOUR-API-KEY&pretty=true
```

The templates are listed out in a name, value structure. To see a specifc template

```sh
curl -XGET YOUR-ES-URL/_template/TEMPLATE-NAME?apikey=YOUR-API-KEY&pretty=true
```

Take the current value and add your adjustments, and replace the current template with your new version

```sh
curl -XPUT YOUR-ES-URL/_template/TEMPLATE-NAME?apikey=YOUR-API-KEY&pretty=true - d 'NEW-TEMPLATE-VALUE'
```

You can check your adjustments by calling the get again too see what the template looks like.

Now the next time a new index is created from the template it will have the new mapping.

We could leave the current index but typically we want indexes to be wildcard searchable meaning
they need non conflicting mappings. Whatmores we probably want to test the new mapping straightaway and 
and don't want to wait a day (or an hour) for a new index to be created. 
Typically mapping changes are done when a logging pattern is being established so it is sufficient to delete the current index. 

You can delete an index by calling

```sh
curl -XDELETE YOUR-ES-URL/INDEX-NAME?apikey=YOUR-API-KEY&pretty=true
```

If the data in the current index is required then it will need to be reindexed using the new mapping.
