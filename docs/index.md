# Lobby

TCP is a stream based protocol, therefore a message must be wrapped inside a length header.


---
## API Calls

### Register

Used to register a client to the lobby server

#### Request
> API: 1

* `apikey`
* `playerId`
* `customData`

| 1 byte        | multi  | 1byte           | multi    | 2 byte             | multi      |
|---------------|--------|-----------------|----------|--------------------|------------|
| apikey length | apikey | playerId length | playerId | customeData length | customData |

#### Reply
> API: -1

* `result`

!!! success
    result = 1

!!! failure
    result = 0


| 1 byte        | 
|---------------|
| result |

---

### Create Room

Used to create a room on the lobby server

#### Request
> API: 2

* `playerId`
* `customData`

| 1byte           | multi    | 2 byte             | multi      |
|-----------------|----------|--------------------|------------|
| playerId length | playerId | customeData length | customData |

#### Reply
> API: -2

* `result`
* `roomId`

!!! success
    result = 1

!!! failure
    result = 0


| 1 byte | 1byte         | multi  |
|--------|---------------|--------|
| result | roomId length | roomId |

---

### Get Rooms

Used to get all rooms of a game on the lobby server

#### Request
> API: 3

* `playerId`
* `pageCount`
* `pageIndex`

| 1byte           | multi    | 1 byte    | 1 byte    |
|-----------------|----------|-----------|-----------|
| playerId length | playerId | pageCount | pageIndex |

#### Reply
> API: -3

* `result`
* `totalPages`
* `totalRooms`
* `currentIndex`
* `currentPageCount`
* `roomIds`

!!! success
    result = 1

!!! failure
    result = 0


| 1 byte | 1byte      | 2byte      | 1byte        | 1byte           | multi  |
|--------|------------|------------|--------------|-----------------|--------|
| result | totalPages | totalRooms | currentIndex |currentPageCount | roomIds|

---

### Join Room

Used to join a room on the lobby server

#### Request
> API: 4

* `playerId`
* `roomId`

| 1byte           | multi    | 1byte         | multi  |
|-----------------|----------|---------------|--------|
| playerId length | playerId | roomId length | roomId |

#### Reply
> API: -4

* `result`

!!! success
    result = 1

!!! failure
    result = 0


| 1 byte |
|--------|
| result |

---

### Join Room (Random)

Used to join a room randomly on the lobby server

#### Request
> API: 5

* `playerId`

| 1byte           | multi    |
|-----------------|----------|
| playerId length | playerId |

#### Reply
> API: -5

* `result`
* `roomId`

!!! success
    result = 1

!!! failure
    result = 0


| 1 byte | 1byte         | multi  |
|--------|---------------|--------|
| result | roomId length | roomId |

---

### Start Room

Used to start a room on the lobby server

#### Request
> API: 6

* `playerId`

| 1byte           | multi    |
|-----------------|----------|
| playerId length | playerId |

#### Reply
> API: -6

* `result`

!!! success
    result = 1

!!! failure
    result = 0


| 1 byte |
|--------|
| result |

---

### Leave Room

Used to leave a room on the lobby server

#### Request
> API: 7

* `playerId`

| 1byte           | multi    |
|-----------------|----------|
| playerId length | playerId |

#### Reply
> API: -7

* `result`

!!! success
    result = 1

!!! failure
    result = 0


| 1 byte |
|--------|
| result |

---
## API Events

### Join Room Event

Fired when a player joined a room

#### Reply
> API: 8

* `playerId`
* `playerCustomData`


| 1byte           | multi    | 2byte             | multi     |
|-----------------|----------|-------------------|-----------|
| playerId length | playerId | customData length | customData|

---
### Room Started Event

Fired when a room started

#### Reply
> API: 9

* `RT port`
* `rpc port`


| 2byte   | 2byte    |
|---------|----------|
| RT port | RPC port |

---
### Leave Room Event

Fired when a player leaved a room

#### Reply
> API: 10

* `playerId`


| 1byte           | multi    |
|-----------------|----------|
| playerId length | playerId |