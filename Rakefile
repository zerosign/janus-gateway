task :default => [:prepare, :compile]

task :prepare do
	sh 'gengetopt --set-package="janus" --set-version="0.11.16" < janus.ggo'
	sh 'gengetopt --set-package="janus-pp-rec" --set-version="0.11.16" -F postprocessing/pp-cmdline < postprocessing/janus-pp-rec.ggo'
end

task :clean do
	sh 'rm -rf build'
end

task :compile do
	sh 'meson build'
	sh 'meson compile -C build'
end
