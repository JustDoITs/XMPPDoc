# 群及讨论组的权限系统
by Rusher

## MUC中的Roles,Affiliations和Privileges

权限管理有两种方式：

1. 针对每个用户设置不同的权限。灵活但是不便与管理
2. 定义一束(一个或多个权限的组合)常用的权限，起一个容易理解的别名，然后赋予给用户

MUC使用第二种方式管理权限。

MUC定义了用户和房间的两大类权限束：Roles和Affiliates。Roles中定义的权限束作用在会话中，例如：用户收发消息的权限，更改昵称的权限等等。而Affilications中定义的关系则从用在房间上，例如：用户能否进入房间的权限，以及管理房间成员的权限等等。基于以上的定义，Roles和Affiliations不存在一一对应的关系。

### Roles

* __Moderator__ :房间会话主持，权限最大的Role，可以踢人，收回/授权发言权；
* __Participant__ :房间的参与者，一直拥有发言的权利
* __Visitor__ :房间访问者，不能发言(取决于房间的设置，后面会提到)
* __None__ :无

Roles相关的权限：

|__Privilege__|__None__|__Visitor__|__Participant__|__Moderator__|
|:-----------:|:------:|:---------:|:-------------:|:-----------:|
|Present in Room|No|Yes|Yes|Yes|
|Receive Messages|No|Yes|Yes|Yes|
|Receive Occupant Presence|No|Yes|Yes|Yes|
|Broadcast Presence to All Occupants|No|Yes|Yes|Yes|
|Change Availability Status|No|Yes|Yes|Yes|
|Change Room Nickname|No|Yes|Yes|Yes|
|Send Private Messages|No|Yes|Yes|Yes|
|Invite Other Users|No|Yes|Yes|Yes|
|Send Messages to All|No|No|Yes|Yes|
|Modify Subject|No|No|Yes|Yes|
|Kick Participants and Visitors|No|No|No|Yes|
|Grant Voice|No|No|No|Yes|
|Revoke Voice|No|No|No|Yes|


### Affiliations

* __Owner__ :房间的拥有者，由Owner维护OwnerList
* __Admin__ :房间管理者
* __Member__ :房间会员
* __Outcast__ :在房间黑名单中的人
* __None__ :无

Affiliations相关的权限：

|__Privilege__|__Outcast__|__None__|__Member__|__Admin__|__Owner__|
|:-----------:|:---------:|:------:|:--------:|:-------:|:-------:|
|Enter Open Room|No|Yes|Yes|Yes|Yes|
|Register with Open Room|No|Yes|N/A|N/A|N/A|
|Retrieve Member List|No|No|Yes|Yes|Yes|
|Enter Members-Only Room|No|No|Yes|Yes|Yes|
|Ban Members and Unaffiliated Users|No|No|No|Yes|Yes|
|Edit Member List|No|No|No|Yes|Yes|
|Assign and Remove Moderator Role|No|No|No|Yes|Yes|
|Edit Admin List|No|No|No|No|Yes|
|Edit Owner List|No|No|No|No|Yes|
|Change Room Configuration|No|No|No|No|Yes|
|Destroy Room|No|No|No|No|Yes|

## 房间设置

本质上，群和讨论组都使MUC中的一个房间(忽略其他的信息)。但是由于不同的应用场景，需要对房间的属性进行设置。

### 群

### 讨论组

## 应用中的权限系统 