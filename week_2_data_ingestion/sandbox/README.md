# Data Lake

Data Lakes are essentially places to read in data as quickly as possible. It's basically a big `data_raw` directory that everything is dumped into so data scientists, data engineers, ML engineers, or their pipelines can get at the data as soon as possible.

Must be secure, scalable, and potentially support fast write.

# ETL: Extract Transform Load

Mainly for feeding data warehouses, which are much smaller than data lakes as they are fed by pipelines that enforce some structure on the data.

# ELT: Extract Load Transform

Mainly for speed. As you load before you transform, structure/schema errors can propagate further.

## Drawbacks of Data Lakes

Format creep can make it very difficult to work with a data set, and as a separate stream is needed to keep track of metadata, it's easy for metadata to get lost.