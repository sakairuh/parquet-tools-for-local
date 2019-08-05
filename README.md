# how to build

```
git clone https://github.com/apache/parquet-mr.git
cd parquet-mr/parquet-tools
mvn clean package -Plocal
```


# commands


## cat
```
$ java -jar ./parquet-tools-1.9.0.jar cat users.parquet
name = Alyssa
favorite_numbers:
.array = 3
.array = 9
.array = 15
.array = 20

name = Ben
favorite_color = red
favorite_numbers:
```

## dump
```
$ java -jar ./parquet-tools-1.9.0.jar dump users.parquet
row group 0
--------------------------------------------------------------------------------
name:              BINARY SNAPPY DO:0 FPO:4 SZ:36/34/0.94 VC:2 ENC:BIT [more]...
favorite_color:    BINARY SNAPPY DO:0 FPO:40 SZ:32/30/0.94 VC:2 ENC:BI [more]...
favorite_numbers:
.array:            INT32 SNAPPY DO:0 FPO:72 SZ:45/45/1.00 VC:5 ENC:PLAIN,RLE

    name TV=2 RL=0 DL=0
    ----------------------------------------------------------------------------
    page 0:  DLE:BIT_PACKED RLE:BIT_PACKED VLE:PLAIN ST:[no stats for  [more]... VC:2

    favorite_color TV=2 RL=0 DL=1
    ----------------------------------------------------------------------------
    page 0:  DLE:RLE RLE:BIT_PACKED VLE:PLAIN ST:[no stats for this column] [more]...

    favorite_numbers.array TV=5 RL=1 DL=1
    ----------------------------------------------------------------------------
    page 0:  DLE:RLE RLE:RLE VLE:PLAIN ST:[no stats for this column] SZ:28 VC:5

BINARY name
--------------------------------------------------------------------------------
*** row group 1 of 1, values 1 to 2 ***
value 1: R:0 D:0 V:Alyssa
value 2: R:0 D:0 V:Ben

BINARY favorite_color
--------------------------------------------------------------------------------
*** row group 1 of 1, values 1 to 2 ***
value 1: R:0 D:0 V:<null>
value 2: R:0 D:1 V:red

INT32 favorite_numbers.array
--------------------------------------------------------------------------------
*** row group 1 of 1, values 1 to 5 ***
value 1: R:0 D:1 V:3
value 2: R:1 D:1 V:9
value 3: R:1 D:1 V:15
value 4: R:1 D:1 V:20
value 5: R:0 D:0 V:<null>
```

## meta

```
$ java -jar ./parquet-tools-1.9.0.jar meta users.parquet
file:             file:/home/ryohei/sources/parquet-mr/parquet-tools/target/users.parquet
creator:          parquet-mr version 1.4.3
extra:            avro.schema = {"type":"record","name":"User","namespace":"example.avro","fields":[{"name":"name","type":"string"},{"name":"favorite_color","type":["string","null"]},{"name":"favorite_numbers","type":{"type":"array","items":"int"}}]}

file schema:      example.avro.User
--------------------------------------------------------------------------------
name:             REQUIRED BINARY O:UTF8 R:0 D:0
favorite_color:   OPTIONAL BINARY O:UTF8 R:0 D:1
favorite_numbers: REQUIRED F:1
.array:           REPEATED INT32 R:1 D:1

row group 1:      RC:2 TS:109 OFFSET:4
--------------------------------------------------------------------------------
name:              BINARY SNAPPY DO:0 FPO:4 SZ:36/34/0.94 VC:2 ENC:BIT_PACKED,PLAIN
favorite_color:    BINARY SNAPPY DO:0 FPO:40 SZ:32/30/0.94 VC:2 ENC:BIT_PACKED,RLE,PLAIN
favorite_numbers:
.array:            INT32 SNAPPY DO:0 FPO:72 SZ:45/45/1.00 VC:5 ENC:RLE,PLAIN
```

## head

```
$ java -jar ./parquet-tools-1.9.0.jar head users.parquet
name = Alyssa
favorite_numbers:
.array = 3
.array = 9
.array = 15
.array = 20

name = Ben
favorite_color = red
favorite_numbers:

[ryohei@nuc target]$ java -jar ./parquet-tools-1.9.0.jar schema users.parquet
message example.avro.User {
  required binary name (UTF8);
  optional binary favorite_color (UTF8);
  required group favorite_numbers (LIST) {
    repeated int32 array;
  }
```}
