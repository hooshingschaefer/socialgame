DB stuff
  table users userid char(16), username varchar(40), last_used_time date
  // userid corresponds to cookie and the username is the display name
  function register_user(char(16), varchar(40))
  checks if the cookie exists and inserts it, otherwise updates


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
  
  
  messages:
    client requests:
      REGISTER_USER  = 1
      MAKE_LOBBY     = 2
      START_GAME     = 3
    server responses:
      ACK            = 1
      NACK           = 2
      
