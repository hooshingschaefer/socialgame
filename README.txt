DB stuff
  table users userid char(16), username varchar(40), last_used_time date
  // userid corresponds to cookie and the username is the display name
  function register_user(char(16), varchar(40))
  checks if the cookie exists and inserts it, otherwise updates
  table lobbies (id int primary key, name varchar(24), owner char(16) references users.id, num_players int )


Protocol stuff
  connection:
    port = 6969
    all http headers are ignored except for Cookie which must be used to identify client unless they are registering
  Cookie:
    format is hauth=<16 alphanumeric characters, randomly generated>
  header:
    HEADER_LEN = 4 (bytes)
    byte 0: message
    byte 1: flags/extention of message (NOT USED)
    bytes 2 and 3: length of payload in little endian format
     <--------- 1 byte ----------> 
    +----------------------------+----------------------------+----------------------------+----------------------------+
    |           message          |           flags/           |   least significant byte   |    most significant byte   |
    |            type            |     extention of message   |       of payload size      |       of payload size      |
    +----------------------------+----------------------------+----------------------------+----------------------------+
    |          payload           |          payload           |          payload           |          payload           |
    |                            |                            |                            |                            |
    +----------------------------+----------------------------+----------------------------+----------------------------+
  
  
  messages: enum class REQUEST or RESPONSE followed by .value in js and ::value in c++
    client requests:
      instant reply expected
        REGISTER_USER    = 1
          expect ack or nack only
          too_long_user //should be implemented on front end?
        MAKE_LOBBY       = 2
        JOIN_LOBBY       = 3 //payload size field will instead be the lobby id (16 bits)
        START_GAME       = 4
        
      polling (response when event occurs):
      
    
    
    server responses:
      ACK              = 1
      NACK             = 2
      IMPROPER_FORMAT  = 3
      BAD_USERNAME     = 4
      NO_COOKIE        = 5 
      ---------below here are not used-----------
      
      
      
thoughts:
on polls respond every couple seconds or so to make sure user is still there but respond immediately if event occurred
