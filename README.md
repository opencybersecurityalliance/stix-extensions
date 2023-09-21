# custom-stix-extensions

This repository contains proposed extensions to the [STIX](https://oasis-open.github.io/cti-documentation/stix/intro.html) standard. 

Though robust, there are still gaps in the threat intel data that can be represented in STIX. The standard allows for custom objects and properties. However, if every source uses it's own names and definitions for these new extenions, this can lead to fragmentation of the data we wish to represent.

This repostitory attempts to normalize custom STIX etensions. This will reduce the duplication of data and allow for frederated search across like-for-like STIX objects and properties, regardless of the source.