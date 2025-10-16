# Extended rrivctl commands



## History

### list history

#### Synopsis

```
list history <device id or connected device>
```

#### Description

List the history of configurations set on a device.  This takes a summarized form, with more detail available via the get history command



### get history

#### Synopsis

```
get history <device id> <timestamp>
```

#### Description

List the full configuration for a device at the time in question



## Library

### list library&#x20;

#### Synopsis

```
list library <type> 
```

#### Description

List library configurations stored for a given type, filterable by context



#### Types

| Type Name  | Description                                                        |
| ---------- | ------------------------------------------------------------------ |
| snapshot   | A combination of datalogger and sensor config that has been stored |
| sensor     | A library config for a single sensor                               |
| datalogger | Configuration for just the datalogger                              |

#### Options

\--context \<context> : filter by context

\--sensor \<sensor type id> : filter sensor libraries by sensor type



### get library

#### Synopsis

```
get library <library id>
```

#### Description

Output the complete library configuration linked to the library id



## Snapshot

### save snapshot

```
save snapshot
```
