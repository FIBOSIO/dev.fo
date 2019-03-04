---
title: Node Introduction
type: tutorials
language: en
order: 300
---

## What is a node

A node is the the terminal responsible for maintaining the running of the network.

In the Internet field, all data operation of an enterprise is centralized in its own server, so this server is a node.

For example, WeChat, which we use, processes so much chat information and money trasnfers every day. The data is stored and run on Tencent's servers. So the server that processes the data, we can call it a node.

Each node in the blockchain network is equivalent to every computer or server terminal that stores all the block data. The production of all new blocks, as well as verification and accounting of transactions, and broadcasting them to the entire network synchronously, is done by the nodes.

Simply put, nodes are dedicated workers. In EOS, nodes on the public chain are rewarded with cryptocurrency by voting, and the top 21 nodes get billing rights and provide services.

## FIBOS Node Type

As we all know, FIBOS is a side chain of EOS, so FIBOS also adopts the DPOS consensus mechanism, and the nodes are divided into super nodes (BP) and ordinary nodes.

The super nodes of FIBOS are the 21 nodes from the standby nodes that have been voted by all coin-holders to obtain the accounting rights.

Supernodes are the core practice of the DPOS consensus. First, because of the decentralized voting mechanism, DPOS is more democratic than other consensus algorithms and is not easy to be monopolized by large holders of the currency.

The 21 supernodes are all created by fair and fair voting. If 21 node representatives fail to perform their duties, such as not generating blocks in time when it is their turn to work, they are removed from the list and a new supernode is selected by the community to replace them.

Second, because the number of nodes is reduced, the operation efficiency of 21 supernodes is higher. It claims to be able to achieve millions of TPS per second under optimal conditions. This exceeds the efficiency of all the running public chain now, and the future is incalculable.

Although the number of supernodes in general is small and some "decentralization" components are sacrificed, it does not lead to the disadvantages of centralization, because any node that does not comply with the constitution of FIBOS will be rejected and replaced by a democratic vote.

In addition, the block order of these 21 nodes and the audit order of the whole network transaction are all set randomly by the system and will change at any time, which can effectively upgrade, prevent cheating and avoid hard bifurcation.

Last but not least, the number of supernodes can be flexible and is not immutable. FIBOS is a community-driven project, so when the number of supernodes cannot meet the development of the project, the community can vote to increase the number of nodes.

## FIBOS Network node information

The current FIBOS network is divided into the FIBOS TestNet and FIBOS main network. The FIBOS foundation has provided several supernodes to help both run since they were launched. Among them, the supernodes of the FIBOS main network have all been replaced by the supernodes entered later. the TestNet is still run by the supernodes provided by the foundation.

### FIBOS TestNet

FIBOS TestNet is a p2p-connected testing chain with FIBOS nodes, which is convenient for developers to test and verify.

Root BP connection information:

```
IP : 'http://api.testnet.fo'
chainID : '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a'
```

Support FIBOS TestNet, account registration: <http://api.testnet.fo/>

(Default account sends 10 EOS to pass-through)

HTTP List

|              URL                | HTTP port |
| :-----------------------------: | :-------: |
|     http://api.testnet.fo     |   80    |


P2P List

|          URL            s| P2P port |
| :---------------------: | :------: |
|  p2p.testnet.fo   |   9870   |


### FIBOS Main Net

At 0 UTC on August 28, 2018, FIBOS main network was successfully launched. The five nodes of Seoul, Tokyo, Canada, London and Virginia successfully connected and produced blocks.

FIBOS RPC List

The RPC HTTP address of part of FIBOS main network is shown as follows:

| Location      | URL(http)                     |
| ------------- | ----------------------------- |
| Tokyo         | http://api.fibos.me           |
| Hong Kong     | http://rpc-mainnet.fibscan.io |
| Oregon        | http://api.bitze.site         |
| San Francisco | http://api.fibos.icu          |
| London        | http://api.fibosutility.com   |

The RPC HTTPS address of part of FIBOS main network is shown as follows:

| Location     | URL(https)                     |
| ------------ | ------------------------------ |
| Tokyo        | https://api.fibos.me           |
| Hong Kong    | https://rpc-mainnet.fibscan.io |
| Oregon       | https://api.bitze.site         |
| San Francisco| https://api.fibos.icu          |
| London       | https://api.fibosutility.com   |

P2P List

The P2P address of the main network of FIBOS is shown as follows:

| Location     | URL(P2P)                     |
| ------------ | ---------------------------- |
| Tokyo        | p2p.mainnet.fibos.me:80      |
| Hong Kong    | seed-mainnet.fibscan.io:9103 |
| Oregon       | seed.bitze.site:9870         |
| San Francisco| seed.fibos.icu:9870          |
| London       | p2p.fibosutility.com:9870    |

**Note**：The above address may change and there may be delays in updating the document.

## Hardware recommended configuration

| Name     | Config          |
| -------- | --------------- |
| CPU      | 8 cores         |
| RAM      | 16GB RAM        |
| Storage  | 200GB Hard Disk |

