DDBMS
=======

DDBMS is a testbed of an OLTP distributed database management system (DBMS). It supports 6 concurrency control algorithms.

This testbed is based on the DBx1000 system, whose concurrency control scalability study can be found in the following paper:

    Staring into the Abyss: An Evaluation of Concurrency Control with One Thousand Cores
    Xiangyao Yu, George Bezerra, Andrew Pavlo, Srinivas Devadas, Michael Stonebraker
    http://voltdb.com/downloads/datasheets_collateral/vdb_whitepaper_staring_into_the_abyss.pdf
    
Build & Test
------------

Build dependent libraries:

    wget https://github.com/jemalloc/jemalloc/releases/download/4.0.3/jemalloc-4.0.3.tar.bz2
    tar -xf jemalloc-4.0.3.tar.bz2
    cd jemalloc-4.0.3
    ./configure --prefix=/path/to/deneva/jemalloc-4.0.3 --with-jemalloc-prefix=je_
    make -jN
    make install
    
    wget -O nanomsg-0.5-beta.tar.gz https://github.com/nanomsg/nanomsg/archive/0.5-beta.tar.gz
    tar -xf nanomsg-0.5-beta.tar.gz
    cd nanomsg-0.5-beta
    ./autogen.sh
    ./configure --prefix=/path/to/deneva/nanomsg-0.5-beta
    make -jN
    make install

Build Deneva:

    make deps
    make -jN

Configuration
-------------

DBMS configurations can be changed in the config.h file. Please refer to README for the meaning of each configuration. Here we only list several most important ones. 

    NODE_CNT          : Number of server nodes in the database
    THREAD_CNT        : Number of worker threads running per server
    WORKLOAD          : Supported workloads include YCSB and TPCC
    CC_ALG            : Concurrency control algorithm. Six algorithms are supported 
                        (NO_WAIT, WAIT_DIE, TIMESTAMP, MVCC, OCC, CALVIN) 
    MAX_TXN_IN_FLIGHT  : Maximum number of active transactions at each server at a given time
    DONE_TIMER        : Amount of time to run experiment
                        
Configurations can also be specified as command argument at runtime. Run the following command for a full list of program argument. 
    
    ./rundb -h

Run
---

The DBMS can be run with 

    ./rundb -nid[N]
    ./runcl -nid[M]

where N and M are the ID of a server and client, respectively
