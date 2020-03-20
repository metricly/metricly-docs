---
title: "Custom Metrics"
#date: 2018-12-11
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#microsoft", "#azure", "#integrations", "#metrics"]
author: Lawrence Lane
---

### Linux

| Fully Qualified Name (FQN)                                  | Type | Units | Statistic | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL | DESCRIPTION |
|-------------------------------------------------------------|------|-------|-----------|-----|-----|----------------------------|------|------|------|-------------|
| azure.virtualmachine.builtindiskaveragediskqueuelength      |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtindiskaveragereadtime             |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtindiskaveragetransfertime         |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtindiskaveragewritetime            |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtindiskbytespersecond              |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtindiskreadbytespersecond          |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtindiskreadspersecond              |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtindisktransferspersecond          |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtindiskwritebytespersecond         |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtindiskwritespersecond             |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystembytespersecond        |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystembytesreadpersecond    |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystembyteswrittenpersecond |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystemfreespace             |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystempercentfreeinodes     |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystempercentfreespace      |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystempercentusedinodes     |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystempercentusedspace      |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystemreadspersecond        |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystemtransferspersecond    |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystemusedspace             |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinfilesystemwritespersecond       |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemoryavailablememory           |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemoryavailableswap             |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemorypagespersec               |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemorypagesreadpersec           |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemorypageswrittenpersec        |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemorypercentavailablememory    |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemorypercentavailableswap      |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemorypercentusedmemory         |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemorypercentusedswap           |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemoryusedmemory                |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinmemoryusedswap                  |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinnetworkbytesreceived            |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinnetworkbytestotal               |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinnetworkbytestransmitted         |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinnetworkpacketsreceived          |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinnetworkpacketstransmitted       |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinnetworktotalcollisions          |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinnetworktotalrxerrors            |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinnetworktotaltxerrors            |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinprocessorpercentidletime        |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinprocessorpercentinterrupttime   |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinprocessorpercentiowaittime      |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinprocessorpercentnicetime        |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinprocessorpercentprivilegedtime  |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinprocessorpercentprocessortime   |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.builtinprocessorpercentusertime        |      |       |           |     |     |                            |      |      |      |             |

### Windows

| Fully Qualified Name (FQN)                                         | Type | Units | Statistic | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL | DESCRIPTION |
|--------------------------------------------------------------------|------|-------|-----------|-----|-----|----------------------------|------|------|------|-------------|
| azure.virtualmachine.processorinformation_total.privilegedtime     |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.processorinformation_total.processorfrequency |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.processorinformation_total.processortime      |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.processorinformation_total.usertime           |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.process_total.handlecount                     |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.process_total.threadcount                     |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.system.contextswitchessec                     |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.system.processes                              |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.system.processorqueuelength                   |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.system.systemuptime                           |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.memory.availablebytes                         |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.memory.cachebytes                             |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.memory.committedbytes                         |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.memory.committedbytesinuse                    |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.memory.pagefaultssec                          |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.memory.pagessec                               |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.memory.poolnonpagedbytes                      |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.memory.poolpagedbytes                         |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.process_total.workingset                      |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.process_total.workingset-private              |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.avg.diskqueuelength         |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.avg.diskreadqueuelength     |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.avg.disksecread             |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.avg.disksectransfer         |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.avg.disksecwrite            |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.avg.diskwritequeuelength    |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.diskbytessec                |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.diskreadbytessec            |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.diskreadssec                |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.diskreadtime                |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.disktime                    |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.disktransferssec            |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.diskwritebytessec           |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.diskwritessec               |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.diskwritetime               |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.freemegabytes               |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.freespace                   |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.logicaldisk_total.idletime                    |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.networkinterface.bytesreceivedsec             |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.networkinterface.bytessentsec                 |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.networkinterface.bytestotalsec                |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.networkinterface.packetsoutbounderrors        |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.networkinterface.packetsreceivederrors        |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.networkinterface.packetsreceivedsec           |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.networkinterface.packetssec                   |      |       |           |     |     |                            |      |      |      |             |
| azure.virtualmachine.networkinterface.packetssentsec               |      |       |           |     |     |                            |      |      |      |             |