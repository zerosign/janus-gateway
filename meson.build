project('janus-gateway', 'c', version: '0.11.2')

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
	'events/eventhandler.h'
]

janus_plugin_sources = [
	headers,
	plugin_headers,
]

janus_transport_sources = [
	headers,
	transport_headers,
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

usrsctp_dep = declare_dependency(
	link_args: ['/usr/lib/libusrsctp.so'],
	sources: [
		'/usr/include/usrsctp.h'
	]
)

conf.set('HAVE_SRTP_2', 1)

# zlib_sp = subproject('zlib')

glib_sp = subproject('glib')
glib_dep = glib_sp.get_variable('libglib_dep')
gio_dep = glib_sp.get_variable('libgio_dep')
zlib_dep = glib_sp.get_variable('libz_dep')

# libnice_sp = subproject('libnice')
# libnice_dep = libnice_sp.get_variable('libnice_dep')

# jansson_sp = subproject('jansson')
# jansson_dep = jansson_sp.get_variable('jansson_dep')

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
	dependency('libsrtp2'),
	dependency('nice'),
	dependency('jansson'),
	dependency('libconfig'),
	dependency('libcurl'),
]

link_args = [
	'-lm',
]

janus_config_install_dir = get_option('datadir') / 'janus'
janus_plugin_install_dir = get_option('libdir') / 'janus' / 'plugin'
janus_transport_install_dir = get_option('libdir') / 'janus' / 'transport'
janus_event_install_dir = get_option('libdir') / 'janus' / 'event'
janus_logger_install_dir = get_option('libdir') / 'janus' / 'logger'

build_args = [
	'-DHAVE_LIBCURL',
	'-DHAVE_SCTP',
	'-DHAVE_SRTP_2',
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

janus_videoroom_plugin_sources = [
	janus_plugin_sources,
	'plugins/janus_videoroom.c',
]

janus_videoroom_plugin = shared_module(
	'janus_videoroom',
	janus_videoroom_plugin_sources,
	dependencies: [janus_dependencies],
	pic: true,
	install: true,
	install_dir: janus_plugin_install_dir,
	c_args: shared_build_args,
	link_args: shared_link_args,
)

janus_textroom_plugin_sources = [
	janus_plugin_sources,
	'plugins/janus_textroom.c',
]

janus_textroom_plugin = shared_module(
	'janus_textroom',
	janus_textroom_plugin_sources,
	dependencies: [janus_dependencies],
	pic: true,
	install: true,
	install_dir: janus_plugin_install_dir,
	c_args: shared_build_args,
	link_args: shared_link_args,
)

janus_audiobridge_plugin_sources = [
	janus_plugin_sources,
	'plugins/janus_audiobridge.c',
]

janus_audiobridge_plugin_build_args = [
	'-DHAVE_LIBOGG',
]

opus_dep = dependency('opus')

# libogg_sp = subproject('ogg')
libogg_dep = dependency('ogg')
	# libogg_sp.get_variable('libogg_dep')

janus_audiobridge_plugin_deps = [
	opus_dep,
	libogg_dep,
]

janus_audiobridge_plugin = shared_module(
	'janus_audiobridge',
	janus_audiobridge_plugin_sources,
	dependencies: [janus_dependencies, janus_audiobridge_plugin_deps],
	pic: true,
	install: true,
	install_dir: janus_plugin_install_dir,
	c_args: [janus_audiobridge_plugin_build_args, shared_build_args],
	link_args: shared_link_args,
)

janus_http_transport_sources = [
	janus_transport_sources,
	'transports/janus_http.c',
]

janus_http_transport_build_args = [
	'-DHAVE_ENUM_MHD_RESULT'
]

# libmicrohttpd_sp = subproject('libmicrohttpd')
# libmicrohttpd_dep = microhttpd_sp.get_variable('libmicrohttpd_dep')

janus_http_transport_deps = [
	# libmicrohttpd_dep,
	dependency('libmicrohttpd'),
]

janus_http_transport = shared_module(
	'janus_http',
	janus_http_transport_sources,
	dependencies: [janus_dependencies, janus_http_transport_deps],
	pic: true,
	install: true,
	install_dir: janus_transport_install_dir,
	c_args: [janus_http_transport_build_args, shared_build_args],
	link_args: shared_link_args,
)

janus_websockets_transport_sources = [
	janus_transport_sources,
	'transports/janus_websockets.c',
]

janus_websockets_transport_build_args = [
	'-DHAVE_ENUM_MHD_RESULT'
]


# libwebsockets_sp = subproject('libwebsockets')
# libwebsockets_dep = libwebsockets_sp.get_variable('libwebsockets_dep')

janus_websockets_transport_deps = [
	# libwebsockets_dep
	dependency('libwebsockets'),
]

janus_websockets_transport = shared_module(
	'janus_websockets',
	janus_websockets_transport_sources,
	dependencies: [janus_dependencies, janus_websockets_transport_deps],
	install: true,
	install_dir: janus_transport_install_dir,
	c_args: [janus_websockets_transport_build_args, shared_build_args],
	link_args: shared_link_args,
)
