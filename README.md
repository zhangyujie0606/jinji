
# websocket - Tiny, cross platform websocket client C library.

### Features

- No additional dependecies
- Single header library interface librws.h with public methods
- Thread safe
- Send/receive logic in background thread
- [text](https://192.168.168.36)
-<https://192.168.168.36/>

### Example
##### Create and store websocket object handle
```c
  // Define variable or field for socket handle
  rws_socket _socket = NULL;
  ............
  // Create socket object
  _socket = rws_socket_create();
```
##### Set websocket connection url
```c
// Combined url: ws://echo.websocket.org:80/
rws_socket_set_scheme(_socket, "ws");
rws_socket_set_host(_socket, "echo.websocket.org");
rws_socket_set_port(_socket, 80);
rws_socket_set_path(_socket, "/");
```
##### Set websocket responce callbacks
Warning: ```rws_socket_set_on_disconnected``` is required
```cMain callbacks functions
 callback trigered on socket disconnected with/without error
static void on_socket_disconnected(rws_socket socket) {
  // process error
  rws_error error = rws_socket_get_error(socket);
  if (error) { 
    printf("\nSocket disconnect with code, error: %i, %s", rws_error_get_code(error), rws_error_get_description(error)); 
  }
  // forget about this socket object, due to next disconnection sequence
  _socket = NULL;
}
// callback trigered on socket connected and handshake done
static void on_socket_connected(rws_socket socket) {
  printf("\nSocket connected");
}
// callback trigered on socket received text
static void on_socket_received_text(rws_socket socket, const char * text, const unsigned int length) {
  printf("\nSocket text: %s", text);
}
..................
// Set socket callbacks
rws_socket_set_on_disconnected(_socket, &on_socket_disconnected); // required
rws_socket_set_on_connected(_socket, &on_socket_connected);
rws_socket_set_on_received_text(_socket, &on_socket_received_text);
