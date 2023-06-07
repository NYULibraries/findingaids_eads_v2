# Special Collections Finding Aids EAD Repository

This repository contains a live cut of the ArchiveSpace-exported EADs describing finding aids from various NYU-associated special collections. This data is harvested into a Solr index for the [finding aids discovery portal](https://github.com/NYULibraries/specialcollections).

The [EAD publishing tool](https://github.com/NYULibraries/git_transactor) has a hook to push out changes here, therefore maintaining one up-to-date repository of EADs.

## Polling Changes and Reindexing

**[The full documentation for the K8s jobs is in a private repos now](https://github.com/NYULibraries/nyulibraries_kubernetes/tree/master/charts/specialcollections)**

### Reindexing changed files in real-time

A K8s job is triggered every time this index is updated. This job calls [a re-index task](https://github.com/NYULibraries/ead_indexer/tree/64d4e0048bf687da15016654d371895ca1a77a1f) which gets the previous commit and updates the Solr index with all the changed files.

### Reindexing changed files nightly and weekly 

In addition to real-time updates we run a nightly job that re-indexes any files changes in commits over the past 24 hours and a weekly job that re-indexes changes in commits over the past 7 days. This serves as a failsafe for any failed rebuilds.

### Full reindex

There is also a job for running a full reindex in case things get out of sync. **Note that these full reindex jobs can take up to 5 days.**

### Single EAD reindex

We can also run single index jobs for a named EAD.
