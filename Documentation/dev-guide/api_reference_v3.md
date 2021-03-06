### etcd API Reference


##### service `Auth` (etcdserver/etcdserverpb/rpc.proto)

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| AuthEnable | AuthEnableRequest | AuthEnableResponse | AuthEnable enables authentication. |
| AuthDisable | AuthDisableRequest | AuthDisableResponse | AuthDisable disables authentication. |
| Authenticate | AuthenticateRequest | AuthenticateResponse | Authenticate processes an authenticate request. |
| UserAdd | AuthUserAddRequest | AuthUserAddResponse | UserAdd adds a new user. |
| UserGet | AuthUserGetRequest | AuthUserGetResponse | UserGet gets detailed user information or lists all users. |
| UserDelete | AuthUserDeleteRequest | AuthUserDeleteResponse | UserDelete deletes a specified user. |
| UserChangePassword | AuthUserChangePasswordRequest | AuthUserChangePasswordResponse | UserChangePassword changes the password of a specified user. |
| UserGrant | AuthUserGrantRequest | AuthUserGrantResponse | UserGrant grants a role to a specified user. |
| UserRevoke | AuthUserRevokeRequest | AuthUserRevokeResponse | UserRevoke revokes a role of specified user. |
| RoleAdd | AuthRoleAddRequest | AuthRoleAddResponse | RoleAdd adds a new role. |
| RoleGet | AuthRoleGetRequest | AuthRoleGetResponse | RoleGet gets detailed role information or lists all roles. |
| RoleDelete | AuthRoleDeleteRequest | AuthRoleDeleteResponse | RoleDelete deletes a specified role. |
| RoleGrant | AuthRoleGrantRequest | AuthRoleGrantResponse | RoleGrant grants a permission of a specified key or range to a specified role. |
| RoleRevoke | AuthRoleRevokeRequest | AuthRoleRevokeResponse | RoleRevoke revokes a key or range permission of a specified role. |



##### service `Cluster` (etcdserver/etcdserverpb/rpc.proto)

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| MemberAdd | MemberAddRequest | MemberAddResponse | MemberAdd adds a member into the cluster. |
| MemberRemove | MemberRemoveRequest | MemberRemoveResponse | MemberRemove removes an existing member from the cluster. |
| MemberUpdate | MemberUpdateRequest | MemberUpdateResponse | MemberUpdate updates the member configuration. |
| MemberList | MemberListRequest | MemberListResponse | MemberList lists all the members in the cluster. |



##### service `KV` (etcdserver/etcdserverpb/rpc.proto)

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| Range | RangeRequest | RangeResponse | Range gets the keys in the range from the key-value store. |
| Put | PutRequest | PutResponse | Put puts the given key into the key-value store. A put request increments the revision of the key-value store and generates one event in the event history. |
| DeleteRange | DeleteRangeRequest | DeleteRangeResponse | DeleteRange deletes the given range from the key-value store. A delete request increments the revision of the key-value store and generates a delete event in the event history for every deleted key. |
| Txn | TxnRequest | TxnResponse | Txn processes multiple requests in a single transaction. A txn request increments the revision of the key-value store and generates events with the same revision for every completed request. It is not allowed to modify the same key several times within one txn. |
| Compact | CompactionRequest | CompactionResponse | Compact compacts the event history in the etcd key-value store. The key-value store should be periodically compacted or the event history will continue to grow indefinitely. |



##### service `Lease` (etcdserver/etcdserverpb/rpc.proto)

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| LeaseGrant | LeaseGrantRequest | LeaseGrantResponse | LeaseGrant creates a lease which expires if the server does not receive a keepAlive within a given time to live period. All keys attached to the lease will be expired and deleted if the lease expires. Each expired key generates a delete event in the event history. |
| LeaseRevoke | LeaseRevokeRequest | LeaseRevokeResponse | LeaseRevoke revokes a lease. All keys attached to the lease will expire and be deleted. |
| LeaseKeepAlive | LeaseKeepAliveRequest | LeaseKeepAliveResponse | LeaseKeepAlive keeps the lease alive by streaming keep alive requests from the client to the server and streaming keep alive responses from the server to the client. |



##### service `Maintenance` (etcdserver/etcdserverpb/rpc.proto)

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| Alarm | AlarmRequest | AlarmResponse | Alarm activates, deactivates, and queries alarms regarding cluster health. |
| Status | StatusRequest | StatusResponse | Status gets the status of the member. |
| Defragment | DefragmentRequest | DefragmentResponse | Defragment defragments a member's backend database to recover storage space. |
| Hash | HashRequest | HashResponse | Hash returns the hash of the local KV state for consistency checking purpose. This is designed for testing; do not use this in production when there are ongoing transactions. |
| Snapshot | SnapshotRequest | SnapshotResponse | Snapshot sends a snapshot of the entire backend from a member over a stream to a client. |



##### service `Watch` (etcdserver/etcdserverpb/rpc.proto)

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| Watch | WatchRequest | WatchResponse | Watch watches for events happening or that have happened. Both input and output are streams; the input stream is for creating and canceling watchers and the output stream sends events. One watch RPC can watch on multiple key ranges, streaming events for several watches at once. The entire event history can be watched starting from the last compaction revision. |



##### message `AlarmMember` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| memberID | memberID is the ID of the member associated with the raised alarm. | uint64 |
| alarm | alarm is the type of alarm which has been raised. | AlarmType |



##### message `AlarmRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| action | action is the kind of alarm request to issue. The action may GET alarm statuses, ACTIVATE an alarm, or DEACTIVATE a raised alarm. | AlarmAction |
| memberID | memberID is the ID of the member associated with the alarm. If memberID is 0, the alarm request covers all members. | uint64 |
| alarm | alarm is the type of alarm to consider for this request. | AlarmType |



##### message `AlarmResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| alarms | alarms is a list of alarms associated with the alarm request. | (slice of) AlarmMember |



##### message `AuthDisableRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `AuthDisableResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthEnableRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `AuthEnableResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthRoleAddRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| name | name is the name of the role to add to the authentication system. | string |



##### message `AuthRoleAddResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthRoleDeleteRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `AuthRoleDeleteResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthRoleGetRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `AuthRoleGetResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthRoleGrantRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| name | name is the name of the role which will be granted the permission. | string |
| perm | perm is the permission to grant to the role. | authpb.Permission |



##### message `AuthRoleGrantResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthRoleRevokeRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `AuthRoleRevokeResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthUserAddRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| name |  | string |
| password |  | string |



##### message `AuthUserAddResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthUserChangePasswordRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| name | name is the name of the user whose password is being changed. | string |
| password | password is the new password for the user. | string |



##### message `AuthUserChangePasswordResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthUserDeleteRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| name | name is the name of the user to delete. | string |



##### message `AuthUserDeleteResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthUserGetRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `AuthUserGetResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthUserGrantRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| user | user is the name of the user which should be granted a given role. | string |
| role | role is the name of the role to grant to the user. | string |



##### message `AuthUserGrantResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthUserRevokeRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `AuthUserRevokeResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `AuthenticateRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| name |  | string |
| password |  | string |



##### message `AuthenticateResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| token | token is an authorized token that can be used in succeeding RPCs | string |



##### message `CompactionRequest` (etcdserver/etcdserverpb/rpc.proto)

CompactionRequest compacts the key-value store up to a given revision. All superseded keys with a revision less than the compaction revision will be removed.

| Field | Description | Type |
| ----- | ----------- | ---- |
| revision | revision is the key-value store revision for the compaction operation. | int64 |
| physical | physical is set so the RPC will wait until the compaction is physically applied to the local database such that compacted entries are totally removed from the backend database. | bool |



##### message `CompactionResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `Compare` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| result | result is logical comparison operation for this comparison. | CompareResult |
| target | target is the key-value field to inspect for the comparison. | CompareTarget |
| key | key is the subject key for the comparison operation. | bytes |
| target_union |  | oneof |
| version | version is the version of the given key | int64 |
| create_revision | create_revision is the creation revision of the given key | int64 |
| mod_revision | mod_revision is the last modified revision of the given key. | int64 |
| value | value is the value of the given key, in bytes. | bytes |



##### message `DefragmentRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `DefragmentResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `DeleteRangeRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| key | key is the first key to delete in the range. | bytes |
| range_end | range_end is the key following the last key to delete for the range [key, range_end). If range_end is not given, the range is defined to contain only the key argument. If range_end is '\0', the range is all keys greater than or equal to the key argument. | bytes |



##### message `DeleteRangeResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| deleted | deleted is the number of keys deleted by the delete range request. | int64 |



##### message `HashRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `HashResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| hash | hash is the hash value computed from the responding member's key-value store. | uint32 |



##### message `LeaseGrantRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| TTL | TTL is the advisory time-to-live in seconds. | int64 |
| ID | ID is the requested ID for the lease. If ID is set to 0, the lessor chooses an ID. | int64 |



##### message `LeaseGrantResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| ID | ID is the lease ID for the granted lease. | int64 |
| TTL | TTL is the server chosen lease time-to-live in seconds. | int64 |
| error |  | string |



##### message `LeaseKeepAliveRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| ID | ID is the lease ID for the lease to keep alive. | int64 |



##### message `LeaseKeepAliveResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| ID | ID is the lease ID from the keep alive request. | int64 |
| TTL | TTL is the new time-to-live for the lease. | int64 |



##### message `LeaseRevokeRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| ID | ID is the lease ID to revoke. When the ID is revoked, all associated keys will be deleted. | int64 |



##### message `LeaseRevokeResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `Member` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| ID | ID is the member ID for this member. | uint64 |
| name | name is the human-readable name of the member. If the member is not started, the name will be an empty string. | string |
| peerURLs | peerURLs is the list of URLs the member exposes to the cluster for communication. | (slice of) string |
| clientURLs | clientURLs is the list of URLs the member exposes to clients for communication. If the member is not started, clientURLs will be empty. | (slice of) string |



##### message `MemberAddRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| peerURLs | peerURLs is the list of URLs the added member will use to communicate with the cluster. | (slice of) string |



##### message `MemberAddResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| member | member is the member information for the added member. | Member |



##### message `MemberListRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `MemberListResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| members | members is a list of all members associated with the cluster. | (slice of) Member |



##### message `MemberRemoveRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| ID | ID is the member ID of the member to remove. | uint64 |



##### message `MemberRemoveResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `MemberUpdateRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| ID | ID is the member ID of the member to update. | uint64 |
| peerURLs | peerURLs is the new list of URLs the member will use to communicate with the cluster. | (slice of) string |



##### message `MemberUpdateResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `PutRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| key | key is the key, in bytes, to put into the key-value store. | bytes |
| value | value is the value, in bytes, to associate with the key in the key-value store. | bytes |
| lease | lease is the lease ID to associate with the key in the key-value store. A lease value of 0 indicates no lease. | int64 |



##### message `PutResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |



##### message `RangeRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| key | key is the first key for the range. If range_end is not given, the request only looks up key. | bytes |
| range_end | range_end is the upper bound on the requested range [key, range_end). If range_end is '\0', the range is all keys >= key. | bytes |
| limit | limit is a limit on the number of keys returned for the request. | int64 |
| revision | revision is the point-in-time of the key-value store to use for the range. If revision is less or equal to zero, the range is over the newest key-value store. If the revision has been compacted, ErrCompaction is returned as a response. | int64 |
| sort_order | sort_order is the order for returned sorted results. | SortOrder |
| sort_target | sort_target is the key-value field to use for sorting. | SortTarget |
| serializable | serializable sets the range request to use serializable member-local reads. Range requests are linearizable by default; linearizable requests have higher latency and lower throughput than serializable requests but reflect the current consensus of the cluster. For better performance, in exchange for possible stale reads, a serializable range request is served locally without needing to reach consensus with other nodes in the cluster. | bool |



##### message `RangeResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| kvs | kvs is the list of key-value pairs matched by the range request. | (slice of) mvccpb.KeyValue |
| more | more indicates if there are more keys to return in the requested range. | bool |



##### message `RequestUnion` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| request | request is a union of request types accepted by a transaction. | oneof |
| request_range |  | RangeRequest |
| request_put |  | PutRequest |
| request_delete_range |  | DeleteRangeRequest |



##### message `ResponseHeader` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| cluster_id | cluster_id is the ID of the cluster which sent the response. | uint64 |
| member_id | member_id is the ID of the member which sent the response. | uint64 |
| revision | revision is the key-value store revision when the request was applied. | int64 |
| raft_term | raft_term is the raft term when the request was applied. | uint64 |



##### message `ResponseUnion` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| response | response is a union of response types returned by a transaction. | oneof |
| response_range |  | RangeResponse |
| response_put |  | PutResponse |
| response_delete_range |  | DeleteRangeResponse |



##### message `SnapshotRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `SnapshotResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header | header has the current key-value store information. The first header in the snapshot stream indicates the point in time of the snapshot. | ResponseHeader |
| remaining_bytes | remaining_bytes is the number of blob bytes to be sent after this message | uint64 |
| blob | blob contains the next chunk of the snapshot in the snapshot stream. | bytes |



##### message `StatusRequest` (etcdserver/etcdserverpb/rpc.proto)

Empty field.



##### message `StatusResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| version | version is the cluster protocol version used by the responding member. | string |
| dbSize | dbSize is the size of the backend database, in bytes, of the responding member. | int64 |
| leader | leader is the member ID which the responding member believes is the current leader. | uint64 |
| raftIndex | raftIndex is the current raft index of the responding member. | uint64 |
| raftTerm | raftTerm is the current raft term of the responding member. | uint64 |



##### message `TxnRequest` (etcdserver/etcdserverpb/rpc.proto)

From google paxosdb paper: Our implementation hinges around a powerful primitive which we call MultiOp. All other database operations except for iteration are implemented as a single call to MultiOp. A MultiOp is applied atomically and consists of three components: 1. A list of tests called guard. Each test in guard checks a single entry in the database. It may check for the absence or presence of a value, or compare with a given value. Two different tests in the guard may apply to the same or different entries in the database. All tests in the guard are applied and MultiOp returns the results. If all tests are true, MultiOp executes t op (see item 2 below), otherwise it executes f op (see item 3 below). 2. A list of database operations called t op. Each operation in the list is either an insert, delete, or lookup operation, and applies to a single database entry. Two different operations in the list may apply to the same or different entries in the database. These operations are executed if guard evaluates to true. 3. A list of database operations called f op. Like t op, but executed if guard evaluates to false.

| Field | Description | Type |
| ----- | ----------- | ---- |
| compare | compare is a list of predicates representing a conjunction of terms. If the comparisons succeed, then the success requests will be processed in order, and the response will contain their respective responses in order. If the comparisons fail, then the failure requests will be processed in order, and the response will contain their respective responses in order. | (slice of) Compare |
| success | success is a list of requests which will be applied when compare evaluates to true. | (slice of) RequestUnion |
| failure | failure is a list of requests which will be applied when compare evaluates to false. | (slice of) RequestUnion |



##### message `TxnResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| succeeded | succeeded is set to true if the compare evaluated to true or false otherwise. | bool |
| responses | responses is a list of responses corresponding to the results from applying success if succeeded is true or failure if succeeded is false. | (slice of) ResponseUnion |



##### message `WatchCancelRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| watch_id | watch_id is the watcher id to cancel so that no more events are transmitted. | int64 |



##### message `WatchCreateRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| key | key is the key to register for watching. | bytes |
| range_end | range_end is the end of the range [key, range_end) to watch. If range_end is not given, only the key argument is watched. If range_end is equal to '\0', all keys greater than or equal to the key argument are watched. | bytes |
| start_revision | start_revision is an optional revision to watch from (inclusive). No start_revision is "now". | int64 |
| progress_notify | progress_notify is set so that the etcd server will periodically send a WatchResponse with no events to the new watcher if there are no recent events. It is useful when clients wish to recover a disconnected watcher starting from a recent known revision. The etcd server may decide how often it will send notifications based on current load. | bool |



##### message `WatchRequest` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| request_union | request_union is a request to either create a new watcher or cancel an existing watcher. | oneof |
| create_request |  | WatchCreateRequest |
| cancel_request |  | WatchCancelRequest |



##### message `WatchResponse` (etcdserver/etcdserverpb/rpc.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| header |  | ResponseHeader |
| watch_id | watch_id is the ID of the watcher that corresponds to the response. | int64 |
| created | created is set to true if the response is for a create watch request. The client should record the watch_id and expect to receive events for the created watcher from the same stream. All events sent to the created watcher will attach with the same watch_id. | bool |
| canceled | canceled is set to true if the response is for a cancel watch request. No further events will be sent to the canceled watcher. | bool |
| compact_revision | compact_revision is set to the minimum index if a watcher tries to watch at a compacted index.  This happens when creating a watcher at a compacted revision or the watcher cannot catch up with the progress of the key-value store.  The client should treat the watcher as canceled and should not try to create any watcher with the same start_revision again. | int64 |
| events |  | (slice of) mvccpb.Event |



##### message `Event` (mvcc/mvccpb/kv.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| type | type is the kind of event. If type is a PUT, it indicates new data has been stored to the key. If type is a DELETE, it indicates the key was deleted. | EventType |
| kv | kv holds the KeyValue for the event. A PUT event contains current kv pair. A PUT event with kv.Version=1 indicates the creation of a key. A DELETE/EXPIRE event contains the deleted key with its modification revision set to the revision of deletion. | KeyValue |



##### message `KeyValue` (mvcc/mvccpb/kv.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| key | key is the key in bytes. An empty key is not allowed. | bytes |
| create_revision | create_revision is the revision of last creation on this key. | int64 |
| mod_revision | mod_revision is the revision of last modification on this key. | int64 |
| version | version is the version of the key. A deletion resets the version to zero and any modification of the key increases its version. | int64 |
| value | value is the value held by the key, in bytes. | bytes |
| lease | lease is the ID of the lease that attached to key. When the attached lease expires, the key will be deleted. If lease is 0, then no lease is attached to the key. | int64 |



##### message `Lease` (lease/leasepb/lease.proto)

| Field | Description | Type |
| ----- | ----------- | ---- |
| ID |  | int64 |
| TTL |  | int64 |



##### message `Permission` (auth/authpb/auth.proto)

Permission is a single entity

| Field | Description | Type |
| ----- | ----------- | ---- |
| key |  | bytes |
| permType |  | Type |



##### message `Role` (auth/authpb/auth.proto)

Role is a single entry in the bucket authRoles

| Field | Description | Type |
| ----- | ----------- | ---- |
| name |  | bytes |
| keyPermission |  | (slice of) Permission |



##### message `User` (auth/authpb/auth.proto)

User is a single entry in the bucket authUsers

| Field | Description | Type |
| ----- | ----------- | ---- |
| name |  | bytes |
| password |  | bytes |
| roles |  | (slice of) string |



