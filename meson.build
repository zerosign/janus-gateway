project('janus-gateway', 'c', version: '0.11.3')

conf = configuration_data()

headers = [
	'apierror.h',
	'config.h',
	'log.h',
	'debug.h',
	'mutex.h',
	'record.h',
	'rtcp.h',
	'rtp.h',
	'rtpsrtp.h',
	'sdp-utils.h',
	'ip-utils.h',
	'utils.h',
	'refcount.h',
	'text2pcap.h'
]

install_headers(headers, subdir: 'janus')

plugin_headers = [
	'plugins/plugin.h'
]

transport_headers = [
	'transports/transport.h'
]

logger_headers = [
	'loggers/logger.h'
]

event_headers = [
	'events/eventhandler.h',
	'events.h',
	'events.c'
]

janus_plugin_sources = [
	headers,
	plugin_headers,
]

janus_transport_sources = [
	headers,
	transport_headers,
]

janus_event_sources = [
	headers,
	event_headers,
]


janus_sources = [
	'apierror.c',
	'apierror.h',
	'auth.c',
	'auth.h',
	'cmdline.c',
	'cmdline.h',
	'config.c',
	'config.h',
	'debug.h',
	'dtls.c',
	'dtls.h',
	'dtls-bio.c',
	'dtls-bio.h',
	'events.c',
	'events.h',
	'janus.c',
	'janus.h',
	'ice.c',
	'ice.h',
	'log.c',
	'log.h',
	'mutex.h',
	'record.c',
	'record.h',
	'refcount.h',
	'rtcp.c',
	'rtcp.h',
	'rtp.c',
	'rtp.h',
	'rtpsrtp.h',
	'sctp.c',
	'sctp.h',
	'sdp.c',
	'sdp.h',
	'sdp-utils.c',
	'sdp-utils.h',
	'ip-utils.c',
	'ip-utils.h',
	'turnrest.c',
	'turnrest.h',
	'utils.c',
	'utils.h',
	'version.c',
	'version.h',
	'text2pcap.c',
	'text2pcap.h',
	'plugins/plugin.c',
	'plugins/plugin.h',
	'transports/transport.h',
	'transports/transport.c',
	'events/eventhandler.h' ,
	'loggers/logger.h'
]

janus_pp_sources = [
	'utils.h',
	'utils.c',
	'config.c',
	'config.h',
	'debug.h',
	'log.c',
	'log.h',
	'version.c',
	'version.h',
	'postprocessing/pp-av1.c',
	'postprocessing/pp-av1.h',
	'postprocessing/pp-avformat.c',
	'postprocessing/pp-avformat.h',
	'postprocessing/pp-binary.c',
	'postprocessing/pp-binary.h',
	'postprocessing/pp-g711.c',
	'postprocessing/pp-g711.h',
	'postprocessing/pp-g722.c',
	'postprocessing/pp-g722.h',
	'postprocessing/pp-h264.c',
	'postprocessing/pp-h264.h',
	'postprocessing/pp-h265.c',
	'postprocessing/pp-h265.h',
	'postprocessing/pp-opus.c',
	'postprocessing/pp-opus.h',
	'postprocessing/pp-opus-silence.h',
	'postprocessing/pp-rtp.h',
	'postprocessing/pp-srt.c',
	'postprocessing/pp-srt.h',
	'postprocessing/pp-webm.c',
	'postprocessing/pp-webm.h',
	'postprocessing/janus-pp-rec.c',
	'postprocessing/pp-cmdline.c',
	'postprocessing/pp-cmdline.h'
]

conf.set('HAVE_SRTP_2', 1)

# zlib_sp = subproject('zlib')

# glib_sp = subproject('glib')
# glib_dep = glib_sp.get_variable('libglib_dep')
# gio_dep = glib_sp.get_variable('libgio_dep')
# zlib_dep = glib_sp.get_variable('libz_dep')

glib_dep = dependency('glib-2.0')
gio_dep = dependency('gio-2.0')
zlib_dep = dependency('zlib')

# libnice_sp = subproject('libnice')
# libnice_dep = libnice_sp.get_variable('libnice_dep')

# jansson_sp = subproject('jansson')
# jansson_dep = jansson_sp.get_variable('jansson_dep')

libusrsctp_dep = dependency('usrsctp')

# libsrtp2_sp = subproject('libsrtp2')
# libsrtp2_dep = libsrtp2_sp.get_variable('libsrtp2_dep')

# libconfig_sp = subproject('libconfig')
# libconfig_dep = libconfig_sp.get_variable('libconfig_dep')

openssl_dep = declare_dependency(
	link_args: ['-L/opt/boringssl/lib', '-lssl', '-lcrypto'],
	include_directories: ['/opt/boringssl/include']
)

janus_dependencies = [
	zlib_dep,
	glib_dep,
	gio_dep,
	openssl_dep,
	libusrsctp_dep,
	dependency('libsrtp2'),
	dependency('nice'),
	dependency('jansson'),
	dependency('libconfig'),
]


janus_pp_dependencies = [
	glib_dep,
	gio_dep,
	zlib_dep,
	libusrsctp_dep,
	dependency('libavutil'),
	dependency('libavformat'),
	dependency('jansson'),
	dependency('libavcodec'),
	dependency('libconfig'),
]


link_args = [
	'-lm',
	'-ldl',
]

janus_config_install_dir = get_option('datadir') / 'janus'
janus_plugin_install_dir = get_option('libdir') / 'janus' / 'plugin'
janus_transport_install_dir = get_option('libdir') / 'janus' / 'transport'
janus_event_install_dir = get_option('libdir') / 'janus' / 'event'
janus_logger_install_dir = get_option('libdir') / 'janus' / 'logger'

build_args = [
	'-DHAVE_BORINGSSL=1',
	'-DHAVE_ICE_NOMINATION=1',
	'-DHAVE_ENUM_MHD_RESULT=1',
	'-DHAVE_SRTP_AESGCM=1',
	'-DHAVE_SCTP=1',
	'-DHAVE_SRTP_2=1',
	'-DHAVE_PORTRANGE=1',
	'-DCONFDIR="@0@"'.format(janus_config_install_dir, 0),
	'-DPLUGINDIR="@0@"'.format(janus_plugin_install_dir, 0),
	'-DTRANSPORTDIR="@0@"'.format(janus_transport_install_dir, 0),
	'-DEVENTDIR="@0@"'.format(janus_event_install_dir, 0),
	'-DLOGGERDIR="@0@"'.format(janus_logger_install_dir, 0),
]

shared_link_args = [
	link_args,
]

shared_build_args = [
	build_args,
]

janus_binary = executable(
	meson.project_name(),
	janus_sources,
	dependencies: janus_dependencies,
	install: true,
	c_args: build_args,
	link_args: link_args,
	export_dynamic: true,
)

janus_pp_binary = executable(
	'janus-pp-rec',
	janus_pp_sources,
	dependencies: janus_pp_dependencies,
	install: true,
	c_args: build_args,
	link_args: link_args,
	export_dynamic: false,
)

janus_videoroom_plugin_sources = [
	janus_plugin_sources,
	'plugins/janus_videoroom.c',
]

janus_videoroom_plugin = build_target(
	'janus_videoroom',
	janus_videoroom_plugin_sources,
	dependencies: [janus_dependencies],
	pic: true,
	install: true,
	install_dir: janus_plugin_install_dir,
	c_args: shared_build_args,
	link_args: shared_link_args,
	target_type: 'shared_module',
	export_dynamic: true,
)

janus_textroom_plugin_sources = [
	janus_plugin_sources,
	'plugins/janus_textroom.c',
]

janus_textroom_plugin = build_target(
	'janus_textroom',
	janus_textroom_plugin_sources,
	dependencies: [janus_dependencies],
	pic: true,
	install: true,
	install_dir: janus_plugin_install_dir,
	c_args: shared_build_args,
	link_args: shared_link_args,
	target_type: 'shared_module',
	export_dynamic: true,
)

janus_streaming_plugin_sources = [
	janus_plugin_sources,
	'plugins/janus_streaming.c',
]

janus_streaming_plugin_build_args = [
	'-DHAVE_LIBOGG=1',
]

# libogg_sp = subproject('ogg')
libogg_dep = dependency('ogg')
# libogg_sp.get_variable('libogg_dep')

janus_streaming_plugin_deps = [
	libogg_dep,
]


janus_streaming_plugin = build_target(
	'janus_streaming',
	janus_streaming_plugin_sources,
	dependencies: [janus_dependencies, janus_streaming_plugin_deps],
	pic: true,
	install: true,
	install_dir: janus_plugin_install_dir,
	c_args: [janus_streaming_plugin_build_args, shared_build_args],
	link_args: shared_link_args,
	target_type: 'shared_module',
	export_dynamic: true,
)

janus_audiobridge_plugin_sources = [
	janus_plugin_sources,
	'plugins/janus_audiobridge.c',
]

janus_audiobridge_plugin_build_args = [
	'-DHAVE_LIBOGG=1',
]

opus_dep = dependency('opus')

# libogg_sp = subproject('ogg')
libogg_dep = dependency('ogg')
	# libogg_sp.get_variable('libogg_dep')

janus_audiobridge_plugin_deps = [
	opus_dep,
	libogg_dep,
]

janus_audiobridge_plugin = build_target(
	'janus_audiobridge',
	janus_audiobridge_plugin_sources,
	dependencies: [janus_dependencies, janus_audiobridge_plugin_deps],
	pic: true,
	install: true,
	install_dir: janus_plugin_install_dir,
	c_args: [janus_audiobridge_plugin_build_args, shared_build_args],
	link_args: shared_link_args,
	target_type: 'shared_module',
	export_dynamic: true,
)

janus_http_transport_sources = [
	janus_transport_sources,
	'transports/janus_http.c',
]

janus_http_transport_build_args = [
	'-DHAVE_ENUM_MHD_RESULT=1'
]

# libmicrohttpd_sp = subproject('libmicrohttpd')
# libmicrohttpd_dep = microhttpd_sp.get_variable('libmicrohttpd_dep')

janus_http_transport_deps = [
	# libmicrohttpd_dep,
	dependency('libmicrohttpd'),
]

janus_http_transport = build_target(
	'janus_http',
	janus_http_transport_sources,
	dependencies: [janus_dependencies, janus_http_transport_deps],
	pic: true,
	install: true,
	install_dir: janus_transport_install_dir,
	c_args: [janus_http_transport_build_args, shared_build_args],
	link_args: shared_link_args,
	target_type: 'shared_module',
	export_dynamic: true,
)

janus_websockets_transport_sources = [
	janus_transport_sources,
	'transports/janus_websockets.c',
]

janus_websockets_transport_build_args = [
	'-DHAVE_ENUM_MHD_RESULT=1'
]

janus_websockets_transport_deps = [
	dependency('libwebsockets'),
]

janus_websockets_transport = build_target(
	'janus_websockets',
	janus_websockets_transport_sources,
	dependencies: [janus_dependencies, janus_websockets_transport_deps],
	pic: true,
	install: true,
	install_dir: janus_transport_install_dir,
	c_args: [janus_websockets_transport_build_args, shared_build_args],
	link_args: shared_link_args,
	target_type: 'shared_module',
	export_dynamic: true,
)

janus_wsevh_event_deps = [
	dependency('libwebsockets')
]

janus_wsevh_event_build_args = [
	'-DLWS_WITHOUT_EXTENSIONS=1'
]

janus_wsevh_event_sources = [
	janus_event_sources,
	'events/janus_wsevh.c'
]

janus_wsevent_event = build_target(
	'janus_wsevh',
	janus_wsevh_event_sources,
	dependencies: [janus_dependencies, janus_wsevh_event_deps],
	pic: true,
	install: true,
	install_dir: janus_event_install_dir,
	c_args: [janus_wsevh_event_build_args, shared_build_args],
	link_args: shared_link_args,
	target_type: 'shared_module',
	export_dynamic: true,
)
