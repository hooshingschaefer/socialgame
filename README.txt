DB stuff
  table users userid char(32), username varchar(40)
  // userid corresponds to cookie and the username is the display name
  function register_user( char(32), varchar(40))
  checks if the cookie exists and inserts it, otherwise updates


Protocol stuff
  HEADER_LEN = 32
  byte 0: message
  byte 1: flags/extention of message (NOT USED)
  bytes 2 and 3: length of payload
     
